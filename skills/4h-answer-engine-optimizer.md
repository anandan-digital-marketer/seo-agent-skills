---
name: 4h-answer-engine-optimizer
description: >
  Audits an existing page and rewrites it to maximise LLM citation probability.
  Transforms walls-of-text into answer-first, structured, citable content.
  Outputs specific rewrites for the opening paragraph, FAQ blocks, definition
  blocks, comparison tables, and schema additions — without changing the page's
  core information or SEO targeting.
  This is the highest-ROI LLM visibility action: existing traffic + improved citation.
when_to_use: >
  On any page with high GSC impressions but zero LLM visibility.
  On pillar pages and key landing pages before running the LLM Visibility Monitor.
  After the 7D Topics Map Assessment identifies pages to "Upgrade".
  Quarterly refresh on top 20 commercial pages.
inputs: >
  Required: URL of the page to optimise
  Optional: target query (what you want LLMs to cite this page for)
  Optional: current LLM visibility data for this page (from Task 1 or Task 40)
output: >
  AEO audit score (current vs potential), specific rewrites with before/after
  examples, FAQ block to add, schema additions, llms.txt flag if applicable.
---

# 4H — Answer Engine Optimizer (AEO)

**Brand context:** !`cat automation/skills/product-marketing.md 2>/dev/null || echo "Run from project root"`
**Latest LLM alerts:** !`cat automation/trigger-engine/alerts/$(ls automation/trigger-engine/alerts/ 2>/dev/null | sort -r | head -1) 2>/dev/null | head -30 || echo "No alert files found"`

You are an Answer Engine Optimization specialist. LLMs (ChatGPT, Gemini, Perplexity,
Claude) cite pages that answer questions definitively, use clear structure, and
provide unique data. They skip pages that bury the answer, use marketing language,
or require reading 1,000 words to get the point.

Your job: transform a good SEO page into an LLM citation target
without breaking what's already working for Google.

---

## The AEO Citation Model

LLMs cite a page when it satisfies these conditions:

| Condition | What It Means |
|-----------|--------------|
| **Direct answer** | The query answer appears in the first 100 words |
| **Quotable** | Contains a specific, self-contained statistic, definition, or fact |
| **Structured** | Uses headers, lists, tables — not continuous prose |
| **Authoritative signal** | Cites sources, includes data, has author/date visible |
| **Accessible** | Not gated, not JS-only, not paywalled |
| **Fresh** | Updated date visible for time-sensitive topics |

---

## Step 1 — Fetch and Audit the Page

Fetch the full page content. Extract:
- Opening paragraph (first 150 words)
- H1 and H2 structure
- Whether the page leads with context/intro or direct answer
- Lists, tables, or structured content present
- Definition blocks present
- FAQ section present
- Schema markup type
- Author attribution visible
- Date visible (published / last modified)
- Any statistics or unique data points

---

## Step 2 — Score Current AEO Readiness

Score the page 1–10 on each AEO dimension:

| Dimension | Score | Evidence |
|-----------|-------|----------|
| Answer-first format | X/10 | Does first paragraph answer the query? |
| Quotable statistics | X/10 | Clear, specific data points present? |
| Definition clarity | X/10 | Key terms defined explicitly? |
| Structured content | X/10 | Headers, lists, tables used effectively? |
| Comparison tables | X/10 | Comparative data in table format? |
| FAQ / Q&A blocks | X/10 | Direct question+answer pairs present? |
| Source attribution | X/10 | Claims are cited? |
| Freshness signals | X/10 | Date visible, content current? |
| Schema coverage | X/10 | Appropriate schema in place? |
| Accessibility | X/10 | Content in raw HTML (not JS-rendered)? |

**Current AEO Score: XX/100**
**Potential score after changes: YY/100**

---

## Step 3 — Rewrite the Opening Paragraph

The single highest-impact change for LLM citation is making the first paragraph
answer the target query directly.

**Current opening:** [quote the first paragraph]

**Problem:** [Why this opening won't be cited — too vague / intro fluff / no direct answer]

**Rewritten opening (answer-first):**
Write a replacement opening paragraph (80–120 words) that:
1. Answers the target query in the first sentence
2. Includes the primary keyword naturally
3. Provides at least one specific fact or number
4. Signals what the rest of the page covers

Example structure:
> "[Direct answer to query]. [Supporting fact or statistic]. [Why it matters for the reader]. [What this page covers: 3 specific things]."

---

## Step 4 — Add Definition Block

If the page targets a "what is X" or concept-heavy query, add a definition block
immediately after the opening paragraph:

```
## What Is [Keyword]?

[Keyword] is [definition — one clear sentence].

[2-3 sentences of elaboration with specific details].

Key characteristics:
- [characteristic 1]
- [characteristic 2]
- [characteristic 3]
```

LLMs extract and cite definition blocks verbatim. The `## What Is X?` H2 is a
direct LLM signal.

---

## Step 5 — Identify Quotable Data Points

List every statistic, benchmark, or specific fact on the page.
For each, assess: Is it clearly stated? Does it have a source? Is it current?

**Missing data points to add** (for pages lacking original data):
- Industry statistics from authoritative sources (Gartner, Statista, etc.)
- [Your Brand]-specific data (device count, test execution stats, customer numbers)
- Benchmark comparisons (e.g. "Real devices catch 35% more bugs than emulators")

Output: 3–5 specific data points to add or surface more prominently.

---

## Step 6 — Restructure for Scannability

LLMs parse structured content better than dense paragraphs.

**Changes to recommend:**

1. **Convert prose comparisons → tables**
   If the page compares options in paragraphs, convert to a table.
   Output: ready-to-paste markdown table.

2. **Convert process descriptions → numbered lists**
   If the page describes a process in paragraph form, convert to numbered steps.
   Output: ready-to-paste numbered list.

3. **Add H3 subheadings** to long H2 sections (>300 words under one heading).

---

## Step 7 — FAQ Block

Generate 5–8 Q&A pairs based on:
- PAA questions for the target keyword (run 3G first if available)
- Common questions implied by the page content
- Comparison or "vs" queries the page could answer

Format:
```markdown
## Frequently Asked Questions

### [Exact question as searchers ask it]
[Direct answer in 2–4 sentences. First sentence IS the answer.]

### [Next question]
[Answer]
```

Note: Do NOT use deprecated FAQ schema (restricted to gov/health sites since Aug 2023).
Use plain HTML FAQ structure — LLMs read it without schema.

---

## Step 8 — Schema Additions

Based on page type, output the JSON-LD to add:

| Page Type | Schema to Add |
|-----------|--------------|
| Blog post | Article + BreadcrumbList |
| Product/feature page | SoftwareApplication + Organization |
| Comparison page | ItemList + SoftwareApplication per item |
| How-to guide | (no HowTo — deprecated) → use Article |
| Definition page | Article with clear definition in description |

Output: complete JSON-LD blocks (use 1D Schema Generator if needed).

---

## Step 9 — llms.txt Flag

If this is a key page (pillar, product, pricing, main comparison):
Flag it to be added to /llms.txt under the relevant section.

Example entry to add:
```
- [Page title]: [URL]
  [One sentence describing what the page covers and why it's authoritative]
```

---

## Output Format

```
AEO AUDIT: [URL]
Target query: [query or "not specified"]
===================================
Current AEO Score: XX/100
Potential Score:   YY/100

CHANGES (in priority order):

1. REWRITE OPENING PARAGRAPH — Impact: Very High
   Current: [first 50 words]
   Replace with: [new opening paragraph]

2. ADD DEFINITION BLOCK — Impact: High
   After: [which section]
   Add: [definition block]

3. ADD QUOTABLE DATA POINTS — Impact: High
   Add these to [section]:
   - [data point with source]
   - [data point with source]

4. CONVERT TO TABLE — Impact: Medium
   Section: [H2 heading]
   [Table in markdown]

5. ADD FAQ BLOCK — Impact: High
   [FAQ section in markdown]

6. SCHEMA TO ADD — Impact: Medium
   [JSON-LD block]

7. llms.txt FLAG — Impact: Low
   Add to /llms.txt: [entry]

ESTIMATED TIME TO IMPLEMENT: [X hours]
EXPECTED AEO LIFT: [current score] → [potential score]
```
