# PyLearn System Optimization Plan

## Executive Summary

PyLearn becomes extremely slow with just 5-10 concurrent users due to critical performance bottlenecks. This plan provides a comprehensive, phased approach to optimize the entire system for production-grade performance with large concurrent users.

**Key Bottlenecks Identified:**
1. **N+1 Query Issues**: Dashboard executes 40+ DB queries per page load; Achievements page executes 150+ queries
2. **Missing Database Indexes**: Critical queries on frequently filtered columns lack indexes
3. **Blocking Code Execution**: Sequential HTTP calls to Piston API (5 tests = 50s+ potential latency)
4. **No Effective Caching**: Empty `invalidate_cache()`, SimpleCache not shared across workers
5. **Inefficient Analytics**: Python loops instead of SQL aggregations
6. **Limited Monitoring**: No database query tracking, N+1 detection, or alerting

**Target Outcome:** Support 100+ concurrent users with <500ms average response time

---

## Phase 1: Database Optimization (Highest Impact)

### Task 1.1: Add Missing Composite Indexes

**Priority:** CRITICAL
**Estimated Effort:** 2 hours
**Files to Create:**
- `migrate_performance_indexes.py`

**Indexes to Add:**

```sql
-- ChallengeAttempt (critical for challenge submissions & achievements)
CREATE INDEX idx_challenge_attempt_user_status ON challenge_attempts(user_id, status);
CREATE INDEX idx_challenge_attempt_user_challenge ON challenge_attempts(user_id, challenge_id);
CREATE INDEX idx_challenge_attempt_user_challenge_status ON challenge_attempts(user_id, challenge_id, status);

-- UserProgress (critical for dashboard, track progress)
CREATE INDEX idx_user_progress_user_status ON user_progress(user_id, status);
CREATE INDEX idx_user_progress_user_module_status ON user_progress(user_id, module_id, status);
CREATE INDEX idx_user_progress_user_lesson ON user_progress(user_id, lesson_id);

-- DailyStreak (streak calculations)
CREATE INDEX idx_daily_streak_user_date ON daily_streaks(user_id, streak_date);

-- Forum (thread/post listings)
CREATE INDEX idx_forum_thread_category_updated ON forum_threads(category_id, updated_at);
CREATE INDEX idx_forum_post_thread_created ON forum_posts(thread_id, created_at);

-- Battle (matchmaking, history)
CREATE INDEX idx_battle_status_created ON battles(status, created_at);
CREATE INDEX idx_battle_submission_battle_user ON battle_submissions(battle_id, user_id);

-- Message (chat history)
CREATE INDEX idx_message_chat_created ON messages(chat_id, created_at);

-- AI Conversation (rate limiting)
CREATE INDEX idx_ai_conversation_user_date ON ai_conversations(user_id, conversation_date);
```

**Verification:**
1. Run `EXPLAIN ANALYZE` on dashboard queries before adding indexes
2. Add indexes
3. Run same queries and compare execution time
4. Expected improvement: 5-10x faster for filtered queries

---

### Task 1.2: Fix N+1 Queries in Dashboard Route

**Priority:** CRITICAL
**Estimated Effort:** 6 hours
**Files to Create:**
- `query_helpers.py` - Batch query helper classes

**Files to Modify:**
- `app.py` (lines 867-955) - Dashboard route

**Current Problem (40+ queries per page):**
```python
# app.py:887-917 - Each iteration triggers multiple queries
for track in tracks:
    progress = ProgressEngine.get_track_progress(current_user, track)  # 3+ queries
    next_lesson = ProgressEngine.get_next_recommended_lesson(current_user, track)  # 2+ queries
    is_locked = not track.is_unlocked_for_user(current_user)  # 5+ queries
```

**Solution - Create `query_helpers.py`:**

```python
"""
Optimized batch query helpers to eliminate N+1 patterns.
All methods use 1-3 queries instead of N queries.
"""
from sqlalchemy import func, and_
from models import db, Track, Module, Lesson, UserProgress, Challenge

class BatchQueryHelper:
    @staticmethod
    def get_all_track_progress(user_id: int) -> dict:
        """
        Get progress for ALL tracks in 3 queries (instead of 3N).
        Returns: {track_id: {'total': int, 'completed': int, 'percentage': float}}
        """
        # Query 1: All module IDs per track
        track_modules = db.session.query(
            Track.id.label('track_id'),
            Module.id.label('module_id')
        ).join(Module, Module.track_id == Track.id).all()

        track_to_modules = {}
        all_module_ids = set()
        for track_id, module_id in track_modules:
            track_to_modules.setdefault(track_id, []).append(module_id)
            all_module_ids.add(module_id)

        # Query 2: Lesson counts per module
        lesson_counts = db.session.query(
            Lesson.module_id, func.count(Lesson.id)
        ).filter(Lesson.module_id.in_(all_module_ids)
        ).group_by(Lesson.module_id).all()
        module_lesson_count = dict(lesson_counts)

        # Query 3: Completed lessons per module for user
        completed = db.session.query(
            UserProgress.module_id, func.count(UserProgress.id)
        ).filter(
            UserProgress.user_id == user_id,
            UserProgress.status == 'completed',
            UserProgress.lesson_id.isnot(None),
            UserProgress.module_id.in_(all_module_ids)
        ).group_by(UserProgress.module_id).all()
        module_completed = dict(completed)

        # Aggregate per track
        result = {}
        for track_id, module_ids in track_to_modules.items():
            total = sum(module_lesson_count.get(mid, 0) for mid in module_ids)
            done = sum(module_completed.get(mid, 0) for mid in module_ids)
            result[track_id] = {
                'total_lessons': total,
                'completed_lessons': done,
                'completion_percentage': round((done / total * 100), 1) if total > 0 else 0
            }
        return result

    @staticmethod
    def get_all_next_lessons(user_id: int) -> dict:
        """
        Get next recommended lesson for ALL tracks in 2 queries.
        Returns: {track_id: Lesson or None}
        """
        # Query 1: All completed lesson IDs
        completed_ids = set(
            r[0] for r in UserProgress.query.with_entities(
                UserProgress.lesson_id
            ).filter(
                UserProgress.user_id == user_id,
                UserProgress.status == 'completed',
                UserProgress.lesson_id.isnot(None)
            ).all()
        )

        # Query 2: All lessons ordered
        lessons = db.session.query(
            Lesson.id, Module.track_id, Module.order_index, Lesson.order_index
        ).join(Module).order_by(
            Module.track_id, Module.order_index, Lesson.order_index
        ).all()

        # Find first incomplete per track (in-memory, fast)
        result = {}
        for lesson_id, track_id, _, _ in lessons:
            if track_id not in result and lesson_id not in completed_ids:
                result[track_id] = Lesson.query.get(lesson_id)
        return result

    @staticmethod
    def get_all_track_unlock_status(user, tracks: list) -> dict:
        """
        Check unlock status for all tracks in 1-2 queries.
        Returns: {track_id: {'is_locked': bool, 'reason': str}}
        """
        from subscription_helpers import is_premium_user
        user_is_premium = is_premium_user(user)

        # Reuse existing progress data
        all_progress = BatchQueryHelper.get_all_track_progress(user.id)
        track_lookup = {t.id: t for t in tracks}

        result = {}
        for track in tracks:
            is_locked = False
            reason = None

            if track.is_premium and not user_is_premium:
                is_locked = True
                reason = 'premium_required'
            elif track.prerequisite_track_id:
                prereq_progress = all_progress.get(track.prerequisite_track_id, {})
                if prereq_progress.get('completion_percentage', 0) < 100:
                    is_locked = True
                    reason = 'prerequisite_incomplete'

            result[track.id] = {
                'is_locked': is_locked,
                'reason': reason,
                'prerequisite': track_lookup.get(track.prerequisite_track_id)
            }
        return result
```

**Modified Dashboard Route (`app.py`):**

```python
@app.route('/dashboard')
@login_required
def dashboard():
    from query_helpers import BatchQueryHelper

    tracks = Track.query.order_by(Track.order_index).all()

    # BATCH QUERIES - 6 queries total instead of 40+
    all_progress = BatchQueryHelper.get_all_track_progress(current_user.id)
    all_next_lessons = BatchQueryHelper.get_all_next_lessons(current_user.id)
    all_unlock_status = BatchQueryHelper.get_all_track_unlock_status(current_user, tracks)

    tracks_with_progress = []
    for track in tracks:
        tracks_with_progress.append({
            'track': track,
            'progress': all_progress.get(track.id, {}),
            'next_lesson': all_next_lessons.get(track.id),
            **all_unlock_status.get(track.id, {})
        })

    # ... rest of dashboard (also optimize)
```

**Verification:**
1. Add query logging temporarily
2. Load dashboard, count queries (should be <10 instead of 40+)
3. Measure response time (should be <200ms instead of 2000ms+)

---

### Task 1.3: Fix N+1 in Achievements Page

**Priority:** HIGH
**Estimated Effort:** 4 hours
**Files to Modify:**
- `gamification.py` (lines 293-465) - AchievementEngine class

**Current Problem (150+ queries):**
```python
# gamification.py - check_all_achievements iterates ALL achievements
for achievement in unearned_achievements:  # Could be 50+ achievements
    if _check_achievement_requirement(user, achievement):  # 3+ queries each
        award_achievement(user, achievement)
```

**Solution - Pre-compute Statistics:**

```python
class AchievementEngine:
    @staticmethod
    def check_all_achievements_optimized(user):
        """
        Optimized achievement check: 150+ queries -> 8 queries.
        """
        # Query 1: Get all unearned achievement IDs
        earned_subq = db.session.query(UserAchievement.achievement_id).filter_by(
            user_id=user.id
        ).subquery()

        unearned = Achievement.query.filter(
            ~Achievement.id.in_(earned_subq)
        ).all()

        if not unearned:
            return []

        # PRE-COMPUTE ALL STATS (5-6 queries total)
        stats = {
            # Query 2: Unique challenges passed
            'challenges_solved': db.session.query(
                func.count(func.distinct(ChallengeAttempt.challenge_id))
            ).filter(
                ChallengeAttempt.user_id == user.id,
                ChallengeAttempt.status == 'passed'
            ).scalar() or 0,

            # Query 3: Lessons completed
            'lessons_completed': UserProgress.query.filter(
                UserProgress.user_id == user.id,
                UserProgress.status == 'completed',
                UserProgress.lesson_id.isnot(None)
            ).count(),

            # Query 4: Modules completed
            'modules_completed': UserProgress.query.filter(
                UserProgress.user_id == user.id,
                UserProgress.status == 'completed',
                UserProgress.module_id.isnot(None),
                UserProgress.lesson_id.is_(None)
            ).count(),

            # Query 5: Battles won
            'battles_won': Battle.query.filter_by(winner_id=user.id).count(),

            # Query 6: Forum stats
            'posts_count': ForumPost.query.filter_by(author_id=user.id).count(),

            # From user object (no query)
            'current_streak': user.current_streak,
            'longest_streak': user.longest_streak,
            'level': user.level,
            'xp': user.xp
        }

        # CHECK ACHIEVEMENTS AGAINST CACHED STATS (no queries)
        newly_earned = []
        for achievement in unearned:
            if AchievementEngine._check_against_stats(achievement, stats):
                if AchievementEngine.award_achievement(user, achievement):
                    newly_earned.append(achievement)

        return newly_earned

    @staticmethod
    def _check_against_stats(achievement, stats) -> bool:
        """Pure function - no database queries"""
        req_type = achievement.requirement_type
        req_value = achievement.requirement_value

        mapping = {
            'challenges_solved': stats['challenges_solved'],
            'challenges_completed': stats['challenges_solved'],
            'lessons_completed': stats['lessons_completed'],
            'lesson_completed': stats['lessons_completed'],
            'streak': max(stats['current_streak'], stats['longest_streak']),
            'level': stats['level'],
            'battles_won': stats['battles_won'],
            'posts': stats['posts_count'],
        }

        return mapping.get(req_type, 0) >= req_value
```

**Verification:**
1. Navigate to `/achievements` page
2. Count queries (should be <15 instead of 150+)
3. Response time should be <300ms

---

### Task 1.4: Fix N+1 in Tracks Page

**Priority:** HIGH
**Estimated Effort:** 3 hours
**Files to Modify:**
- `app.py` (lines 958-1002) - `/tracks` route

**Apply same BatchQueryHelper pattern as Task 1.2**

---

## Phase 2: Redis Caching with Upstash

### Task 2.1: Setup Upstash Redis Integration

**Priority:** HIGH
**Estimated Effort:** 4 hours
**Files to Create:**
- `cache_keys.py` - Centralized cache key definitions
- `redis_client.py` - Upstash-specific client wrapper

**Files to Modify:**
- `config_production.py` - Add Upstash config
- `caching.py` - Implement proper invalidation
- `requirements.txt` - Add `upstash-redis` package

**Upstash Configuration (`config_production.py`):**

```python
# Upstash Redis (serverless, pay-per-request)
# Uses existing REDIS_URL environment variable
REDIS_URL = os.environ.get('REDIS_URL')

if REDIS_URL:
    CACHE_TYPE = 'RedisCache'
    CACHE_REDIS_URL = REDIS_URL
else:
    CACHE_TYPE = 'SimpleCache'
```

**Create `cache_keys.py`:**

```python
"""Centralized cache key definitions"""

class CacheKeys:
    """Cache key patterns with TTL values"""

    # User-specific (invalidate on user action)
    USER_STATS = "user:stats:{user_id}"               # TTL: 5 min
    USER_TRACK_PROGRESS = "user:tracks:{user_id}"     # TTL: 5 min
    USER_ACHIEVEMENTS = "user:achievements:{user_id}" # TTL: 10 min

    # Global (shared across users)
    LEADERBOARD_GLOBAL = "leaderboard:global"         # TTL: 2 min
    LEADERBOARD_WEEKLY = "leaderboard:weekly"         # TTL: 2 min
    TRACK_LIST = "tracks:all"                         # TTL: 30 min

    # Analytics
    ANALYTICS_USER = "analytics:{user_id}"            # TTL: 10 min


class CacheTTL:
    SHORT = 120    # 2 minutes
    MEDIUM = 300   # 5 minutes
    LONG = 600     # 10 minutes
    STATIC = 1800  # 30 minutes
```

**Enhanced `caching.py`:**

```python
"""Enhanced caching with proper invalidation"""

from flask_caching import Cache
from functools import wraps
import logging

logger = logging.getLogger(__name__)
cache = Cache()

class CacheManager:
    @staticmethod
    def get_or_set(key: str, factory_func, ttl: int = 300):
        """Get from cache or compute and store"""
        result = cache.get(key)
        if result is not None:
            logger.debug(f"Cache HIT: {key}")
            return result

        logger.debug(f"Cache MISS: {key}")
        result = factory_func()
        cache.set(key, result, timeout=ttl)
        return result

    @staticmethod
    def invalidate_user_caches(user_id: int):
        """Invalidate all caches for a user"""
        from cache_keys import CacheKeys
        keys = [
            CacheKeys.USER_STATS.format(user_id=user_id),
            CacheKeys.USER_TRACK_PROGRESS.format(user_id=user_id),
            CacheKeys.USER_ACHIEVEMENTS.format(user_id=user_id),
            CacheKeys.ANALYTICS_USER.format(user_id=user_id),
        ]
        for key in keys:
            cache.delete(key)
        logger.info(f"Invalidated caches for user {user_id}")

    @staticmethod
    def invalidate_leaderboards():
        """Invalidate leaderboard caches (after XP changes)"""
        from cache_keys import CacheKeys
        cache.delete(CacheKeys.LEADERBOARD_GLOBAL)
        cache.delete(CacheKeys.LEADERBOARD_WEEKLY)
```

**Add Invalidation Hooks (`gamification.py`):**

```python
class GamificationEngine:
    @staticmethod
    def award_xp(user, amount, reason):
        # ... existing XP logic ...
        db.session.commit()

        # INVALIDATE CACHES
        from caching import CacheManager
        CacheManager.invalidate_user_caches(user.id)
        CacheManager.invalidate_leaderboards()
```

**Verification:**
1. Set up Upstash Redis account and get credentials
2. Add `REDIS_URL` environment variable (e.g., `redis://default:xxx@xxx.upstash.io:6379`)
3. Monitor cache hit/miss ratio in logs
4. Verify response times improve on repeated requests

---

### Task 2.2: Cache Dashboard Data

**Priority:** HIGH
**Estimated Effort:** 3 hours
**Files to Modify:**
- `app.py` - Dashboard route

**Implementation:**

```python
@app.route('/dashboard')
@login_required
def dashboard():
    from caching import CacheManager
    from cache_keys import CacheKeys, CacheTTL

    # Cache track progress (most expensive query)
    track_progress_key = CacheKeys.USER_TRACK_PROGRESS.format(user_id=current_user.id)
    track_data = CacheManager.get_or_set(
        track_progress_key,
        lambda: BatchQueryHelper.get_all_track_progress(current_user.id),
        ttl=CacheTTL.MEDIUM
    )

    # ... use cached data ...
```

---

## Phase 3: Code Execution Optimization

### Task 3.1: Parallel Test Case Execution

**Priority:** HIGH
**Estimated Effort:** 5 hours
**Files to Modify:**
- `code_execution.py` - CodeExecutor class

**Current Problem:**
- 5 test cases = 5 sequential HTTP requests
- Each request can take 2-10 seconds
- Total: 10-50 seconds for challenge submission

**Solution - ThreadPoolExecutor with Rate Limiting:**

```python
import concurrent.futures
import requests
from requests.adapters import HTTPAdapter
from urllib3.util.retry import Retry

class CodeExecutor:
    def __init__(self):
        self.api_url = 'https://emkc.org/api/v2/piston'
        self.execute_endpoint = f'{self.api_url}/execute'

        # Connection pooling for efficiency
        self.session = requests.Session()
        retry_strategy = Retry(
            total=3,
            backoff_factor=0.5,
            status_forcelist=[429, 500, 502, 503, 504]
        )
        adapter = HTTPAdapter(
            pool_connections=10,
            pool_maxsize=10,
            max_retries=retry_strategy
        )
        self.session.mount('https://', adapter)

        # Rate limiting (unknown Piston limits, be conservative)
        self.max_concurrent = 3  # Start conservative

    def execute_python_code_parallel(self, code: str, test_cases: list,
                                     time_limit: int = 10) -> dict:
        """
        Execute tests in parallel (3 concurrent max).
        Reduces 25s -> 8s for 5 test cases.
        """
        # Validate syntax first
        is_valid, error = self.validate_python_syntax(code)
        if not is_valid:
            return {'status': 'error', 'error_message': error, 'test_results': []}

        results = [None] * len(test_cases)

        with concurrent.futures.ThreadPoolExecutor(max_workers=self.max_concurrent) as executor:
            future_to_idx = {
                executor.submit(
                    self._run_single_test_safe,
                    code, tc, time_limit
                ): i
                for i, tc in enumerate(test_cases)
            }

            for future in concurrent.futures.as_completed(future_to_idx):
                idx = future_to_idx[future]
                try:
                    results[idx] = future.result()
                    results[idx]['test_number'] = idx + 1
                except Exception as e:
                    results[idx] = {
                        'test_number': idx + 1,
                        'passed': False,
                        'error': str(e)
                    }

        all_passed = all(r.get('passed', False) for r in results)
        return {
            'status': 'passed' if all_passed else 'failed',
            'test_results': results,
            'error_message': None if all_passed else 'Some tests failed'
        }

    def _run_single_test_safe(self, code: str, test_case: dict, time_limit: int) -> dict:
        """Run single test with fallback on rate limit"""
        import time

        for attempt in range(3):
            try:
                result = self.run_single_test(
                    code,
                    test_case.get('input', ''),
                    test_case.get('expected_output') or test_case.get('expected', ''),
                    test_case.get('code'),
                    time_limit
                )
                return result
            except requests.exceptions.HTTPError as e:
                if e.response.status_code == 429:  # Rate limited
                    time.sleep(1 * (attempt + 1))  # Exponential backoff
                    continue
                raise

        return {'passed': False, 'error': 'Rate limited, please try again'}
```

**Update Challenge Submission Route (`app.py`):**

```python
# In submit_challenge route, replace:
# result = executor.execute_python_code(code, all_tests)
# With:
result = executor.execute_python_code_parallel(code, all_tests)
```

**Verification:**
1. Time challenge submission with 5 test cases
2. Before: ~25 seconds, After: ~8 seconds
3. Monitor for rate limit errors, adjust `max_concurrent` if needed

---

## Phase 4: Enhanced System Monitoring (APM-Style)

### Task 4.1: Database Query Tracking

**Priority:** MEDIUM
**Estimated Effort:** 5 hours
**Files to Create:**
- `query_tracker.py` - SQLAlchemy query interceptor

**Implementation:**

```python
"""
Database query tracking for N+1 detection and slow query identification.
"""

import time
import threading
from collections import deque, defaultdict
from datetime import datetime
from sqlalchemy import event
from sqlalchemy.engine import Engine

class QueryTracker:
    """Track database queries per request"""

    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
            cls._instance._init()
        return cls._instance

    def _init(self):
        self.enabled = True
        self.slow_threshold_ms = 100
        self._request_local = threading.local()
        self._lock = threading.RLock()

        # Global stats
        self.slow_queries = deque(maxlen=500)
        self.query_patterns = defaultdict(lambda: {'count': 0, 'total_ms': 0})
        self.total_queries = 0

    def start_request(self):
        """Call at request start"""
        self._request_local.queries = []
        self._request_local.start = time.time()

    def record_query(self, sql: str, duration_ms: float):
        """Record a query execution"""
        if not self.enabled:
            return

        with self._lock:
            self.total_queries += 1

            # Normalize SQL to pattern
            pattern = self._normalize_sql(sql)

            query_data = {
                'sql': sql[:300],
                'pattern': pattern,
                'duration_ms': round(duration_ms, 2),
                'timestamp': datetime.utcnow().isoformat()
            }

            # Request-local tracking
            if hasattr(self._request_local, 'queries'):
                self._request_local.queries.append(query_data)

            # Slow query tracking
            if duration_ms > self.slow_threshold_ms:
                self.slow_queries.append(query_data)

            # Pattern tracking
            self.query_patterns[pattern]['count'] += 1
            self.query_patterns[pattern]['total_ms'] += duration_ms

    def end_request(self, endpoint: str) -> dict:
        """Analyze queries at request end, detect N+1"""
        queries = getattr(self._request_local, 'queries', [])

        # Detect N+1: >5 similar queries
        pattern_counts = defaultdict(int)
        for q in queries:
            pattern_counts[q['pattern']] += 1

        n_plus_one = [
            {'pattern': p[:100], 'count': c, 'endpoint': endpoint}
            for p, c in pattern_counts.items() if c > 5
        ]

        return {
            'query_count': len(queries),
            'total_ms': sum(q['duration_ms'] for q in queries),
            'n_plus_one': n_plus_one
        }

    def _normalize_sql(self, sql: str) -> str:
        """Normalize SQL for pattern matching"""
        import re
        normalized = re.sub(r'\b\d+\b', '?', sql)
        normalized = re.sub(r"'[^']*'", "'?'", normalized)
        return normalized[:150]

    def get_stats(self) -> dict:
        """Get query statistics for monitoring dashboard"""
        with self._lock:
            top_patterns = sorted(
                self.query_patterns.items(),
                key=lambda x: x[1]['count'],
                reverse=True
            )[:20]

            return {
                'total_queries': self.total_queries,
                'slow_count': len(self.slow_queries),
                'slow_queries': list(self.slow_queries)[-50:],
                'top_patterns': [
                    {
                        'pattern': p[:80],
                        'count': d['count'],
                        'avg_ms': round(d['total_ms'] / max(1, d['count']), 2)
                    }
                    for p, d in top_patterns
                ]
            }


query_tracker = QueryTracker()


def init_query_tracking(app, engine):
    """Hook into SQLAlchemy events"""

    @event.listens_for(Engine, "before_cursor_execute")
    def before_execute(conn, cursor, statement, parameters, context, executemany):
        conn.info.setdefault('query_start', []).append(time.time())

    @event.listens_for(Engine, "after_cursor_execute")
    def after_execute(conn, cursor, statement, parameters, context, executemany):
        start_times = conn.info.get('query_start', [])
        if start_times:
            duration_ms = (time.time() - start_times.pop()) * 1000
            query_tracker.record_query(statement, duration_ms)

    @app.before_request
    def before_request():
        query_tracker.start_request()

    @app.after_request
    def after_request(response):
        from flask import request, g
        stats = query_tracker.end_request(request.endpoint or request.path)

        # Log N+1 warnings
        for issue in stats.get('n_plus_one', []):
            app.logger.warning(
                f"N+1 DETECTED on {issue['endpoint']}: "
                f"{issue['pattern'][:50]}... ({issue['count']}x)"
            )

        g.query_stats = stats
        return response
```

**Initialize in `app.py`:**

```python
from query_tracker import init_query_tracking

# After db.init_app(app)
init_query_tracking(app, db.engine)
```

---

### Task 4.2: Persistent Monitoring Metrics

**Priority:** MEDIUM
**Estimated Effort:** 4 hours
**Files to Create:**
- `migrate_monitoring_tables.py`

**Files to Modify:**
- `models.py` - Add MonitoringMetric model
- `system_monitor.py` - Add persistence layer

**New Model (`models.py`):**

```python
class MonitoringMetric(db.Model):
    """Persisted monitoring metrics for historical analysis"""
    __tablename__ = 'monitoring_metrics'

    id = db.Column(db.Integer, primary_key=True)
    timestamp = db.Column(db.DateTime, nullable=False, index=True)
    metric_type = db.Column(db.String(50), nullable=False, index=True)

    # Aggregated values
    total_requests = db.Column(db.Integer, default=0)
    error_count = db.Column(db.Integer, default=0)
    slow_request_count = db.Column(db.Integer, default=0)
    avg_response_ms = db.Column(db.Float, default=0)
    p95_response_ms = db.Column(db.Float, default=0)
    active_users = db.Column(db.Integer, default=0)
    query_count = db.Column(db.Integer, default=0)

    # JSON for detailed breakdown
    endpoint_stats = db.Column(db.JSON)


class AlertHistory(db.Model):
    """Persisted alerts for investigation"""
    __tablename__ = 'alert_history'

    id = db.Column(db.Integer, primary_key=True)
    timestamp = db.Column(db.DateTime, nullable=False, index=True)
    alert_type = db.Column(db.String(50), nullable=False)
    severity = db.Column(db.String(20), nullable=False)
    message = db.Column(db.Text)
    endpoint = db.Column(db.String(200))
    resolved_at = db.Column(db.DateTime)
```

**Periodic Persistence (add to `system_monitor.py`):**

```python
class MetricsPersistence:
    """Periodically save metrics to database"""

    @staticmethod
    def save_hourly_snapshot():
        """Save aggregated metrics every hour"""
        from models import MonitoringMetric, db

        overview = monitor.get_overview()
        endpoint_stats = monitor.get_endpoint_stats()

        metric = MonitoringMetric(
            timestamp=datetime.utcnow(),
            metric_type='hourly',
            total_requests=overview['total_requests'],
            error_count=overview['total_errors'],
            slow_request_count=overview['slow_requests_count'],
            avg_response_ms=overview.get('avg_response_ms', 0),
            active_users=overview['active_users_5m'],
            endpoint_stats=endpoint_stats[:20]
        )

        db.session.add(metric)
        db.session.commit()
```

---

### Task 4.3: Enhanced Admin Monitor Dashboard

**Priority:** MEDIUM
**Estimated Effort:** 6 hours
**Files to Create:**
- `templates/admin/advanced_monitor.html`

**Files to Modify:**
- `premium_admin_routes.py` - New routes
- `templates/admin_system_monitor.html` - Enhance existing

**New Admin Route (`premium_admin_routes.py`):**

```python
@app.route('/admin/system-monitor/data')
@admin_required
def admin_system_monitor_data():
    """Enhanced monitoring data endpoint"""
    from system_monitor import monitor
    from query_tracker import query_tracker

    return jsonify({
        'overview': monitor.get_overview(),
        'endpoint_stats': monitor.get_endpoint_stats(),
        'slow_requests': monitor.get_slow_requests(50),
        'recent_requests': monitor.get_recent_requests(100),
        'request_sources': monitor.get_request_sources(),
        'active_users': _get_active_user_details(),

        # NEW: Query tracking
        'query_stats': query_tracker.get_stats(),

        # NEW: Alerts
        'alerts': monitor.get_active_alerts() if hasattr(monitor, 'get_active_alerts') else []
    })


@app.route('/admin/performance-trends')
@admin_required
def admin_performance_trends():
    """Historical performance trends"""
    from models import MonitoringMetric

    # Last 24 hours of hourly metrics
    cutoff = datetime.utcnow() - timedelta(hours=24)
    metrics = MonitoringMetric.query.filter(
        MonitoringMetric.timestamp >= cutoff,
        MonitoringMetric.metric_type == 'hourly'
    ).order_by(MonitoringMetric.timestamp).all()

    return jsonify({
        'metrics': [
            {
                'timestamp': m.timestamp.isoformat(),
                'requests': m.total_requests,
                'errors': m.error_count,
                'avg_ms': m.avg_response_ms,
                'active_users': m.active_users
            }
            for m in metrics
        ]
    })
```

**Enhanced Monitor Template Features:**
1. Query count per request tracking
2. N+1 detection warnings panel
3. Slow query log with SQL snippets
4. Historical trends charts (using Chart.js)
5. Alert notifications panel
6. Database connection pool stats
7. Memory usage tracking

---

### Task 4.4: Alert System

**Priority:** LOW
**Estimated Effort:** 3 hours
**Files to Modify:**
- `system_monitor.py`

**Implementation:**

```python
class AlertManager:
    """Performance alert management"""

    def __init__(self):
        self.thresholds = {
            'error_rate': 5.0,        # Alert if >5% errors
            'avg_response_ms': 2000,  # Alert if >2s avg response
            'slow_percent': 20.0,     # Alert if >20% slow requests
            'n_plus_one_count': 10,   # Alert if N+1 detected
        }
        self.alerts = deque(maxlen=100)

    def check_and_alert(self, overview: dict, query_stats: dict = None):
        """Check conditions and generate alerts"""
        new_alerts = []

        if overview['error_rate_percent'] > self.thresholds['error_rate']:
            new_alerts.append({
                'type': 'high_error_rate',
                'severity': 'critical',
                'message': f"Error rate {overview['error_rate_percent']}% exceeds {self.thresholds['error_rate']}%",
                'timestamp': datetime.utcnow().isoformat()
            })

        if query_stats:
            for issue in query_stats.get('n_plus_one', []):
                if issue['count'] > self.thresholds['n_plus_one_count']:
                    new_alerts.append({
                        'type': 'n_plus_one',
                        'severity': 'warning',
                        'message': f"N+1 query on {issue['endpoint']}: {issue['count']} similar queries",
                        'timestamp': datetime.utcnow().isoformat()
                    })

        self.alerts.extend(new_alerts)
        return new_alerts
```

---

## Phase 5: Analytics Optimization

### Task 5.1: SQL Aggregations Instead of Python Loops

**Priority:** MEDIUM
**Estimated Effort:** 3 hours
**Files to Modify:**
- `analytics.py` (lines 200-255)

**Current Problem:**
```python
# 7 separate queries for daily study time
for day_offset in range(7):
    streak = DailyStreak.query.filter_by(user_id=user.id, streak_date=date).first()
```

**Solution - Single Query:**

```python
@staticmethod
def get_study_time_week(user_id: int) -> list:
    """Get study time for last 7 days in ONE query"""
    start_date = datetime.utcnow().date() - timedelta(days=6)

    results = db.session.query(
        DailyStreak.streak_date,
        DailyStreak.xp_earned
    ).filter(
        DailyStreak.user_id == user_id,
        DailyStreak.streak_date >= start_date
    ).order_by(DailyStreak.streak_date).all()

    # Fill in missing days
    result_map = {r.streak_date: r.xp_earned for r in results}
    return [
        {
            'date': (start_date + timedelta(days=i)).strftime('%a'),
            'xp': result_map.get(start_date + timedelta(days=i), 0)
        }
        for i in range(7)
    ]


@staticmethod
def get_challenges_by_week(user_id: int, weeks: int = 4) -> list:
    """Get challenge completion by week in ONE query (PostgreSQL)"""
    start_date = datetime.utcnow() - timedelta(weeks=weeks)

    results = db.session.query(
        func.date_trunc('week', ChallengeAttempt.submitted_at).label('week'),
        func.count(func.distinct(ChallengeAttempt.challenge_id)).label('count')
    ).filter(
        ChallengeAttempt.user_id == user_id,
        ChallengeAttempt.status == 'passed',
        ChallengeAttempt.submitted_at >= start_date
    ).group_by(
        func.date_trunc('week', ChallengeAttempt.submitted_at)
    ).order_by('week').all()

    return [{'week': f'Week {i+1}', 'count': c} for i, (_, c) in enumerate(results)]
```

---

## Phase 6: Background Job Processing (Future)

### Task 6.1: Cloud Tasks Integration

**Priority:** LOW (for future scaling)
**Estimated Effort:** 8 hours

**Note:** For Cloud Run, Google Cloud Tasks is more appropriate than Celery.

**Tasks to offload:**
1. Achievement checking after challenge completion
2. Email notifications
3. Leaderboard recalculation
4. Analytics aggregation

**This phase can be deferred** until user scale requires it.

---

## Implementation Order

| Priority | Phase/Task | Effort | Impact |
|----------|-----------|--------|--------|
| 1 | Task 1.1: Add Indexes | 2h | Very High |
| 2 | Task 1.2: Dashboard N+1 | 6h | Very High |
| 3 | Task 3.1: Parallel Execution | 5h | High |
| 4 | Task 1.3: Achievements N+1 | 4h | High |
| 5 | Task 2.1: Redis Setup | 4h | High |
| 6 | Task 2.2: Cache Dashboard | 3h | High |
| 7 | Task 1.4: Tracks N+1 | 3h | Medium |
| 8 | Task 4.1: Query Tracking | 5h | Medium |
| 9 | Task 4.2: Persistent Metrics | 4h | Medium |
| 10 | Task 4.3: Enhanced Dashboard | 6h | Medium |
| 11 | Task 5.1: Analytics SQL | 3h | Medium |
| 12 | Task 4.4: Alerts | 3h | Low |

**Total Estimated Effort:** ~48 hours

---

## Files to Create (Summary)

1. `query_helpers.py` - Batch query helpers
2. `cache_keys.py` - Cache key definitions
3. `query_tracker.py` - SQL query tracking
4. `migrate_performance_indexes.py` - Index migration
5. `migrate_monitoring_tables.py` - Monitoring tables migration
6. `templates/admin/advanced_monitor.html` - Enhanced dashboard

## Files to Modify (Summary)

1. `app.py` - Dashboard, tracks, challenge routes
2. `gamification.py` - Achievement checking
3. `code_execution.py` - Parallel execution
4. `caching.py` - Redis integration, invalidation
5. `config_production.py` - Upstash config
6. `analytics.py` - SQL aggregations
7. `system_monitor.py` - Alerts, persistence
8. `premium_admin_routes.py` - New monitoring routes
9. `models.py` - Monitoring models
10. `templates/admin_system_monitor.html` - UI enhancements

---

## Verification Checklist

### Before Implementation
- [ ] Record baseline metrics:
  - Dashboard load time: ___ms
  - Achievements page load time: ___ms
  - Challenge submission time: ___ms
  - Query count per dashboard: ___

### After Each Phase
- [ ] Phase 1: Query count reduced by 80%+
- [ ] Phase 2: Cache hit ratio >70%
- [ ] Phase 3: Challenge submission <10s
- [ ] Phase 4: N+1 detection working
- [ ] Phase 5: Analytics <500ms

### Production Monitoring
- [ ] Response time P95 <1000ms
- [ ] Error rate <1%
- [ ] Support 100+ concurrent users
- [ ] No N+1 warnings in logs

---

## Environment Variables Required

```bash
# Upstash Redis (uses existing REDIS_URL variable name)
REDIS_URL=redis://default:xxx@xxx.upstash.io:6379

# Optional: External monitoring
SENTRY_DSN=https://xxx@sentry.io/xxx
```

---

## Rollback Plan

Each phase is independent and can be rolled back:

1. **Indexes**: `DROP INDEX idx_name;`
2. **Query helpers**: Revert to original routes
3. **Redis**: Falls back to SimpleCache automatically
4. **Parallel execution**: Use sequential method
5. **Query tracking**: Disable with `query_tracker.enabled = False`
