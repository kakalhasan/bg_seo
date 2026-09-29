# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-29
**Status:** 🟢 Clean sweep — no technical/schema/AEO/E-E-A-T issues found across all 52 pages, no data changes needed. Local Reach Gaps: found a genuinely West-side-specific landmark for the long-open Dahisar West candidate (Kandarpada metro station), but its road-distance estimate is nearly identical to the existing "Dahisar" entry, so it stays deferred rather than risk a near-duplicate page. One new candidate (Kopar Khairane, Navi Mumbai) checked and rejected — over the 10km ceiling. WebFetch remains blocked for every domain tried (Nominatim, Wikipedia, 99acres, and the live site itself), now the 5th consecutive run — WebSearch used throughout as in prior runs.

Site: 52 pages (1 homepage + 5 store pages + 46 locality pages) generated from `data/stores.json` via `generate.py`. Unchanged since 2026-09-28.

**Housekeeping:** checkout was on a detached HEAD matching `origin/main` at run start (one commit behind, `743e6ab`), left over from a prior run. Fast-forward pulled 6 commits onto `main`, no reconciliation conflicts. Regenerated the site (`python3 generate.py`) to verify output matches source data — output was byte-identical except `sitemap.xml`'s `lastmod` dates (bumped to today's run date, the known per-run stamping issue logged 2026-09-18), which was reverted before the audit since it's not a real content change worth committing on its own.

**Network access note — fifth consecutive run:** WebFetch returned `EGRESS_BLOCKED` for every domain tried this run: `nominatim.openstreetmap.org`, `en.wikipedia.org`, `www.99acres.com`, and `helmetstorenearme.in` itself (tested directly this run to see if the live-site check specifically might be exempted — it isn't). This continues to contradict the task prompt's assumption that WebFetch bypasses the sandbox's egress block; the block is a blanket one, not domain-specific. WebSearch continues to work fully and was used for all geocoding and landmark research this run. Live-site verification (confirming the deployed site matches the repo) has now been unavailable for 5 consecutive runs.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 52/52 match exactly, no drift, no missing/extra URLs either direction |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 52 pages (programmatic parse of every `<script type="application/ld+json">` block) |
| Broken internal links | ✅ 0 found (every `href` resolves to a file on disk once fragments/external/tel/mailto are excluded) |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 52 ≤60 chars, all unique |
| Meta description length/uniqueness | ✅ All 52 unique, all ≤140 chars (decoded-entity length) |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch to the live domain itself returned `EGRESS_BLOCKED` this run (see network note above) |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 51 store/locality pages; `Organization` + 5×`SportingGoodsStore` on the homepage.
- Re-scanned all 52 pages' JSON-LD for any `Review` node carrying a `reviewRating` field (the fabrication pattern fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` correctly present only where `reviews.rating` is a real, non-null value (Malad 4.7, Thane 4.5). Correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating: null` in source data).
- No data changes this run, so no new fields to check for fabrication risk.

## 3. AI Citability / AEO

- Entity-coverage re-check (programmatic, HTML-entity-aware — the earlier plain-string check flagged the two `&`-containing categories, "Touring Luggage & Bags" and "Bike Accessories & Electronics", as missing purely because they render as `&amp;` in HTML; decoding entities before matching confirmed both are present verbatim on every store page): all 6 categories, all 3 brands (LS2, Crank1, MadDog), the EMI policy sentence, and the 7-day return policy sentence each appear on all 5 store pages. No gap.
- `llms.txt` regenerated and spot-checked: store count, brand list and every locality name across all 5 "Serves:" lines match current `data/stores.json`. No drift.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run — no changes made to any of these (bucket C).
- NAP consistency re-verified programmatically across all 52 pages: all 5 stores' phone numbers appear byte-for-byte on every page belonging to that store, including every locality page.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` unchanged since 2026-09-17 — still the human's active research doc, not touched.

## 5. Platform Optimization

- FAQs unchanged this run; still cover the full natural buying-decision set (certification, try-before-buy, stock-check, EMI/returns, brands carried, exact location) on every page.

## 6. Local Reach Gaps

One open candidate going into this run (Dahisar West, assigned to Mira Road, carried since 2026-09-28 — the only landmark previously found, the shared Dahisar railway station, sits on the East/West boundary and would duplicate the existing "Dahisar" entry).

**Re-investigated Dahisar West:** WebSearch initially surfaced a conflicting claim (one source described "Anand Nagar metro station" as being in Dahisar West on New Link Road; a second, more specific search clarified Anand Nagar is actually in **Dahisar East**, and the station immediately before it on the same Yellow Line 2A, **Kandarpada metro station**, is the one genuinely located in Kandarpada, Dahisar West). This is a real, specific, West-side-only landmark — a first for this candidate. Geocoded Kandarpada metro station (19.2565999, 72.8506506) and computed distance to the Mira Road store (19.2843751, 72.8772246): straight-line 4.16 km → **road-est 5.41 km**, comfortably within the ~10km ceiling.

**Still not added, however:** 5.41 km is nearly identical to the existing "Dahisar" entry's 5.6 km, and that entry's blurb already describes a WEH-service-road / Dahisar-Toll-Naka route. I don't have confident enough knowledge of Mumbai road geography to state whether a Kandarpada-based rider would actually take a meaningfully different route (e.g. via New Link Road north into Mira-Bhayandar Road) rather than crossing over to the same WEH corridor the existing entry already describes — writing a blurb that just swapped the landmark name while describing an effectively identical route and near-identical distance would be exactly the near-duplicate "doorway page" pattern this site is built to avoid. Deferred again, with the specific landmark now logged for whoever (human or a future run with stronger routing confidence) picks this up next.

**New candidate checked and rejected:** Kopar Khairane (Navi Mumbai side), suggested by general knowledge of areas near Nerul/Seawoods. Geocoded via Kopar Khairane railway station (19.1033, 73.0113) → straight-line 10.23 km from the Navi Mumbai store (19.0120102, 73.0235427) → **road-est 13.3 km**, over the ~10km ceiling. Rejected, not logged as a standing candidate (clearly over threshold, not a borderline case worth re-checking later).

**Also considered and set aside without geocoding:** Poonam Sagar Complex, Shanti Nagar and Silver Park, all suggested by search results as "nearby" Mira Road East localities. All three turned out to be sub-neighbourhoods *within* Mira Road East itself — the store's own area — rather than distinct nearby towns like Bhayandar or Kashimira. Adding these would pad the locality count without a genuine separate-commute story (no real distance or route distinct from the store's own page), so they were not pursued as candidates.

### Verification performed before closing out this run

- `python3 generate.py` re-run: confirmed 52 pages, zero errors, output unchanged from committed state except the sitemap `lastmod` stamp (reverted, not a real change).
- Full technical checklist (titles/descriptions, JSON-LD, broken links, alt text, sitemap-vs-files parity, robots.txt, llms.txt) — all pass, see Section 1.
- Entity-coverage (HTML-entity-aware, fixed a false-positive in the check method itself this run — see Section 3) and NAP checks — both pass.
- Confirmed the reviewRating-fabrication fix still holds across all 52 pages — 0 hits.
- No data or generated-page changes were made this run, so nothing new to verify beyond the above sweep.

---

## Candidate localities awaiting human geocoding

| Locality | Candidate store | Note |
|---|---|---|
| Dahisar West | Mira Road | A genuine West-side landmark now identified — Kandarpada metro station (19.2565999, 72.8506506), road-est 5.41 km from the store. Not added because that distance is nearly identical to the existing "Dahisar" entry (5.6 km) and I'm not confident the commute route is meaningfully different from the WEH-corridor route that entry already describes — adding it risks a near-duplicate page. Needs either stronger route-distinctness confidence or a human call on whether the West-side framing alone justifies a separate page. |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Dahisar West candidate still open, previous landmark (shared railway station) was ambiguous East/West | Local Reach | Found a genuinely West-side-only landmark (Kandarpada metro station) via WebSearch, geocoded it, computed distance — but held off adding the page since the resulting distance/route look near-identical to the existing "Dahisar" entry | See Section 6; candidate stays open with a stronger note for next time |
| Possible new Navi Mumbai locality (Kopar Khairane) | Local Reach | Geocoded and checked — 13.3km road-est, over the 10km ceiling | Rejected, not logged as a standing candidate |
| Entity-coverage check flagged two categories as "missing" on first pass | AI Citability / AEO | False positive in the check method (didn't decode HTML entities before string-matching `&`); re-ran with entity decoding, confirmed both categories are present on every store page | No site change needed — this was an audit-tooling issue, not a site issue |
| Full technical/schema/AEO/E-E-A-T sweep across all 52 pages | All | Re-verified, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt all clean |
| WebFetch blocked for every domain tested, including the live site itself — fifth consecutive run | Technical GEO/SEO | Flagged again, not fixable from this session — environment-level egress proxy blocks WebFetch entirely, not just specific domains | Adapted to WebSearch-only geocoding again; live-site verification skipped for the 5th run running |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| WebFetch returns `EGRESS_BLOCKED` for every external domain tried in this environment (Nominatim, Wikipedia, 99acres, and the live site itself), despite being expected to work per the task prompt | Technical GEO/SEO / Local Reach | Open, now 5 consecutive runs — worked around via WebSearch each time; live-site checks remain unavailable until this is fixed at the environment level | 2026-09-25 |
| Dahisar West — a genuine West-side landmark (Kandarpada metro station) is now identified, but its distance/route look near-identical to the existing "Dahisar" entry | Local Reach | Open — see Candidate table above | 2026-09-28 |
