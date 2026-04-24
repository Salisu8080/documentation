# PyLearn — Product Overview

---

## Elevator Pitch

PyLearn is an AI-powered, gamified Python learning platform built for African developers. It pairs a personalized Gemini AI tutor with real-time coding battles, structured learning tracks, and a deep gamification engine — turning the isolating grind of self-taught coding into a competitive, social, rewarding journey. Designed first for Nigerian learners and expanding across Africa and the global diaspora, PyLearn makes professional-grade Python education accessible at African price points while delivering an experience that rivals the world's best ed-tech platforms.

---

## Target Audience

### B2C Personas

**Persona 1 — The Nigerian University Student (Primary)**
- Age: 18–25, studying CS, engineering, or a non-tech course who wants to break into tech
- Goals: Get hired as a developer or freelancer; build portfolio projects; stand out from peers
- Pain points: University curricula are outdated; Udemy courses are passive and expensive; no accountability; no community; expensive bootcamps (₦200k–₦500k)
- Where they are: WhatsApp groups, Twitter/X, Instagram, campus forums
- Trigger to act: Fear of unemployment, peer comparison, NYSC approaching

**Persona 2 — The NYSC Corps Member**
- Age: 22–26, finished university, using service year to upskill before entering the job market
- Goals: Build a marketable technical skill before service year ends; impress employers
- Pain points: Unstructured free time; plenty of motivation but no clear path; budget-constrained
- Trigger: Sees peers getting developer jobs; wants to capitalize on the 12-month window

**Persona 3 — The Career Switcher**
- Age: 25–35, currently in finance, education, or admin; wants to transition into tech
- Goals: Python for data, automation, or backend development; career change in 6–12 months
- Pain points: Can't afford full-time bootcamp; doesn't know where to start; needs structured path with AI guidance
- Trigger: Tech salary articles, layoffs in their field, LinkedIn developer posts

**Persona 4 — The African Diaspora Learner**
- Location: UK, USA, Canada, Germany, Netherlands (Nigerian/African diaspora)
- Age: 20–40, has more disposable income, still wants culturally relevant community
- Goals: Upskill for career advancement; stay connected to African developer community
- Pain points: Existing platforms (Codecademy, Coursera) feel generic; no African tech community angle
- Price sensitivity: Low — will pay $10–$20/month without hesitation if the product delivers

**Persona 5 — The International Beginner (Expansion)**
- Location: Non-African countries; discovered PyLearn through search or YouTube
- Goals: Learn Python affordably with a fun, gamified experience
- Pain points: Codecademy is expensive ($20/month); freeCodeCamp has no AI guidance
- Price sensitivity: Medium — will compare to alternatives

### B2B Personas

**Persona 6 — University / Polytechnic CS Department**
- Decision maker: HOD of Computer Science, IT faculty director
- Need: Structured Python curriculum for 50–300 students; progress tracking; reduced lecturer workload
- Budget cycle: Tied to school session resumption (September, January)
- Pain: No affordable LMS built for African coding education

**Persona 7 — Private Coding Bootcamp**
- Decision maker: Founder/Director
- Need: Replace or supplement in-house curriculum; AI tutor reduces instructor burden; battle mode keeps cohorts engaged
- Budget: ₦100k–₦500k/month depending on cohort size
- Pain: High instructor cost; student dropout; lack of engagement tools

**Persona 8 — Corporate L&D / Tech Company**
- Decision maker: HR Manager, CTO, L&D Lead
- Need: Upskill junior developers or non-tech staff in Python; track completion
- Budget: ₦200k–₦2M/quarter depending on company size
- Pain: External training is expensive and untracked

---

## User Journey

### Discovery
- Referred by a friend (referral link with 500 XP incentive for referrer)
- Saw a Python tip post or Reel on Instagram/Twitter/Facebook
- Found the platform via Google search ("learn Python Nigeria", "free Python course Nigeria")
- Shared WhatsApp/Telegram group link from a study group or NYSC group

### Signup
- Lands on public homepage; can browse track list before registering
- Signs up with email, password, full name, phone, and country
- Optionally enters referral code
- Auto-enrolled in free tier immediately — no credit card required

### Activation (Day 1–3)
- Prompted to choose a learning track based on pace preference (slow/medium/fast)
- Completes first lesson; receives XP notification
- Attempts first challenge; earns Py-Coins
- Starts first streak; sees streak counter increment
- Receives a welcome notification encouraging them to return tomorrow

### Free Tier Experience (Day 1–14)
- Progresses through free tracks; gamification loop builds habit
- Uses AI tutor (Gemini) up to 10 times per day for help with challenges
- Joins a battle or checks the leaderboard; sees competitive peers
- Notices premium tracks are locked; sees "Premium Only" labels

### Friction Points (Upgrade Triggers)
- **AI limit hit**: Free user hits 10 AI conversations in a day; upgrade prompt shown
- **Premium track locked**: Tries to access exclusive content; upgrade modal shown
- **Leaderboard comparison**: Sees premium users with higher XP and levels
- **Battle/tournament feature**: Certain tournaments require premium membership

### Conversion
- Clicks upgrade; sees plan comparison (monthly vs. annual)
- 7-day trial available (monthly) or 14-day trial (annual)
- Pays via Paystack (card, bank transfer, USSD)
- Subscription activated immediately; premium tracks unlock; AI limit removed

### Premium Experience
- Unlimited AI tutoring with personality mode selection
- All learning tracks unlocked including advanced tracks
- Access to exclusive tournaments, premium projects
- Priority in leaderboards; premium badge on profile

### Retention Loop
- Daily streak reminder notifications
- Weekly leaderboard resets drive competitive re-engagement
- New challenges and track content added regularly
- Referral programme: share link → friend activates → earn premium days
- Achievements and badges provide ongoing dopamine rewards

---

## Feature Catalogue

### Learning Content
| Feature | Description |
|---|---|
| Learning Tracks | 20+ structured Python paths from beginner to advanced, organized with prerequisites |
| Modules | Units within tracks; each module groups related lessons |
| Lessons | Tutorial content with explanations, code examples, and embedded challenges |
| Challenges | 5 types: fill-in-the-blank, debug, scratch (write from scratch), optimize, multiple-choice |
| Difficulty Levels | Easy / Medium / Hard per challenge; affects XP reward |
| Hidden Test Cases | Challenges have visible + hidden test cases to prevent brute-forcing |
| Hints System | Pay Py-Coins to unlock progressive hints |

### AI Tutor
| Feature | Description |
|---|---|
| Gemini AI Tutor | Powered by Google Gemini 2.5 Flash; answers Python questions in real time |
| 4 Tutor Personas | Friendly, Strict, Encouraging, Peer — user selects preferred teaching style |
| Context-Aware Help | AI knows the user's current lesson, module, and skill level |
| Daily Usage Limit | Free users: 10 conversations/day; Premium: unlimited |
| Streaming Responses | AI replies stream token-by-token for a live chat experience |

### Code Execution
| Feature | Description |
|---|---|
| Browser-Based Execution | Run Python code directly in the browser via Piston API (no local install needed) |
| Syntax Validation | Pre-checks code before submission to surface errors quickly |
| Test Case Runner | Runs code against challenge test cases; shows pass/fail per case |
| Anti-Paste Protection | Prevents mass-pasting to encourage genuine coding practice |
| Execution Time Tracking | Records how long code takes to run (used for optimize challenges) |

### Gamification
| Feature | Description |
|---|---|
| XP & Levels | 30-level progression system; XP earned from lessons, challenges, battles, streaks |
| Py-Coins | In-game currency earned and spent; used for hints and cosmetics |
| Daily Streaks | Tracks consecutive days of activity; losing a streak creates urgency to return |
| Achievements | 50+ badges across categories: learning milestones, social actions, battle wins |
| Leaderboards | Global, weekly, and track-specific rankings to drive competition |
| Level-Up Notifications | Real-time celebration when a user reaches a new level |

### Battles & Tournaments
| Feature | Description |
|---|---|
| 1v1 Coding Battles | Real-time competitive coding against another user via WebSocket |
| Tournaments | Single-elimination or round-robin formats with brackets |
| Battle Spectators | Other users can watch live battles |
| XP Rewards | Winning battles earns bonus XP |
| Battle Matchmaking | Auto-matches users of similar skill level |

### Projects
| Feature | Description |
|---|---|
| Guided Projects | Step-by-step projects with milestones and validation |
| Open Projects | Freeform projects where users build and showcase work |
| Mini Projects | Short, focused challenges for quick skill application |
| Project Reviews | Community and AI-generated code reviews with ratings |
| Project Upvoting | Community discovery and social proof |
| Public Portfolio | Shareable portfolio page showing completed projects |

### Community & Social
| Feature | Description |
|---|---|
| Forum | Category-based discussions: General, Track-Specific, Help Desk |
| Direct Messaging | Private 1:1 messages with read receipts and emoji reactions |
| User Profiles | Public profile showing level, XP, achievements, and completed tracks |
| Follow System | Follow other users; see activity in feed |
| Code Snippets | Share reusable code with upvotes and search |

### Notifications & Analytics
| Feature | Description |
|---|---|
| Real-Time Notifications | In-app alerts for follows, upvotes, messages, battle invites, achievements |
| Email Preferences | Customizable daily/weekly digest emails |
| Progress Dashboard | Per-track and per-module completion percentages |
| Activity Heatmap | Visual calendar of daily engagement |
| Personal Stats | XP trends, streak history, challenge success rates |

### Referral System
| Feature | Description |
|---|---|
| Referral Codes | Every user gets a unique 12-character code (PY-XXXXXX format) |
| Qualified Referrals | Referral counts only when referred user completes a module AND a challenge |
| XP + Coin Rewards | 500 XP + 100 Py-Coins per qualified referral |
| Milestone Rewards | 5 referrals → 30 days premium; 10 → 60 days; 20 → 90 days; 50 → 365 days premium |
| Fraud Detection | Device fingerprinting to flag same-device multi-account abuse |

### Organization (B2B)
| Feature | Description |
|---|---|
| Org Creation | Any user can request an organization; admin approves |
| Member Management | Org admin adds/removes members via dashboard or CSV bulk upload |
| Track Assignments | Assign specific learning tracks to organization members |
| Progress Tracking | Org admin sees each member's completion progress |
| Custom Pricing | Admin sets payment amount per org; can waive payment |
| Lifecycle Management | Org goes through PENDING → APPROVED → ACTIVE → EXPIRED states |

### Admin Dashboard
| Feature | Description |
|---|---|
| User Management | View, ban, search, and manage all users |
| Content Management | Import/manage tracks, modules, lessons, challenges via UI |
| Subscription Controls | View and modify any user's subscription status |
| System Monitor | Request performance metrics, endpoint stats, error tracking |
| Audit Logs | Full log of admin actions for compliance |
| System Settings | Dynamic configuration without code redeployment |
| AI Prompt Editor | Edit the system prompt sent to Gemini AI from the admin panel |

---

## Pricing and Business Model

### Current Tiers

| Tier | Price | Key Limits |
|---|---|---|
| Free | ₦0/forever | 10 AI conversations/day; free tracks only |
| Premium Monthly | ₦5,000/month | Unlimited AI; all tracks; 7-day free trial |
| Premium Annual | ₦50,000/year | Same as monthly; 14-day free trial; ~17% savings |
| Organization | Custom | Everything in premium × N members; custom pricing |

### Revenue Model
- **Subscription revenue**: Recurring monthly or annual premium subscriptions from individuals
- **Organization licensing**: Custom-priced annual or periodic contracts with schools, bootcamps, companies
- **Referral-driven growth**: Premium days as referral rewards reduce CAC while creating organic acquisition loops
- **Payment processing**: All transactions via Paystack (card, bank transfer, USSD) in NGN; international capability via Paystack international card processing

### Current Revenue (April 2026)
- 2 active organization accounts generating ₦550,000 (total raised to date, not monthly recurring)
- 0 individual premium subscribers
- 500 total registered users; ~100 new users/month

---

## Competitive Positioning

| Dimension | PyLearn | Codecademy | freeCodeCamp | Udemy Python Courses |
|---|---|---|---|---|
| Price (Nigeria) | ₦2,500–5,000/month | ~₦15,000/month ($15 USD) | Free | ₦5,000–20,000 one-time |
| AI Tutoring | Yes (Gemini, 4 personas) | Limited (Pro tier) | None | None |
| Gamification | Deep (XP, battles, streaks, coins) | Basic | Basic | None |
| Real-Time Battles | Yes | No | No | No |
| African Community | Yes (Nigerian/African focus) | No | No | No |
| B2B / Org Features | Yes (org management, progress tracking) | Enterprise only | None | None |
| Referral Programme | Sophisticated (premium day rewards) | None | None | None |
| Price (International) | $9/month (proposed) | $20/month | Free | One-time |
| Language Support | English (African context) | English | English | English |

**Key differentiators:**
1. **AI tutor that knows your context** — Gemini knows your current lesson, pace, and level; generic platforms don't
2. **Real-time competitive coding** — 1v1 battles are unique in this price tier
3. **African price point with African community** — Codecademy costs 3–6x more; PyLearn targets the continent's learners directly
4. **Gamification depth** — 30-level XP system, 50+ achievements, Py-Coins, streaks; stronger than any direct competitor
5. **Referral engine** — Users earn premium access by referring friends; fundamentally different acquisition model
