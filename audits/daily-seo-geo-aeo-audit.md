# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-11-19
**Status:** 🟢 Clean sweep. Fresh programmatic sweep of all 64 pages found **0 issues**. No new locality pages added this run — the three remaining open candidates (Uttan, Ghatkopar West, Kamothe) were re-checked via WebSearch with no new tie-breaking data; all three stay unresolved. Site remains **64 pages** (1 homepage + 5 store pages + 58 locality pages), unchanged since 2026-11-06.

**Housekeeping:** Session started with `HEAD` detached at a commit one ahead of the local `main` branch ref (prior run's work, already pushed to `origin/main`). Checked out `main` and fast-forwarded it to `origin/main` (`495615f` → `e8eb4a4`) — no work lost, no reconciliation conflicts.

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

**No new locality pages added this run.** All three open candidates were re-investigated via WebSearch with fresh queries; none produced new data that resolves them either direction.

- **Uttan (Mira Road) — still unresolved.** New search turned up only the same Wikipedia town-center point (19.280°N, 72.785°E) plus a secondary source stating "Uttan is 8km from Bhayandar" — consistent with, not better than, the existing 9.69km×1.3=12.6km figure (over the ~10km ceiling). No junction/naka-level coordinate found for Uttan itself. Left open.
- **Ghatkopar West (Santacruz) — still unresolved.** New third-party distance figures (rome2rio): "Santacruz to Ghatkopar generally, driving distance 10km/~11min"; a related pair (Ghatkopar East–Santacruz) gives 12km/12min; Yometro's metro-route distance is ~10km. These numbers straddle the ~10km ceiling in the same way as the previously-recorded 9.6–10.8km range — no new data moves this cleanly under or over. Left open; still needs a real routing-API check or human call, not just another search pass.
- **Kamothe (Navi Mumbai) — still unresolved.** New search confirms (again, qualitatively) that Kamothe directly adjoins CBD Belapur, and surfaces a project-listing data point ("Kamothe Junction ~1.21km from one CBD Belapur-area project") — but this is a single landmark-to-project distance, not a sector-boundary coordinate, and doesn't materially improve on the existing Sector 18 point (9.0km×1.3, single-sourced). Left open.
- **New-locality scan:** reviewed all 5 stores' current `localities` arrays (58 total) against the long-standing previously-examined-and-rejected list (Shilphata, Kasarvadavali, Aarey Colony, Ulwe, Mira Road West, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Taloja, Poonam Sagar, Hiranandani Estate, Bandra Kurla Complex, Teen Hath Naka/Khopat/Kopri, Golden Nest, Naigaon, Oshiwara cluster, Dindoshi, Powai, Kalina, Seawoods, "Upper Thane", Chincholi Bunder, Louiswadi, Liberty Garden, Thakur Village, Koparkhairane/Ghansoli/Airoli, Beverly Park, Minakshi Nagar, Anand Nagar, Prabhadevi) plus general knowledge of the surrounding Mumbai/Navi Mumbai/Thane area. No genuinely well-known, high-confidence new candidate surfaced this run.

Coverage remains at 58 localities across all 5 stores. Precise geocoding (Nominatim via WebFetch) remains blocked at the session network-policy level — confirmed again this run against both Nominatim and the live site. WebSearch-sourced cross-referencing of a specific named landmark/station remains the viable path to resolve further candidates, as it was for Yeoor and Waghbil — but for all three remaining open candidates, the blocker is no longer geocoding precision alone; it's missing junction/sector-level source data (Uttan, Kamothe) or an unreliable straight-line×1.3 heuristic on a cross-city hop (Ghatkopar West).

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script covering sitemap-vs-pages, robots.txt bot coverage, JSON-LD parsing, all internal links, image alt text, title/description length and uniqueness, and canonical tags (64 pages, 0 issues). No regeneration was needed since no data changed.
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness against source `reviews.rating`, FAQPage/BreadcrumbList/SportingGoodsStore/openingHoursSpecification completeness) — **0 issues found**.
- Entity-coverage (brand-wide categories, brands_carried, policies, description), NAP, and `llms.txt` drift checks, all re-verified programmatically against current `data/stores.json` — **0 issues found**.
- Git state checked and reconciled at run start (detached HEAD fast-forwarded onto `main`/`origin/main`, clean tree).
- WebFetch re-tested directly against both `nominatim.openstreetmap.org` and `helmetstorenearme.in` — confirmed still blocked (`getaddrinfo ENOTFOUND`) for both. WebSearch confirmed working and used for all research.
- All three open candidates re-investigated via WebSearch with fresh queries; none resolved either direction — see Local Reach Gaps above.
- No `python3 generate.py` run this run — no data changes were made, so no regeneration was needed.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Town-center coordinate (19.280°N, 72.785°E) gives 9.69km straight-line × 1.3 = 12.6km from the Mira Road store — over the ~10km threshold. No naka/junction-level point exists for Uttan itself. Re-checked this run via WebSearch; no new coordinate found. Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. | 2026-10-22 |
| Ghatkopar West | Santacruz (nominal nearest) | Station-level points give 9.85–9.87km straight-line×1.3 — just under the ceiling — but real third-party driving-distance figures (rome2rio, Yometro) range ~9.6–12km depending on exact endpoint/route, straddling the ceiling, since there's no direct road (crosses via JVLR/SCLR through the hills) and the ×1.3 heuristic is unreliable for this hop. Re-checked this run with fresh distance figures; still straddles the ceiling. Needs a real routing-API check or a human call. | 2026-10-24 |
| Kamothe | Navi Mumbai (nominal nearest) | Real-estate sources confirm it directly adjoins CBD Belapur (~15–20min driving), but candidate points vary by sector: village-center gives 9.99km×1.3 (at the ceiling); a single-sourced Sector 18 point gives 9.0km×1.3. No source confirms coordinates for the sectors (1–2) likely nearest the actual border. Re-checked this run; a project-listing landmark distance surfaced but doesn't resolve the sector-boundary question. Needs a confirmed sector-boundary map or a human call before adding. | 2026-11-04 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep | All | Verified via a fresh programmatic sweep over all 64 pages — **0 issues found** | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ/BreadcrumbList/SportingGoodsStore/openingHoursSpecification coverage, reviewRating-fabrication pattern all clean. No (A) fixes needed. |
| Uttan (Mira Road), Ghatkopar West (Santacruz), Kamothe (Navi Mumbai) locality candidates | Local Reach | Re-investigated via WebSearch with fresh queries; no new data moves any of the three under/over the threshold | Left in candidate table, unchanged |
| New-locality scan (all 5 stores) | Local Reach | Checked against general knowledge and the long-standing rejected list; no new genuinely well-known, high-confidence candidate found | No action |
| WebFetch blocked — re-confirmed against both Nominatim and the live site | Technical GEO/SEO / Local Reach | Re-tested directly; confirmed still blocked (`getaddrinfo ENOTFOUND`) for both hosts despite this run's instructions claiming otherwise | WebSearch confirmed working and used for all research and geocoding this run |
| Git state at run start | Housekeeping | Detached `HEAD` fast-forwarded onto `main`/`origin/main` | No work lost, no conflicts |

**This run's site/data changes:** none. No (A) mechanical fixes were needed and no (B) new locality pages were added — the technical/schema/AEO/E-E-A-T sweep found 0 issues, and all locality-candidate research this run resulted in "still unresolved." `data/stores.json` and all generated output are unchanged from 2026-11-06.

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (session network-policy block) | Technical GEO/SEO / Local Reach | Open — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until the relevant hosts are added to the session's network allowlist. Re-confirmed this run against both Nominatim and the live site directly. | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-22 |
| Ghatkopar West — candidate locality needing a real-route distance check or human call | Local Reach | Open, re-checked this run with new distance figures — see candidate table above | 2026-10-24 |
| Kamothe (Navi Mumbai) — candidate locality, right at the ~10km ceiling with sector-boundary uncertainty | Local Reach | Open, re-checked this run — see candidate table above | 2026-11-04 |

*(Three other items — "no press/backlinks" (first flagged 2026-09-15), "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18), and "MadDog brand not named verbatim in homepage's brand-description copy" (first flagged 2026-09-16, not a real entity-coverage gap since MadDog is already quotable on all 5 store pages) — remain open >30 days and continue to be trimmed from this table per the 30-day rule, since none needs daily re-litigation: the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, the sitemap item needs a one-time human decision on approach, and the MadDog item is a non-issue under this audit's own entity-coverage criterion.)*
