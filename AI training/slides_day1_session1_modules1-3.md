# Day 1 — Session 1: AI Foundations, Prompt Engineering & Core Techniques
**Covers: Modules 1–3 | Duration: ~3 hours | Format: 80% Hands-on**

---

## Slide 1: Welcome & Training Overview

**Prompt Engineering for Leveraging AI in Teaching and Research**

**2-Day Training Structure:**
- **Day 1 AM:** AI Foundations + Prompt Engineering Essentials (this session)
- **Day 1 PM:** AI for Teaching — Content Creation & Student Engagement
- **Day 2 AM:** AI for Research, Academic Writing & Critical Evaluation
- **Day 2 PM:** Ethics, Policy & Building Your AI Workflow

**Your LMS Access:** All detailed lessons, examples, and practice challenges are in the LMS track — use it as your ongoing reference after this training.

> Speaker notes: Introduce the training. Emphasize that this is a hands-on workshop — participants will be using AI tools throughout. Ensure everyone has access to at least one AI tool (ChatGPT, Claude, Gemini, or DeepSeek). Share LMS login credentials.

---

## Slide 2: What You Need to Know About AI (5 Minutes)

**Three things that matter for prompt engineering:**

1. **AI predicts text, it does not "know" facts**
   - LLMs generate the most likely next word based on patterns from training data
   - This is why they can be fluently wrong (hallucinations)

2. **Your prompt shapes the output**
   - Vague prompt → generic response
   - Specific prompt → useful, targeted response

3. **Different tools have different strengths**
   - ChatGPT: writing & brainstorming | Claude: long documents & reasoning
   - Gemini: Google integration | Perplexity: sourced research
   - Elicit/Consensus: academic paper discovery

> Speaker notes: Keep this brief — 5 minutes max. The point is to set the mental model, not teach AI theory. Refer participants to **Module 1, Lessons 1–3** in the LMS for the full conceptual foundation.

📖 **LMS Reference:** Module 1 — Lessons 1, 2, and 3

---

## Slide 3: Hands-On — Explore and Compare AI Tools (20 min)

**Activity: Ask the Same Question to 2+ AI Tools**

1. Pick an academic question from your field that you already know the answer to
2. Use this prompt in at least 2 different AI tools:

> You are a university lecturer in [your field]. Explain [your topic] for second-year undergraduate students. Include a practical example and note common misconceptions.

3. Compare the responses using this checklist:

| Criteria | Tool 1 | Tool 2 |
|----------|--------|--------|
| Accuracy | | |
| Detail level | | |
| Example quality | | |
| Usefulness for teaching | | |

4. **Discussion (5 min):** Share findings — which tool worked better for your task?

> Speaker notes: Circulate and help participants who are new to certain tools. This activity builds intuition about tool selection that pays off throughout the training. Full activity details in **Module 1, Lesson 4** in the LMS.

📖 **LMS Reference:** Module 1 — Activity: Explore and Compare AI Tools

---

## Slide 4: The 5-Component Prompt Framework

**Every powerful prompt uses some combination of:**

| Component | What It Does | Example |
|-----------|-------------|---------|
| **Role** | Sets expertise/perspective | "You are a peer reviewer for a top journal" |
| **Context** | Provides background | "I teach 200 first-year students in Nigeria" |
| **Task** | States what to do | "Create 10 MCQs on depreciation methods" |
| **Format** | Structures the output | "Format as a table with columns..." |
| **Constraints** | Sets boundaries | "Under 300 words, no jargon" |

**The master template:**
> **[Role]** You are [specific expertise].
> **[Context]** [Background about audience, situation].
> **[Task]** [Specific, actionable instruction].
> **[Format]** Format as [specific structure].
> **[Constraints]** [Limitations or requirements].

> Speaker notes: This is the single most important framework in the training. Spend 5 minutes explaining it with one live example. Then immediately move to hands-on practice. Full explanation and examples in **Module 2, Lesson 2**.

📖 **LMS Reference:** Module 2 — Lesson 2: Anatomy of an Effective Prompt

---

## Slide 5: Hands-On — Prompt Transformation Workshop (25 min)

**Activity: Transform 3 Weak Prompts Using the 5-Component Framework**

**Step 1:** Choose 3 weak prompts from this list (or use your own):
- "Explain supply and demand"
- "Help with my research on student motivation"
- "Create a quiz for my class"
- "Write an introduction for my paper"
- "Suggest teaching activities"

**Step 2:** For each, identify which components are missing (Role? Context? Task? Format? Constraints?)

**Step 3:** Rewrite each prompt using all 5 components

**Step 4:** Test BOTH versions (weak and strong) in your AI tool — compare the results

**Step 5 (Discussion):** Which component made the biggest difference?

> Speaker notes: This is the core hands-on activity for prompt engineering foundations. Give participants 20 minutes to work, then 5 minutes for group discussion. Detailed instructions and more weak prompt examples are in **Module 2, Lesson 4** in the LMS.

📖 **LMS Reference:** Module 2 — Lessons 3 & 4 (Transformations + Workshop)

---

## Slide 6: Three Power Techniques

| Technique | When to Use | How It Works |
|-----------|-------------|-------------|
| **Few-Shot** | Need consistent style/format | Provide 2-3 examples before your actual task |
| **Chain-of-Thought** | Complex reasoning tasks | Ask AI to "think step-by-step" with numbered steps |
| **Role-Based** | Need expert-level output | Assign a detailed persona with expertise + style |

**Combining them is even more powerful:**
> You are a senior research methodologist **(Role)**. Evaluate this study design step-by-step: **(Chain-of-Thought)** First assess the research question, then evaluate sampling, then analyze data collection. Here is an example of the feedback format I want: **(Few-Shot)** [example]

> Speaker notes: Introduce all three techniques together — 5 minutes of explanation. Refer participants to **Module 3, Lessons 1-3** for detailed explanations and academic examples of each technique. Then move directly to hands-on practice.

📖 **LMS Reference:** Module 3 — Lessons 1, 2, and 3

---

## Slide 7: Few-Shot Prompting — Quick Demo

**The pattern: Show 2-3 examples → AI follows the pattern**

**When to use:** Grading consistency, research coding, formatting standards

**Structure:**
```
[Describe the task]
Example 1: [input] → [desired output]
Example 2: [input] → [desired output]
Now do this: [your actual task]
```

**Key rules:**
- 2-3 examples is the sweet spot (more is rarely better)
- Use diverse examples (show range, not just one type)
- Include both positive and negative examples when relevant

> Speaker notes: Show one quick live example — e.g., few-shot for grading student responses with consistent rubric application. Full examples including grading and research coding are in **Module 3, Lesson 1**.

📖 **LMS Reference:** Module 3 — Lesson 1: Zero-Shot and Few-Shot Prompting

---

## Slide 8: Chain-of-Thought — Quick Demo

**The pattern: Ask AI to reason through steps before answering**

**Trigger phrases that work:**
- "Think step-by-step"
- "First... then... next... finally..."
- "Walk me through your reasoning"
- "Break this down into steps"

**When to use:** Research methodology, complex analysis, teaching explanations

**Key rules:**
- Number the steps explicitly in your prompt
- Use for reasoning tasks, not simple factual lookups
- Read the reasoning, not just the conclusion — that is where you catch errors

> Speaker notes: Show one quick live example — e.g., chain-of-thought for evaluating a research methodology. Full examples for teaching and research are in **Module 3, Lesson 2**.

📖 **LMS Reference:** Module 3 — Lesson 2: Chain-of-Thought Prompting

---

## Slide 9: Role-Based Prompting — Quick Demo

**The pattern: Assign a detailed persona to shift AI's expertise**

**Basic role (okay):** "You are an expert."
**Detailed persona (much better):** "You are a senior research methodology professor with 20 years of experience supervising PhD students in social sciences. You are constructively critical — you identify weaknesses but always suggest concrete improvements."

**Effective academic roles:**
- Peer reviewer for a top journal in [field]
- Socratic tutor who guides through questions
- Curriculum design specialist
- Research supervisor guiding a PhD student
- Academic editor improving scholarly writing

> Speaker notes: The key insight is that specificity matters — "expert" vs. a detailed persona produces dramatically different outputs. Full role examples for teaching, research, and writing are in **Module 3, Lesson 3**.

📖 **LMS Reference:** Module 3 — Lesson 3: Role-Based and Persona Prompting

---

## Slide 10: Hands-On — Technique Practice Lab (30 min)

**Activity: Apply All Three Techniques to Your Own Work**

**Step 1:** Choose ONE teaching task and ONE research task from your actual work

**Step 2:** For your **teaching task**, create 3 prompts:
- **Prompt A (Few-Shot):** Provide 2 examples of desired output, then ask for the new one
- **Prompt B (Chain-of-Thought):** Ask AI to think step-by-step with numbered steps
- **Prompt C (Role-Based):** Assign a specific academic persona

**Step 3:** Test all 3 prompts in your AI tool and rate each output:
- Relevance (1-5) | Quality (1-5) | Usability (1-5)

**Step 4:** Repeat for your **research task**

**Step 5 (Discussion):** Which technique worked best for teaching? For research? Why?

> Speaker notes: This is the most important activity in this session — 25 min working, 5 min discussion. Starter templates for each technique are in **Module 3, Lesson 4** in the LMS.

📖 **LMS Reference:** Module 3 — Activity: Technique Practice Lab

---

## Slide 11: Combining Everything — The Complete Prompt

**Real example combining all elements:**

> **[Role]** You are an experienced accounting professor who uses active learning strategies.
>
> **[Context]** I teach second-year undergraduates (80 students). They have completed introductory accounting. This is their first exposure to cash flow statements.
>
> **[Task]** Create a 90-minute lesson plan on "Cash Flow Statement Preparation."
>
> **[Chain-of-Thought]** Think through the lesson flow: First, design an engaging opener. Then, structure the main content in segments. Next, include a group activity. Finally, add a formative assessment.
>
> **[Format]** Format as a table with columns: Time, Activity, Description, Learning Objective.
>
> **[Constraints]** No technology required. Include at least one real-world Nigerian business example.

> Speaker notes: Walk through this example to show how the 5-component framework + techniques work together. This sets up the afternoon session where participants will build complete teaching packages.

---

## Slide 12: Session 1 Summary & Key Takeaways

**What you learned:**
- AI predicts text — specific prompts get specific results
- The 5-Component Framework: Role + Context + Task + Format + Constraints
- Three power techniques: Few-Shot, Chain-of-Thought, Role-Based
- Combining techniques produces the best results

**What you practiced:**
- Compared AI tools on the same question
- Transformed weak prompts into strong ones
- Applied all three techniques to your own teaching and research tasks

**Coming up next (Day 1 PM):** Using these skills to create real teaching materials — lesson plans, assessments, slide outlines, case studies, and student feedback

📖 **LMS Reference for self-study:** Modules 1, 2, and 3 (all lessons)

> Speaker notes: Quick recap. Encourage participants to explore the full lessons in Modules 1-3 on the LMS for deeper understanding and more examples. Break before afternoon session.
