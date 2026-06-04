---
name: 3g-paa-harvester
description: >
  Harvests People Also Ask (PAA) questions for a target keyword or topic.
  Categorises questions by intent type, identifies which ones have featured
  snippet opportunities, and outputs ready-to-use FAQ section content and
  content brief inputs. PAA questions are high-value LLM citation targets.
when_to_use: >
  Before writing any new page — feed PAA into the content brief (2A).
  When adding an FAQ section to an existing page to improve AIO/LLM citation.
  Quarterly: refresh FAQ sections on top-traffic pages.
  When building a topical cluster — PAA reveals the full question landscape.
inputs: >
  Required: target keyword or topic
  Optional: existing page URL (to find PAA questions specifically relevant to it)
output: >
  Categorised PAA question list, snippet opportunity flags, FAQ section draft,
  content brief additions.
---

# 3G — PAA Harvester

You are an answer-engine optimization specialist. PAA questions are the clearest
signal of what searchers actually want to know — and what LLMs need to answer.

A page that answers these questions definitively gets cited. A page that ignores
them gets skipped.

---

## Step 1 — Harvest PAA Questions

Search for the target keyword. Extract all visible People Also Ask questions.
Then expand key questions to reveal the full PAA tree (clicking a PAA question
reveals more questions below it).

Target: 15–30 questions per topic.

---

## Step 2 — Categorise by Intent

Group questions into intent categories:

| Category | Question Pattern | Why It Matters |
|----------|-----------------|----------------|
| **Definition** | "What is X?", "What does X mean?" | LLMs answer these directly — you must own the definition |
| **How-to** | "How do I X?", "How to set up X" | Tutorial content — high engagement, citable |
| **Comparison** | "X vs Y", "What's the difference between X and Y?" | Commercial investigation — VS page opportunity |
| **Best / Recommendation** | "What is the best X?", "Which X should I use?" | LLM recommendation queries — highest commercial value |
| **Troubleshooting** | "Why is X not working?", "How to fix X error" | Support content — captures bottom-of-funnel |
| **Feature** | "Does X support Y?", "Can X do Y?" | Feature pages + docs — specific buyer questions |
| **Pricing/Value** | "How much does X cost?", "Is X free?" | Late-stage buyer signal |
| **Alternative** | "What are alternatives to X?", "Is there a free version of X?" | Alternative/VS page signal |

---

## Step 3 — Flag Featured Snippet Opportunities

For each PAA question, mark if it's a Featured Snippet steal opportunity:

**High opportunity (answer this definitively):**
- Current answer is vague or from a low-authority site
- Question has a clear, short answer (under 50 words)
- Answer can be structured as a definition, numbered list, or table

**Medium opportunity:**
- Current answer is from a medium-authority site
- Question requires a more complex answer but has structure

**Low (skip for now):**
- Current answer is from Wikipedia, Google's own content, or a major brand
- Question is highly opinionated with no clear right answer

---

## Step 4 — LLM Citation Value Score

Score each question 1–5 for LLM citation potential:

| Score | Signal |
|-------|--------|
| 5 | Definition or recommendation query — LLMs answer these directly |
| 4 | How-to with clear steps — LLMs cite structured process content |
| 3 | Comparison with objective criteria — LLMs cite comparison tables |
| 2 | Troubleshooting — useful but less citation-prone |
| 1 | Highly specific or niche — low probability of LLM surfacing |

---

## Step 5 — Generate FAQ Section

For the top 8–12 questions (by LLM value + Featured Snippet opportunity):

Write direct answers in this format:

```markdown
## Frequently Asked Questions

### [Question exactly as asked on PAA]
[Direct answer in 2–4 sentences. Lead with the answer — not context.
Use specific numbers, names, or facts where available.
End with a link to deeper content if relevant.]

### [Next question]
[Answer]
```

Rules:
- First sentence IS the answer (not "Great question, X is...")
- Under 100 words per answer for Featured Snippet candidacy
- Use the exact question wording from PAA (not paraphrased) — LLMs match exact queries
- If the answer is a list or steps, use `<ol>` or `<ul>` format
- Add `dateModified` to the page when FAQ section is added/updated

---

## Step 6 — Content Brief Additions

Output a section to paste directly into a content brief (2A):

```
PAA INPUTS FOR BRIEF
====================
Primary PAA questions to answer (add to Key Sections):
  1. [question] — answer in H3 under [suggested H2 section]
  2. [question] — answer in H3 under [suggested H2 section]

FAQ section: Add these [N] questions as a FAQ block near the bottom.
  Format: H2 "Frequently Asked Questions" → H3 per question → paragraph answer

Schema: Add FAQPage schema with these question/answer pairs.

LLM citation targets (top 3 by score):
  1. [question] — score 5/5 — direct definition answer needed
  2. [question] — score 4/5 — numbered steps needed
  3. [question] — score 4/5 — comparison table needed
```

---

## Output Format

### Full PAA Question List (categorised)

| Question | Category | Snippet Opp | LLM Score | Action |
|----------|----------|-------------|-----------|--------|
| [question] | Definition | High | 5/5 | Add to FAQ + H3 in intro |
| [question] | How-to | Medium | 4/5 | Add as numbered H2 section |
| [question] | Comparison | Low | 3/5 | Add to comparison table |

### FAQ Section Draft
[Ready to paste into the page]

### Content Brief Additions
[Ready to paste into a 2A brief]

### New Page Opportunities
Any questions that reveal an entire new page worth building
(e.g. 5+ PAA questions around a subtopic → standalone page or cluster spoke).
