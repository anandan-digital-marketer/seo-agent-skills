# Agent Guidelines — SEO Agent Skills

This repository hosts Agent Skills for SEO, LLM visibility, and technical auditing.
Skills install to `.agents/skills/` and work with Claude Code, Cursor, Codex, and
any Agent Skills spec-compliant agent.

---

## Repository Structure

```
seo-agent-skills/
├── skills/          ← 29 SEO skill .md files
├── templates/       ← Setup templates (product-marketing, MCP config)
├── README.md
├── AGENTS.md        ← This file
└── LICENSE
```

---

## Skill File Format

Each skill is a `SKILL.md` file with YAML frontmatter:

```yaml
---
name: skill-name
description: >
  What the skill does. When to use it. Trigger phrases Claude will match.
  Keep under 1,024 characters.
---
```

**Body rules:**
- Under 500 lines
- H2 headers for main sections
- Bold for key terms, tables for data, code blocks for examples
- Active voice, specific language, second person ("You are...")
- Trigger phrases in the description so Claude auto-selects the skill

---

## Brand Context Pattern

All skills in this pack are designed to auto-read `.agents/product-marketing.md`
before executing. This makes generic skills brand-specific without modifying them.

Skills reference it via Claude Code shell injection:
```
**Brand context:** !`cat .agents/product-marketing.md 2>/dev/null || echo "Add .agents/product-marketing.md"`
```

Create your own `product-marketing.md` using the template in `templates/`.

---

## Naming Rules

- 1–64 characters, lowercase a–z, numbers, hyphens only
- Cannot start/end with hyphen or have consecutive hyphens
- Must match the file name exactly (without `.md`)
- Examples: `seo-director`, `3c-serp-analysis`, `6c-vs-page-generator`

---

## Writing Style

- **Direct and instructional** — "You are a [role]. Your job is to [task]."
- **Specific over vague** — name exact tools, frameworks, metrics
- **One idea per section** — H2 per major step or concept
- **No filler** — every sentence earns its place
- **Real examples** — show what good output looks like

---

## Contributing

1. Fork the repo
2. Create a branch: `feature/skill-name`
3. Add your skill to `skills/`
4. Follow naming and format rules above
5. Open a PR — include: what the skill does, example trigger phrases, sample output

**PR checklist:**
- [ ] Name is valid (lowercase, hyphens only)
- [ ] Description is under 1,024 chars with trigger phrases
- [ ] Skill file is under 500 lines
- [ ] No sensitive data or credentials
- [ ] Tested with at least one agent (Claude Code preferred)

---

## MCP Integration

Skills marked with live data capabilities work best with MCP servers configured.
See `templates/mcp-setup-guide.md` for setup instructions for:
- Google Search Console MCP
- Google Analytics 4 MCP
- Semrush MCP
