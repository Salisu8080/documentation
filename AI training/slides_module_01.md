# Module 1: Understanding AI and Large Language Models
**Estimated Time:** 2.5 hours | **XP Reward:** 600

---

## Slide 1: Module Title

**Understanding AI and Large Language Models**

- Build a practical, non-technical understanding of AI
- Learn how Large Language Models actually work
- Explore the landscape of AI tools for academic work
- Hands-on: Compare AI tools for your academic tasks

> Speaker notes: Welcome participants. This first module establishes the foundation. No technical background needed — we focus on practical understanding that makes you a better AI user.

---

## Slide 2: What is Artificial Intelligence?

**AI is a computer system designed to perform tasks that typically require human intelligence**

- **Artificial Intelligence (AI):** The broad field of building intelligent systems
- **Machine Learning (ML):** AI that learns from data rather than following rules
- **Generative AI:** ML that creates new content (text, images, code)

> When you use ChatGPT, Claude, or Gemini — you are using **Generative AI**

> Speaker notes: Most participants have used AI without understanding what it is. Clarify these three nested terms. Generative AI is what matters most for our training.

---

## Slide 3: Traditional Software vs. AI

| Traditional Software | AI Systems |
|---------------------|------------|
| Follows explicit rules | Learns patterns from data |
| Programmer writes rules | Discovers rules on its own |
| Same output every time | Output can vary |
| Only handles anticipated situations | Can handle novel situations |

> **Key insight for prompt engineering:** Because AI discovers patterns, the way you phrase your request significantly affects the response.

> Speaker notes: This distinction is crucial. Traditional software is deterministic — same input, same output. AI is probabilistic — same input can give different outputs. This is why prompt engineering matters.

---

## Slide 4: What AI Can and Cannot Do

**AI CAN:**
- Generate human-like text (drafts, summaries, explanations)
- Identify patterns in large amounts of information
- Brainstorm ideas and suggest research directions
- Help structure and organize your thoughts

**AI CANNOT:**
- Guarantee factual accuracy
- Replace expert judgment in your field
- Produce genuinely original research insights
- Access real-time information (training cutoff dates)

> Speaker notes: Set realistic expectations early. Neither fear nor blind trust is appropriate. AI is a powerful but imperfect tool.

---

## Slide 5: Common Misconceptions

| Misconception | Reality |
|--------------|---------|
| "AI knows everything" | AI predicts plausible text, not verified facts |
| "AI will replace researchers" | AI augments human capability, not replaces it |
| "AI output is always plagiarism" | Depends on context and transparency |
| "All AI tools are the same" | Different tools have very different strengths |

> Speaker notes: Address these head-on. Many participants hold at least one of these misconceptions (the survey data confirms this). Create a brief discussion moment.

---

## Slide 6: Why Understanding AI Matters for Prompting

**Understanding how AI works explains why certain prompts work better:**

- Specific prompts → Specific responses (more patterns to draw from)
- Context helps AI perform better (better pattern matching)
- AI can be wrong confidently (must always verify)
- Different phrasings → Different results (the art of prompt engineering)

> **The better you understand the tool, the better you can use it.**

> Speaker notes: This is the bridge from "understanding AI" to "prompt engineering." Everything we learn about AI mechanics has practical implications for how we write prompts.

---

## Slide 7: Lesson 2 — How Large Language Models Work

**LLMs predict the next word based on patterns learned from billions of documents**

Think of it this way:
- "The capital of Nigeria is..." → You predict **"Abuja"**
- LLMs do the same thing, but trained on billions of documents
- They can predict continuations for virtually any topic

> **Critical insight:** LLMs do NOT look up facts in a database. They predict statistically likely text.

> Speaker notes: This is the single most important concept for the entire training. Repeat it. LLMs predict — they don't know. This explains hallucinations, which we cover in Module 8.

---

## Slide 8: How LLMs Are Trained

**Three stages of training:**

1. **Pre-training** — Read billions of web pages, books, articles
   - Learn patterns: word relationships, sentence structures, topic connections
2. **Fine-tuning** — Refined to follow instructions and answer helpfully
   - This makes ChatGPT conversational, not just predictive
3. **Alignment** — Human reviewers rate responses
   - Model learns to produce helpful, accurate, appropriate outputs

> Speaker notes: Keep this conceptual. No math. The point is that LLMs learn from text, not from a database of facts. This is why they can be fluent but factually wrong.

---

## Slide 9: Why LLMs "Hallucinate"

**LLMs predict text, they don't retrieve verified facts**

- When asked "Who wrote Things Fall Apart?" → predicts "Chinua Achebe" (correct, common in training data)
- When asked for a specific citation → predicts what a citation *should look like* (may be completely fabricated)

**The AI does not know the difference between truth and plausible fiction.**

> We will cover hallucinations in depth in Module 8.

> Speaker notes: Plant this seed now. Participants need to understand that hallucinations are structural — not bugs, not laziness. It's how the technology works.

---

## Slide 10: Tokens and Context Windows

**Tokens** = basic units LLMs process (~3-4 characters per token)

**Context Window** = maximum tokens in one conversation

| Tool | Context Window | Approximate Words |
|------|---------------|-------------------|
| ChatGPT-4 | 128,000 tokens | ~96,000 words |
| Claude | 200,000 tokens | ~150,000 words |
| Gemini | 1,000,000 tokens | ~750,000 words |
| DeepSeek | 128,000 tokens | ~96,000 words |

**Practical implication:** For very long documents, you may need to break work into smaller pieces.

> Speaker notes: Keep this brief. The practical takeaway is that AI has memory limits within a conversation. Very long tasks may need to be broken up.

---

## Slide 11: How AI "Sees" Your Prompt

**When you type a prompt, here is what happens:**

1. Your text is broken into tokens
2. Each token is converted to numbers
3. The model processes ALL tokens and relationships
4. It predicts the most likely next token
5. Repeats steps 3-4 until the response is complete

**Why this matters for prompt engineering:**
- More context → better predictions
- Roles → shift to relevant expertise patterns
- Examples → AI follows the demonstrated pattern
- Being specific → narrows prediction to what you need

> Speaker notes: The model considers EVERYTHING in your prompt. This is why adding context, roles, and examples changes the output — you're changing which patterns the model draws from.

---

## Slide 12: Lesson 3 — AI Tools Landscape for Academics

**Categories of AI Tools:**

1. **General-Purpose AI Assistants** — ChatGPT, Claude, Gemini, DeepSeek, Perplexity
2. **Research-Specific Tools** — Elicit, Consensus, SciSpace, Semantic Scholar
3. **Writing & Editing Tools** — Grammarly, Quillbot, Wordtune

> Speaker notes: Transition to the practical landscape. Many participants only know ChatGPT. This lesson broadens their toolkit.

---

## Slide 13: General-Purpose AI Tools

| Tool | Best For | Key Strength |
|------|----------|-------------|
| **ChatGPT** | Writing, brainstorming, quizzes | Versatile, large knowledge base |
| **Claude** | Long document analysis, nuanced writing | 200K token context, careful reasoning |
| **Gemini** | Factual queries, Google integration | Access to Google search |
| **DeepSeek** | Analytical tasks, budget-conscious users | Strong reasoning, generous free tier |
| **Perplexity** | Fact-checking, sourced research | Provides citations with answers |

> Speaker notes: Brief overview of each. Encourage participants to try tools they haven't used. No single tool is "best" — it depends on the task.

---

## Slide 14: Research-Specific AI Tools

| Tool | What It Does |
|------|-------------|
| **Elicit** | Finds papers using natural language questions |
| **Consensus** | Shows research consensus ("85% of studies found...") |
| **SciSpace** | Explains complex papers in simple language |
| **Semantic Scholar** | AI-powered paper discovery + citation analysis |

**Why these matter:** They are purpose-built for academic research and reduce hallucination risk compared to general AI.

> Speaker notes: Many participants won't have heard of these. If possible, do a quick live demo of Elicit or Consensus. These tools are game-changers for research.

---

## Slide 15: Choosing the Right Tool

| Task | Recommended Tool |
|------|-----------------|
| Literature discovery | Perplexity, Elicit, Consensus |
| Drafting & writing | ChatGPT, Claude |
| Teaching content | ChatGPT, Claude |
| Methodology guidance | Claude, ChatGPT |
| Fact-checking | Perplexity, Google Scholar |
| Grammar & editing | Grammarly, Quillbot |
| Long document analysis | Claude |

> **Use multiple tools rather than relying on one.**

> Speaker notes: The key takeaway is tool selection by task. This table can be a handout for participants.

---

## Slide 16: Data Privacy Reminder

**Before using any AI tool, consider:**

- What data am I inputting?
- Could it be seen by the company or used for training?
- Would it be acceptable if this data became public?

**Never input:** Student data, unpublished research data, exam papers, confidential information

> We cover data privacy in depth in Module 9.

> Speaker notes: Brief but important. Plant the privacy awareness seed now. Many participants are unaware that their inputs may be stored or used for training.

---

## Slide 17: Activity — Explore and Compare AI Tools

**Objective:** Experience how different AI tools respond to the same academic question

**What you'll do:**
1. Choose an academic question from your field (something you know the answer to)
2. Ask the same question to 2-3 different AI tools
3. Compare: accuracy, detail, usefulness, format
4. Document your findings

**Time:** 45 minutes

> Speaker notes: Guide participants through the activity. Circulate and help those who are new to certain tools. Encourage them to use the same prompt in each tool for fair comparison.

---

## Slide 18: Activity — Suggested Questions

**Pick one or create your own:**

- "What are the key differences between IFRS and GAAP?"
- "Explain the principal-agent problem in corporate governance"
- "What research methods are most appropriate for studying organizational behavior?"
- "Describe the concept of double-entry bookkeeping for beginners"

**Use this prompt format:**
> You are a university lecturer in [your field]. Explain [your topic] for second-year undergraduate students. Include a practical example and note common misconceptions.

> Speaker notes: Having pre-written options helps beginners get started. Encourage experienced users to use their own questions.

---

## Slide 19: Activity — Comparison Template

| Criteria | Tool 1: _____ | Tool 2: _____ | Tool 3: _____ |
|----------|--------------|--------------|--------------|
| Length & detail | | | |
| Accuracy | | | |
| Example quality | | | |
| Misconceptions addressed? | | | |
| Overall usefulness | | | |

> Speaker notes: Provide this as a handout or display on screen. Structured comparison helps participants think systematically rather than just saying "this one is better."

---

## Slide 20: Debrief and Discussion

**Discussion Questions:**

1. Which tool gave the most useful response? Why?
2. Did any tool produce information you know to be inaccurate?
3. Were you surprised by any differences?
4. Which tool(s) will you use most in your work?

**Key takeaway:** Different tools have different strengths. The best approach is to use the right tool for each task.

> Speaker notes: Facilitate a group discussion. Ask 3-4 participants to share their findings. Highlight that tool choice matters — this sets up the multi-tool workflow we cover in Module 10.

---

## Slide 21: Module 1 Summary

**Key Takeaways:**

- AI predicts text based on patterns — it does not "know" facts
- Understanding AI mechanics explains why prompt engineering works
- Different AI tools excel at different tasks
- Research-specific tools (Elicit, Consensus) reduce hallucination risk
- Always verify AI-generated factual claims
- Consider data privacy before inputting information

**Next Module:** Foundations of Prompt Engineering — The 5-Component Framework
