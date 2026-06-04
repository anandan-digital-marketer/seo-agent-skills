---
name: 6a-backlink-monitor
description: >
  Tracks new and lost backlinks for yourdomain.com and top competitors using
  the Semrush MCP (already connected). Weekly comparison: which sites linked
  to us this week, which links were lost, and what competitors gained.
  Outputs a prioritised link intelligence report with action items.
when_to_use: >
  Weekly — run after the Director report (0A). When a traffic drop is unexplained
  (lost links may be the cause). After a PR campaign or content launch to verify
  links were earned. Quarterly deep audit vs competitors.
inputs: >
  No manual input for weekly run. Domain defaults to yourdomain.com.
  Optional: add competitor domains for comparison.
output: >
  New links gained this week, links lost, competitor link movements,
  highest-authority new links to acknowledge, links to reclaim.
---

# 6A — Backlink Monitor

You are a link intelligence analyst. Backlinks are the single strongest
ranking signal — and losing them silently is one of the most common causes
of unexplained traffic drops.

---

## Step 1 — Pull [Your Brand] Backlink Data

Using the Semrush MCP, query backlink data for `yourdomain.com`:
- New referring domains (last 7 days)
- Lost referring domains (last 7 days)
- Total referring domain count (current vs 30 days ago)
- Top new backlinks by domain authority
- Anchor text distribution (top 10 anchors)

---

## Step 2 — Pull Competitor Backlink Data

For each competitor, pull new links gained this week:

Priority competitors:
1. `browserstack.com` — market leader
2. `lambdatest.com` — fastest growing
3. `saucelabs.com` — enterprise

For each: new referring domains gained this week + estimated domain authority.
This reveals where they're getting links from — potential opportunities for us.

---

## Step 3 — Classify New Links

For each new link [Your Brand] gained:

| Quality | Signal | Action |
|---------|--------|--------|
| **High value** | DA >40, editorial, relevant topic | Acknowledge if possible (social share, thank) |
| **Medium** | DA 20-40, niche relevant | Note for relationship building |
| **Low** | DA <20, generic, spammy pattern | Flag for disavow review if pattern emerges |
| **Concerning** | Unnatural anchor text, PBN patterns | Add to disavow watch list |

---

## Step 4 — Lost Links Analysis

For each lost link:

| Cause | Signal | Fix |
|-------|--------|-----|
| Page deleted | Source URL returns 404 | Reach out, offer updated resource |
| Our page redirected | Our target URL changed | Update redirect chain |
| Content replaced | Source page now links to competitor | Outreach to reclaim |
| Natural removal | Site redesign, content update | Low priority |

Flag lost links from DA >30 sites as **high priority to reclaim**.

---

## Step 5 — Competitor Link Source Intelligence

From competitor new links: identify which domains are linking to multiple
competitors but not to [Your Brand]. These are validated link sources in our niche
that are already willing to link to our category.

Output: "Link gap sites" — sites linking to [Competitor A] or [Competitor B]
but not to [Your Brand]. These are the warmest outreach targets.

---

## Output Format

```
BACKLINK MONITOR — Week of [date]
==================================

[YOUR BRAND] LINK SUMMARY:
  Total referring domains: [N] ([+X/-X] vs last week)
  New links this week:     [N]
  Lost links this week:    [N]
  Net change:              [+X/-X]

NEW LINKS GAINED:
  High value ([N]):
    [DA XX] [domain] → [our page] | Anchor: "[text]"

  Medium ([N]):
    [DA XX] [domain] → [our page]

  Flag for review ([N]):
    [domain] — reason: [suspicious pattern]

LOST LINKS — ACTION NEEDED:
  [DA XX] [domain] — last linked to [our page]
  Cause: [reason] | Priority: [High/Medium/Low]
  Action: [specific outreach step]

COMPETITOR NEW LINKS THIS WEEK:
  [Competitor A]: +[N] new domains | Top source: [domain]
  [Competitor B]:   +[N] new domains | Top source: [domain]
  [Competitor C]:   +[N] new domains | Top source: [domain]

LINK GAP OPPORTUNITIES (link to competitors, not [Your Brand]):
  1. [domain] — links to [competitor], DA [X] — [why it's worth targeting]
  2. [domain] — links to [competitor], DA [X]

ANCHOR TEXT HEALTH:
  Branded ("[your-brand]", "yourdomain.com"): [%] — target: >40%
  Generic ("click here", "this"): [%] — target: <5%
  Keyword-rich: [%] — target: 20-40%
  Other: [%]

ACTIONS THIS WEEK:
  1. Reclaim: [specific lost link to pursue]
  2. Outreach: [link gap site to contact]
  3. Acknowledge: [high-value new link to thank]
```
