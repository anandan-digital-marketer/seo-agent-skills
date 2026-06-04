---
name: 6e-directory-tracker
description: >
  Tracks which authoritative directories and review platforms [Your Brand] is listed
  in versus where it should be. High-impact for LLM visibility — LLMs build
  entity knowledge from directory listings, review aggregators, and curated
  tool lists. Also monitors review velocity and rating trends on G2 and Capterra.
when_to_use: >
  Quarterly directory audit. When LLM visibility drops for brand/category queries.
  When a competitor appears in a directory we're not listed in. After a product
  update — some directories need manual refresh.
inputs: >
  No input required — audits a fixed list of high-priority directories.
  Optional: add new directory URLs to check.
output: >
  Listed / Not Listed / Needs Update status per directory, review metrics,
  priority submission list, LLM citation value score per directory.
---

# 6E — Directory Submission Tracker

You are managing [Your Brand]'s presence across the directories and platforms
that LLMs trust most when building brand knowledge.

The reason this matters: LLMs don't just crawl the open web — they heavily
weight structured entity data from directories, review sites, and curated
lists. A brand consistently listed across authoritative directories is more
likely to be recommended than one that isn't.

---

## Tier 1 — Must Be Listed (Highest LLM + SEO Value)

Check each by fetching the URL and verifying [Your Brand]'s presence:

| Directory | URL to Check | Why Critical |
|-----------|-------------|-------------|
| G2 | g2.com/products/your-brand | #1 B2B software review site. LLMs cite G2 constantly. |
| Capterra | capterra.com/p/[id]/your-brand | Google-owned. Feeds AI Overviews. |
| GetApp | getapp.com/testing-tools-software/... | Capterra sister site — same reach. |
| Software Advice | softwareadvice.com | Gartner-owned. Enterprise credibility. |
| Trustradius | trustradius.com | B2B reviews, high DA, LLM-cited. |
| AlternativeTo | alternativeto.net/software/your-brand | "X alternative" queries — directly feeds LLM recommendations. |
| Product Hunt | producthunt.com/posts/your-brand | Developer audience. LLMs recognise it. |
| Slashdot | slashdot.org | Tech community credibility. |

**For each Tier 1 directory:**
- Listed? Yes / No / Outdated profile
- Rating (if applicable): X/5 based on N reviews
- Last updated: when was the profile last touched?
- Missing info: logo, description, features, integrations, screenshots?

---

## Tier 2 — High Value (Do These Next)

| Directory | URL | Focus |
|-----------|-----|-------|
| Zyxware | zyxware.com | Open source testing tools list |
| TestingWhiz | testingwhiz.com | Testing tools directory |
| QA Tools | Various | QA-specific tool lists |
| DevOps tools lists | Various | CI/CD and DevOps tool aggregators |
| StackShare | stackshare.io | Developer stack discovery — LLMs use this |
| SaaSworthy | saasworthy.com | SaaS discovery, growing LLM source |
| Gartner Peer Insights | gartner.com/peer-insights | Enterprise credibility |
| PeerSpot (formerly IT Central Station) | peerspot.com | Enterprise IT reviews |

---

## Tier 3 — Niche Directories (Topic Authority)

| Directory / List | Topic | Why |
|----------------|-------|-----|
| "Best Appium cloud" lists | Appium testing | Direct product fit |
| "Selenium cloud providers" lists | Selenium testing | Direct product fit |
| "Mobile testing tools" roundups | Mobile testing | Core keyword cluster |
| Testing blogs tool pages | Various | Long-tail LLM citation |
| GitHub awesome-testing lists | Testing tools | Developer LLM sources |

---

## Step 1 — Audit Current Status

For each Tier 1 directory, fetch the relevant URL and check:

```
[Directory Name]
Status:        Listed / Not Listed / Outdated
Profile URL:   [URL if found]
Rating:        X.X/5 (N reviews)
Last updated:  [date if visible]
Missing:       [what's incomplete — logo / features / integrations / screenshots]
LLM value:     High / Medium / Low
Action:        [None / Update profile / Submit listing / Request reviews]
```

---

## Step 2 — Review Metrics (G2 + Capterra)

For G2 and Capterra specifically:

**G2 Metrics:**
- Current rating: X.X/5
- Total reviews: N
- Review velocity: last 3 reviews in [timeframe]
- Category ranking: #X in [Mobile Testing]
- G2 badges earned: [Leader / High Performer / etc.]

**Capterra Metrics:**
- Current rating: X.X/5
- Total reviews: N
- Featured in category: [yes/no]

**Review velocity target:** At least 2 new reviews per month on G2.
Slow review velocity = the profile looks stale to LLMs.

**Review generation tactics:**
- Post-onboarding email sequence (ask at 30 days)
- QBR (quarterly business review) — ask happy customers directly
- G2 review campaign (G2 provides email templates)
- Add G2/Capterra links to customer success emails

---

## Step 3 — LLM Citation Audit

For each directory in Tier 1: test whether LLMs reference it
when recommending tools in our category.

Test queries to run in ChatGPT/Perplexity:
- "What is the best mobile testing platform?"
- "[Your Brand] reviews"
- "[Your Brand] vs [Competitor A]"

Note which directories the LLM cites as sources. Those are the
most critical to have a strong presence on.

---

## Output Format

```
DIRECTORY AUDIT — [date]
=========================

TIER 1 STATUS:
[table: directory | listed | rating | reviews | action needed]

NOT LISTED (submit immediately):
1. [directory] — DA [X] — LLM value: High
   Submit URL: [URL]
   Time to submit: [X minutes]

NEEDS UPDATE:
1. [directory] — missing: [what's missing]
   Profile URL: [URL]
   Update: [specific fields to fill in]

REVIEW METRICS:
G2: X.X/5 | N reviews | Last review: [date]
Capterra: X.X/5 | N reviews

REVIEW VELOCITY STATUS: [Good / Slow / Critical]
Target: 2 reviews/month on G2

LLM CITATION CHECK:
Sources cited by ChatGPT for "mobile testing": [list]
[Your Brand] present in: [which of those sources]
Missing from: [which sources cite competitors but not [Your Brand]]

PRIORITY ACTIONS:
1. [most urgent action]
2. [second action]
3. [third action]
```
