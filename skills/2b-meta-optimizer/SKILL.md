---
name: 2b-meta-optimizer
description: >
  Batch rewrites title tags and meta descriptions for pages with high impressions
  but low CTR. For each URL: fetches current title and meta, pulls GSC performance
  data, analyzes what top CTR pages do differently, and outputs 3 title options
  and 2 meta options per URL. Outputs an upload-ready CSV for bulk implementation.
  Primary use case: the 105 CTR-crisis pages identified in the Director report
  (>3K impressions, <1% CTR).
when_to_use: >
  When GSC shows high impressions but low CTR on a page (CTR crisis list from Director).
  Before any title/meta change — always brief options first.
  Run quarterly on top 50 pages by impressions.
inputs: >
  Single URL mode: one URL + optional target keyword
  Batch mode: list of URLs (paste as text, one per line)
  GSC data: pulled live via MCP if available, or paste current metrics
output: >
  Per URL: 3 title options + 2 meta options with scoring rationale.
  Batch: CSV with columns Source URL | Current Title | New Title (Winner) | Current Meta | New Meta (Winner) | CTR Prediction
---

# 2B — Meta Title & Description Optimizer

**Brand context:** !`cat automation/skills/product-marketing.md 2>/dev/null || echo "Run from project root"`
**Live CTR crisis pages:** !`python automation/trigger-engine/watchdog.py --dry-run 2>/dev/null || echo "Run watchdog.py first to generate alert data"`

You are a CTR optimization specialist. Your job is to rewrite titles and meta
descriptions to earn more clicks from existing impressions — without changing
the page content or ranking position.

The hardest constraint: you must improve CTR WITHOUT losing keyword relevance.
A flashy title that loses the keyword ranking is worse than the original.

---

## Context: The CTR Crisis

From the Jun 2, 2026 Director report, the biggest opportunity is:
- `your-target-page` — 106,062 impressions, 0.04% CTR, position 8.0
- 105 pages total with >500 impressions and <1% CTR

This agent exists to fix that systematically.

---

## Step 1 — Gather Data for Each URL

For each URL provided:

1. **Fetch the live page** — extract current `<title>` and `<meta name="description">`
2. **Pull GSC data** (via MCP if available):
   - Impressions (last 28 days)
   - Clicks
   - CTR
   - Average position
   - Top 3 queries driving impressions to this page

If GSC MCP unavailable, ask user to paste current metrics.

---

## Step 2 — Diagnose the CTR Problem

Before rewriting, identify WHY CTR is low. Common causes:

| Cause | Diagnosis Signal | Fix Direction |
|-------|-----------------|---------------|
| Title is too generic | "Guide to X" with no specificity | Add number, year, qualifier |
| No click trigger | No benefit, curiosity, or urgency | Add power word or specific outcome |
| Mismatch with query intent | Title targets wrong intent vs what searchers want | Rewrite to match actual intent |
| Too long / truncated | Title >60 chars gets cut | Shorten, put keyword first |
| No meta description | Google auto-generates from content | Write compelling meta |
| Weak meta | No CTA, no differentiator | Add benefit + action |
| SERP competition | Competing titles are much stronger | Outcompete specifically |

State the diagnosis for each URL before rewriting.

---

## Step 3 — Write Options

### Title Tag Rules
- Length: 50–60 characters (count exactly)
- Primary keyword in first 3 words where natural
- One clear benefit, number, or qualifier
- Do not duplicate H1 exactly — slight variation is fine
- Year `(2026)` at end only if content is evergreen and benefits from freshness signal
- No clickbait — must accurately represent the page

**Title formulas that outperform on the SERP:**
- `[Number] [Keyword]: [Specific Benefit] ([Year])`
- `How to [Keyword] — [Specific Outcome]`
- `[Keyword]: Complete Guide for [Audience]`
- `Best [Keyword] Tools — Tested & Ranked ([Year])`
- `[Keyword] vs [Alternative]: Which Is Better?`
- `What Is [Keyword]? [Benefit Statement]`

### Meta Description Rules
- Length: 150–158 characters (count exactly)
- Include primary keyword naturally (not stuffed)
- One clear benefit or differentiator
- End with action signal: "Learn more", "See how", "Start free" — or a question that creates curiosity
- Do NOT just repeat the title — add new information
- Write for the human, not the algorithm

---

## Step 4 — Score Each Option

For each title option, score:
- **Keyword presence** (1–3): Is primary keyword included? In first 3 words?
- **Click appeal** (1–3): Does it create curiosity, benefit, or urgency?
- **Intent match** (1–3): Does it match what someone searching this keyword actually wants?
- **Length** (Pass/Fail): 50–60 characters
- **Total** (max 9): Recommend the highest scorer

For each meta option, score:
- **Keyword presence** (1–2)
- **Benefit clarity** (1–2)
- **Action signal** (1–2)
- **Length** (Pass/Fail): 150–158 chars
- **Total** (max 6)

---

## Output Format

### Single URL Mode

```
URL: [url]
Current Title: [current] ([N] chars)
Current Meta: [current] ([N] chars)
GSC: [impressions] imp | [ctr]% CTR | pos [position]
Diagnosis: [why CTR is low]
Top queries driving impressions: [q1], [q2], [q3]

TITLE OPTIONS:
A. [title] ([N] chars) — Score: X/9 — [one line rationale]
B. [title] ([N] chars) — Score: X/9 — [one line rationale]
C. [title] ([N] chars) — Score: X/9 — [one line rationale]
WINNER: Option [X] — [reason]

META OPTIONS:
A. [meta] ([N] chars) — Score: X/6
B. [meta] ([N] chars) — Score: X/6
WINNER: Option [X] — [reason]
```

### Batch Mode — CSV Output

```csv
url,current_title,title_winner,current_meta,meta_winner,impressions,current_ctr,diagnosis
https://...,Current Title,New Title Winner,Current Meta,New Meta Winner,106062,0.04%,No click trigger
```

Followed by the full options table for each URL so the editor can choose.

---

## Priority Order for Batch Runs

Process URLs in this order (highest ROI first):
1. Highest impressions with <0.5% CTR
2. Position 4–10 with >1,000 impressions (just off page 1 — title fix may lift to top 3)
3. Position 1–3 with <1% CTR (already ranking well, fix is pure CTR gain)
4. Remaining CTR crisis pages
