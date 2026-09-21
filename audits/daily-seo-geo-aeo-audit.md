# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-21
**Status:** 🟢 Clean run — zero issues found across all six categories. No auto-fixes needed. Four new candidate localities logged (Borivali near Malad, Bandra East near Santacruz, Kalwa near Thane, Turbhe near Navi Mumbai); no candidates carried over from before, since the 2026-09-21 human session resolved and shipped all 7 that were queued.

Site: 37 pages (1 homepage + 5 store pages + 31 locality pages) generated from `data/stores.json` via `generate.py`. Live network access to `helmetstorenearme.in` and `nominatim.openstreetmap.org` remains categorically blocked in this sandbox (failing since 2026-09-13) — audit performed entirely against the local generated output and source data, per the revised process.

**Housekeeping note:** local checkout started on a detached HEAD at `335f08b` (a same-day human session's commit adding 7 geocoded locality pages), which was already 4 commits ahead of what the local `main` branch ref pointed to. Fetched `origin/main`, confirmed it matched the detached HEAD exactly, and fast-forwarded local `main` onto it — no lost work, nothing to reconcile beyond that.

**Generator note:** `python3 generate.py` was re-run to confirm zero drift between source data and committed HTML. All 37 pages, including `sitemap.xml`, matched byte-for-byte this run — the human session's commit was made today, so the `<lastmod>` date the generator stamps happened to already equal today's date. This is coincidental, not a fix; the underlying behavior (unconditional re-stamp to run date rather than tracking real content changes) is unchanged and remains carried over below.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 37/37 match exactly, no drift, no missing/extra URLs either direction |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 37 pages (programmatic parse of every `<script type="application/ld+json">` block) |
| Broken internal links | ✅ 0 found (every `href="/..."` resolves to a file on disk) |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 37 ≤60 chars, all unique |
| Meta description length/uniqueness | ✅ All 37 unique, all ≤140 chars (decoded-entity length) |
| Canonical tags | ✅ Present and correct on every page |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 36 store/locality pages; `Organization` + 5×`SportingGoodsStore` on the homepage.
- Re-scanned all 37 pages' JSON-LD for any `Review` node carrying a `reviewRating` field (the fabrication pattern fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` correctly present only where `reviews.rating` is a real, non-null value in `data/stores.json` (Malad 4.7/2445, Thane 4.5/34 — appearing on the homepage plus each of their own store + locality pages, 17 pages total); correctly absent for Santacruz, Mira Road and Navi Mumbai, whose source data has `rating: null`. Honest missing data, not a bug.
- No other plausible-looking-guess values found in schema; every field traces to an explicit value in `data/stores.json`.

## 3. AI Citability / AEO

- Entity-coverage re-check (programmatic, HTML-entity-aware, across all 5 store pages): all 6 categories (including the two with `&` in the name — "Touring Luggage & Bags", "Bike Accessories & Electronics", which render HTML-escaped as `&amp;` and are correctly present), all 3 brands (LS2, Crank1, MadDog), ISI/ECE/DOT certification, EMI policy, and 7-day return policy each appear on 5/5 store pages — the brand-wide EMI/returns and brands-carried FAQ that `generate.py` appends to every page covers the policy/brand facts, and the per-store hand-written FAQs cover certification, try-before-buy, location and stock-check. No gap found.
- Every store and locality page states a real, specific address, phone number, named landmark, and real distance/ride-time — no generic filler.
- `llms.txt` cross-checked field-by-field against current `data/stores.json` — every phone number, every `maps_url`, and every locality name across all 5 stores confirmed present — 100% accurate, no drift.

## 4. Content E-E-A-T / Brand Authority

- Reviews are real and sourced (`source` + `source_url` present at the reviews-block level for all 5 stores, quotes attributed by name).
- Real store photos: all gallery files referenced in `data/stores.json` verified present on disk for all 5 stores (4 for Malad/Santacruz, 3 for Mira Road/Thane/Navi Mumbai).
- Real videos: a distinct YouTube store-tour `youtube_id` present for all 5 stores.
- NAP consistency: verified programmatically — all 5 stores' phone numbers appear byte-for-byte on their store page and every one of their locality pages.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` last touched 2026-09-17, unchanged since — still the human's active research doc. No repo state change to note this run; remains human-executed outreach work, not touched by this routine.

## 5. Platform Optimization

- FAQs cover the full natural buying-decision set: certification, try-before-buy, stock-check, EMI/returns, brands carried, exact location.
- No further gaps found against the "what would an AI Overview/ChatGPT/Perplexity want to quote" checklist this run.

## 6. Local Reach Gaps

- Network egress to `nominatim.openstreetmap.org` and `helmetstorenearme.in` remains blocked — no live geocoding attempted, per the revised process. Bucket (B) not used this run.
- No candidates carried over: the 2026-09-21 human session geocoded and shipped all 7 that were queued as of the previous run (see repo history — 31 localities now live, up from 24).
- Four new candidates identified this run by adjacency to already-covered localities, added to the list below with no distance claimed:
  - **Borivali** (Malad store) — the next major, well-known Mumbai western-suburb node immediately north of Kandivali West/East, which are already covered.
  - **Bandra East** (Santacruz store) — a distinct, well-known locality directly across the tracks from Bandra West, which is already covered.
  - **Kalwa** (Thane store) — a well-known locality directly across Thane creek from Thane East, which is already covered.
  - **Turbhe** (Navi Mumbai store) — a well-known Navi Mumbai node a short distance from Nerul/Seawoods along the same Sion-Panvel highway corridor as Vashi/Sanpada, which are already covered.

---

## Candidate localities awaiting human geocoding

| Locality | Store | Why it's a plausible candidate |
|---|---|---|
| Borivali | Malad | Immediately north of Kandivali West/Kandivali East (both already covered), major well-known Mumbai suburb |
| Bandra East | Santacruz | Adjacent to Bandra West (already covered), distinct well-known commercial/residential locality |
| Kalwa | Thane | Directly across Thane creek from Thane East (already covered), well-known locality |
| Turbhe | Navi Mumbai | Near Vashi/Sanpada (already covered) along the same Navi Mumbai corridor |

No distances are stated above — a human must geocode these (as with the 2026-09-17 batch) before any locality page is written.

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 37 pages | All | Re-verified, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt all clean |
| `generate.py` re-run produced zero diff, including `sitemap.xml` | Technical GEO/SEO | No action needed this run | Coincidental — today's run date matches the human session's commit date, not a fix; see carried-over item below |
| Four new candidate localities identified (Borivali, Bandra East, Kalwa, Turbhe) | Local Reach | Logged to candidate list, no page written | Awaiting human geocoding, per revised process |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
