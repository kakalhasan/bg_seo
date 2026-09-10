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

## 3. Local SEO/AEO/GEO site — helmetstorenearme.in

A static site (this repo, served via GitHub Pages, custom domain `helmetstorenearme.in`)
built to drive walk-in traffic to Bikester Global's physical stores. One page per store
plus a page per nearby locality (~10km radius), each with three CTAs — Call, Get
Directions, WhatsApp — and `SportingGoodsStore`/`FAQPage`/`BreadcrumbList` JSON-LD.

**Deliberately not a daily-auto-generated doorway-page mill.** Google's spam policy
("scaled content abuse") targets exactly that pattern, and it's a real risk for a brand
new domain. Instead: a genuinely-differentiated batch built once, expanded a few pages
at a time as real content (new localities, seasonal content, blog/guide pages) rather
than churned indefinitely.

- Source data: `data/stores.json` — edit this to add a store, add a locality, or update
  hours/phone/address. Each locality needs real lat/lng (see geocoding note below) and a
  **hand-written**, distinct blurb — never a template with only the place name swapped.
- Generator: `python3 generate.py` — rebuilds every HTML page, `sitemap.xml`, `robots.txt`
  and `llms.txt` from `data/stores.json`. Re-run after any data edit.
- To geocode a new locality: query `https://nominatim.openstreetmap.org/search` with a
  descriptive `q` (locality + city + state), a real `User-Agent`, and rate-limit to ~1
  req/sec (OSM usage policy). See git history of `generate.py`'s companion commands for
  the exact pattern used for the first batch.
- Deploy: push to `main` — GitHub Pages serves the repo root directly (`.nojekyll` present,
  no Jekyll processing). DNS: A records + CNAME per GitHub Pages docs, pointed at
  `helmetstorenearme.in` (see `CNAME` file).

## Structure

```
audits/         Dated site-wide GEO/SEO audit reports (md/json/pdf)
product-seo/    Per-product SEO/GEO metadata snapshots, keyed by SKU
data/           stores.json — canonical store + locality data for the local SEO site
generate.py     Static site generator (reads data/stores.json, writes HTML + sitemap)
assets/         CSS + logo/icon images for the local SEO site
stores/         Generated: one page per store (do not hand-edit — edit data/ + regenerate)
near/           Generated: one page per nearby locality (do not hand-edit)
```
