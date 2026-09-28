# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-28
**Status:** 🟢 3 new locality pages shipped this run (Jogeshwari West → Malad, resolving last run's open candidate; Malvani → Malad; Kolshet Road → Thane). Site grew from 49 to 52 pages. WebFetch tested again this run — still blocked (`EGRESS_BLOCKED`) for every domain tried (Nominatim, Wikipedia), now 4 consecutive runs; WebSearch used as the geocoding substitute as in prior runs. No other technical/schema/AEO/E-E-A-T issues found; full 52-page verification sweep clean.

Site: 52 pages (1 homepage + 5 store pages + 46 locality pages) generated from `data/stores.json` via `generate.py`.

**Housekeeping:** checkout was on a detached HEAD at `76e708c` (matching `origin/main`) at run start, likely left over from a prior run. Switched to `main` and fast-forward pulled 5 commits — no data loss, no reconciliation conflicts.

**Network access note — still open, fourth consecutive run:** WebFetch returned `EGRESS_BLOCKED` for both Nominatim and a Wikipedia control this run — same blanket block reported on 2026-09-25, 26 and 27. This still contradicts the task prompt's assumption that WebFetch bypasses the sandbox's network block. WebSearch continues to work fully and was used for all geocoding this run, cross-checked against specific named landmarks (metro stations, roads) rather than generic locality-name searches, then distance computed locally via Bash/python3 haversine. Live-site verification (confirming the deployed site matches the repo) remains skipped for the 4th run in a row.

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
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch to the live domain not tested separately this run since Nominatim/Wikipedia controls both failed first (see network note above) |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 51 store/locality pages; `Organization` + 5×`SportingGoodsStore` on the homepage.
- Re-scanned all 52 pages' JSON-LD for any `Review` node carrying a `reviewRating` field (the fabrication pattern fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` correctly present only where `reviews.rating` is a real, non-null value (Malad, Thane). Correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating: null` in source data).
- New locality entries (Jogeshwari West, Malvani, Kolshet Road) carry only `name`, `slug`, `km`, `minutes`, `blurb` — same four fields as every existing locality. No new field fabricated; distance/minutes computed, not invented.

## 3. AI Citability / AEO

- Entity-coverage re-check (programmatic, HTML-entity-aware): all 6 categories, all 3 brands (LS2, Crank1, MadDog), the EMI policy sentence, and the 7-day return policy sentence each still appear on all 5 store pages after regeneration. No gap.
- All 3 new locality pages state a real, specific named landmark/route and a concrete distance/ride-time — no generic filler (Oshiwara metro station/New Link Road/film-studio hub for Jogeshwari West; Malvani Road/Ambojwadi/Gate No. 8 for Malvani; Kolshet Creek/Hiranandani Estate/industrial belt for Kolshet Road).
- `llms.txt` regenerated and spot-checked: all 3 new locality names now appear in their correct store's "Serves:" line; phone numbers and `maps_url`s unchanged and correct.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run — no changes made to any of these (bucket C).
- NAP consistency re-verified programmatically across all 52 pages: all 5 stores' phone numbers appear byte-for-byte on every page including the 3 new locality pages.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` unchanged since 2026-09-17 — still the human's active research doc, not touched.

## 5. Platform Optimization

- FAQs unchanged this run; still cover the full natural buying-decision set (certification, try-before-buy, stock-check, EMI/returns, brands carried, exact location) on every page, including the 3 new locality pages (which reuse each store's FAQ set, same as every other locality page).

## 6. Local Reach Gaps

One open candidate going into this run (Jogeshwari West, ambiguous Malad-vs-Santacruz assignment, carried from 2026-09-26/27). Per the revised process (Nominatim itself still blocked — see network note — so used WebSearch to find a specific, well-known landmark's coordinates rather than a generic locality-name search), re-investigated it and also scanned nearby stores' catchments for other well-known localities not yet covered, prioritizing Mira Road (only 5 localities vs 10-11 for the other stores).

Checked 5 candidates: Jogeshwari West, Uttan (Mira Road), Dahisar West (Mira Road), Kolshet Road (Thane), Malvani (Malad). **3 resolved and shipped, 2 checked and rejected/deferred.**

### Added this run

| Locality | Store | Road-est km | Minutes | Source |
|---|---|---|---|---|
| Jogeshwari West | Malad | 4.7 | 16-20 | Oshiwara metro station coordinates (19.1460351, 72.8339520 — on New Link Road, Anand Nagar, Jogeshwari West, via Wikipedia through WebSearch) gave a clear margin: 4.7km road-est to Malad vs 8.6km road-est to Santacruz — a 3.9km gap, unlike the near-tie from the vaguer general-Jogeshwari-West coordinate used on 2026-09-26/27. Minutes interpolated between the Kandivali East (4.0km/15-20min) and Goregaon East (5.5km/18-22min) entries, the closest existing ratio analogs for this store |
| Malvani | Malad | 3.7 | 10-14 | Malvani Road coordinates (19.176215, 72.809731, via findlatitudeandlongitude.com through WebSearch) → 3.7km road-est, well within range. Minutes matched to the similar-distance Malad East (2.9km/10-12min), Charkop (3.3km/10-12min) and Kandivali West (3.9km/10-15min) entries, all clustered around 10-14min for this store's near band |
| Kolshet Road | Thane | 6.1 | 16-20 | Kolshet Road coordinates (19.2411248, 72.9898536, via coordinatesfinder.com through WebSearch) → 6.1km road-est. Minutes interpolated between the Mulund West (5.2km/15-18min) and Ghodbunder Road (7.5km/20-25min) entries, the closest existing ratio analogs for this store |

All 3 blurbs are hand-written and name real, specific landmarks confirmed via WebSearch before writing: the Oshiwara metro station, New Link Road and its film-production-office reputation for Jogeshwari West; Malvani Road, Ambojwadi and Gate No. 8 for Malvani; Kolshet Creek, the Kolshet industrial area and Hiranandani Estate for Kolshet Road. None is a template with only the name swapped — each frames a distinct rider motivation (studio-corridor commuters, dense-residential first-time buyers, industrial/warehouse shift workers) consistent with its store's existing locality voice.

### Logged / checked — not resolved this run

| Locality | Store (candidate) | Reason not added |
|---|---|---|
| Uttan | Mira Road | Coordinates (19.280, 72.785, via Wikipedia through WebSearch) → 12.6km road-est. Over the ~10km ceiling. |
| Dahisar West | Mira Road | The only specific landmark found (Dahisar railway station, 19.2501, 72.8593) sits on the boundary between Dahisar East and West and is effectively the same coordinate the existing "Dahisar" entry would already represent (that entry's blurb already references the WEH/Dahisar Toll Naka side). Not confident enough that a "Dahisar West" page would be genuinely distinct rather than a near-duplicate of the existing entry — needs a more specific West-side landmark (a road/station clearly on that side) to justify a separate page. |

### Verification performed before shipping

- `python3 generate.py` re-run: 49 → 52 pages, zero errors.
- Re-ran the full technical checklist (titles/descriptions, JSON-LD, broken links, alt text, sitemap-vs-files parity, robots.txt, llms.txt) against the regenerated output — all pass, see Section 1.
- Re-ran entity-coverage (HTML-entity-aware) and NAP checks — both still pass with the new pages included.
- Confirmed the reviewRating-fabrication fix still holds across all 52 pages (grep-equivalent scan of JSON-LD for `reviewRating` — 0 hits).
- Confirmed the 3 new blurbs are unique strings (no accidental duplication) and spot-checked each new page's `<title>`/meta description for correct length and content.

---

## Candidate localities awaiting human geocoding

| Locality | Candidate store | Note |
|---|---|---|
| Dahisar West | Mira Road | Needs a specific, clearly-West-side landmark (not the shared railway station) to confidently distinguish it from the existing "Dahisar" entry and avoid near-duplicate content. |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Jogeshwari West candidate was a near-tie in the last 2 runs (Malad vs Santacruz) | Local Reach | Re-geocoded using a specific landmark (Oshiwara metro station) instead of the general locality name — resolved to Malad with a confident 3.9km margin. Added as a new locality page. | See Section 6 for method and sources |
| Mira Road store notably sparse (5 localities vs 10-11 for other stores) | Local Reach | Investigated as a candidate-search target this run; checked Uttan (rejected, over threshold) and Dahisar West (deferred, insufficiently distinct landmark) | No pages added for Mira Road this run — genuine gap check, not a mandate to pad the count |
| Kolshet Road and Malvani identified as missing, geocodable, well-known localities near Thane and Malad respectively | Local Reach | Geocoded via WebSearch (Nominatim still blocked, see network note), added as new locality pages | See Section 6 for sources and distances |
| Full technical/schema/AEO/E-E-A-T sweep across all 52 pages | All | Re-verified, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt all clean post-regeneration |
| WebFetch blocked for every domain tested (Nominatim, Wikipedia control) — fourth consecutive run | Technical GEO/SEO | Flagged again, not fixable from this session — environment-level egress proxy blocks WebFetch entirely | Adapted to WebSearch-only geocoding again; live-site verification skipped for the 4th run running |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| WebFetch returns `EGRESS_BLOCKED` for external domains in this environment (Nominatim, Wikipedia, and previously the live site), despite being expected to work per the task prompt | Technical GEO/SEO / Local Reach | Open, now 4 consecutive runs — worked around via WebSearch each time; live-site checks remain unavailable until this is fixed at the environment level | 2026-09-25 |
| Dahisar West — insufficiently distinct landmark vs existing "Dahisar" entry | Local Reach | Open — see Candidate table above | 2026-09-28 |
