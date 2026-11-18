# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-11-18
**Status:** 🟢 Clean sweep. Fresh programmatic sweep of all 64 pages found **0 issues**. No new locality pages added this run — the three remaining open candidates (Uttan, Ghatkopar West, Kamothe) stay unresolved after a fresh WebSearch pass, and **Prabhadevi** is reclassified from "open/uncertain" to a confident reject (see below) and dropped from the candidate table. Site remains **64 pages** (1 homepage + 5 store pages + 58 locality pages), unchanged since 2026-11-06.

**Housekeeping:** Repo was already on `main`, fast-forwarded to `origin/main`, clean working tree at session start — no reconciliation needed this run.

**Gap note:** No audit commits are recorded between 2026-11-06 and today (2026-11-18). Cause not investigated (outside this run's scope — likely the schedule not firing on those days rather than a site issue); flagged here for awareness, not acted on.

**Network access note — WebFetch still blocked at the session network-policy level:** This run's instructions again stated WebFetch/WebSearch now bypass the sandbox VM's network block. Tested directly this run against **both** `nominatim.openstreetmap.org` and the live site `helmetstorenearme.in` — both failed with `getaddrinfo ENOTFOUND`, the tool's own error text confirming both hosts are outside this session's allowed network domains. Per the tool's own guidance not to keep trying further hosts once that pattern repeats, no other hosts were tested. `WebSearch` works fully and was used for all research and geocoding this run, the same workaround used in every prior run since 2026-09-25.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 64/64 match exactly, 0 missing, 0 extra |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 64 pages |
| Broken internal links | ✅ 0 found (fresh link-checker sweep over all internal links) |
| Image alt text | ✅ All `<img>` tags have non-empty, descriptive alt text |
| Title tag length | ✅ All 64 ≤60 chars (post-entity-decode), all unique |
| Meta description length/uniqueness | ✅ All 64 unique, all ≤140 chars |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch confirmed blocked against the live host this run (tested directly, `getaddrinfo ENOTFOUND`) |

**This run's check script:** written fresh in the scratchpad (not committed — disposable tooling), covering sitemap-vs-pages, robots.txt, JSON-LD parse + schema-type completeness (`SportingGoodsStore`/`FAQPage`/`BreadcrumbList`/`openingHoursSpecification`), the reviewRating-fabrication pattern, `AggregateRating` value-correctness against `reviews.rating`/`reviews.count`, broken internal links, alt text, title/description length+uniqueness, and canonical tags. **0 issues.**

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes. Still needs a human call on approach. First flagged 2026-09-18, unchanged this run.

**Minor observation, not actioned:** `data/stores.json`'s brand-wide `tagline` ("Ride your dream") is not rendered verbatim on any page — `generate.py` doesn't currently use it. This isn't an entity-coverage gap under this audit's own criterion (brands/categories/hours/policies/certifications — a tagline is marketing copy, not a quotable fact), and inserting it into page copy is a brand-voice/design decision, so left untouched (bucket C).

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` present on all 63 store/locality pages, verified programmatically this run — 0 missing.
- `openingHoursSpecification` present on all 63 store/locality pages — 0 missing.
- Re-scanned all pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` programmatically re-verified against source `reviews.rating`/`reviews.count`: Malad (4.7/2445) and Thane (4.5/34) carry correct values; Santacruz, Mira Road and Navi Mumbai correctly carry no `AggregateRating` (source `reviews.rating` is `null` for all three, even though `reviews.count` is populated for Santacruz/Mira Road). 0 mismatches, 0 fabrications.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 brand-wide categories, all 3 brands (LS2, Crank1, MadDog), both brand-wide policy sentences (EMI, 7-day return), and the brand description all appear verbatim (post-`html.unescape()`) somewhere on the site. 0 gaps against this audit's criterion.
- `llms.txt` re-checked programmatically against current `data/stores.json` — every store name, every phone number, and all 58 locality names found verbatim. No drift.
- No new entity-coverage or FAQ gaps surfaced this run.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all store/locality pages: each store's phone number appears on every page belonging to that store, 0 mismatches.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` last modified 2026-09-17, unchanged since — still the human's own active track, not touched this run.

## 5. Platform Optimization

- Spot-checked FAQ coverage across all 5 stores (4 FAQs each, consistent pattern). No new buying-decision gap surfaced this run.

## 6. Local Reach Gaps

**No new locality pages added this run.** A dedicated WebSearch research pass was run against all four open candidates plus a fresh scan for any missing well-known localities.

- **Prabhadevi (Santacruz) — reclassified from "open/uncertain" to a confident reject, dropped from the candidate table.** Previous runs used the neighborhood-center coordinate (7.80km×1.3=10.14km). This run found the actual Parel–Prabhadevi railway station — the real point of interest for a "near me" search — cross-referenced from two independent sources agreeing within ~150m (19.008085°N,72.836527°E and 19.0075°N,72.8359°E). Straight-line from the Santacruz store = 8.71–8.78km × 1.3 = **11.3–11.4km**, more confidently over the ~10km ceiling than the earlier estimate, not less. Since the station sits *further* from the store than the neighborhood center, no plausible future data point moves this back under the ceiling. Also redundant with the existing Mahim entry (7.0km) covering the same southward corridor. Not re-queued; moved to the rejected-candidates list.
- **Ghatkopar West (Santacruz) — still unresolved, new data recorded.** Found two independently-close station-level points (Ghatkopar railway station 19.0857°N,72.9081°E; Ghatkopar metro station 19.086660°N,72.90799°E, agreeing within ~150m) instead of the vague area center used before. Straight-line×1.3 from these = 9.85–9.87km, technically just under the ceiling — but real third-party driving-distance figures (rome2rio) range 9.6–10.8km depending on exact endpoint (West vs. general vs. East), straddling the ceiling. This confirms the existing note's concern: the straight-line×1.3 heuristic is unreliable for this hop since there's no direct road (it crosses via JVLR/SCLR through the hills). Left open — needs a real routing-API check or human call, not just a tighter geocode.
- **Uttan (Mira Road) — still unresolved.** No naka/junction-level coordinate exists for Uttan itself (only the town-center point, 19.280°N,72.785°E = 9.69km×1.3 = 12.6km, unchanged and still over the ceiling). "Navghar Naka" is a staging point for transport *toward* Uttan, not in Uttan itself, so it doesn't help. Left open.
- **Kamothe (Navi Mumbai) — still unresolved.** No sector-boundary coordinates found for the sectors (1–2) likely nearest the CBD Belapur border; only the previously-used Sector 18 point (9.0km×1.3) is sourced, and only from a single uncorroborated source. A resident review confirms a qualitative "15–20 minutes" Kamothe-to-CBD-Belapur driving time, consistent with being near/at the ceiling but not a usable km figure. Left open.
- **New-locality scan:** checked all 5 stores' `localities` arrays against general knowledge of nearby well-known Mumbai/Navi Mumbai/Thane suburbs within ~10km. No genuinely well-known, high-confidence locality found missing that isn't already covered by the long-standing previously-examined-and-rejected list (Shilphata, Kasarvadavali, Aarey Colony, Ulwe, Mira Road West, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Taloja, Poonam Sagar, Hiranandani Estate, Bandra Kurla Complex, Teen Hath Naka/Khopat/Kopri, Golden Nest, Naigaon, Oshiwara cluster, Dindoshi, Powai, Kalina, Seawoods, "Upper Thane", Chincholi Bunder, Louiswadi, Liberty Garden, Thakur Village, Koparkhairane/Ghansoli/Airoli, Beverly Park, Minakshi Nagar, Anand Nagar).

Coverage remains at 58 localities across all 5 stores. Precise geocoding (Nominatim via WebFetch) remains blocked at the session network-policy level — confirmed again this run against both Nominatim and the live site. WebSearch-sourced cross-referencing of a specific named landmark/station (not just the locality's general area) remains the viable path to resolve further candidates, as it was for Yeoor and Waghbil — but for Ghatkopar West and Uttan the blocker isn't geocoding precision any more, it's that the straight-line×1.3 heuristic itself breaks down on these particular cross-city/isolated hops (confirmed by comparing against real third-party driving-distance figures this run).

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script covering sitemap-vs-pages, robots.txt bot coverage, JSON-LD parsing, all internal links, image alt text, title/description length and uniqueness, and canonical tags (64 pages, 0 issues). No regeneration was needed since no data changed.
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness against source `reviews.rating`, FAQPage/BreadcrumbList/SportingGoodsStore/openingHoursSpecification completeness) — **0 issues found**.
- Entity-coverage (brand-wide categories, brands_carried, policies, description), NAP, and `llms.txt` drift checks, all re-verified programmatically against current `data/stores.json` — **0 issues found**.
- Git state checked and reconciled at run start (already on `main`, up to date with `origin/main`, clean tree).
- WebFetch re-tested directly against both `nominatim.openstreetmap.org` and `helmetstorenearme.in` — confirmed still blocked (`getaddrinfo ENOTFOUND`) for both. WebSearch confirmed working and used for all research.
- All four open candidates re-investigated via WebSearch with new, more specific data points (station/landmark coordinates rather than area centers) and cross-referenced against third-party driving-distance figures where available. Prabhadevi resolved as a confident reject; the other three remain genuinely unresolved for distinct reasons (over ceiling / heuristic breakdown / missing sector data).
- No `python3 generate.py` run this run — no data changes were made, so no regeneration was needed.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Town-center coordinate (19.280°N, 72.785°E) gives 9.69km straight-line × 1.3 = 12.6km from the Mira Road store — over the ~10km threshold. No naka/junction-level point exists for Uttan itself ("Navghar Naka" is a staging point toward it, not in it). Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. | 2026-10-22 |
| Ghatkopar West | Santacruz (nominal nearest) | Station-level points (Ghatkopar railway station / metro station, agreeing within ~150m) give 9.85–9.87km straight-line×1.3 — just under the ceiling — but real third-party driving-distance figures range 9.6–10.8km depending on exact endpoint, since there's no direct road (crosses via JVLR/SCLR through the hills) and the ×1.3 heuristic is unreliable for this hop. Needs a real routing-API check or a human call, not just a tighter geocode. | 2026-10-24 |
| Kamothe | Navi Mumbai (nominal nearest) | Real-estate sources say it directly adjoins CBD Belapur (~15-20min driving, confirmed again this run via a qualitative resident review), but candidate points vary by sector: village-center gives 9.99km×1.3 (at the ceiling); a single-sourced Sector 18 point gives 9.0km×1.3. No source confirms coordinates for the sectors (1-2) likely nearest the actual border. Needs a confirmed sector-boundary map or a human call before adding. | 2026-11-04 |

**Resolved this run (moved out of this table): Prabhadevi (Santacruz)** — now a confident reject rather than an open candidate. The actual Parel–Prabhadevi railway station (the real point of interest, cross-referenced from two sources agreeing within ~150m) is 8.71–8.78km×1.3 = 11.3–11.4km from the Santacruz store — more clearly over the ceiling than the earlier neighborhood-center estimate, and redundant with the existing Mahim entry covering the same corridor. Folded into the long-standing previously-examined-and-rejected list; not expected to need re-litigation.

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep | All | Verified via a fresh programmatic sweep over all 64 pages — **0 issues found** | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ/BreadcrumbList/SportingGoodsStore/openingHoursSpecification coverage, reviewRating-fabrication pattern all clean. No (A) fixes needed. |
| Prabhadevi (Santacruz) locality candidate | Local Reach | Re-investigated via WebSearch using the actual railway-station point instead of the neighborhood center; confirmed more clearly over the ~10km ceiling (11.3-11.4km) | Reclassified from open candidate to confident reject; dropped from the awaiting-geocoding table |
| Ghatkopar West (Santacruz) locality candidate | Local Reach | Re-investigated via WebSearch; found tighter station-level coordinates (just under ceiling by straight-line×1.3) but real driving-distance figures straddle the ceiling, confirming the heuristic itself is unreliable for this hop | Left in candidate table with updated note — needs a real routing-API check or human call |
| Uttan (Mira Road), Kamothe (Navi Mumbai) locality candidates | Local Reach | Re-investigated via WebSearch; no new data moves either under/over the threshold | Left in candidate table, unchanged |
| New-locality scan (all 5 stores) | Local Reach | Checked against general knowledge; no new genuinely well-known, high-confidence candidate found | No action |
| WebFetch blocked — re-confirmed against both Nominatim and the live site | Technical GEO/SEO / Local Reach | Re-tested directly; confirmed still blocked (`getaddrinfo ENOTFOUND`) for both hosts despite this run's instructions claiming otherwise | WebSearch confirmed working and used for all research and geocoding this run |
| Git state at run start | Housekeeping | Already on `main`, up to date with `origin/main`, clean tree | No reconciliation needed |

**This run's site/data changes:** none. No (A) mechanical fixes were needed and no (B) new locality pages were added — the technical/schema/AEO/E-E-A-T sweep found 0 issues, and all locality-candidate research this run resulted in either "still unresolved" or a reclassification within the audit file itself (Prabhadevi), not a `data/stores.json` change. `data/stores.json` and all generated output are unchanged from 2026-11-06.

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (session network-policy block) | Technical GEO/SEO / Local Reach | Open — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until the relevant hosts are added to the session's network allowlist. Re-confirmed this run against both Nominatim and the live site directly. | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-22 |
| Ghatkopar West — candidate locality needing a real-route distance check or human call | Local Reach | Open, re-checked this run with new station-level data — see candidate table above | 2026-10-24 |
| Kamothe (Navi Mumbai) — candidate locality, right at the ~10km ceiling with sector-boundary uncertainty | Local Reach | Open, re-checked this run — see candidate table above | 2026-11-04 |

*(Prabhadevi, first flagged 2026-10-27, is resolved as of this run — see above — and is no longer carried over. Three other items — "no press/backlinks" (first flagged 2026-09-15), "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18), and "MadDog brand not named verbatim in homepage's brand-description copy" (first flagged 2026-09-16, not a real entity-coverage gap since MadDog is already quotable on all 5 store pages) — remain open >30 days and continue to be trimmed from this table per the 30-day rule, since none needs daily re-litigation: the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, the sitemap item needs a one-time human decision on approach, and the MadDog item is a non-issue under this audit's own entity-coverage criterion.)*
