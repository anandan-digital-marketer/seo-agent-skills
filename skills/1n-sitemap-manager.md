---
name: 1n-sitemap-manager
description: >
  Generate a fresh XML sitemap from live GSC data, or validate an existing
  sitemap against GSC indexed URLs. Flags non-200 URLs, noindexed pages in
  sitemap, redirected URLs that should be updated, and split recommendations
  for large sitemaps (>50,000 URLs). Also generates the robots.txt sitemap
  reference line.
when_to_use: >
  After a large batch of new pages is published. After executing blog redirects
  (1M). Quarterly sitemap health check. When GSC reports sitemap errors.
inputs: >
  Mode A (validate): existing sitemap URL to fetch and audit
  Mode B (generate): site URL + page list (from GSC data or crawl)
output: >
  Validation report with pass/fail per check, or clean XML sitemap ready to upload.
---

# 1N — Sitemap Manager

You are a technical SEO engineer managing XML sitemaps.

---

## Step 1 — Determine Mode

**Mode A: Validate existing sitemap**
→ Fetch the sitemap URL provided, run all validation checks, output issues.

**Mode B: Generate new sitemap**
→ Use GSC data or page list provided, build clean XML output.

If not specified, ask: "Do you want to validate an existing sitemap or generate a new one?"

---

## Mode A: Validate Existing Sitemap

Fetch the sitemap XML. For sitemap index files, fetch and check each referenced sitemap.

### Validation Checks

| Check | Pass Condition | Severity if Fail |
|-------|---------------|-----------------|
| Valid XML format | Parses without errors | Critical |
| URL count per file | Under 50,000 | Critical if over |
| All URLs return 200 | HTTP status 200 | High |
| No noindexed URLs | Pages in sitemap must be indexable | High |
| No redirected URLs | Should point to final destination | Medium |
| `<lastmod>` accuracy | Dates are real, not all identical | Low |
| No `<priority>` or `<changefreq>` | Ignored by Google — clean to remove | Info |
| Sitemap referenced in robots.txt | `Sitemap: [url]` line present | Medium |
| HTTPS URLs only | No HTTP URLs | High |
| Domain consistency | All URLs use same domain (www vs non-www) | High |

### Common Issues
| Issue | Fix |
|-------|-----|
| >50,000 URLs in one file | Split into sitemap index + multiple files |
| Non-200 URLs | Remove or fix the pages |
| Noindexed pages in sitemap | Remove from sitemap |
| Redirected URLs | Update to final destination URL |
| All identical lastmod dates | Use real modification timestamps |

---

## Mode B: Generate New Sitemap

### Site Architecture Templates

**SaaS / Software company (like [Your Brand]):**
Priority pages to include:
1. Homepage
2. All product/feature landing pages (`/mobile-app-testing/`, `/real-device-testing/`, etc.)
3. All blog posts (`/blogs/*`)
4. Documentation pages (`/docs/*`)
5. Integration pages (`/integrations/*`)
6. Comparison/VS pages
7. About, Pricing, Contact, Careers
8. Release notes

Pages to EXCLUDE from sitemap:
- `noindex` pages
- Paginated pages beyond page 1 (`?page=2`, etc.)
- Tag/category archive pages (unless they have real content)
- Search results pages
- Admin pages
- Thank-you / confirmation pages
- 301 redirect sources

### XML Format Rules

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://www.yourdomain.com/page-slug/</loc>
    <lastmod>YYYY-MM-DD</lastmod>
  </url>
</urlset>
```

**Do NOT include `<priority>` or `<changefreq>`** — Google ignores both.
`<lastmod>` should be the actual last-modified date, not today's date for every URL.

### Sitemap Index (for >50,000 URLs or multiple content types)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<sitemapindex xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <sitemap>
    <loc>https://www.yourdomain.com/sitemap-pages.xml</loc>
    <lastmod>YYYY-MM-DD</lastmod>
  </sitemap>
  <sitemap>
    <loc>https://www.yourdomain.com/sitemap-blogs.xml</loc>
    <lastmod>YYYY-MM-DD</lastmod>
  </sitemap>
  <sitemap>
    <loc>https://www.yourdomain.com/sitemap-docs.xml</loc>
    <lastmod>YYYY-MM-DD</lastmod>
  </sitemap>
</sitemapindex>
```

### robots.txt Reference

Always end with the robots.txt Sitemap line:
```
Sitemap: https://www.yourdomain.com/sitemap.xml
```

---

## Step 3 — GSC Comparison (if GSC data available)

If GSC data is available via MCP:
1. Pull indexed URLs from GSC
2. Compare against sitemap URLs
3. Flag: URLs in sitemap but NOT indexed (possible issues)
4. Flag: URLs indexed but NOT in sitemap (missing from sitemap)
5. Flag: URLs in sitemap that GSC marks as "Excluded"

---

## Output Format

### Mode A: Validation Report

```
Sitemap: [URL]
URLs found: [N]
Validation date: [YYYY-MM-DD]

PASS/FAIL per check (table)
Issues by severity: Critical → High → Medium → Low
Specific URLs causing each issue (up to 10 examples per issue type)
Corrected XML for any fixable issues
```

### Mode B: Generated Sitemap

Complete XML file ready to upload to server root.
Robots.txt Sitemap line.
Submission instructions for GSC.
