# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-11-20
**Status:** 🟢 Clean sweep. Fresh programmatic sweep of all 64 pages found **0 issues**. No new locality pages added this run — the three remaining open candidates (Uttan, Ghatkopar West, Kamothe) were re-checked via WebSearch; one new (unconfirmed, low-confidence) data point surfaced for Uttan but wasn't acted on — see Local Reach Gaps. Two new candidate localities (Madh Island, Marol) identified and logged, not added (no confident geocode). Site remains **64 pages** (1 homepage + 5 store pages + 58 locality pages), unchanged since 2026-11-06.

**Housekeeping:** Session started with `HEAD` detached at a commit (`8a5c0b6`) two commits ahead of the local `main` branch ref, with that commit already on `origin/main` (prior run's work, already pushed). Reset local `main` to `origin/main` (`495615f` → `8a5c0b6`) — no work lost, no reconciliation conflicts.

**Network access note — WebFetch still blocked at the session network-policy level:** This run's instructions again stated WebFetch/WebSearch now bypass the sandbox VM's network block. Tested directly this run against **both** `nominatim.openstreetmap.org` and the live site `helmetstorenearme.in` — both failed with `getaddrinfo ENOTFOUND`, consistent with every prior test since 2026-09-25. `WebSearch` works fully and was used for all research and geocoding this run, same as every prior run.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 64/64 match exactly, 0 missing, 0 extra |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 64 pages |
| Broken internal links | ✅ 0 found (1,199 internal hrefs checked across all 64 pages) |
| Image alt text | ✅ All `<img>` tags have non-empty, descriptive alt text |
| Title tag length | ✅ All 64 ≤60 chars (post-entity-decode), all unique |
| Meta description length/uniqueness | ✅ All 64 unique, all ≤140 chars |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch confirmed blocked against the live host this run (tested directly, `getaddrinfo ENOTFOUND`) |

**This run's check script:** written fresh in the scratchpad (not committed — disposable tooling), covering sitemap-vs-pages, robots.txt, JSON-LD parse + schema-type completeness (`SportingGoodsStore`/`FAQPage`/`BreadcrumbList`/`openingHoursSpecification`), the reviewRating-fabrication pattern, `AggregateRating` value-correctness against `reviews.rating`/`reviews.count`, broken internal links, alt text, title/description length+uniqueness, canonical tags, NAP consistency, entity coverage, and `llms.txt` drift. **0 issues.**

**This run's resolved key-name note:** `data/stores.json`'s per-store fields are `phone_display`/`phone_tel` (not `phone`) and each locality's distance/time fields are `km`/`minutes` (not `distance_km`/`ride_minutes`) — corrected in the check script after an initial `KeyError`; no data issue, just a reminder for next run's tooling.

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes. Still needs a human call on approach. First flagged 2026-09-18, unchanged this run.

**Minor observation, not actioned:** `data/stores.json`'s brand-wide `tagline` ("Ride your dream") is not rendered verbatim on any page — `generate.py` doesn't currently use it. Not an entity-coverage gap under this audit's criterion (a tagline is marketing copy, not a quotable fact); inserting it is a brand-voice/design decision, left untouched (bucket C).

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` present on all 63 store/locality pages, verified programmatically this run — 0 missing.
- `openingHoursSpecification` present on all 63 store/locality pages — 0 missing.
- Re-scanned all pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` programmatically re-verified against source `reviews.rating`/`reviews.count`: Malad (4.7/2445) and Thane (4.5/34) carry correct values; Santacruz, Mira Road and Navi Mumbai correctly carry no `AggregateRating` (source `reviews.rating` is `null` for all three). 0 mismatches, 0 fabrications.

## 3. AI Citability / AEO

- Entity-coverage re-check: all brand-wide `categories`, all `brands_carried`, and the brand description all appear verbatim (post-`html.unescape()`) somewhere on the site. 0 gaps against this audit's criterion.
- `llms.txt` re-checked programmatically against current `data/stores.json` — every store name, every phone number, and all 58 locality names found verbatim. No drift.
- No new entity-coverage or FAQ gaps surfaced this run.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all store/locality pages: each store's phone number appears on every page belonging to that store, 0 mismatches.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` last modified 2026-09-17, unchanged since — still the human's own active track, not touched this run.

## 5. Platform Optimization

- Spot-checked FAQ coverage across all 5 stores (4 FAQs each, consistent pattern: certification, try-on, location, stock-check). No new buying-decision gap surfaced this run.

## 6. Local Reach Gaps

**No new locality pages added this run.** All three open candidates were re-investigated via WebSearch with fresh queries; none resolved cleanly enough to act on. Two new candidate names surfaced during a general-knowledge scan and were researched the same run (per the "resolve immediately, don't wait" instruction) but neither had a confident-enough geocode to add, so both were logged instead.

- **Uttan (Mira Road) — still unresolved, one new data point, not actionable.** Fresh search surfaced a second coordinate for Uttan from a housing.com listings page: 19.2683°N, 72.8102°E, which gives 9.44km straight-line × 1.3 ≈ **9.4km** from the Mira Road store (`19.2843751, 72.8772246`) — under the ~10km ceiling, unlike the existing Wikipedia town-center point (19.280°N, 72.785°E → 12.6km). However, the search itself flagged that "the two sources don't agree on a single centre for the town" (a ~3km spread), and a real-estate listings-aggregator coordinate is exactly the kind of low-quality, non-suburb/junction/station source this process is supposed to discourage over a proper Nominatim geocode. Not confident enough to add; left open, now with both competing coordinates noted in the candidate table.
- **Ghatkopar West (Santacruz) — still unresolved.** New rome2rio figures: Santacruz→Ghatkopar West driving 9.6km/~10min; Santacruz→Ghatkopar (general) 10.3km/~11min; Yometro metro-corridor ~10km vs. mumbaimetroroute.com's 12.0km. Still straddles the ~10km ceiling exactly as in every prior run — no new data moves it cleanly under or over. Left open.
- **Kamothe (Navi Mumbai) — still unresolved.** New search reconfirms Kamothe borders CBD Belapur (15–20min driving) and gives CBD Belapur's Wikipedia coordinate (19.01694°N, 73.03944°E, matching the Navi Mumbai store's own location almost exactly) but still no Kamothe sector-1/2-specific coordinate. Left open.
- **New-locality scan — two new names found, researched, neither added:**
  - **Madh Island (Malad)** — plausible (it's the natural extension of the already-listed Marve Road locality, a real riding/weekend-ride destination). But distance data conflicts hard: Squareyards puts Marve-to-Madh at 6.5km (which stacked on Marve Road's existing 2.2km gives ~8.7km road-distance from the store, under ceiling), while MyGate puts Malad-to-Madh at ~10km and Squareyards separately puts Malad West-to-Madh at 11.3km (both over ceiling). No single source gives store-to-Madh directly, and no Nominatim geocode available to settle it. Logged as a new candidate, not added.
  - **Marol / Marol Naka (Santacruz)** — plausible (well-known MIDC industrial/commercial junction with heavy two-wheeler commuter traffic, a natural Santacruz-store customer base). Road-distance estimates from rome2rio conflict: a stated "7km" summary figure vs. a 9.4km taxi-route figure from the same source (with an even-less-trustworthy 8.4km walking figure printed alongside, undermining confidence in the set). Both numbers are plausibly under the ~10km ceiling, but with no confirmed single-point geocode for Marol Naka itself, logged as a new candidate rather than added on a guess.
- **Previously-rejected list unchanged this run** (Shilphata, Kasarvadavali, Aarey Colony, Ulwe, Mira Road West, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Taloja, Poonam Sagar, Hiranandani Estate, Bandra Kurla Complex, Teen Hath Naka/Khopat/Kopri, Golden Nest, Naigaon, Oshiwara cluster, Dindoshi, Powai, Kalina, Seawoods, "Upper Thane", Chincholi Bunder, Louiswadi, Liberty Garden, Thakur Village, Koparkhairane/Ghansoli/Airoli, Beverly Park, Minakshi Nagar, Anand Nagar, Prabhadevi).

Coverage remains at 58 localities across all 5 stores. Precise geocoding (Nominatim via WebFetch) remains blocked at the session network-policy level — confirmed again this run against both Nominatim and the live site (both `getaddrinfo ENOTFOUND`). WebSearch remains the only viable research path, and for all five open candidates (3 carried-over + 2 new), the blocker is now consistently the same: conflicting or missing precise source coordinates, not a lack of search effort. A real routing-API/geocoder reachable from this session, or a human call, is what would actually move these forward.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script covering sitemap-vs-pages, robots.txt bot coverage, JSON-LD parsing, all internal links, image alt text, title/description length and uniqueness, and canonical tags (64 pages, 0 issues). No regeneration was needed since no data changed.
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness against source `reviews.rating`, FAQPage/BreadcrumbList/SportingGoodsStore/openingHoursSpecification completeness) — **0 issues found**.
- Entity-coverage (brand-wide categories, brands_carried, policies, description), NAP, and `llms.txt` drift checks, all re-verified programmatically against current `data/stores.json` — **0 issues found**.
- Git state checked and reconciled at run start (detached HEAD at a commit already on `origin/main`; local `main` reset to match, clean tree, no lost work).
- WebFetch re-tested directly against both `nominatim.openstreetmap.org` and `helmetstorenearme.in` — confirmed still blocked (`getaddrinfo ENOTFOUND`) for both. WebSearch confirmed working and used for all research.
- All three open candidates re-investigated via WebSearch with fresh queries; one new (unconfirmed) data point surfaced for Uttan, none resolved either direction — see Local Reach Gaps above.
- Two new candidate names (Madh Island, Marol) found via general-knowledge scan, researched the same run, neither had a confident enough single-point geocode to add — logged instead.
- No `python3 generate.py` run this run — no data changes were made, so no regeneration was needed.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Two competing coordinates: Wikipedia town-center (19.280°N, 72.785°E) gives 12.6km (over ceiling); a housing.com listings-page point (19.2683°N, 72.8102°E) gives 9.4km (under ceiling) — but the two disagree by ~3km and the search itself noted the sources "don't agree on a single centre," and a listings-aggregator point is a weak substitute for a proper suburb/junction geocode. No naka/junction-level point exists for Uttan itself. Re-checked this run via WebSearch; new data found but not trustworthy enough to act on. Needs Nominatim (once reachable) or a human call. | 2026-10-22 |
| Ghatkopar West | Santacruz (nominal nearest) | Station-level points give 9.85–9.87km straight-line×1.3 — just under the ceiling — but real third-party driving-distance figures (rome2rio: 9.6km/10.3km; Yometro ~10km; mumbaimetroroute.com 12.0km) straddle the ceiling, since there's no direct road (crosses via JVLR/SCLR through the hills) and the ×1.3 heuristic is unreliable for this hop. Re-checked this run with fresh distance figures; still straddles the ceiling. Needs a real routing-API check or a human call. | 2026-10-24 |
| Kamothe | Navi Mumbai (nominal nearest) | Real-estate sources confirm it directly adjoins CBD Belapur (~15–20min driving), but candidate points vary by sector: village-center gives 9.99km×1.3 (at the ceiling); a single-sourced Sector 18 point gives 9.0km×1.3. No source confirms coordinates for the sectors (1–2) likely nearest the actual border. Re-checked this run; CBD Belapur's own coordinate reconfirmed (near-identical to the store's own location) but still no Kamothe-sector-specific point. Needs a confirmed sector-boundary map or a human call before adding. | 2026-11-04 |
| Madh Island | Malad (nominal nearest, natural extension of existing Marve Road locality) | Conflicting distance data: Marve-to-Madh (Squareyards) 6.5km, which stacked on Marve Road's existing 2.2km from-store figure implies ~8.7km road-distance (under ceiling) — but Malad-to-Madh (MyGate) ~10km and Malad West-to-Madh (Squareyards) 11.3km both suggest over ceiling. No single store-to-Madh figure found, no Nominatim geocode available. New this run. | 2026-11-20 |
| Marol / Marol Naka | Santacruz (nominal nearest; well-known MIDC junction, heavy two-wheeler-commuter area) | rome2rio gives conflicting figures for the same route: a "7km" summary line vs. a 9.4km taxi-route figure vs. an 8.4km walking-route figure (walking shorter than driving is itself a red flag on data quality). Plausibly under the ~10km ceiling but no confirmed single-point geocode for Marol Naka itself. New this run. | 2026-11-20 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep | All | Verified via a fresh programmatic sweep over all 64 pages — **0 issues found** | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ/BreadcrumbList/SportingGoodsStore/openingHoursSpecification coverage, reviewRating-fabrication pattern all clean. No (A) fixes needed. |
| Uttan (Mira Road), Ghatkopar West (Santacruz), Kamothe (Navi Mumbai) locality candidates | Local Reach | Re-investigated via WebSearch with fresh queries; one new but low-confidence data point for Uttan, no data moved any of the three cleanly under/over the threshold | Left in candidate table, Uttan entry updated with the new (conflicting) coordinate |
| Madh Island (Malad), Marol/Marol Naka (Santacruz) — two new candidate names | Local Reach | Identified via general-knowledge scan, researched same run via WebSearch; both have plausible-but-conflicting road-distance data and no confirmed single-point geocode | Logged to candidate table rather than added, per the "don't guess" rule |
| WebFetch blocked — re-confirmed against both Nominatim and the live site | Technical GEO/SEO / Local Reach | Re-tested directly; confirmed still blocked (`getaddrinfo ENOTFOUND`) for both hosts despite this run's instructions claiming otherwise | WebSearch confirmed working and used for all research and geocoding this run |
| Git state at run start | Housekeeping | Detached `HEAD` (already on `origin/main`) reconciled; local `main` reset to match | No work lost, no conflicts |

**This run's site/data changes:** none. No (A) mechanical fixes were needed and no (B) new locality pages were added — the technical/schema/AEO/E-E-A-T sweep found 0 issues, and all locality-candidate research this run resulted in "still unresolved" or "logged, not added." `data/stores.json` and all generated output are unchanged from 2026-11-06. Only this audit file was updated.

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (session network-policy block) | Technical GEO/SEO / Local Reach | Open — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until the relevant hosts are added to the session's network allowlist. Re-confirmed this run against both Nominatim and the live site directly. | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run (new conflicting coordinate found, not actioned) — see candidate table above | 2026-10-22 |
| Ghatkopar West — candidate locality needing a real-route distance check or human call | Local Reach | Open, re-checked this run with new distance figures — see candidate table above | 2026-10-24 |
| Kamothe (Navi Mumbai) — candidate locality, right at the ~10km ceiling with sector-boundary uncertainty | Local Reach | Open, re-checked this run — see candidate table above | 2026-11-04 |
| Madh Island (Malad) — candidate locality, conflicting road-distance data (~8.7–11.3km depending on source) | Local Reach | New this run — see candidate table above | 2026-11-20 |
| Marol/Marol Naka (Santacruz) — candidate locality, conflicting road-distance data from a single source (7–9.4km) | Local Reach | New this run — see candidate table above | 2026-11-20 |

*(Three other items — "no press/backlinks" (first flagged 2026-09-15), "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18), and "MadDog brand not named verbatim in homepage's brand-description copy" (first flagged 2026-09-16, not a real entity-coverage gap since MadDog is already quotable on all 5 store pages) — remain open >30 days and continue to be trimmed from this table per the 30-day rule, since none needs daily re-litigation: the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, the sitemap item needs a one-time human decision on approach, and the MadDog item is a non-issue under this audit's own entity-coverage criterion.)*
