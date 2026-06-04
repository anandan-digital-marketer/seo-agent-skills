---
name: 6f-entity-builder
description: >
  Tracks and grows [Your Brand]'s entity presence — the structured knowledge that
  LLMs and Google use to understand what the brand IS. Covers Wikipedia/Wikidata
  eligibility, Google Knowledge Panel status, brand mentions on authority sites,
  and the entity signals that determine whether LLMs confidently recommend the brand.
  Entity strength is the root cause of LLM visibility — brands with strong entities
  get recommended; brands without them get skipped.
when_to_use: >
  Quarterly entity audit. When LLM visibility is low despite good content.
  When Google Knowledge Panel is missing or incomplete. When the brand changes
  its name, category, or positioning. Before a major PR campaign.
inputs: >
  Domain and brand name (defaults to [Your Brand] / yourdomain.com).
output: >
  Entity strength score, Wikipedia/Wikidata status, Knowledge Panel audit,
  brand mention analysis, entity signal gaps, build priority list.
---

# 6F — Entity Building Tracker

You are an entity SEO strategist. The shift from keyword matching to entity
understanding is the most important change in both Google and LLM search.

An entity is what a brand IS in the knowledge graph — not just what pages it has.
LLMs trained on entity-rich data confidently recommend brands.
LLMs trained on sparse entity data say "I'm not sure, but maybe try [Competitor A]."

---

## What Makes a Strong Entity

Google and LLMs build entity knowledge from:

| Source | Weight | [Your Brand] Status |
|--------|--------|---------------|
| Wikipedia article | Very High | Check |
| Wikidata entry | High | Check |
| Google Knowledge Panel | Very High | Check |
| Crunchbase profile | High | Check |
| LinkedIn company page | High | Check |
| Social profiles (sameAs) | Medium | Check |
| News mentions (authority sites) | High | Check |
| Directory listings (G2, Capterra) | Medium | See 6E |
| Consistent NAP (Name, Address, Phone) | Medium | Check |
| Schema Organization markup | Medium | See 1D |

---

## Step 1 — Wikipedia & Wikidata Audit

### Wikipedia
Search `en.wikipedia.org/wiki/[Your Brand]` and `en.wikipedia.org/wiki/[Your Brand]`.

**If no article exists:**
- Check Wikipedia's notability criteria for software companies
- Has [Your Brand] been covered in notable publications (TechCrunch, VentureBeat, etc.)?
- Are there enough third-party citations to support a stub article?
- If eligible: draft a neutral stub (not marketing copy)

**If article exists:**
- Is it up to date?
- Does it link to yourdomain.com?
- Are all facts accurate?
- Is the company correctly categorised?

### Wikidata
Search `wikidata.org` for "[Your Brand]".

**Key Wikidata properties to have:**
- P31 (instance of): software company / cloud computing service
- P856 (official website): https://www.yourdomain.com
- P17 (country): India
- P112 (founded by): [founders]
- P571 (inception): [year founded]
- P154 (logo image): [logo URL]
- P749 (parent organization): [if part of larger group]
- P856: yourdomain.com

**Wikidata is directly parsed by many LLMs.** A correct Wikidata entry
significantly improves brand recognition in AI-generated answers.

---

## Step 2 — Google Knowledge Panel

Search Google for "[Your Brand]" and "yourdomain.com".

Does a Knowledge Panel appear on the right side of results?

**If yes — audit the panel:**
- Is the description accurate and up to date?
- Is the logo correct?
- Is the founding date correct?
- Are social profiles linked?
- Is the HQ location correct?
- Are any competitors listed as "people also search for"?

To update an incorrect Knowledge Panel:
- Go to the panel → "Suggest an edit"
- Schema markup on yourdomain.com/about/ helps Google verify corrections
- Wikidata corrections are reflected in Knowledge Panels (usually 2-4 weeks)

**If no Knowledge Panel exists:**
Signals needed to trigger one:
- Consistent mentions across high-DA sites
- Wikidata entry
- Organization schema with sameAs on yourdomain.com
- Google Business Profile (if applicable)

---

## Step 3 — Brand Mention Audit

Search for [Your Brand] mentions across authority sites:

| Category | Search Query |
|----------|-------------|
| Tech media | `"[your-brand]" site:techcrunch.com OR site:venturebeat.com OR site:infoq.com` |
| Industry analysts | `"[your-brand]" site:gartner.com OR site:forrester.com` |
| Developer sites | `"[your-brand]" site:dev.to OR site:medium.com OR site:dzone.com` |
| Testing communities | `"[your-brand]" site:testingwhiz.com OR site:ministryoftesting.com` |
| News | `"[your-brand]" after:2025-01-01` (recent coverage) |

**For each mention found:**
- Is it positive, neutral, or negative?
- Is the brand spelled correctly ([Your Brand] not [Your Brand])?
- Is there a link to yourdomain.com?
- Is the mention from a high-DA source that LLMs would trust?

---

## Step 4 — sameAs Schema Audit

The Organization schema's `sameAs` property tells Google and LLMs which
profiles belong to the brand. Check yourdomain.com for Organization schema
(run 1D — Schema Generator if needed).

**Required sameAs entries:**
```json
"sameAs": [
  "https://www.linkedin.com/company/your-brand",
  "https://twitter.com/your-brand",
  "https://github.com/your-brand",
  "https://www.g2.com/products/your-brand",
  "https://www.capterra.com/p/[id]/your-brand",
  "https://www.crunchbase.com/organization/your-brand",
  "https://en.wikipedia.org/wiki/[Your Brand]"
]
```

Missing entries = entity signal gaps.

---

## Step 5 — Entity Strength Score

Score [Your Brand]'s entity strength 1-100:

| Factor | Max | Score |
|--------|-----|-------|
| Wikipedia article exists | 15 | |
| Wikidata entry with key properties | 10 | |
| Google Knowledge Panel present | 15 | |
| Knowledge Panel accurate + complete | 10 | |
| sameAs profiles all linked in schema | 10 | |
| News/media mentions (authority sites) | 15 | |
| Consistent brand name across web | 10 | |
| Director + team profiles (LinkedIn) | 5 | |
| Brand mentions with correct spelling | 10 | |
| **Total** | **100** | |

**Score interpretation:**
- 80-100: Strong entity — LLMs confidently recommend
- 60-79: Moderate — LLMs know the brand but with uncertainty
- 40-59: Weak — LLMs may mention but unsure, may say "I think"
- <40: Minimal — LLMs unlikely to recommend without strong content signals

---

## Output Format

```
ENTITY AUDIT: [Your Brand]
======================
Date: [YYYY-MM-DD]
Entity Strength Score: XX/100

WIKIPEDIA: [Exists / Missing / Outdated]
  URL: [if exists]
  Action: [None / Update / Create stub]

WIKIDATA: [Exists / Missing / Incomplete]
  URL: [if exists]
  Missing properties: [list]
  Action: [None / Add properties / Create entry]

KNOWLEDGE PANEL: [Present / Missing / Inaccurate]
  Accuracy issues: [list if any]
  Action: [suggest edits / build signals]

sameAs COVERAGE: [N/8 profiles linked]
  Missing: [which profiles not in schema]

BRAND MENTIONS:
  Authority sites: [N mentions found]
  Top sources: [list]
  Missing from: [sites that mention competitors but not [Your Brand]]

PRIORITY BUILD ACTIONS:
1. [Most impactful action]
2. [Second action]
3. [Third action]

ESTIMATED ENTITY LIFT: +X points in [timeframe] if actions completed
```
