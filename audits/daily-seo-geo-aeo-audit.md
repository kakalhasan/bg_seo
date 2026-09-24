# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-24
**Status:** 🟢 Clean run — zero issues found across all six categories. No auto-fixes needed. No new candidate localities logged this run (existing 10-candidate list already covers the well-known areas adjacent to current coverage with genuine confidence; carried over unchanged).

Site: 37 pages (1 homepage + 5 store pages + 31 locality pages) generated from `data/stores.json` via `generate.py`. Live network access to `helmetstorenearme.in` and `nominatim.openstreetmap.org` remains categorically blocked in this sandbox (failing since 2026-09-13) — audit performed entirely against the local generated output and source data, per the revised process.

**Housekeeping note:** local checkout started on a detached HEAD at `40a95af` (yesterday's pushed commit), one commit behind `origin/main` had nothing further — `origin/main` was actually at the same commit after fetch (yesterday's push had landed). Reconciled with `git checkout main && git merge --ff-only origin/main`; clean fast-forward, no divergence, no lost work.

**Generator note:** `python3 generate.py` was re-run to confirm zero drift between source data and committed HTML. The only diff produced was `sitemap.xml`'s `<lastmod>` values re-stamping to today's date — expected, unrelated to any real content change (see carried-over item below), so that diff was discarded (`git checkout -- sitemap.xml`) rather than committed. All page content matched byte-for-byte. `data/stores.json` is unchanged since the last human edit (commit `335f08b`, 2026-09-21) — no drift to reconcile.

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
- `AggregateRating` correctly present only where `reviews.rating` is a real, non-null value in `data/stores.json` (Malad 4.7/2445, Thane 4.5/34). Correctly absent for Santacruz, Mira Road and Navi Mumbai, whose source data has `rating: null` — including Navi Mumbai, which has 6 real quotes but no aggregate rating/count (newly opened store, per its own review text); no rating is fabricated to fill that gap.
- No other plausible-looking-guess values found in schema; every field traces to an explicit value in `data/stores.json`.

## 3. AI Citability / AEO

- Entity-coverage re-check (programmatic, HTML-entity-aware, across all 5 store pages): all 6 categories (including the two with `&` in the name — "Touring Luggage & Bags", "Bike Accessories & Electronics"), all 3 brands (LS2, Crank1, MadDog), the EMI policy sentence, and the 7-day return policy sentence each appear on 5/5 store pages. No gap found.
- Every store and locality page states a real, specific address, phone number, named landmark, and real distance/ride-time — no generic filler.
- `llms.txt` cross-checked field-by-field against current `data/stores.json` — every phone number, every `maps_url`, and every locality name across all 5 stores confirmed present — 100% accurate, no drift.

## 4. Content E-E-A-T / Brand Authority

- Reviews are real and sourced (`source` + `source_url` present at the reviews-block level for all 5 stores, quotes attributed where they exist). Santacruz and Mira Road carry review count + source only (empty `quotes` array) — longstanding known state, not a new gap; no quotes fabricated to fill it.
- Real store photos: all gallery files referenced in `data/stores.json` verified present on disk for all 5 stores.
- Real videos: a distinct YouTube store-tour `youtube_id` present for all 5 stores.
- NAP consistency: verified programmatically — all 5 stores' phone numbers appear byte-for-byte on their store page and every one of their locality pages.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` unchanged since 2026-09-17 — still the human's active research doc. No repo state change to note this run; remains human-executed outreach work, not touched by this routine.

## 5. Platform Optimization

- FAQs cover the full natural buying-decision set: certification, try-before-buy, stock-check, EMI/returns, brands carried, exact location.
- No further gaps found against the "what would an AI Overview/ChatGPT/Perplexity want to quote" checklist this run.

## 6. Local Reach Gaps

- Network egress to `nominatim.openstreetmap.org` and `helmetstorenearme.in` remains blocked — no live geocoding attempted, per the revised process. Bucket (B) not used this run.
- Checked the existing 10-candidate list against current `data/stores.json` localities — none have been geocoded/shipped yet, so all remain open and are carried over rather than re-added.
- No new candidates logged this run: reviewed the areas immediately adjacent to each store's current coverage and found nothing beyond the existing list that I have genuine, confident general knowledge of as a real, well-known Mumbai/Navi Mumbai locality in range — didn't want to pad the list with lower-confidence guesses.

---

## Candidate localities awaiting human geocoding

| Locality | Store | Why it's a plausible candidate |
|---|---|---|
| Borivali | Malad | Immediately north of Kandivali West/Kandivali East (both already covered), major well-known Mumbai suburb |
| Bandra East | Santacruz | Adjacent to Bandra West (already covered), distinct well-known commercial/residential locality |
| Kalwa | Thane | Directly across Thane creek from Thane East (already covered), well-known locality |
| Turbhe | Navi Mumbai | Near Vashi/Sanpada (already covered) along the same Navi Mumbai corridor |
| Goregaon East | Malad | Twin locality across the tracks from Goregaon West (already covered) |
| Vile Parle East | Santacruz | Twin locality across the tracks from Vile Parle West (already covered) |
| Mulund | Thane | Adjoins Thane West along LBS Marg at the Mumbai–Thane boundary |
| Naigaon | Mira Road | Next Western Line station north of Bhayandar (both East/West already covered) — flagging distance uncertainty, may be at the edge of range |
| Andheri East | Santacruz | Twin locality across the tracks from Andheri West (already covered) |
| Kopar Khairane | Navi Mumbai | Harbour-line locality immediately adjacent to Vashi (already covered) |

No distances are stated above — a human must geocode these (as with the 2026-09-17 batch) before any locality page is written.

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 37 pages | All | Re-verified, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt all clean |
| `generate.py` re-run produced zero content diff; only `sitemap.xml` lastmod changed | Technical GEO/SEO | No action needed this run | Discarded the lastmod-only diff — not a real fix; see carried-over item below |
| Reviewed candidate-locality list for new well-known nearby areas | Local Reach | No new candidates added | Existing 10 already cover the areas I have genuine confidence in; avoided padding with low-confidence guesses |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| Ten candidate localities (Borivali, Bandra East, Kalwa, Turbhe, Goregaon East, Vile Parle East, Mulund, Naigaon, Andheri East, Kopar Khairane) awaiting human geocoding | Local Reach | Open — not yet geocoded/shipped | 2026-09-21 / 2026-09-22 / 2026-09-23 |
