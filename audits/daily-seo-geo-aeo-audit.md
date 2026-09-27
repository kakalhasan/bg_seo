# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-27
**Status:** 🟢 2 new locality pages shipped this run (Jogeshwari East → Malad, Manpada → Thane), both geocoded via WebSearch this run. Site grew from 47 to 49 pages. Refined the open Jogeshwari candidate: splitting it into Jogeshwari East (now resolved, closer to Malad) and Jogeshwari West (still genuinely ambiguous — near-tie between Malad and Santacruz). 3 new candidates checked and rejected as clearly over the 10km threshold (Kopar Khairane, Ghansoli, Airoli — all Navi Mumbai). No other technical/schema/AEO/E-E-A-T issues found; full 49-page verification sweep clean.

Site: 49 pages (1 homepage + 5 store pages + 43 locality pages) generated from `data/stores.json` via `generate.py`.

**Housekeeping:** checkout was on a detached HEAD at `07334ed` (matching `origin/main`) at run start, likely left over from a prior run. Switched to `main` and fast-forward pulled — no data loss, no reconciliation conflicts.

**Network access note — still open, third consecutive run:** WebFetch returned `EGRESS_BLOCKED` for every domain tested this run (Nominatim, the live site `helmetstorenearme.in`, and even `en.wikipedia.org` as a control) — confirming this is a blanket egress-proxy block on WebFetch in this environment, not a domain-specific one. This contradicts the task prompt's assumption that WebFetch/WebSearch bypass the sandbox VM's network block. WebSearch continues to work fully and was used as the geocoding substitute again — coordinates cross-referenced across multiple independent sources (Wikipedia, findlatitudeandlongitude.com) before computing distance, same method as the last two runs. Live-site verification (confirming the deployed site matches the repo) remains skipped for the third run in a row. This should get a human look — WebFetch has now never worked in this environment across 3 runs.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 49/49 match exactly, no drift, no missing/extra URLs either direction |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 49 pages (programmatic parse of every `<script type="application/ld+json">` block) |
| Broken internal links | ✅ 0 found (every `href` resolves to a file on disk once fragments are stripped correctly) |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 49 ≤60 chars, all unique |
| Meta description length/uniqueness | ✅ All 49 unique, all ≤140 chars (decoded-entity length) |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch to the live domain returned `EGRESS_BLOCKED` this run again (see network note above) |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 48 store/locality pages; `Organization` + 5×`SportingGoodsStore` on the homepage.
- Re-scanned all 49 pages' JSON-LD for any `Review` node carrying a `reviewRating` field (the fabrication pattern fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` correctly present only where `reviews.rating` is a real, non-null value (Malad, Thane). Correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating: null` in source data).
- New locality entries (Jogeshwari East, Manpada) carry only `name`, `slug`, `km`, `minutes`, `blurb` — same four fields as every existing locality. No new field fabricated; distance/minutes computed, not invented.

## 3. AI Citability / AEO

- Entity-coverage re-check (programmatic, HTML-entity-aware): all 6 categories, all 3 brands (LS2, Crank1, MadDog), the EMI policy sentence, and the 7-day return policy sentence each still appear on 5/5 store pages after regeneration. No gap. (First pass of the checker flagged a false positive on "Bike Accessories & Electronics" / "Touring Luggage & Bags" — the content is present, just HTML-entity-escaped as `&amp;`, which the checker's literal string match missed on first pass; confirmed present on inspection.)
- Both new locality pages state a real, specific named landmark/route and a concrete distance/ride-time — no generic filler (JVLR/Jogeshwari East metro station/NESCO for Jogeshwari East; Cadbury Junction/Pokhran Road No. 1/Vasant Vihar/Hiranandani Meadows for Manpada).
- `llms.txt` regenerated and spot-checked: both new locality names now appear in their correct store's "Serves:" line; phone numbers and `maps_url`s unchanged and correct.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run — no changes made to any of these (bucket C).
- NAP consistency re-verified programmatically across all 49 pages: all 5 stores' phone numbers appear byte-for-byte on every page including the 2 new locality pages.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` unchanged since 2026-09-17 — still the human's active research doc, not touched.

## 5. Platform Optimization

- FAQs unchanged this run; still cover the full natural buying-decision set (certification, try-before-buy, stock-check, EMI/returns, brands carried, exact location) on every page, including the 2 new locality pages (which reuse each store's FAQ set, same as every other locality page).

## 6. Local Reach Gaps

One open candidate going into this run (Jogeshwari, ambiguous Malad-vs-Santacruz assignment). Per the revised process, re-investigated it with more specific sub-area coordinates, and also scanned for other well-known nearby localities not yet covered. Method: WebSearch for coordinates (Nominatim/WebFetch still blocked — see network note), haversine distance to the assigned store's lat/lng, ×1.3 road-estimate, minutes derived from that store's existing km→minutes ratios, hand-written blurb naming a real, specific route/landmark.

Checked 5 candidates: Jogeshwari East, Jogeshwari West, Manpada, and (Navi Mumbai) Kopar Khairane, Ghansoli, Airoli. **2 resolved and shipped, 1 refined-but-still-ambiguous, 3 confirmed over threshold.**

### Added this run

| Locality | Store | Straight-line km | Road-est km (×1.3) | Minutes | Source |
|---|---|---|---|---|---|
| Jogeshwari East | Malad | 4.42 | 5.7 | 18-22 | Jogeshwari East metro station coordinates (19.14302, 72.85510, via Wikipedia through WebSearch) resolved to a clearly closer distance to Malad (5.7km road-est) than Santacruz (8.6km road-est) — a comfortable 2.9km margin, unlike the ambiguous general-Jogeshwari coordinate used in the 2026-09-26 attempt. Minutes matched directly to the Goregaon East entry (5.5km/18-22min), the closest existing distance/corridor analog for this store (both reached via the WEH service road past NESCO) |
| Manpada | Thane | 3.25 | 4.2 | 12-16 | Coordinates (19.2308, 72.9741) sourced via WebSearch/findlatitudeandlongitude.com. Minutes linearly interpolated between the Wagle Estate/Kalwa entry (3.3km/10-13min) and the Mulund West entry (5.2km/15-18min), the two closest existing ratio analogs for this store |

Both blurbs are hand-written and name real, specific landmarks confirmed via WebSearch before writing: the JVLR (Jogeshwari-Vikhroli Link Road) junction with the Western Express Highway and the Jogeshwari East metro station for Jogeshwari East; Cadbury Junction, Pokhran Road No. 1, Vasant Vihar and Hiranandani Meadows for Manpada (all confirmed as real Thane landmarks via search before use, not guessed). Neither is a template with only the name swapped.

### Logged / checked — not resolved this run

| Locality | Store (candidate) | Reason not added |
|---|---|---|
| Jogeshwari West | Malad or Santacruz (ambiguous) | Refined coordinates (19.13341, 72.84863, via findlatitudeandlongitude.com) put it at 6.75km road-est from Malad vs 7.01km road-est from Santacruz — both well under the 10km ceiling, but a 0.26km difference is well within geocoding uncertainty for a broad locality name. Not confident enough to assign either way without a more precise sub-area landmark to anchor the blurb to. Carried forward as the (now narrower) open candidate. |
| Kopar Khairane | Navi Mumbai | Railway station coordinates (19.1033, 73.0113) → 13.3km road-est. Over the ~10km ceiling. |
| Ghansoli | Navi Mumbai | Railway station coordinates (19.1164, 73.0070) → 15.3km road-est. Over the ~10km ceiling. |
| Airoli | Navi Mumbai | Railway station coordinates (19.1586, 72.9994) → 21.5km road-est. Well over the ~10km ceiling. |

### Verification performed before shipping

- `python3 generate.py` re-run: 47 → 49 pages, zero errors.
- Re-ran the full technical checklist (titles/descriptions, JSON-LD, broken links, alt text, sitemap-vs-files parity, llms.txt) against the regenerated output — all pass, see Section 1.
- Re-ran entity-coverage (HTML-entity-aware) and NAP checks — both still pass with the new pages included.
- Confirmed the reviewRating-fabrication fix still holds across all 49 pages (grep-equivalent scan of JSON-LD for `reviewRating` — 0 hits).

---

## Candidate localities awaiting human geocoding

| Locality | Candidate store | Note |
|---|---|---|
| Jogeshwari West | Malad or Santacruz | Near-tie on road-est distance (6.75km vs 7.01km, see Section 6) — needs either a human call on which store's catchment it belongs to, or a more precise sub-locality landmark (a specific road/station within Jogeshwari West) to anchor a confident assignment and blurb. |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Jogeshwari East and Manpada identified as missing, geocodable localities | Local Reach | Geocoded via WebSearch (Nominatim/WebFetch blocked, see network note), added as new locality pages | See Section 6 for sources and distances |
| Jogeshwari (general) candidate was too ambiguous to resolve on 2026-09-26 | Local Reach | Split into Jogeshwari East (resolved, closer to Malad by 2.9km) and Jogeshwari West (still ambiguous, refined to a 0.26km near-tie) | Narrows the open candidate rather than leaving it as a single vague entry |
| Kopar Khairane, Ghansoli, Airoli checked as Navi Mumbai candidates | Local Reach | All 3 confirmed clearly over the 10km threshold, not added | See Section 6 table |
| Full technical/schema/AEO/E-E-A-T sweep across all 49 pages | All | Re-verified, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt all clean post-regeneration |
| WebFetch blocked for every domain tested (Nominatim, live site, Wikipedia control) — third consecutive run | Technical GEO/SEO | Flagged again, not fixable from this session — environment-level egress proxy blocks WebFetch entirely | Adapted to WebSearch-only geocoding again; live-site verification skipped for the 3rd run running |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| WebFetch returns `EGRESS_BLOCKED` for external domains in this environment (Nominatim, the live site, and now a Wikipedia control), despite being expected to work per the task prompt | Technical GEO/SEO / Local Reach | Open, now 3 consecutive runs — worked around via WebSearch each time; live-site checks remain unavailable until this is fixed at the environment level | 2026-09-25 |
| Jogeshwari West — ambiguous store assignment | Local Reach | Open — see Candidate table above (narrowed from the original general-Jogeshwari entry) | 2026-09-26 |
