# Module 3: Core Prompt Engineering Techniques
**Estimated Time:** 3.0 hours | **XP Reward:** 750

---

## Slide 1: Module Title

**Core Prompt Engineering Techniques**

Three powerful techniques that transform AI output quality:
1. Zero-Shot and Few-Shot Prompting
2. Chain-of-Thought Prompting
3. Role-Based and Persona Prompting

> Speaker notes: These three techniques, combined with the 5-component framework, form the complete prompt engineering toolkit. Mastering these makes participants effective AI users.

---

## Slide 2: Lesson 1 — Zero-Shot vs. Few-Shot Prompting

**Zero-shot:** Ask AI to perform a task WITHOUT examples
**Few-shot:** Provide 1-3 EXAMPLES before asking

The terms come from machine learning:
- "Shot" = example
- Zero-shot = zero examples
- Few-shot = a few examples

> Speaker notes: Simple concept, powerful impact. Most participants have only used zero-shot prompting. Few-shot is a game-changer for consistency.

---

## Slide 3: When Zero-Shot Works

**Zero-shot is sufficient when:**
- The task is straightforward ("Summarize this paragraph")
- Your instructions are very detailed and unambiguous
- The output format is standard (bullet points, paragraphs)

**Example:**
> Classify this essay response as "Excellent," "Good," "Satisfactory," or "Needs Improvement" based on argumentation, evidence, and clarity.

**Problem:** The AI has to guess YOUR standards for each category.

> Speaker notes: Zero-shot works for simple tasks. But for anything subjective — like grading — you need to show the AI what YOU mean by "excellent."

---

## Slide 4: When Few-Shot is Essential

**Few-shot is essential when:**
- You need the AI to follow YOUR specific pattern, style, or format
- The task is subjective (grading, evaluation)
- Zero-shot consistently misinterprets your instructions
- You need consistent output across multiple uses

> **Few-shot = Teaching AI by showing examples of what you want**

> Speaker notes: The power of few-shot is consistency. Show 2-3 examples of YOUR grading style, and the AI matches it. This is invaluable for assessment.

---

## Slide 5: Few-Shot Example — Grading Consistency

> **Example 1:**
> Student: "CSR is when companies donate money to charity."
> Rating: **Needs Improvement**
> Feedback: "Too narrow. CSR encompasses environmental stewardship, ethical labor practices, and stakeholder engagement. Expand your definition."
>
> **Example 2:**
> Student: "CSR refers to operating ethically, considering social, environmental, and economic impact on all stakeholders. Carroll's pyramid suggests four levels..."
> Rating: **Excellent**
> Feedback: "Strong, comprehensive understanding with theoretical framework."
>
> **Now evaluate this:** [new student response]

> Speaker notes: Walk through this example carefully. The AI learns YOUR grading voice, standards, and feedback style from just 2 examples. Demonstrate live if possible.

---

## Slide 6: Few-Shot Example — Research Coding

> **Excerpt 1:** "I worry students will copy everything from ChatGPT"
> **Code:** Academic Integrity Concern | **Sub-code:** Critical Thinking Erosion
>
> **Excerpt 2:** "I use AI to generate quiz questions — saves 2 hours per week"
> **Code:** Teaching Efficiency | **Sub-code:** Assessment Preparation
>
> **Excerpt 3:** "The university has no AI policy, so we're all guessing"
> **Code:** Institutional Policy Gap | **Sub-code:** Lack of Guidelines
>
> **Now code this:** "I tried Gemini to outline my paper, but suggestions were too generic"

> Speaker notes: Qualitative researchers will immediately see the value. The 3 examples establish a clear coding scheme, format, and granularity level.

---

## Slide 7: How Many Examples Do You Need?

| Examples | When to Use |
|----------|------------|
| 1 (one-shot) | Simple format matching (citation style) |
| 2-3 (few-shot) | Most tasks — shows the pattern clearly |
| 4+ | Complex, highly subjective tasks only |

**More is not always better.** Beyond 3-4 examples, you may waste context space without improving quality.

**Tips for choosing examples:**
- Use diverse examples (not all similar)
- Use real examples from your work
- Include both positive and negative examples

> Speaker notes: Keep it practical. 2-3 examples is the sweet spot for 90% of academic tasks.

---

## Slide 8: Lesson 2 — Chain-of-Thought Prompting

**Ask AI to show its reasoning step-by-step before giving the final answer**

**Instead of:** "What causes inflation in developing economies?"

**Use:** "Explain the causes of inflation in developing economies. Think step-by-step: First, identify major categories. Then, for each category, explain the mechanism and give a real-world example."

> **The difference:** Bullet list vs. structured, reasoned analysis you can evaluate.

> Speaker notes: Chain-of-thought is the most powerful technique for complex tasks. It dramatically improves accuracy and depth. The AI shows its work, making errors easier to spot.

---

## Slide 9: The Trigger Phrases

**These phrases reliably activate step-by-step reasoning:**

- "Think step-by-step"
- "Walk me through your reasoning"
- "First... then... next... finally..."
- "Break this down into steps"
- "Let us approach this systematically"
- "Explain your reasoning at each stage"

> **Combine with numbered steps for best results.**

> Speaker notes: Have participants practice by adding these phrases to prompts they've already written. The improvement is often immediate and dramatic.

---

## Slide 10: Chain-of-Thought Example — Research

> You are an expert research methodologist. I am designing a study on AI adoption in accounting practices in Nigerian SMEs.
>
> Think through this step-by-step:
> 1. **First,** identify key variables (independent, dependent, confounding)
> 2. **Then,** suggest an appropriate research design and justify why
> 3. **Next,** recommend data collection methods for each variable
> 4. **Finally,** note potential limitations and how to mitigate them
>
> Walk me through each step with clear reasoning.

**Result:** Structured methodology analysis, not a generic "use surveys" response.

> Speaker notes: Walk through this example step by step. Point out how each numbered step constrains the AI to address a specific aspect thoroughly.

---

## Slide 11: Chain-of-Thought Example — Teaching

> I teach Financial Accounting to students who struggle with abstract concepts.
>
> Think step-by-step:
> 1. Start with a real-world analogy from daily life
> 2. Then define depreciation formally
> 3. Walk through straight-line method with numbers
> 4. Explain why depreciation matters in financial statements
> 5. End with the most common student misconception and how to correct it

**Result:** Pedagogically sound explanation moving from concrete to abstract.

> Speaker notes: This prompt produces a mini-lesson ready for class use. The step-by-step structure mirrors good teaching practice.

---

## Slide 12: When to Use Chain-of-Thought

| Use Chain-of-Thought | Don't Bother |
|---------------------|-------------|
| Complex analysis tasks | Simple factual lookups |
| Methodology design | "What year was ABU founded?" |
| Multi-step reasoning | Formatting tasks |
| Critical evaluation | Translation |
| Argument construction | Brainstorming lists |

> **Rule of thumb:** If the task requires REASONING, use chain-of-thought.

> Speaker notes: Help participants develop intuition for when to apply this technique. It adds value for complex tasks but is overkill for simple ones.

---

## Slide 13: Lesson 3 — Role-Based and Persona Prompting

**Assigning AI a role activates specific expertise patterns**

**Without role:**
> "Feedback on academic papers usually includes comments on the thesis, evidence, and writing quality."

**With role ("You are a peer reviewer for a leading education journal"):**
> "The paper's contribution is unclear. The literature review fails to establish the gap. The methodology needs explicit justification for sample size..."

> **The role transforms generic descriptions into actionable, expert-level output.**

> Speaker notes: This is the most intuitive technique. Most participants will immediately see the difference. Live demonstration is very effective here.

---

## Slide 14: Effective Academic Roles

**For Teaching:**
- Experienced professor with active learning expertise
- Socratic tutor who guides through questions
- Curriculum design specialist
- Education technologist

**For Research:**
- Senior research methodologist (specify area)
- Peer reviewer for a top-tier journal
- Research supervisor guiding a PhD student
- Statistician specializing in social science

**For Writing:**
- Academic editor improving clarity and flow
- Grant proposal reviewer
- Journal editor evaluating argumentation

> Speaker notes: Provide this as a handout. Participants can reference it when crafting prompts throughout the rest of the training.

---

## Slide 15: Crafting Detailed Personas

**Basic role:** "You are a research expert."

**Detailed persona:** "You are a senior research methodology professor with 20 years of experience supervising PhD students in social sciences. You are constructively critical — you identify weaknesses but always suggest concrete improvements. You prioritize methodological rigor and practical feasibility."

**A detailed persona includes:**
1. **Expertise area** — what they specialize in
2. **Experience level** — how senior they are
3. **Communication style** — direct, supportive, rigorous
4. **Priorities** — what they value most

> Speaker notes: The more specific the persona, the better the output. Encourage participants to think about whose expertise they want the AI to emulate.

---

## Slide 16: Combining Techniques

**Techniques are most powerful when combined:**

| Combination | Example |
|------------|---------|
| Role + Chain-of-Thought | "You are a methodology expert. Evaluate this study step-by-step..." |
| Role + Few-Shot | "You are a grading assistant. Here are 2 examples of my grading style..." |
| Role + Context + Constraints | "You are a curriculum specialist. I teach in Nigeria with large classes and limited tech..." |
| All three techniques | Role + examples + step-by-step reasoning |

> Speaker notes: The techniques are building blocks. Advanced users combine them fluently. We'll practice combinations in the activity.

---

## Slide 17: Activity — Technique Practice Lab

**Objective:** Apply all three techniques to real academic tasks

**What you'll do:**
1. Choose one **teaching task** and one **research task** from your work
2. For each task, create THREE prompts:
   - **Prompt A:** Few-shot (provide 2 examples)
   - **Prompt B:** Chain-of-thought (numbered steps)
   - **Prompt C:** Role-based (detailed persona)
3. Test all 6 prompts in an AI tool
4. Rate each output: Relevance (1-5), Quality (1-5), Usability (1-5)
5. Write brief analysis: which technique worked best for which task?

**Time:** 45 minutes

> Speaker notes: This is a rigorous activity. Participants create 6 prompts and compare systematically. Help them manage time — suggest spending 7 minutes per prompt.

---

## Slide 18: Activity Debrief

**Discussion:**

1. Which technique worked best for teaching tasks? For research tasks?
2. Could you combine techniques in a single prompt? How?
3. When would you use each technique in your daily workflow?

**Typical findings:**
- Few-shot excels at consistency tasks (grading, formatting)
- Chain-of-thought excels at analysis and reasoning tasks
- Role-based excels at changing depth and perspective

> Speaker notes: Facilitate discussion. Most participants find that different techniques suit different tasks. The key insight is to match technique to task type.

---

## Slide 19: Module 3 Summary

**Key Takeaways:**

- **Few-shot:** Provide 2-3 examples to teach AI your exact pattern and standards
- **Chain-of-thought:** Ask for step-by-step reasoning for complex tasks
- **Role-based:** Assign detailed personas to shift expertise and perspective
- Techniques are most powerful when **combined**
- **Match the technique to the task** — few-shot for consistency, chain-of-thought for analysis, roles for perspective

**Next Module:** AI for Teaching — Curriculum and Content Creation
