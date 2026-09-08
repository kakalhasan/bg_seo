# bg_seo

SEO / AEO / GEO working repo for **Bikester Global** (bikesterglobal.com), the Shopify motorcycle-gear store.

Two tracks of work live here:

## 1. Site-wide GEO/SEO audits
Run using the installed `geo-seo-claude` Claude Code skill (`~/.claude/skills/geo/`).

- `/geo audit https://bikesterglobal.com` — full GEO+SEO audit, composite score
- `/geo quick https://bikesterglobal.com` — fast visibility snapshot
- `/geo citability <product-url>` — AI citation readiness for a specific product page
- `/geo crawlers https://bikesterglobal.com` — AI crawler access check (robots.txt, headers)
- `/geo schema <product-url>` — structured data / JSON-LD audit

Save each run's output under `audits/YYYY-MM-DD/`.

## 2. Per-listing SEO/GEO metadata
Every product draft created via the Bikester Shopify listing workflow includes an
SEO/GEO engine step (SEO Title, SEO Description, and optimization notes for Google
Search, Merchant Center, ChatGPT Search, Perplexity, Gemini, Claude, Copilot).
Reference copies of that metadata for tracked products live under `product-seo/`,
keyed by SKU (see the SKU/product-data Google Sheet for the canonical record).

## Structure

```
audits/         Dated site-wide GEO/SEO audit reports (md/json/pdf)
product-seo/    Per-product SEO/GEO metadata snapshots, keyed by SKU
```
