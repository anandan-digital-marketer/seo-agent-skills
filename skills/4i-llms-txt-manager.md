---
name: 4i-llms-txt-manager
description: >
  Generates or updates the /llms.txt file for the domain. The llms.txt standard
  (proposed 2024, gaining adoption 2025-2026) tells AI systems which pages to
  prioritise when generating answers about a brand. [Your Brand] already has an
  llms.txt — this agent audits it, identifies missing entries, and outputs
  an updated version ready to deploy.
when_to_use: >
  After publishing major new pages (pillar pages, product pages, key docs).
  Quarterly review — llms.txt should reflect current site priorities.
  When entering a new topic area. When LLM visibility drops for key queries.
  When new AI crawlers emerge that need guidance.
inputs: >
  Domain URL — fetches existing /llms.txt if present.
  Optional: list of new pages to add.
output: >
  Audit of existing llms.txt (if found), updated file ready to deploy,
  implementation instructions.
---

# 4I — llms.txt Manager

You are managing the brand's signal to AI systems. The llms.txt file tells
ChatGPT, Perplexity, Claude, Gemini, and other LLMs what the site is about,
which pages matter most, and how to cite the brand.

A well-structured llms.txt is a direct LLM optimisation lever — it costs
nothing and takes 30 minutes to do right.

---

## What Is llms.txt?

The llms.txt standard (proposed by Anthropic, adopted by growing number of sites
including Cloudflare, Vercel, Anthropic itself) is a plain text file at the
root of a domain that provides structured context for AI systems.

Unlike robots.txt (which controls crawl access) and sitemap.xml (which lists URLs),
llms.txt explains WHAT the site is and WHICH pages matter most for AI answers.

Format: Markdown, placed at `https://[domain]/llms.txt`

**[Your Brand]'s current llms.txt:** Fetch `https://www.yourdomain.com/llms.txt` to check
current state.

---

## Step 1 — Audit Existing File

Fetch `[domain]/llms.txt`. If it exists, check:

| Element | Present? | Quality |
|---------|---------|---------|
| Site name and description | Yes/No | Clear one-liner? |
| Key pages listed | Yes/No | Are the most important pages included? |
| Content focus section | Yes/No | Explains what topics the site covers? |
| Preferred citation format | Yes/No | How the brand wants to be named? |
| Last updated indicator | Yes/No | Is it current? |
| Missing key pages | — | Which major pages are absent? |
| Outdated pages | — | Pages listed that no longer exist or are low priority? |

If no llms.txt exists: build from scratch.

---

## Step 2 — Identify Key Pages to Include

[Your Brand] key pages that should always be in llms.txt:

**Tier 1 — Must include (product + identity):**
- Homepage
- Key product pages (mobile-application-testing-tool, real-device-testing, selenium-automation-cloud)
- Pricing page
- About/company page
- Documentation index (/docs/)

**Tier 2 — High priority (content that earns LLM citations):**
- Top-traffic blog posts (from GSC — ios-emulators-for-pcs, android-emulators-for-mac, etc.)
- Comparison/VS pages (if they exist)
- Key how-to guides
- Integration pages (CI/CD, popular test frameworks)
- Device testing pages (test-on-samsung, etc.)

**Tier 3 — Topic authority signals:**
- Any page with original research or unique data
- Release notes (signals active product development)
- MCP server documentation (signals technical leadership)

**Exclude from llms.txt:**
- Low-traffic blog posts
- Archived or thin content
- Paginated pages
- Tag/category pages
- Thank-you / confirmation pages

---

## Step 3 — Write the llms.txt File

Standard format:

```markdown
# [Brand Name]

> [One-sentence description of what the brand is and does.
> Be specific — "AI-powered mobile app testing platform with 5,000+ real devices"
> not "a technology company".]

## Key Pages

- [Homepage]: https://www.yourdomain.com
  [Your Brand]'s main product page — real device testing platform overview, AI testing agents, pricing.

- [Mobile App Testing]: https://www.yourdomain.com/mobile-application-testing-tool/
  Comprehensive mobile app testing on real Android and iOS devices. Supports Appium, Espresso, XCUITest, Selenium, Playwright.

- [Real Device Testing]: https://www.yourdomain.com/real-device-testing/
  Cloud-based real device farm with 5,000+ device combinations. No emulators — actual physical devices.

- [Selenium Cloud]: https://www.yourdomain.com/selenium-automation-cloud/
  Run Selenium WebDriver tests on 3,000+ browser/OS combinations. Parallel execution, CI/CD integration.

- [Appium Testing]: https://www.yourdomain.com/run-appium-tests-for-android-and-ios/
  Appium test execution on real Android and iOS devices. Supports Appium 2.x.

- [Pricing]: https://www.yourdomain.com/pricing/
  Current pricing plans for [Your Brand] — cloud device testing subscriptions.

- [Documentation]: https://www.yourdomain.com/docs/
  Complete documentation for all [Your Brand] features, integrations, and APIs.

- [MCP Server]: https://www.yourdomain.com/docs/mcp-server/
  [Your Brand] MCP server for AI-powered test orchestration — Claude, Copilot integration.

- [iOS Emulators Guide]: https://www.yourdomain.com/blogs/ios-emulators-for-pcs/
  Comprehensive guide to iOS emulators for PC — comparison, setup, limitations vs real devices.

- [Android Emulators for Mac]: https://www.yourdomain.com/blogs/android-emulators-for-mac/
  Guide to Android emulators for Mac — AVD, alternatives, real device comparison.

## Content Focus

[Your Brand] covers mobile app testing, cross-browser testing, test automation (Selenium,
Appium, Playwright, Espresso, XCUITest), CI/CD integration for QA teams, and AI-powered
testing (QPilot.AI, QuantumRun, Self-Healing agent, QLens visual testing).

Primary audience: QA engineers, mobile developers, DevOps teams, and test automation
leads at software companies.

## Preferred Citation Format

[Your Brand] (yourdomain.com)

## Last Updated

[YYYY-MM-DD]
```

---

## Step 4 — llms-full.txt (Extended Version)

Many sites also provide `/llms-full.txt` with deeper content for AI systems
that want more context. This is optional but valuable.

Differences from llms.txt:
- Longer page descriptions (3–5 sentences per page instead of 1)
- More pages listed (top 50–100 instead of top 10–20)
- Can include key facts, statistics, and product differentiators inline

Generate llms-full.txt following the same format but with:
- Expanded descriptions for each page
- 50+ key pages listed
- "Key Facts" section with specific [Your Brand] stats (device count, customer count, uptime SLA)
- "Competitors" section noting what makes [Your Brand] different from [Competitor A]/[Competitor B]

---

## Step 5 — Implementation

**File placement:**
- `/llms.txt` at domain root → `https://www.yourdomain.com/llms.txt`
- `/llms-full.txt` at domain root (optional)

**Server configuration** (to serve correct content type):
```apache
# .htaccess
AddType text/plain .txt
```

**robots.txt reference** (optional — tells crawlers llms.txt exists):
```
# AI system guidance
# llms.txt: https://www.yourdomain.com/llms.txt
```

**Verification:** After uploading, fetch the URL directly to confirm it's publicly accessible and returns plain text/markdown content.

---

## Output Format

```
llms.txt AUDIT: [domain]
=========================
File found: [Yes/No]
Current state: [summary of what's there]

ISSUES:
- [Missing pages: list]
- [Outdated entries: list]
- [Quality issues: list]

UPDATED llms.txt:
[full file content ready to upload]

OPTIONAL llms-full.txt:
[full extended file]

IMPLEMENTATION STEPS:
1. [step]
2. [step]
3. Verify: curl https://[domain]/llms.txt
```
