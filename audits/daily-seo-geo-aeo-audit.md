# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-11-03
**Status:** 🟢 Clean sweep, no changes needed. Fresh programmatic sweep of all 62 pages (sitemap-vs-pages, robots.txt, JSON-LD parsing/schema completeness, internal links, alt text, title/description length+uniqueness, canonicals, reviewRating-fabrication pattern, AggregateRating correctness, entity coverage, llms.txt drift, NAP consistency) found **0 issues**. No new locality pages added this run — the four open candidates (Uttan, Ghatkopar West, Waghbil, Prabhadevi) were re-checked via WebSearch; none resolved to a confident add, reasoning unchanged/refined (see below). No new candidate surfaced. Site stays at **62 pages** (1 homepage + 5 store pages + 56 locality pages).

**Housekeeping:** Session started on a detached HEAD at the same commit as `origin/main` (3 commits behind due to a stale local `main` ref, no divergence, no lost work) — reconciled with `git checkout main` + `git merge --ff-only origin/main`. Working tree was clean throughout.

**Network access note — WebFetch still blocked at the session network-policy level, 38th consecutive run:** This run's instructions again stated WebFetch/WebSearch now bypass the sandbox VM's network block since they run on Anthropic's infrastructure. Tested directly: `WebSearch` works fully and was used for all research this run. `WebFetch` against `nominatim.openstreetmap.org` still fails with `getaddrinfo ENOTFOUND` — the tool's own error confirms the host is outside this session's allowed network domains and instructs to stop trying further hosts once the pattern repeats, so the live-site host wasn't retried this run. The block remains a session-level allowlist restriction on WebFetch specifically, unaffected by this run's claim. Precise Nominatim JSON geocoding remains unavailable; all geocoding this run used WebSearch's synthesized answers (citing Wikipedia/OpenStreetMap node pages/Rome2Rio/etc.) plus manual haversine computation against `data/stores.json` coordinates — the same workaround used for the prior 37 runs.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 62/62 match exactly, 0 missing, 0 extra |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 62 pages |
| Broken internal links | ✅ 0 found (fresh link-checker sweep) |
| Image alt text | ✅ All `<img>` tags have non-empty, descriptive alt text |
| Title tag length | ✅ All 62 ≤60 chars (post-entity-decode), all unique |
| Meta description length/uniqueness | ✅ All 62 unique, all ≤140 chars (post-entity-decode) |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch failed, session-level network block (see network note above) |

**Housekeeping note:** `python3 generate.py` was run to confirm output matches current `data/stores.json` — it regenerated identically except for `sitemap.xml`'s `lastmod` dates bumping to today (the known issue below). Since no real content changed, that no-op diff was reverted with `git checkout -- sitemap.xml` rather than committed.

**This run's check script:** written fresh in the scratchpad (not committed — disposable tooling), covering sitemap-vs-pages, robots.txt, JSON-LD parse + schema-type completeness (`SportingGoodsStore`/`FAQPage`/`BreadcrumbList`/`openingHoursSpecification`), the reviewRating-fabrication pattern, `AggregateRating` value-correctness against `reviews.rating`/`reviews.count` (including checking it's correctly *absent* on the 3 stores with null `reviews.rating`), broken internal links, alt text, title/description length+uniqueness, and canonical tags, across all 62 pages programmatically. **0 issues on every check.**

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes (`generate.py` — `TODAY = datetime.date.today().isoformat()`). Still needs a human call on approach (hash-based or data-driven lastmod). First flagged 2026-09-18.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` present on all 61 store/locality pages, verified programmatically this run — 0 missing.
- `openingHoursSpecification` present on all 61 store/locality pages — 0 missing.
- Re-scanned all 62 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds. No individual `Review` object anywhere on the site carries a `reviewRating`.
- `AggregateRating` programmatically re-verified against source `reviews.rating`/`reviews.count`: Malad (4.7/2445) and Thane (4.5/34) carry correct values; Santacruz, Mira Road and Navi Mumbai correctly carry no `AggregateRating` (source `reviews.rating` is `null` for all three). 0 mismatches, 0 fabrications.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 brand-wide categories, all 3 brands (LS2, Crank1, MadDog), and both brand-wide policy sentences (EMI, 7-day return) appear verbatim (post-`html.unescape()`) somewhere on the site. 0 gaps.
- `llms.txt` re-checked programmatically against current `data/stores.json` — every store name, every phone number (`phone_display`), and all 56 locality names found verbatim. No drift.
- No new entity-coverage or FAQ gaps surfaced this run.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 61 store/locality pages: each store's `phone_display` appears on every page belonging to that store, 0 mismatches.
- Authoritativeness (press/backlinks): still the human's active research track via `audits/backlink-citation-plan.md`; no change to that file this run, not touched.

## 5. Platform Optimization

- Spot-checked FAQ coverage across all 5 stores (certification, try-on, location, stock-check — 4 FAQs each, identical pattern per store). No new buying-decision gap surfaced.

## 6. Local Reach Gaps

**No new locality pages added this run.** All four previously-logged candidates (Waghbil, Prabhadevi, Uttan, Ghatkopar West) were re-checked via WebSearch; none resolved to a confident add. No genuinely new candidate was found confident enough to pursue.

- **Waghbil (Thane) — re-checked, reasoning refined but still unresolved.** This run tried bracketing via nearby OpenStreetMap bus-stop nodes instead of just area centroids: found OSM nodes for "Uthalsar Naka" (19.2029803, 72.9780533) and "Majiwada Naka" (19.2151588, 72.9781249), but neither is Waghbil Naka itself. Using the Wikipedia area-centroid (19.266°N/72.985°E) the straight-line to the Thane store is 7.24km (×1.3 = **9.42km**, just under the ceiling); the older mirror centroid (19.253°N/72.978°E) gives 5.73km (×1.3 = **7.45km**). Both are now under 10km, and this is directionally consistent with Waghbil sitting just past the existing Patlipada entry (4.9km/14-17min) on the Ghodbunder Road corridor. However, both figures are still area-centroid estimates, not a geocode of "Waghbil Naka" the landmark — and the ~1.5km spread between sources is enough to materially change the minutes-range. Not confident enough to add without a tighter geocode; still needs Nominatim or a human call.
- **Ghatkopar West (nominal nearest: Santacruz store) — re-checked, conclusion unchanged.** Fresh WebSearch this run: Yometro gives ~10km, Mumbai Metro Route gives 12.0km (via a line change at Marol Naka), Rome2Rio's road estimate is ~10km/11min but its own taxi-route figure is 9.6km and walking-route 8.7km. Still straddling the ~10km ceiling with the same cross-city (JVLR/SCLR, over the hills) routing ambiguity that makes the ×1.3 multiplier unreliable for this specific hop. Not added.
- **Prabhadevi (nominal nearest: Santacruz store) — re-checked, conclusion unchanged.** Fresh WebSearch gave the same cluster of coordinates as prior runs (19.0166°N/72.8295°E consensus, with latlong.net/indiamapia.com within ~0.01° of each other). Against the Santacruz store's actual lat/lng (19.086455, 72.8358556): haversine straight-line ≈ 7.8km, ×1.3 ≈ **10.1-10.2km**, confirming the standing just-over-threshold conclusion.
- **Uttan (Mira Road) — re-checked, conclusion unchanged.** Still no direct Uttan-to-Mira-Road-store route figure; Uttan sits roughly 10.3km straight-line (~13.4km ×1.3) from the Mira Road store's own coordinates — clearly over threshold.
- **New candidates considered and not pursued:** Re-ran a WebSearch for localities around the Mira Road store (still the store with the most headroom at 7 localities). Same name-drops resurfaced — "Beverly Park", "Minakshi Nagar", plus a new one, "Anand Nagar" — all real-estate-portal pocket names with no confirmed coordinates and no landmark/route detail confident enough for a genuinely specific, non-generic blurb, and "Anand Nagar" is also too generic a name (multiple areas in Mumbai share it) to geocode confidently. Not added to the candidate table.
- No other genuinely new, confidently-resolvable candidate surfaced this run. The long-standing previously-examined-and-rejected list (Shilphata, Kasarvadavali, Aarey Colony, Ulwe, Mira Road West, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Taloja, Poonam Sagar, Hiranandani Estate, Bandra Kurla Complex, Teen Hath Naka/Khopat/Kopri, Golden Nest, Naigaon, Oshiwara cluster, Dindoshi, Powai, Kalina, Seawoods, "Upper Thane", Chincholi Bunder, Louiswadi, Liberty Garden, Thakur Village, Koparkhairane/Ghansoli/Airoli) was not re-litigated — their reasoning stands.

Coverage remains close to saturation for genuinely distinct, in-range localities across all 5 stores. Precise geocoding (Nominatim via WebFetch) remains blocked at the session network-policy level, so the four open candidates stay stuck on the same ambiguity until either that block lifts or a human supplies tighter coordinates/a real-route distance check.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script covering sitemap-vs-pages, robots.txt bot coverage, JSON-LD parsing, internal links, image alt text, title/description length and uniqueness, and canonical tags — **0 issues found** across all 62 pages.
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness against source `reviews.rating`, FAQPage/BreadcrumbList/SportingGoodsStore/openingHoursSpecification completeness) — **0 issues found**.
- Entity-coverage, NAP, and `llms.txt` drift checks, all re-verified programmatically against current `data/stores.json` — **0 issues found**.
- `python3 generate.py` re-run to confirm output matches current data; only the known `lastmod`-bump no-op diff appeared, reverted without committing.
- Git state checked and reconciled at run start (detached HEAD at a stale commit, local `main` 3 commits behind `origin/main`, no divergence) — `git checkout main` + `git merge --ff-only origin/main`.
- WebFetch re-tested against `nominatim.openstreetmap.org` — confirmed still blocked session-wide (`getaddrinfo ENOTFOUND`), and per the tool's own guidance not to keep trying further hosts once that pattern appears, the live site wasn't separately re-tested this run. WebSearch confirmed working and used for all research. 38th consecutive run with the WebFetch block.
- All four open candidates re-checked via WebSearch + manual haversine distance computation against actual store coordinates — Waghbil's bracket refined using nearby OSM bus-stop nodes (still inconclusive for the landmark itself); the other three reconfirmed unchanged. None resolved, none re-logged with duplicate reasoning.
- One new potential-candidate lead ("Anand Nagar" near Mira Road, alongside the already-rejected Beverly Park / Minakshi Nagar) investigated and not pursued — too vague/generic to log.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Own coordinates (19.2810°N, 72.7790°E approx.) put it at ~10.3km straight-line / ~13.4km ×1.3 from the Mira Road store — over the ~10km threshold; no direct Uttan-to-store route figure exists to double-check against. Re-checked 2026-11-03, conclusion unchanged. Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. | 2026-10-22 |
| Ghatkopar West | Santacruz (nominal nearest) | Road-estimate to Santacruz sits right at the ~10km ceiling (8.7-12km depending on which endpoint/source/mode is used), but the ×1.3 multiplier is unreliable for this cross-city, opposite-side-of-Mumbai hop (no direct road — via JVLR/SCLR across the hills), and Ghatkopar isn't a natural "near me" catchment for a Santacruz-area search. Needs a human call or a real-route (not straight-line) distance check before adding. Re-checked 2026-11-03, unchanged. | 2026-10-24 |
| Waghbil | Thane | Already named as a landmark in the existing Patlipada blurb, so a real place, but its own coordinates vary ~1.5km between sources and no source gives coordinates for "Waghbil Naka" specifically (only the wider village/area). This run bracketed against nearby OSM bus-stop nodes (Uthalsar Naka, Majiwada Naka) — neither is Waghbil Naka — and found both area-centroid estimates now land just under the ~10km ceiling (7.45km and 9.42km ×1.3), consistent with Waghbil sitting just past the existing Patlipada entry (4.9km) on the Ghodbunder Road corridor. Still not a direct geocode of the landmark itself, and the ~1.5km source spread would materially change the minutes-range. Needs a tighter geocode or a human call before adding. Re-checked 2026-11-03, reasoning refined, still open. | 2026-10-27 |
| Prabhadevi | Santacruz (nominal nearest) | Coordinates are consistent across sources; the site's own straight-line×1.3 methodology (from the store's actual lat/lng) puts it at 10.1-10.2km, just over the ~10km ceiling, and farther from the store than the existing Mahim entry (7.0km) which already covers the same southward corridor. Needs a human call on whether to extend the ceiling for this specific locality, or leave as-is. Re-checked 2026-11-03, unchanged. | 2026-10-27 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 62 pages | All | Verified via a fresh programmatic sweep — **0 issues found** | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ/BreadcrumbList/SportingGoodsStore/openingHoursSpecification coverage, reviewRating-fabrication pattern all clean. No code or data changes made this run. |
| Waghbil (Thane) locality lead | Local Reach | Re-investigated via WebSearch using nearby OSM bus-stop nodes to bracket the area; both centroid estimates now land under the ~10km ceiling but neither is the landmark itself | Left in candidate table, reasoning refined, no duplicate re-log |
| Prabhadevi (Santacruz) locality lead | Local Reach | Re-investigated with fresh haversine calc against store's own coordinates (10.1-10.2km) | Left in candidate table, no duplicate re-log |
| Uttan (Mira Road) locality lead | Local Reach | Re-investigated with fresh haversine calc against store's own coordinates (~13.4km) | Left in candidate table, no duplicate re-log |
| Ghatkopar West (Santacruz) locality lead | Local Reach | Re-checked via WebSearch with fresh sources (Yometro/Mumbai Metro Route/Rome2Rio); estimate spread (8.7-12km) still straddles the ~10km ceiling | Left in candidate table, unchanged |
| "Anand Nagar" (Mira Road) — new lead | Local Reach | Investigated via WebSearch; too vague/generic (real-estate listing name-drop, name shared by multiple Mumbai areas, no confident landmark detail) | Not added to candidate table — not pursued further |
| WebFetch blocked for Nominatim, 38th consecutive run | Technical GEO/SEO / Local Reach | Re-tested; confirmed still blocked despite this run's instructions claiming otherwise | WebSearch confirmed working and used for all research this run |
| Detached HEAD / stale local `main` at run start | Housekeeping | Reconciled: `git checkout main` + `git merge --ff-only origin/main` (3 commits, no divergence, no lost work) | No action needed beyond reconciliation |

**No commit this run** — no (A) fixes or (B) new localities; everything checked clean or stayed in the candidate queue unchanged.

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (session network-policy block) | Technical GEO/SEO / Local Reach | Open, now 38 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until the relevant hosts are added to the session's network allowlist. This run's instructions again claimed the block was lifted for WebFetch/WebSearch; WebSearch works, WebFetch does not. | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-22 |
| Ghatkopar West — candidate locality needing a real-route distance check or human call | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-24 |
| Waghbil (Thane) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run, reasoning refined — see candidate table above | 2026-10-27 |
| Prabhadevi (Santacruz) — candidate locality, borderline over the ~10km ceiling | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-27 |

*(Three items — "no press/backlinks" (first flagged 2026-09-15), "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18), and "MadDog brand not named verbatim in homepage's brand-description copy" (first flagged 2026-09-16, not a real entity-coverage gap since MadDog is already quotable on all 5 store pages) — remain open >30 days and continue to be trimmed from this table per the 30-day rule. All three remain unresolved/unchanged. None needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, the sitemap item needs a one-time human decision on approach, and the MadDog item is a non-issue under this audit's own entity-coverage criterion.)*
