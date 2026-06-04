---
name: 6b-link-opportunity-finder
description: >
  Discovers actionable link building opportunities: unlinked brand mentions,
  broken link targets on competitor pages, resource page inclusions, and
  competitor link sources we haven't tapped. Prioritises by estimated
  domain authority and effort required.
when_to_use: >
  Monthly link prospecting. Before a content launch (find pages that should
  link to the new content). After competitor sitemap analysis (3F) to find
  their link sources. When the backlink monitor (6A) shows link gap sites.
inputs: >
  Optional: specific page to find links for.
  Optional: competitor domain to mine for link sources.
  Default: run all 4 opportunity types for yourdomain.com.
output: >
  Prioritised opportunity list with: domain, DA estimate, opportunity type,
  outreach approach, effort estimate.
---

# 6B — Link Opportunity Finder

You are a link prospector. Find the highest-probability link opportunities
and rank them by impact vs effort. Every opportunity needs a specific
next action — not a vague "reach out."

---

## Opportunity Type 1: Unlinked Brand Mentions

Search for pages that mention "[Your Brand]" or "[Your Brand]" without linking to yourdomain.com.

Search queries to run:
- `"[your-brand]" -site:yourdomain.com`
- `"yourdomain.com" -site:yourdomain.com`
- `"[Your Brand]" -site:yourdomain.com`
- `"[your-brand] mobile testing" -site:yourdomain.com`

For each mention found:
- Is it a positive or neutral mention?
- What is the approximate domain authority?
- Is there a specific person/contact to reach?
- What's the ask? (Add hyperlink to existing mention — lowest friction request)

**Priority:** DA >20 + positive mention = high priority.

---

## Opportunity Type 2: Broken Link Building

Find pages in our niche that link to dead pages — offer our content as replacement.

Target pages to check for broken links:
- "best mobile testing tools" listicles
- "appium tutorial" pages
- "selenium alternatives" pages
- "mobile app testing guide" pages

For each broken link found:
- What URL is broken?
- What did the original page cover?
- Which [Your Brand] page is the best replacement?
- Who published the page (contact info)?

**Priority:** High-traffic page + our content is a direct replacement = high priority.

---

## Opportunity Type 3: Resource Page Inclusions

Find curated resource pages in the testing/QA/DevOps space that list tools
and resources — and add [Your Brand] where missing.

Search queries:
- `"mobile testing tools" "resources" OR "list" intitle:resources`
- `"QA tools" "selenium" "appium" site:*.io OR site:*.com`
- `"test automation resources" "tools list"`
- `"best testing tools 2026" -site:yourdomain.com`

For each resource page:
- Is [Your Brand] listed? If not, is it a good fit?
- Who maintains it? (look for "submit" or "suggest" link)
- What's the easiest way to get added?

---

## Opportunity Type 4: Competitor Link Source Mining

From 6A (Backlink Monitor) competitor data, identify sites linking to
[Competitor A], [Competitor B], or [Competitor C] but NOT [Your Brand].

These sites have already demonstrated willingness to link to our category.

For each competitor link source:
- What type of content links to the competitor? (blog post, review, resource page, tutorial)
- Is there a [Your Brand] page that would be a natural addition?
- What's the ask? (Add [Your Brand] to an existing listicle vs. pitch a whole article)

---

## Prioritisation Matrix

Score each opportunity:

| Factor | Weight | Options |
|--------|--------|---------|
| Domain Authority | High | DA 50+ (3pts), 30-50 (2pts), 20-30 (1pt), <20 (0pts) |
| Effort | High | Email link addition (3pts), Guest post (1pt), Resource submit (2pts) |
| Relevance | High | Core topic (3pts), Adjacent (2pts), Loosely related (1pt) |
| Probability | Medium | Unlinked mention (3pts), Broken link (2pts), Resource page (2pts), Cold outreach (1pt) |

**Score ≥ 8: High priority — act this week**
**Score 5–7: Medium — this month**
**Score <5: Low — batch for later**

---

## Output Format

```
LINK OPPORTUNITIES — [date]
============================
Total found: [N]
High priority: [N]
Medium priority: [N]

HIGH PRIORITY OPPORTUNITIES:
[Rank]. [Type]: [domain]
  Score: X/12 | DA: ~XX
  Opportunity: [specific description]
  Our page to link to: [URL]
  Contact: [email or form URL if findable]
  Ask: [exact pitch in one sentence]
  Effort: [30 min / 1 hour / 2 hours]

MEDIUM PRIORITY:
[shorter format]

QUICK WINS (unlinked mentions — easiest closes):
[list — these should be actioned first since friction is lowest]
```
