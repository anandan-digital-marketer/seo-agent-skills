---
name: 5j-competitor-traffic
description: >
  Estimates competitor organic traffic and share-of-voice using the Semrush MCP
  (already connected) and GSC data. For each competitor domain: estimates monthly
  organic traffic, identifies their top keywords, measures share-of-voice on shared
  keywords, and surfaces where competitors are growing fastest.
  Use quarterly to benchmark against competitors and identify content gaps.
when_to_use: >
  Quarterly competitive benchmarking. Before planning a VS/comparison page campaign.
  When a competitor suddenly gains impressions on keywords you track (from 5I report).
  When the Director report shows impression drops — check if a competitor gained those.
inputs: >
  Competitor domains to analyse (default list: [Competitor A], [Competitor B], [Competitor C],
  HeadSpin, Perfecto). Or specify a single domain.
output: >
  Traffic estimates per competitor, top keywords, share-of-voice on tracked keywords,
  fastest-growing competitor topics, gap opportunities.
---

# 5J — Competitor Traffic Estimator

You are a competitive intelligence analyst. Use the Semrush MCP and GSC data
to estimate how much organic traffic competitors receive and where they are
outperforming [Your Brand].

This is not about exact numbers — Semrush estimates are directionally accurate,
not precise. Use for trend analysis and gap identification, not financial modelling.

---

## Primary Competitors ([Your Brand])

| Competitor | Domain | Tier |
|-----------|--------|------|
| [Competitor A] | browserstack.com | P1 — market leader |
| [Competitor B] | lambdatest.com | P1 — fastest growing |
| [Competitor C] | saucelabs.com | P1 — enterprise |
| HeadSpin | headspin.io | P2 — AI testing |
| Perfecto | perfecto.io | P2 — enterprise |
| TestGrid | testgrid.io | P3 — emerging |

---

## Step 1 — Semrush Traffic Overview

Using the Semrush MCP tool, query each competitor domain for:
- Estimated monthly organic traffic
- Number of organic keywords ranking
- Traffic trend (month-over-month, year-over-year)
- Top 20 organic keywords by traffic

**Semrush MCP query pattern:**
Ask Claude to use the `semrush` MCP tool to pull domain overview data.

For each competitor, collect:
```
Domain:            [competitor.com]
Est. Monthly Traffic: [N]
Organic Keywords:  [N]
Traffic Change MoM: [%]
Top Traffic Keywords:
  1. [keyword] — pos [X] — est. [N] traffic
  2. [keyword] — pos [X] — est. [N] traffic
  ...
```

---

## Step 2 — [Your Brand] Benchmarks

Pull same metrics for yourdomain.com from Semrush for direct comparison.

Build a comparison table:

| Metric | [Your Brand] | [Competitor A] | [Competitor B] | [Competitor C] |
|--------|---------|-------------|-----------|-----------|
| Est. Monthly Traffic | | | | |
| Organic Keywords | | | | |
| MoM Traffic Change | | | | |
| Traffic Index | 1.0x | Xx | Xx | Xx |

**Traffic Index:** Competitor traffic / [Your Brand] traffic. Shows the gap.

---

## Step 3 — Share-of-Voice on Tracked Keywords

For each keyword in `automation/rank-tracker/target-keywords.json`:

Compare [Your Brand]'s GSC position against competitor positions from Semrush.

Apply the CTR curve to estimate traffic share:

| SERP Position | Estimated CTR |
|-------------|--------------|
| 1 | 28–35% |
| 2 | 15–20% |
| 3 | 10–14% |
| 4 | 7–10% |
| 5 | 5–7% |
| 6–10 | 2–5% |
| 11–20 | 0.5–2% |
| 21+ | <0.5% |

**Share-of-voice formula:**
```
SOV% for keyword = (Brand estimated clicks / Total estimated clicks for keyword) × 100
Total estimated clicks = monthly search volume × average CTR at rank 1
```

Output for each keyword:
```
[keyword] (monthly volume: ~N)
  [Your Brand]: pos X.X → est. N clicks/month → SOV X%
  [Competitor A]: pos X → est. N clicks/month → SOV X%
  [Competitor B]: pos X → est. N clicks/month → SOV X%
  Gap: [Competitor A] gets Xx more traffic on this keyword
```

---

## Step 4 — Fastest Growing Competitor Topics

From Semrush, identify which topics each competitor is growing fastest in
(keywords they recently entered top 10 for, or where they gained significant positions).

This signals:
- Topics they're prioritising → we should respond
- Content gaps they've identified → we may also be missing these

**Output:** Top 5 growing topics per competitor with their new rankings.

---

## Step 5 — Gap Opportunities

Cross-reference competitor top keywords vs [Your Brand]'s ranking data:

1. **Competitor ranking in top 10, [Your Brand] not ranking at all** → highest priority gap
2. **Competitor ranking 1–3, [Your Brand] ranking 11+** → competitive content needed
3. **[Your Brand] ranking 1–5, no major competitor** → protect and expand this position

**Opportunity scoring:**
- High: Competitor ranks 1–5, [Your Brand] not ranking, keyword has commercial intent
- Medium: Competitor ranks 1–10, [Your Brand] ranks 11–30
- Low: Both ranking but competitor slightly ahead

---

## Output Format

```
COMPETITOR TRAFFIC ANALYSIS
============================
Date: [YYYY-MM-DD]
Data source: Semrush MCP + GSC

TRAFFIC BENCHMARKS:
[comparison table]

SHARE-OF-VOICE — TRACKED KEYWORDS:
[per-keyword SOV table]
[Your Brand] overall SOV: X%
Largest SOV gaps: [top 5 keywords where we're most behind]

FASTEST GROWING COMPETITOR TOPICS:
[Competitor A]: [top 3 growing topics]
[Competitor B]:   [top 3 growing topics]

GAP OPPORTUNITIES:
High priority:   [N] keywords
Medium priority: [N] keywords
Keywords to protect ([Your Brand] leading): [list]

RECOMMENDED ACTIONS:
1. [specific content to build based on gap analysis]
2. [specific keyword to protect/strengthen]
3. [competitor movement to monitor]
```

---

## Note on Data Accuracy

Semrush organic traffic estimates are directional — typically accurate within
±20-30% of actual traffic. Use for:
- Trend direction (growing vs declining)
- Relative gap size (competitor 3x larger vs 10x larger)
- Keyword opportunity identification

Do not use for: revenue projections, investor reporting, or any
context requiring precise traffic numbers.

Actual [Your Brand] traffic data from GA4 (Task 29) is always more accurate
than Semrush estimates for our own site.
