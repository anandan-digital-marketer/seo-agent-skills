---
name: 5i-rank-tracker
description: >
  Tracks week-over-week SERP position changes for a defined list of priority
  keywords. Pulls live GSC position data, stores history in rank-history.json,
  and outputs a WoW movement report showing keywords gained, lost, stable, and
  newly ranking. Run weekly on the same day for consistent comparisons.
when_to_use: >
  Every Monday (after the SEO Director report). After publishing new content
  targeting tracked keywords. When a core algorithm update is suspected.
  Quarterly review: add new keywords, retire ones no longer relevant.
inputs: >
  No manual input — reads target-keywords.json automatically.
  Optional: --report flag to generate report from stored data without new API call.
output: >
  rank-report-YYYY-MM-DD.md — keywords gained/lost/stable with position deltas.
  rank-history.json — cumulative history (last 26 weeks per keyword).
---

# 5I — Rank Position Tracker

Tracks SERP positions for priority keywords over time. The only way to know
if SEO work is moving the needle — or if a competitor just took your spot.

---

## Run Commands

```powershell
# Pull fresh GSC data and generate report (run weekly)
& ".\automation\gsc\mcp-gsc\.venv\Scripts\python.exe" "automation\rank-tracker\track_ranks.py"

# Generate report from stored history only (no API call)
& ".\automation\gsc\mcp-gsc\.venv\Scripts\python.exe" "automation\rank-tracker\track_ranks.py" --report
```

---

## File Structure

```
automation/rank-tracker/
├── track_ranks.py          <- main script
├── target-keywords.json    <- edit this to add/remove keywords
├── rank-history.json       <- auto-generated, cumulative history
└── output/
    └── rank-report-YYYY-MM-DD.md  <- weekly WoW report
```

---

## Managing Target Keywords

Edit `target-keywords.json` to add or remove keywords.
Keywords are grouped by topic — add new groups or extend existing ones.

Current keyword groups:
- `core_product` — main product keywords
- `automation_frameworks` — Appium, Selenium, Playwright, etc.
- `browser_testing` — cross-browser, Safari, mobile browser
- `emulators` — Android/iOS emulator keywords (high traffic)
- `competitor_adjacent` — alternative/comparison keywords
- `llm_visibility` — keywords we want LLM recommendations for

**To add a new keyword:**
```json
"core_product": [
  "mobile app testing",
  "your new keyword here"
]
```

---

## Reading the Report

### Positions Gained
Keywords that moved up 2+ positions WoW.
Sorted by delta (largest gain first).
**Action:** Note what content changes or links were added that week.

### Positions Lost
Keywords that dropped 2+ positions WoW.
**Action:** Check for algorithm changes, competitor new content, or technical issues.

### New Rankings
Keywords appearing for the first time — either newly published content indexed,
or a page that just crossed the threshold.

### Stable
Movement <2 positions — within normal weekly fluctuation.

---

## Integration with Director Report

The Director report (0A) shows site-wide avg position.
This tracker shows keyword-level movements.

Run both together every Monday:
```
1. collect_outputs.py  (0C)
2. track_ranks.py      (5I) <- add to Monday workflow
3. fetch_data.py       (0A)
4. run_director.py     (0A)
```

The rank report output is picked up by collect_outputs.py (0C) automatically
since it saves to automation/rank-tracker/output/ which is scanned each week.

---

## Interpreting Position Data

GSC "average position" is the mean rank across all queries that showed your
page — this tracks the same keyword weekly for trend analysis.

**Position tiers to watch:**
- 1–3: Page 1 visibility — protect these
- 4–10: Page 1 but below fold — optimise titles (2B) to gain clicks
- 11–20: Page 2 — one strong push can get to page 1
- 21–50: Ranking but far — need content upgrade or links
- Not ranking: Fresh content or keyword not yet targeted

**Alert thresholds:**
- Drop >5 positions in one week → investigate immediately
- Drop >10 positions → possible penalty or major competitor change
- Gain >10 positions → note what caused it — replicate across similar pages
