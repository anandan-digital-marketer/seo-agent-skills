---
name: 6c-vs-page-generator
description: >
  Generates SEO-optimised competitor comparison pages: "X vs Y" head-to-head,
  "Alternatives to X" listicles, and "Best [Category] Tools" roundups.
  These pages target high-commercial-intent searchers in evaluation mode and
  are among the highest LLM citation content types. Two use cases:
  (A) "[Your Brand] vs [Competitor]" — direct comparison favouring [Your Brand],
  (B) "[Competitor A] vs [Competitor B]" — where [Your Brand] appears as the
  recommended alternative for searchers who don't love either option.
when_to_use: >
  Before building any VS or alternative page. When competitor traffic analysis
  (5J) shows high-volume comparison keywords. When topical cluster builder (3H)
  identifies comparison pages as missing spokes.
inputs: >
  Page type: A ([Your Brand] vs Competitor), B (Competitor vs Competitor), or C (Alternatives list)
  Competitor name(s) and domain(s)
  Optional: specific differentiators to highlight
output: >
  Complete page content in markdown, feature comparison table, schema markup,
  meta tags, keyword strategy, CTA suggestions.
---

# 6C — VS Page Generator

**Brand context:** !`cat automation/skills/product-marketing.md 2>/dev/null || echo "Run from project root"`
**Today's date (for pricing disclaimers):** !`date +%B\ %Y 2>/dev/null || powershell -Command "Get-Date -Format 'MMMM yyyy'"`

You are a conversion-focused content strategist. VS pages attract searchers
in active evaluation mode — the highest-intent audience in SEO.

Build a page that is factually accurate, genuinely useful, and honest about
tradeoffs. Fake comparisons that only favour one side rank poorly because
they have high bounce rates — readers can tell.

---

## Page Type Selection

### Type A: "[Your Brand] vs [Competitor]"
**Target keyword:** `pcloudy vs [competitor]`
**Intent:** User knows both products, wants a direct comparison
**Winner framing:** [Your Brand] wins for [specific use case]. Honest about where competitor is stronger.

### Type B: "[Competitor A] vs [Competitor B]"
**Target keyword:** `[competitor A] vs [competitor B]`
**Intent:** User is choosing between two competitors — doesn't know [Your Brand] exists
**[Your Brand] angle:** Both have limitations → "There's a third option worth considering"
Place [Your Brand] in the conclusion as the recommended alternative for specific use cases.

### Type C: "Alternatives to [Competitor]" or "Best [Category] Tools"
**Target keyword:** `[competitor] alternatives`, `best mobile testing tools`
**Intent:** User is unhappy with current tool or exploring the category
**[Your Brand] angle:** Position as the best alternative for [specific ICP]

---

## Step 1 — Research the Competitor

Fetch the competitor's website. Extract:
- Main product features and positioning
- Pricing tiers (note the date — pricing changes)
- Target audience claims
- G2/Capterra rating and review count
- Key differentiators they claim

Note everything with "as of [month year]" — comparison pages go stale fast.

---

## Step 2 — Build Feature Comparison Table

Identify the 10 most important features for the target audience (QA teams, mobile developers):

| Feature | [Your Brand] | [Competitor] |
|---------|---------|-------------|
| Real device count | 5,000+ | [fetch from their site] |
| Android support | Yes | [fetch] |
| iOS support | Yes | [fetch] |
| Appium support | Yes | [fetch] |
| Selenium support | Yes | [fetch] |
| Playwright support | Yes | [fetch] |
| Parallel test execution | Yes | [fetch] |
| CI/CD integrations | 50+ | [fetch] |
| AI testing agents | Yes (QPilot, QuantumRun, Self-Healing) | [fetch] |
| Free trial | Yes | [fetch] |
| G2 rating | [pull from G2] | [pull from G2] |
| Pricing (starting) | [from pricing page] | [from their pricing page] |

Use: ✅ Yes / ❌ No / ⚠️ Limited / 🔶 Paid add-on

---

## Page Structure (Type A: [Your Brand] vs Competitor)

**Target keyword:** `pcloudy vs [competitor]`
**Title formula:** `[Your Brand] vs [Competitor]: [Key Differentiator] ([Year])`
**Minimum word count:** 1,500 words

```
1. QUICK VERDICT (above fold — 100 words)
   "Choose [Your Brand] if [use case]. Choose [Competitor] if [use case]."
   No winner-takes-all framing — specific use case guidance.

2. OVERVIEW (200 words)
   Brief intro to both products. Neutral tone. What each does best.

3. FEATURE COMPARISON TABLE
   [full table from Step 2]

4. DEEP DIVE SECTIONS (one H2 per key differentiator)
   - Device Coverage & Real Devices
   - Test Automation Framework Support
   - AI-Powered Testing Features
   - CI/CD & DevOps Integration
   - Pricing Comparison
   - Support & Documentation

5. WHO SHOULD CHOOSE PCLOUDY
   Specific use cases where [Your Brand] wins:
   - Teams needing real device testing at scale
   - Appium/Selenium/Playwright users wanting cloud execution
   - Teams needing AI testing agents (QPilot, self-healing)
   - BFSI/fintech teams needing compliance-grade testing

6. WHO SHOULD CHOOSE [COMPETITOR]
   Honest assessment. If you're dishonest, readers bounce.
   E.g. "[Competitor A] if you need the largest browser matrix"

7. FINAL VERDICT + CTA
   "For most mobile testing teams... [Your Brand] is the better choice because..."
   Primary CTA: "Start Free Trial" | Secondary: "Book a Demo"

8. FAQ (5-6 questions)
   Pull from PAA (3G) for this comparison keyword.
   Include: "Is [Your Brand] cheaper than [competitor]?", "Can I migrate from [competitor]?"
```

---

## Page Structure (Type B: Competitor A vs Competitor B)

**Target keyword:** `[competitor A] vs [competitor B]`
**Title:** `[Competitor A] vs [Competitor B]: [Key Difference] ([Year])`
**Strategy:** Impartial comparison. [Your Brand] appears at the end as "third option."

```
1. QUICK VERDICT — who each is best for
2. OVERVIEW of both competitors
3. FEATURE COMPARISON TABLE (no [Your Brand] column — keep it independent)
4. DEEP DIVE SECTIONS
5. WHO SHOULD CHOOSE [A] vs [B]
6. WAIT — CONSIDER A THIRD OPTION
   "If neither quite fits, [[Your Brand]] offers [specific advantage]:
   [2 sentences max — keep subtle. Don't make this page about [Your Brand].]"
7. FINAL VERDICT
8. FAQ
```

---

## Page Structure (Type C: Alternatives List)

**Title:** `[N] Best [Competitor] Alternatives in [Year] (Free & Paid)`
**Minimum word count:** 2,000 words

```
1. WHY LOOK FOR ALTERNATIVES (factual pain points, not attacks)
2. COMPARISON TABLE (all alternatives, key features)
3. ALTERNATIVES LIST (min 6, [Your Brand] first or in top 3)
   For each: Best for / Pricing / Pros / Cons / Link
4. HOW TO CHOOSE (decision framework)
5. FINAL RECOMMENDATION + CTA
6. FAQ
```

---

## Schema Markup

### For VS pages (Type A & B): SoftwareApplication per product

```json
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "[Your Brand]",
  "applicationCategory": "DeveloperApplication",
  "operatingSystem": "Web",
  "offers": {"@type": "Offer", "price": "0", "priceCurrency": "USD"},
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "[G2 rating]",
    "reviewCount": "[G2 review count]",
    "bestRating": "5"
  }
}
```

### For alternatives pages (Type C): ItemList

```json
{
  "@context": "https://schema.org",
  "@type": "ItemList",
  "name": "Best [Competitor] Alternatives [Year]",
  "numberOfItems": [N],
  "itemListElement": [{"@type": "ListItem", "position": 1, "name": "[Your Brand]", "url": "https://www.yourdomain.com"}]
}
```

---

## Priority VS Pages to Build

Based on competitor data and keyword volume:

| Page | Type | Target Keyword | Priority |
|------|------|---------------|----------|
| [Your Brand] vs [Competitor A] | A | pcloudy vs browserstack | 🔴 High |
| [Your Brand] vs [Competitor B] | A | pcloudy vs lambdatest | 🔴 High |
| [Competitor A] vs [Competitor B] | B | browserstack vs lambdatest | 🔴 High (high volume) |
| [Competitor A] vs [Competitor C] | B | browserstack vs sauce labs | 🟡 Medium |
| [Competitor A] Alternatives | C | browserstack alternatives | 🔴 High |
| [Competitor B] Alternatives | C | lambdatest alternatives | 🟡 Medium |
| Best Mobile Testing Tools | C | best mobile testing tools | 🔴 High |

---

## Trust & Legal Guidelines

- All competitor data must be sourced from their public website
- Add "as of [Month Year]" to all pricing information
- State clearly which product is [Your Brand]'s
- Never make false or exaggerated claims about competitors
- Plan to review quarterly — pricing and features change
