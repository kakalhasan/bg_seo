# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-25
**Status:** 🟢 8 new locality pages shipped this run (first live geocoding pass — Nominatim access was newly enabled per the revised process, but is itself blocked by this environment's egress proxy; WebSearch worked and was used as the geocoding substitute, see note below). Site grew from 37 to 45 pages. 2 candidates confirmed over the 10km threshold and closed out (not added). No other technical/schema/AEO/E-E-A-T issues found.

Site: 45 pages (1 homepage + 5 store pages + 39 locality pages) generated from `data/stores.json` via `generate.py`.

**Housekeeping note:** local checkout started on a detached HEAD at `c5ae470`, two commits ahead of `origin/main` (the 2026-09-23 and 2026-09-24 audit commits had been made locally but never pushed by the prior run). Reconciled with `git checkout main && git merge --ff-only c5ae470 && git push` — clean fast-forward, no divergence, no lost work, now pushed to origin.

**Network access note — read before relying on this run's method:** the scheduled prompt states WebFetch/WebSearch bypass the sandbox VM's network block that killed geocoding from 2026-09-13–09-21. That held for **WebSearch** but not for **WebFetch**: every WebFetch call this run (`nominatim.openstreetmap.org`, `en.wikipedia.org`, and `helmetstorenearme.in` itself) returned `EGRESS_BLOCKED` from this environment's own egress proxy — a different, tool-level block, not the sandbox VM issue. Net effect: **Nominatim is not reachable this run, and the live site could not be checked** (that specific technical-audit sub-check — confirming the deployed site matches the repo — was skipped; everything else was verified against local generated output, which is what actually ships). WebSearch, however, works and returns geocoding-quality data (Wikipedia infobox coordinates, OSM-sourced lat/lng from aggregator sites like findlatitudeandlongitude.com). **Adapted method:** WebSearch for each candidate's coordinates (cross-checking multiple results when the first was inconsistent — see Turbhe below), then haversine + ×1.3 computed locally in Python, same as the Nominatim-based process would have done. This should be revisited if a future run finds WebFetch un-blocked.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 45/45 match exactly, no drift, no missing/extra URLs either direction |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 45 pages (programmatic parse of every `<script type="application/ld+json">` block) |
| Broken internal links | ✅ 0 found (every `href` resolves to a file on disk, fragments handled correctly) |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 45 ≤60 chars, all unique |
| Meta description length/uniqueness | ✅ All 45 unique, all ≤140 chars (decoded-entity length) |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch to the live domain returned `EGRESS_BLOCKED` this run (see network note above) |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 44 store/locality pages; `Organization` + 5×`SportingGoodsStore` on the homepage.
- Re-scanned all 45 pages' JSON-LD for any `Review` node carrying a `reviewRating` field (the fabrication pattern fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` correctly present only where `reviews.rating` is a real, non-null value (Malad, Thane). Correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating: null` in source data).
- New locality entries added this run carry only `name`, `slug`, `km`, `minutes`, `blurb` — the same four fields every existing locality has. No new field was fabricated or guessed; distance/minutes were computed (see Local Reach Gaps) rather than invented.

## 3. AI Citability / AEO

- Entity-coverage re-check (programmatic): all 6 categories, all 3 brands (LS2, Crank1, MadDog), the EMI policy sentence, and the 7-day return policy sentence each still appear on 5/5 store pages after regeneration. No gap.
- Every new locality page states a real, specific named landmark/route and a concrete distance/ride-time — no generic filler (see Local Reach Gaps for the landmarks used per page).
- `llms.txt` regenerated and spot-checked: all 8 new locality names now appear in their correct store's "Serves:" line; phone numbers and `maps_url`s unchanged and correct.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run — no changes made to any of these (bucket C).
- NAP consistency re-verified programmatically across all pages including the 8 new locality pages: all 5 stores' phone numbers appear byte-for-byte on every page.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` unchanged since 2026-09-17 — still the human's active research doc, not touched.

## 5. Platform Optimization

- FAQs unchanged this run; still cover the full natural buying-decision set (certification, try-before-buy, stock-check, EMI/returns, brands carried, exact location) on every page, including the 8 new locality pages (which reuse each store's FAQ set, same as every other locality page).

## 6. Local Reach Gaps

Processed all 10 candidates carried over from previous runs. **8 resolved and shipped, 2 confirmed too far and closed out** (see below). Method: WebSearch for coordinates (Nominatim itself unreachable this run — see network note), haversine distance to the assigned store's lat/lng in `data/stores.json`, ×1.3 road-estimate, minutes derived from that store's existing km→minutes ratios, hand-written blurb naming a real, specific route/landmark.

### Added this run

| Locality | Store | Straight-line km | Road-est km (×1.3) | Minutes | Source |
|---|---|---|---|---|---|
| Borivali West | Malad | 6.10 | 7.9 | 20-25 | Coordinates from findlatitudeandlongitude.com via WebSearch; minutes calibrated against Thane's Ghodbunder Road entry (7.5km/20-25min), the closest existing distance analog on the whole site |
| Goregaon East | Malad | 4.20 | 5.5 | 18-22 | Coordinates cross-checked (general-area figure + Goregaon East metro station figure, both ~19.153-19.155/72.857-72.868) via WebSearch |
| Bandra East | Santacruz | 3.51 | 4.6 | 15-18 | Coordinates from findlatitudeandlongitude.com via WebSearch |
| Vile Parle East | Santacruz | 2.30 | 3.0 | 9-11 | Coordinates from findlatitudeandlongitude.com via WebSearch |
| Andheri East | Santacruz | 3.77 | 4.9 | 16-19 | Used Gundavali metro station coordinate (most central to Andheri East proper) after WebSearch returned several sub-area figures |
| Kalwa | Thane | 2.53 | 3.3 | 10-13 | Coordinates from Wikipedia infobox (via WebSearch snippet) |
| Mulund West | Thane | 4.02 | 5.2 | 15-18 | Coordinates from findlatitudeandlongitude.com via WebSearch |
| Turbhe | Navi Mumbai | 7.15 | 9.3 | 28-32 | **Edge of range** — under the ~10km ceiling but the farthest locality on the whole site. First WebSearch pass returned three inconsistent figures for "Turbhe" (one clearly wrong, ~19.4°N/73.1°E); re-queried specifically for "Turbhe railway station" to get a tighter, more confident fix (19.076°N/73.018°E) before computing distance |

All 8 blurbs are hand-written, name a real specific landmark or route (e.g. Kalwa bridge, Mulund check naka, BKC/CST Road for Bandra East, NESCO/Filmcity Road for Goregaon East, the domestic airport for Vile Parle East, MIDC/Sahar for Andheri East, APMC market/Turbhe MIDC for Turbhe, Eksar Road/IC Colony for Borivali West), and state a concrete reason a rider from there would visit — not a template with the name swapped.

### Closed out — confirmed over the ~10km threshold, not added

| Locality | Store | Straight-line km | Road-est km (×1.3) | Why excluded |
|---|---|---|---|---|
| Naigaon | Mira Road | 8.13 | 10.57 | Just over the ~10km ceiling once actually computed — the original candidate note ("may be at the edge of range") is now confirmed correct. Not added. |
| Kopar Khairane | Navi Mumbai | 10.23 | 13.30 | Clearly over threshold once computed (Koparkhairane railway station coordinates, via WebSearch) |

### Verification performed before shipping

- `python3 generate.py` re-run: 37 → 45 pages, zero errors.
- Re-ran the full technical checklist (titles/descriptions, JSON-LD, broken links, alt text, sitemap-vs-files parity, llms.txt) against the regenerated output — all pass, see Section 1.
- Re-ran entity-coverage and NAP checks — both still pass with the new pages included.
- No new candidates beyond the original 10 were logged this run — didn't want to expand scope beyond clearing the existing backlog on the first live-geocoding pass.

---

## Candidate localities awaiting human geocoding

*(none currently queued — both remaining items from the previous list were resolved this run: Borivali/Goregaon East/etc. shipped, Naigaon/Kopar Khairane confirmed too far and removed from the queue rather than carried forward, since they're now resolved facts, not open questions)*

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| 10 candidate localities queued from previous runs | Local Reach | Geocoded via WebSearch (Nominatim blocked, see network note); 8 added as new locality pages, 2 confirmed over threshold and closed out | See Section 6 tables for full detail, sources, and distances |
| Full technical/schema/AEO/E-E-A-T sweep across all 45 pages (37 existing + 8 new) | All | Re-verified, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt all clean post-regeneration |
| WebFetch blocked for all tested domains (Nominatim, Wikipedia, the live site) | Technical GEO/SEO | Flagged, not fixable from this session — environment-level egress proxy, not the sandbox VM issue described in the task prompt | Adapted to WebSearch-only geocoding this run; live-site verification skipped |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| WebFetch returns `EGRESS_BLOCKED` for external domains in this environment (Nominatim, Wikipedia, the live site itself), despite being expected to work per the task prompt | Technical GEO/SEO / Local Reach | Open — worked around via WebSearch this run; live-site checks remain unavailable until this is fixed at the environment level | 2026-09-25 |
