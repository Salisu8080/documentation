# Module 10: Building Your AI-Enhanced Academic Workflow
**Estimated Time:** 3.0 hours | **XP Reward:** 700

---

## Slide 1: Module Title

**Building Your AI-Enhanced Academic Workflow**

- Advanced multi-step prompting and prompt chaining
- Combining multiple AI tools for complex tasks
- Creating your personal prompt template library
- Final Activity: Build your prompt toolkit

> Speaker notes: This final module synthesizes everything. Participants will leave with advanced techniques and a personalized toolkit they can use immediately.

---

## Slide 2: Lesson 1 — Prompt Chaining

**Breaking complex tasks into sequential prompts where each builds on the previous one**

**Single massive prompt (less effective):**
> "Write a complete literature review including themes, studies, gaps, and framework."

**Prompt chain (more effective):**
> Step 1: "Identify 5 key themes"
> Step 2: "For theme 1, outline existing findings"
> Step 3: "Based on these themes, where are the gaps?"
> Step 4: "Suggest a framework addressing these gaps"

> Speaker notes: This is the most advanced technique. It's how professional AI users work on complex tasks.

---

## Slide 3: Why Chaining Works Better

| Single Prompt | Prompt Chain |
|--------------|-------------|
| AI tries to do everything at once | Each step has one clear objective |
| Errors propagate silently | You review and correct at each step |
| Higher hallucination risk | Focused prompts = more reliable output |
| Less control over process | You guide the direction |
| Hope for the best | Iterate based on results |

> Speaker notes: The key benefit is quality control. You can catch and correct errors before they compound.

---

## Slide 4: The Basic Chain Pattern

**Step 1: Outline** → Get the high-level structure

**Step 2: Draft** → Develop each section

**Step 3: Refine** → Improve quality, add detail

**Step 4: Finalize** → Polish and format

> **Review before proceeding to the next step. Garbage from Step 2 propagates to all subsequent steps.**

> Speaker notes: Write this pattern on the board. It applies to almost any complex task — papers, courses, proposals, presentations.

---

## Slide 5: Chain Example — Research Paper

**Step 1 (Outline):**
> "Outline the Discussion section with 5 key points for my TAM study on AI adoption."

**Step 2 (Develop):**
> "Develop Point 1: perceived usefulness was the strongest predictor (beta=0.42). How does this align with existing TAM literature?"

**Step 3 (Refine):**
> "Review this discussion paragraph. Identify logical gaps and suggest stronger connections to theory." [paste draft]

**Step 4 (Polish):**
> "Edit for academic clarity and flow. Maintain my voice." [paste revised text]

> Speaker notes: Walk through each step. Show how the output of each step feeds into the next. The researcher maintains control throughout.

---

## Slide 6: Chain Example — Course Design

**Step 1:** "Suggest a 14-week topic progression for 'AI Applications in Accounting'"

**Step 2:** "For Week 3, create a detailed lesson plan with objectives and activities"

**Step 3:** "Create 5 assessment questions aligned with Week 3's objectives"

**Step 4:** "Review the complete Week 3 package for alignment between objectives, content, and assessment"

> **Each step produces input for the next. You review at each stage.**

> Speaker notes: This example shows chaining for teaching. The quality check in Step 4 is crucial — it catches misalignment.

---

## Slide 7: When to Chain vs. Single Prompt

| Use Chaining | Use Single Prompt |
|-------------|------------------|
| Complex multi-part tasks | Simple, well-defined tasks |
| Quality control needed at each stage | You know exactly what you want |
| Long-form content | Quick lookups or brainstorming |
| Each step depends on previous | One-off requests |

> **Rule of thumb:** If the task has more than 3 parts, chain it.

> Speaker notes: Help participants develop judgment about when chaining adds value. Not every task needs it.

---

## Slide 8: Lesson 2 — Multi-Tool Workflows

**No single AI tool excels at everything. Use the right tool for each sub-task.**

| Tool | Best For |
|------|---------|
| **Perplexity / Elicit** | Finding papers, sourced research |
| **Claude** | Analyzing long documents, nuanced reasoning |
| **ChatGPT** | Writing, brainstorming, creative tasks |
| **Grammarly / Quillbot** | Grammar, style, paraphrasing |
| **Consensus** | Evidence synthesis |

> Speaker notes: Recap from Module 1, now with practical workflow application.

---

## Slide 9: Multi-Tool Workflow — Research Paper

**Stage 1: Discovery** (Perplexity + Elicit)
- Find papers with sourced results
- Identify key studies and consensus

**Stage 2: Analysis** (Claude)
- Analyze long documents (200K context)
- Identify themes across abstracts

**Stage 3: Writing** (ChatGPT)
- Brainstorm outlines, draft sections
- Iterative refinement

**Stage 4: Polish** (Grammarly)
- Grammar, style, academic tone
- Final proofread

> Speaker notes: This is the professional workflow. Each tool does what it's best at. The result is better than any single tool could produce.

---

## Slide 10: Multi-Tool Workflow — Teaching

**Stage 1: Research** (Perplexity)
> "Find recent real-world examples of AI in accounting firms"

**Stage 2: Create** (ChatGPT / Claude)
> "Using these examples, create a case study exercise for students"

**Stage 3: Assess** (ChatGPT)
> "Generate assessment questions aligned with the case study"

**Stage 4: Verify** (Perplexity)
> "Verify these facts used in my teaching materials"

**Stage 5: Polish** (Grammarly)
> Final editing pass

> Speaker notes: The verification step (Stage 4) is critical. Always fact-check teaching materials before presenting to students.

---

## Slide 11: When Multi-Tool Helps vs. Overcomplicates

**Adds value when:**
- Task is complex enough to benefit from specialization
- You need sourced/verified info alongside creative content
- Quality improvement justifies the extra time

**Unnecessary when:**
- Task is simple enough for one tool
- Improvement is marginal
- Overhead exceeds the benefit

> **Learn 2-3 tools deeply rather than 10 superficially.**

> Speaker notes: Practical advice. Most participants should master ChatGPT + one research tool (Perplexity or Elicit) + Grammarly. That covers most needs.

---

## Slide 12: Lesson 3 — Your Prompt Template Library

**The most productive AI users don't write prompts from scratch. They maintain a library of tested templates.**

**Why templates work:**
1. **Consistency** — Best practices baked in
2. **Efficiency** — Fill in placeholders, not write from scratch
3. **Quality** — Refined over time for better results

> **Think of it like document templates — you don't format a paper from scratch each time.**

> Speaker notes: This is the practical takeaway participants will use daily. Templates turn prompt engineering from an art into a repeatable process.

---

## Slide 13: Template Structure

**Every template should include:**

1. **Template name** — What task it's for
2. **When to use** — Brief description
3. **The prompt** — With [PLACEHOLDERS]
4. **Placeholder instructions** — What to fill in
5. **Usage notes** — Tips for best results
6. **Last updated** — Date

> Speaker notes: Show a complete example template. Emphasize placeholder instructions — they're essential for reuse months later.

---

## Slide 14: Example Template — Lesson Plan Generator

> **Name:** Lesson Plan Generator
>
> **Prompt:**
> You are an experienced [SUBJECT] professor using [APPROACH] strategies.
> Create a [DURATION]-minute lesson plan on "[TOPIC]" for [LEVEL] students who [PRIOR KNOWLEDGE].
> Include: [NUMBER] learning objectives, engaging opener, [NUMBER] content segments, one [ACTIVITY TYPE] activity for [CLASS SIZE] students, formative assessment.
> Format: table (Time, Activity, Description, Objective).
> Constraints: [CONSTRAINTS].
>
> **Placeholders:** SUBJECT, APPROACH, DURATION, TOPIC, LEVEL, PRIOR KNOWLEDGE, ACTIVITY TYPE, CLASS SIZE, CONSTRAINTS

> Speaker notes: Walk through filling in each placeholder with a real example. Show how quickly a tested template produces usable output.

---

## Slide 15: Example Template — Paper Feedback

> **Name:** Manuscript Section Reviewer
>
> **Prompt:**
> You are a peer reviewer for a [JOURNAL TYPE] journal in [FIELD]. Read the following [SECTION] of my paper on "[TOPIC]."
> Evaluate: (1) [CRITERION 1], (2) [CRITERION 2], (3) [CRITERION 3], (4) [CRITERION 4].
> For each: (a) what's done well, (b) needs improvement, (c) specific revision suggestion.
> Tone: [TONE].
> [PASTE TEXT]

> Speaker notes: This template works for any paper section — introduction, methods, discussion. The criteria change based on the section.

---

## Slide 16: Organizing Your Library

**Organize by academic function:**

| Category | Templates |
|----------|----------|
| **Teaching** | Lesson plan, quiz creator, rubric designer, concept simplifier, case study generator, feedback provider |
| **Research** | Question refiner, literature summarizer, methodology evaluator, analysis advisor |
| **Writing** | Abstract drafter, section reviewer, reviewer response, cover letter, grant outliner |
| **Admin** | Email drafter, meeting agenda, report outliner |

**Storage:** Document file, spreadsheet, or note app — whatever you'll actually use.

> Speaker notes: Simple is better. A Google Doc with 10 excellent templates beats a complex system with 50 mediocre ones.

---

## Slide 17: Final Activity — Build Your Prompt Toolkit

**Objective:** Create 5 reusable prompt templates tailored to YOUR academic work

**What you'll produce:**
1. Identify your 5 most common AI-assisted tasks
2. Create a complete template for each (with placeholders and instructions)
3. Test each template with real data
4. Refine based on results
5. Organize in an accessible format

**Requirements:** Mix of teaching AND research templates. Use techniques from this training.

**Time:** 45 minutes

> Speaker notes: This is the capstone activity of the entire training. Participants leave with an immediately usable toolkit. Circulate and help with template design.

---

## Slide 18: Activity — Template Format

**For each of your 5 templates, document:**

> **Template Name:** _______________
> **Category:** Teaching / Research / Writing
> **When to Use:** _______________
> **Technique Used:** 5-component / few-shot / chain-of-thought / role-based / chaining
>
> **Prompt:**
> [Your complete prompt with [PLACEHOLDERS]]
>
> **Placeholder Guide:**
> - [PLACEHOLDER 1]: _______________
> - [PLACEHOLDER 2]: _______________
>
> **Usage Notes:** _______________
> **Tested:** Yes / No | **Date:** _______________

> Speaker notes: Provide this as a handout. Having a structured format ensures consistency across all 5 templates.

---

## Slide 19: Activity Debrief and Sharing

**Discussion:**

1. Which template will you use most frequently?
2. How will you store and access your templates?
3. What additional templates would be valuable to create?

**Sharing round:** Each participant shares their ONE best template with the group.

> Speaker notes: The sharing round is valuable — participants learn from each other's templates. Consider creating a shared document where everyone contributes their best template.

---

## Slide 20: Module 10 Summary

**Key Takeaways:**

- **Prompt chaining** breaks complex tasks into sequential, reviewable steps
- **Multi-tool workflows** leverage each tool's strengths for better results
- **Template libraries** make prompt engineering efficient and consistent
- Start with 5 templates for your most common tasks
- Review and update templates regularly

---

## Slide 21: Full Training Recap

**What You've Learned Across All 10 Modules:**

1. How AI and LLMs actually work (and why it matters)
2. The **5-Component Framework**: Role, Context, Task, Format, Constraints
3. Three core techniques: **Few-Shot, Chain-of-Thought, Role-Based**
4. AI for teaching: lesson plans, assessments, slides, feedback
5. AI for research: questions, literature, methodology
6. AI for academic writing: manuscripts, abstracts, reviewer responses
7. **Critical evaluation** and hallucination detection
8. **Ethics, integrity, and data privacy**
9. **Advanced workflows**: chaining, multi-tool, templates

> Speaker notes: Quick recap of the full journey. Emphasize how each module built on the previous ones.

---

## Slide 22: Your AI Toolkit Checklist

**Before you leave, make sure you have:**

- [ ] The 5-Component Framework memorized
- [ ] At least 3 core techniques you can apply immediately
- [ ] 5 tested prompt templates in your toolkit
- [ ] A personal fact-checking workflow
- [ ] An AI use policy (draft) for your context
- [ ] A list of 2-3 AI tools you will use regularly

> Speaker notes: This is a practical checklist. Go through each item and confirm participants have completed it.

---

## Slide 23: What's Next?

**Continue building your AI skills:**

- Practice daily — use AI for at least one task every day this week
- Refine your templates based on real-world use
- Share knowledge with colleagues
- Stay updated — AI tools evolve rapidly
- Revisit the PyLearn track for deeper content on each module

**Resources:**
- PyLearn platform: Access the full track content anytime
- Training materials: Available for reference
- Community: Connect with fellow participants

> Speaker notes: Encourage continued practice. The skill develops with use. Suggest a follow-up session in 4-6 weeks to share experiences.

---

## Slide 24: Thank You

**Leveraging AI for Teaching and Research**

Organized by: **Saypeace Solutions Ltd** in collaboration with **Department of Accounting, Ahmadu Bello University, Zaria**

Thank you for your participation!

> Speaker notes: Close with appreciation. Collect feedback if you have an evaluation form. Remind participants of the PyLearn platform access.
