# SEO Agent Skills

> 29 AI agent skills for SEO, LLM visibility, technical auditing, and GEO optimization.
> Works with Claude Code, Cursor, Codex, and any Agent Skills-compatible platform.

[![Skills](https://img.shields.io/badge/skills-29-blue)](https://github.com/anandan-digital-marketer/seo-agent-skills)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-orange)](https://agentskills.io)

---

## Install

```bash
npx skills add anandan-digital-marketer/seo-agent-skills
```

Skills install to `.agents/skills/` and auto-symlink to Claude Code, Cursor, and Codex.

---

## What Makes This Different

Most Claude Code + SEO setups rely on CSV exports and static prompts.
These skills are built for **live data** — connecting directly to GSC, GA4, Semrush,
and rank history via MCP servers. No manual exports. No copy-paste.

| Capability | Standard approach | This pack |
|-----------|------------------|-----------|
| SEO data | Manual CSV export | Live MCP — GSC + GA4 + Semrush |
| LLM / GEO visibility | Not covered | 3 dedicated skills (AEO, llms.txt, crawler audit) |
| Feedback loop | Not covered | Outcome tracking — measures if fixes worked |
| Authority building | Generic | Full 7-skill track (backlinks, entity, reviews, VS pages) |
| Nervous system | Not covered | Watchdog + action executor patterns included |

---

## What's Covered — All 9 Functions

```
Strategy      → keyword scoring, SERP analysis, competitor intel, topical clusters
Content       → content briefs, meta optimization, internal linking, freshness audit
Technical SEO → page scoring, schema generation, redirects, sitemap management
LLM / GEO     → answer engine optimization, llms.txt, AI crawler audit
Analytics     → rank tracking, competitor traffic, live GSC/GA4 via MCP
Authority     → backlink monitoring, link prospecting, VS pages, entity building
CRM / Leads   → lead enrichment, ICP scoring, outreach angles
Social        → content repurposing, post performance tracking
Direction     → weekly director — orchestrates all agents, prioritizes actions
```

---

## Skills Index (29 skills)

### Agent 0 — Director
| Skill | What It Does |
|-------|-------------|
| `seo-director` | Weekly orchestrator — reads live GSC+GA4, outputs prioritized action plan, agent deployment schedule, risk flags |

### Agent 1 — Technical SEO
| Skill | What It Does |
|-------|-------------|
| `1b-single-page-scorer` | Deep audit on one URL — 8 categories, scored /100, schema opportunities, AI citation readiness |
| `1d-schema-generator` | Generates complete JSON-LD from scratch — 5 templates, deprecated type checker |
| `1m-redirect-implementation` | Converts redirect plan to .htaccess + Nginx + WordPress Redirection CSV |
| `1n-sitemap-manager` | Validate existing sitemap or generate fresh one with GSC comparison |

### Agent 2 — Content & On-Page
| Skill | What It Does |
|-------|-------------|
| `2a-content-brief-generator` | Keyword → 10-point brief including LLM citation optimizations + cannibalization check |
| `2b-meta-optimizer` | Diagnoses WHY CTR is low, then 3 title + 2 meta options per URL, batch CSV output |
| `2c-internal-linking-strategist` | 20 specific source→target link pairs with exact anchor text + topic cluster map |
| `2d-content-freshness-auditor` | Staleness score based on age × topic volatility, GSC trend check, refresh instructions |

### Agent 3 — Strategy & Keywords
| Skill | What It Does |
|-------|-------------|
| `3b-keyword-scorer` | 5-dimension scoring (intent, difficulty, volume, fit, SERP opp) → Quick Win / Medium / Long tiers |
| `3c-serp-analysis` | Full page-1 map, SERP features, AI Overview triggers, difficulty 1–100, exact content spec |
| `3f-competitor-sitemap-analyst` | Reverse-engineers competitor site architecture → 5 moves to match, 5 gaps to attack |
| `3g-paa-harvester` | Harvests + categorizes PAA questions, writes FAQ section, flags LLM citation targets |
| `3h-topical-cluster-builder` | Hub/spoke map per topic, missing spokes, LLM citation gaps, internal link actions |

### Agent 4 — LLM Visibility & GEO
| Skill | What It Does |
|-------|-------------|
| `4h-answer-engine-optimizer` | AEO audit score, rewrites opening paragraph, adds FAQ block, schema — makes pages LLM-citable |
| `4i-llms-txt-manager` | Generates/audits /llms.txt + /llms-full.txt for AI crawler guidance |
| `4j-ai-crawler-auditor` | Audits robots.txt — which AI bots are allowed/blocked, citation impact per crawler |

### Agent 5 — Analytics
| Skill | What It Does |
|-------|-------------|
| `5i-rank-tracker` | Track keyword positions WoW via GSC, 26-week history, movement alerts |
| `5j-competitor-traffic` | Estimate competitor organic traffic via Semrush MCP + share-of-voice analysis |

### Agent 6 — Authority & Links
| Skill | What It Does |
|-------|-------------|
| `6a-backlink-monitor` | New/lost links, competitor link movements, link gap sites (warm outreach targets) |
| `6b-link-opportunity-finder` | 4 opportunity types scored by DA × effort: unlinked mentions, broken links, resources, competitor sources |
| `6c-vs-page-generator` | Build "X vs Y", "Alternatives to X", "Best [Category] Tools" pages with schema |
| `6d-outreach-drafter` | 4 outreach email templates, 80–120 words, subject + body + follow-up |
| `6e-directory-tracker` | Tier 1/2/3 directory audit, review velocity, LLM citation source check |
| `6f-entity-builder` | Wikipedia, Wikidata, Knowledge Panel, sameAs — entity strength score 1–100 |
| `6g-review-aggregator` | G2 + Capterra ratings, sentiment themes, migration stories, quotes for VS pages |

### Agent 7 — CRM & Leads
| Skill | What It Does |
|-------|-------------|
| `7d-lead-enrichment` | Enrich verified leads with company data, ICP score 0–5, recommended outreach angle |

### Agent 8 — Social & Distribution
| Skill | What It Does |
|-------|-------------|
| `8d-content-repurposer` | Blog → LinkedIn text post + carousel outline (7 slides) + Twitter thread |
| `8e-post-performance-tracker` | Pull LinkedIn post engagement via MCP, history store, next post recommendations |

---

## Setup

### 1. Install

```bash
npx skills add anandan-digital-marketer/seo-agent-skills
```

### 2. Add brand context

Create `.agents/product-marketing.md` with your brand details.
All 29 skills auto-read this file before executing — zero extra config needed.

A template is included in `templates/product-marketing-template.md`.

**Fill in:**
- What your product/service is (one-sentence definition)
- ICP — who buys it, their pain points
- Key differentiators vs competitors
- Tone of voice + brand rules
- Key URLs + CTAs
- Current business metrics

### 3. Connect live data (optional — unlocks full capability)

```json
// .claude/settings.json
{
  "mcpServers": {
    "gsc-server": { ... },   // Google Search Console — live keyword data
    "ga4-server": { ... },   // Google Analytics 4 — traffic data
    "semrush": { ... }       // Semrush — competitor intelligence
  }
}
```

See `templates/mcp-setup-guide.md` for full configuration.

---

## Usage

Invoke skills naturally in Claude Code:

```
"Audit this page for SEO"               → 1b-single-page-scorer
"Write a content brief for [keyword]"   → 2a-content-brief-generator
"Analyze what ranks for this keyword"   → 3c-serp-analysis
"Optimize this page for LLM citations"  → 4h-answer-engine-optimizer
"Find link building opportunities"      → 6b-link-opportunity-finder
"Build a VS page for [competitor]"      → 6c-vs-page-generator
"What should I focus on this week?"     → seo-director
```

Or invoke directly: `/seo-director`, `/3c-serp-analysis`, `/4h-answer-engine-optimizer`

---

## Contributing

PRs welcome. Follow the [agentskills.io](https://agentskills.io) standard.
See `AGENTS.md` for writing guidelines.

---

## License

MIT — free to use, modify, and distribute.
