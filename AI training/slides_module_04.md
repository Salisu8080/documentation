# Module 4: AI for Teaching — Curriculum and Content Creation
**Estimated Time:** 3.0 hours | **XP Reward:** 700

---

## Slide 1: Module Title

**AI for Teaching — Curriculum and Content Creation**

- Creating lesson plans and course outlines
- Generating assessments: quizzes, exams, and rubrics
- Creating lecture slides and visual aids
- Hands-on: Build a complete teaching package

> Speaker notes: Now we apply everything learned so far to real teaching tasks. This module is highly practical — participants will produce materials they can use immediately.

---

## Slide 2: Lesson 1 — Lesson Plans with AI

**Essential components to specify in your prompt:**

1. Subject and specific topic
2. Student level and prior knowledge
3. Duration of the class
4. Learning objectives (specify Bloom's level)
5. Teaching approach (lecture, active learning, case study)
6. Assessment component
7. Constraints (class size, technology, room setup)

> **The more specific your prompt, the more usable the lesson plan.**

> Speaker notes: Walk through each component. Emphasize that missing any one of these leads to generic, unusable output.

---

## Slide 3: Lesson Plan Prompt Example

> You are an experienced accounting professor who uses active learning. Create a 2-hour lesson plan for 2nd-year students on "Cash Flow Statement Preparation."
>
> Students understand income statements and balance sheets but this is their first exposure to cash flow statements.
>
> Include: 3 learning objectives (at least one at application level), 10-minute engaging opener, 3 content segments with timing, group activity for 80 students, 5-minute formative assessment, materials needed.
>
> Format: table with Time, Activity, Description, Resources columns.

> Speaker notes: Demonstrate this prompt live if possible. Walk through how each line maps to the 5-component framework.

---

## Slide 4: Iterative Refinement

**The first AI output is a starting point, not a finished product.**

**Follow-up prompts to refine:**
- "The group activity is too complex for 80 students. Suggest a simpler alternative."
- "Add a Nigerian business example to the cash flow lesson."
- "The pacing feels too fast. Redistribute over two sessions."

> **Professional prompt engineers expect to iterate 2-3 times.** This is normal, not failure.

> Speaker notes: Set expectations. Even excellent prompts rarely produce perfect first outputs. The skill is in knowing how to refine.

---

## Slide 5: Lesson Plan Template

**Save and reuse:**

> You are [ROLE]. Create a [DURATION]-minute lesson plan on "[TOPIC]" for [LEVEL] students who [PRIOR KNOWLEDGE].
>
> Include: [COMPONENTS LIST].
>
> Constraints: [CLASS SIZE, TECH, LIMITATIONS].
>
> Format: [TABLE/OUTLINE].

> Speaker notes: Encourage participants to write this template down. They will use it repeatedly. We revisit templates in Module 10.

---

## Slide 6: Lesson 2 — Generating Assessments

**Assessment generation requires MORE precise prompting because:**

- Questions must be unambiguous with clear correct answers
- Difficulty levels must be intentional
- Questions should test understanding, not just memorization
- MCQ distractors need to be plausible
- Rubrics need specific, observable descriptors

> Speaker notes: Assessment is the highest-stakes teaching task for AI assistance. Errors here directly affect students. Emphasize the need for quality-checking.

---

## Slide 7: Specifying Assessment Quality

**Key elements to include in assessment prompts:**

| Element | Example |
|---------|---------|
| Topic coverage | "Cover depreciation, inventory, intangible assets" |
| Question types | "5 MCQs, 3 short-answer, 1 case-based" |
| Difficulty mix | "40% recall, 40% application, 20% analysis" |
| Bloom's levels | "At least 3 questions at application level or higher" |
| Answer keys | "Include correct answers and explanations" |
| Marking scheme | "Point allocations for each step" |

> Speaker notes: Walk through each element. The more specific you are about assessment design, the less editing you'll need afterward.

---

## Slide 8: Quiz Generation Example

> You are an assessment expert with knowledge of Bloom's taxonomy. Create a formative quiz for 2nd-year Auditing students on "Internal Controls."
>
> Generate: 5 MCQs (2 knowledge, 3 application), 3 short-answer (application), 1 case-based question (analysis).
>
> MCQs: question, 4 options, correct answer, explanation of why correct answer is right AND why the most tempting wrong answer is wrong.
>
> Cover: objectives of internal controls, COSO framework, control weaknesses, segregation of duties.

> Speaker notes: Point out the detail — especially asking for explanations of wrong answers. This helps participants verify question quality.

---

## Slide 9: Rubric Creation Example

> Create a grading rubric for undergraduate research proposals with 5 criteria:
> 1. Research Problem (clarity, significance)
> 2. Literature Review (depth, synthesis)
> 3. Methodology (appropriateness, detail)
> 4. Writing Quality (academic tone, structure)
> 5. Contribution (originality, impact)
>
> 4 performance levels: Excellent (4), Good (3), Satisfactory (2), Needs Improvement (1).
>
> Format: table. Each cell must contain **specific, observable descriptors** — not vague terms like "good" or "adequate."

> Speaker notes: Emphasize "specific, observable descriptors." AI often defaults to vague rubric language. The constraint forces concrete descriptions.

---

## Slide 10: Quality-Checking AI Assessments

**Always verify:**

| Check | What to Look For |
|-------|-----------------|
| Accuracy | Are all correct answers actually correct? |
| Unambiguity | Can each question be interpreted only one way? |
| Distractor quality | Are wrong MCQ options plausible but clearly wrong? |
| Difficulty | Appropriate for your students' level? |
| Coverage | All intended topics adequately covered? |
| Alignment | Each question tests a stated learning objective? |

> **Generate more questions than you need, then select the best ones.**

> Speaker notes: This is non-negotiable. AI-generated assessments MUST be reviewed. Share a story of an AI-generated question with multiple correct answers to illustrate why.

---

## Slide 11: Lesson 3 — Lecture Slides and Visual Aids

**What AI CAN do for presentations:**
- Structure presentations into logical slide flows
- Generate concise bullet points and talking points
- Suggest visual elements (charts, diagrams, images)
- Adapt content for different audiences

**What AI CANNOT do:**
- Create actual PowerPoint files (most tools)
- Design visual layouts
- Generate images for slides (general LLMs)

> Speaker notes: Set expectations. AI generates content and structure — you design the actual slides. This is still a massive time-saver.

---

## Slide 12: Slide Outline Example

> You are an experienced lecturer who creates engaging presentations. Create a 15-slide outline for "Introduction to Corporate Governance" (45 minutes, final-year undergraduates).
>
> For each slide: title, 3-4 bullet points (max 6 words each), talking points (2-3 sentences), suggested visual element.
>
> Structure: Opening hook (1), key concepts (8), case study (3), summary and discussion (2), next class preview (1).

**Key trick:** Separate slide text (concise) from talking points (detailed).

> Speaker notes: Emphasize the "max 6 words per bullet" constraint. Without it, AI generates paragraph-length bullets unsuitable for slides.

---

## Slide 13: Activity — Build a Complete Teaching Package

**Objective:** Create a full set of teaching materials for one lesson

**What you'll produce:**
1. A detailed lesson plan (with objectives, activities, timing)
2. 5 assessment questions (varied types and difficulty)
3. A slide outline (10-12 slides with bullet points and notes)

**Then critically evaluate:** accuracy, alignment, usability

**Time:** 45 minutes

> Speaker notes: This is the capstone activity for the teaching modules. Participants produce real materials they can use. Circulate and help with topic selection.

---

## Slide 14: Activity — Step-by-Step

**Step 1:** Select a topic you teach (specific enough for one lesson)

**Step 2:** Generate lesson plan using the template from Slide 5

**Step 3:** Generate 5 assessment questions:
> "Based on the lesson above, create 3 MCQs and 2 short-answer questions aligned with the learning objectives."

**Step 4:** Generate slide outline:
> "Create 10-12 slides for this lesson. Each slide: title, 3-4 bullets (max 8 words), talking points."

**Step 5:** Critically evaluate all three outputs

**Step 6:** Refine at least one output with a follow-up prompt

> Speaker notes: Guide participants through each step. Suggest they spend 10 min on lesson plan, 10 min on assessment, 10 min on slides, 15 min on evaluation and refinement.

---

## Slide 15: Activity Debrief

**Discussion:**

1. How much time did this take compared to creating from scratch?
2. What was most useful? What needed the most editing?
3. Are the three components (plan, assessment, slides) coherent with each other?
4. Would you feel comfortable using these in your classroom after edits?

> Speaker notes: Most participants report significant time savings. Use this discussion to reinforce the iterative refinement workflow.

---

## Slide 16: Module 4 Summary

**Key Takeaways:**

- Lesson plans need all components specified: topic, level, duration, objectives, approach, constraints
- Assessment prompts require difficulty distribution, Bloom's levels, and answer keys
- Always quality-check AI assessments before using them
- Slide content should separate concise bullets from detailed talking points
- Iterate and refine — first drafts are starting points
- AI accelerates preparation but requires your expert judgment

**Next Module:** AI for Teaching — Student Engagement and Feedback
