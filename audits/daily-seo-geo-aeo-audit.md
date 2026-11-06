# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-11-06
**Status:** 🟢 Clean sweep + 1 new locality page added. Fresh programmatic sweep of all 64 pages found **0 issues**. One new locality, **Waghbil** (Thane, on Ghodbunder Road past Patlipada, anchored to the Suraj Water Park at the naka), was geocoded via WebSearch (two independent sources — AroundUs and EverybodyWiki — agreeing within ~0.003° on the park's own coordinates), computed at 5.99km×1.3 ≈ 7.8km road-distance estimate from the Thane store, and added with a hand-written blurb. Site grows to **64 pages** (1 homepage + 5 store pages + 58 locality pages). Waghbil had been an open candidate since 2026-10-27 — this run's new lead (the water park's exact coordinates) resolved it. The remaining three candidates (Ghatkopar West, Prabhadevi, Uttan) were not re-searched this run (no new info expected); Kamothe was re-checked with a fresh search but remains unresolved — see below.

**Housekeeping:** Session started on a detached HEAD matching `origin/main`'s latest commit, but the local `main` branch ref was 6 commits behind — reconciled with `git checkout main` + `git merge --ff-only origin/main` (fast-forward, no divergence, no lost work).

**Network access note — WebFetch still blocked at the session network-policy level, 41st consecutive run:** This run's instructions again stated WebFetch/WebSearch now bypass the sandbox VM's network block, executed by Anthropic's infrastructure rather than the sandbox VM. Tested directly against `nominatim.openstreetmap.org`: failed with `getaddrinfo ENOTFOUND`, with the tool's own error text confirming the host is outside this session's allowed network domains. Per the tool's own guidance ("if another host has failed the same way, stop trying more sites"), no further hosts were tested this run. `WebSearch` works fully and was used for all research and geocoding this run (cross-referencing independent sources — AroundUs and EverybodyWiki for Suraj Water Park's coordinates — plus manual haversine computation in Python against `data/stores.json` coordinates), the same workaround used for the prior 40 runs.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 64/64 match exactly, 0 missing, 0 extra (after Waghbil added + regenerated) |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 64 pages |
| Broken internal links | ✅ 0 found (fresh link-checker sweep over all 1,262 internal links, re-run after Waghbil added) |
| Image alt text | ✅ All `<img>` tags have non-empty, descriptive alt text |
| Title tag length | ✅ All 64 ≤60 chars (post-entity-decode), all unique — new Waghbil page's title verified at 43 chars |
| Meta description length/uniqueness | ✅ All 64 unique, all ≤140 chars — new Waghbil page's description verified within limit |
| Canonical tags | ✅ Present and correct on every page, including new Waghbil page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch confirmed blocked against Nominatim this run; per tool guidance, no further hosts (including the live site) were tried once the pattern repeated |

**This run's check script:** written fresh in the scratchpad (not committed — disposable tooling), covering sitemap-vs-pages, robots.txt, JSON-LD parse + schema-type completeness (`SportingGoodsStore`/`FAQPage`/`BreadcrumbList`/`openingHoursSpecification`), the reviewRating-fabrication pattern, `AggregateRating` value-correctness against `reviews.rating`/`reviews.count` (including checking it's correctly *absent* on the 3 stores with null `reviews.rating`), broken internal links (all 1,262, resolved against disk including anchor-stripped `#stores` links), alt text, title/description length+uniqueness, and canonical tags. Run after the Waghbil addition and regeneration. **0 issues.**

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes (`generate.py` — `TODAY = datetime.date.today().isoformat()`). Still needs a human call on approach (hash-based or data-driven lastmod). First flagged 2026-09-18, unchanged this run.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` present on all 64 store/locality pages (including new Waghbil page), verified programmatically this run — 0 missing.
- `openingHoursSpecification` present on all 64 store/locality pages — 0 missing.
- Re-scanned all 64 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds. No individual `Review` object anywhere on the site carries a `reviewRating`.
- `AggregateRating` programmatically re-verified against source `reviews.rating`/`reviews.count`: Malad (4.7/2445) and Thane (4.5/34) carry correct values, including the new Waghbil page which correctly inherits Thane's 4.5/34; Santacruz, Mira Road and Navi Mumbai correctly carry no `AggregateRating` (source `reviews.rating` is `null` for all three). 0 mismatches, 0 fabrications.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 brand-wide categories, all 3 brands (LS2, Crank1, MadDog), and both brand-wide policy sentences (EMI, 7-day return) appear verbatim (post-`html.unescape()`) somewhere on the site. 0 gaps.
- `llms.txt` re-checked programmatically against current `data/stores.json` — every store name, every phone number (`phone_display`), and all 58 locality names (including the new Waghbil) found verbatim. No drift.
- New Waghbil page's title (`Helmet Store Near Waghbil | Bikester Global`, 43 chars) and description are both within limits and state a specific, quotable fact (7.8km from the Thane store, on Ghodbunder Road, anchored to the Suraj Water Park).
- No other new entity-coverage or FAQ gaps surfaced this run.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 64 store/locality pages: each store's `phone_display` appears on every page belonging to that store, 0 mismatches.
- Authoritativeness (press/backlinks): still the human's active research track via `audits/backlink-citation-plan.md`; no change to that file this run, not touched.

## 5. Platform Optimization

- Spot-checked FAQ coverage across all 5 stores (certification, try-on, location, stock-check — 4 FAQs each, identical pattern per store). No new buying-decision gap surfaced.

## 6. Local Reach Gaps

**One new locality page added this run: Waghbil (Thane).** This candidate had been open since 2026-10-27, blocked on not having a point-level geocode for "Waghbil Naka" itself (only the wider village/area, which varied ~1.5km between sources). This run's fresh WebSearch surfaced the Suraj Water Park's own coordinates from two independent sources, resolving it.

- **New addition: Waghbil (Thane) — geocoded and added.** Waghbil sits on Ghodbunder Road past Patlipada. The existing candidate-table note already identified that Suraj Water Park is reportedly sited at the naka itself, so this run searched for the park's own coordinates rather than the village-area coordinate used previously. Two independent sources agree closely: AroundUs gives 19.25530°N, 72.97050°E (MH SH 42, Dongripada, Thane West, on Ghodbunder Highway) and EverybodyWiki gives 19°15′19″N 72°58′14″E = 19.255272°N, 72.970475°E. Averaged/either point gives the same result to 3 decimal places. Haversine straight-line distance from the Thane store's actual lat/lng (19.201555, 72.9749461) = 5.99km, ×1.3 = **7.8km**, comfortably inside the ~10km ceiling and just past the existing Ghodbunder Road entry (7.5km, 20-25min). Minutes range (21-25) derived by comparing to Ghodbunder Road's own entry (7.5km/20-25min) and Mulund East (6.8km/18-22min) — nudged up slightly for the extra 0.3km. Blurb names the real, verified landmark (Suraj Water Park) and real route (Ghodbunder Road, LBS Marg, Khopat) — Waghbil was already named as a landmark in the existing Ghodbunder Road and Patlipada blurbs, so this page is a genuinely distinct, non-overlapping treatment of the same real place. Added to `data/stores.json`, regenerated, and verified (JSON-LD valid, title 43 chars, description within limit, canonical correct, 0 broken links, NAP/llms.txt consistent).
- **Kamothe (Navi Mumbai) — re-checked, still unresolved.** Fresh WebSearch for sector-level coordinates near the CBD Belapur border found Sector 18 (19.013599°N, 73.08938°E, 9.0km×1.3 from the store) and an unnamed-road point (9.87km×1.3), both lower than the previously-used village-center coordinate (9.99km×1.3) — but no source confirms which sector actually sits on the CBD Belapur-adjoining edge, so the ~1km spread between candidate points is still unresolved ambiguity, not a tighter fix. Left open; needs a human call or a confirmed sector-boundary map.
- **Ghatkopar West, Prabhadevi, Uttan — not re-searched this run** (no new leads surfaced recently for any of the three; re-litigating with no new information would just repeat prior conclusions). All three remain in the candidate table, unchanged.
- No other genuinely new, confidently-resolvable candidate surfaced this run beyond Waghbil. The long-standing previously-examined-and-rejected list (Shilphata, Kasarvadavali, Aarey Colony, Ulwe, Mira Road West, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Taloja, Poonam Sagar, Hiranandani Estate, Bandra Kurla Complex, Teen Hath Naka/Khopat/Kopri, Golden Nest, Naigaon, Oshiwara cluster, Dindoshi, Powai, Kalina, Seawoods, "Upper Thane", Chincholi Bunder, Louiswadi, Liberty Garden, Thakur Village, Koparkhairane/Ghansoli/Airoli, Beverly Park, Minakshi Nagar, Anand Nagar) was not re-litigated — their reasoning stands.

Coverage is now at 58 localities across all 5 stores after today's addition. Precise geocoding (Nominatim via WebFetch) remains blocked at the session network-policy level — confirmed this run against `nominatim.openstreetmap.org` — so remaining open candidates stay stuck on the same ambiguity until either that block lifts or a human supplies tighter coordinates/a real-route distance check. WebSearch-sourced cross-referencing (two independent sources agreeing closely on a specific landmark's coordinates, as with Waghbil's water park) remains the viable path to resolve further candidates without Nominatim — the lesson from both Yeoor and Waghbil is that anchoring to a specific named landmark (not just the locality's general area) is what makes a candidate resolvable.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script covering sitemap-vs-pages, robots.txt bot coverage, JSON-LD parsing, all 1,262 internal links, image alt text, title/description length and uniqueness, and canonical tags — run **after** the Waghbil addition and regeneration (64 pages, 0 issues).
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness against source `reviews.rating`, FAQPage/BreadcrumbList/SportingGoodsStore/openingHoursSpecification completeness) — **0 issues found**.
- Entity-coverage (brand-wide categories, brands_carried, policies), NAP, and `llms.txt` drift checks, all re-verified programmatically against current `data/stores.json` after the Waghbil addition — **0 issues found**.
- `python3 generate.py` run once, producing 64 pages (up from 63) including the new Waghbil page; diff reviewed and confirmed as real content (new page + updated Thane-store areaServed/sitemap/llms.txt), not a no-op.
- Git state checked and reconciled at run start (detached HEAD matching `origin/main`, local `main` ref 6 commits behind, no divergence) — `git checkout main` + `git merge --ff-only origin/main`.
- WebFetch re-tested against `nominatim.openstreetmap.org` — confirmed still blocked (`getaddrinfo ENOTFOUND`), and per the tool's own guidance not to keep trying further hosts once that pattern repeats, no other hosts were tried. WebSearch confirmed working and used for all research. 41st consecutive run with the WebFetch block.
- Kamothe re-checked via WebSearch + manual haversine against actual store coordinates — still unresolved, not re-logged with duplicate reasoning (new sector-level data point added to the candidate table note). Ghatkopar West, Prabhadevi, and Uttan left unchanged (not re-searched, no new info expected).
- Waghbil resolved via WebSearch (two independently-agreeing sources on the water park's exact coordinates) + haversine (7.79km×1.3, comfortably inside ceiling) — added as a new locality page, with full verification above.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Own coordinates (19.2810°N, 72.7790°E approx.) put it at ~10.3km straight-line / ~13.4km ×1.3 from the Mira Road store — over the ~10km threshold; no direct Uttan-to-store route figure exists to double-check against. Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. Not re-searched 2026-11-06 (no new info expected). | 2026-10-22 |
| Ghatkopar West | Santacruz (nominal nearest) | Road-estimate to Santacruz sits right at/over the ~10km ceiling (8.7-12km depending on which endpoint/source/mode is used), but the ×1.3 multiplier is unreliable for this cross-city, opposite-side-of-Mumbai hop (no direct road — via JVLR/SCLR across the hills), and Ghatkopar isn't a natural "near me" catchment for a Santacruz-area search. Needs a human call or a real-route (not straight-line) distance check before adding. Not re-searched 2026-11-06 (no new info expected). | 2026-10-24 |
| Prabhadevi | Santacruz (nominal nearest) | Coordinates are consistent across sources; the site's own straight-line×1.3 methodology (from the store's actual lat/lng) puts it at 10.1-10.2km, just over the ~10km ceiling (third-party road-distance estimates of 8-9km are in the same ballpark but not directly comparable to the site's own methodology), and farther from the store than the existing Mahim entry (7.0km) which already covers the same southward corridor. Needs a human call on whether to extend the ceiling for this specific locality, or leave as-is. Not re-searched 2026-11-06 (no new info expected). | 2026-10-27 |
| Kamothe | Navi Mumbai (nominal nearest) | Real-estate sources say it directly adjoins CBD Belapur (~15-20min driving), but candidate points vary by sector: the village-center coordinate gives 9.99km×1.3 (right at the ceiling); a Sector 18 point gives 9.0km×1.3; an unnamed-road point gives 9.87km×1.3. No source confirms which sector actually sits on the border-adjoining edge, so this ~1km spread is unresolved ambiguity, not a fix. Needs a confirmed sector-boundary map or a human call before adding. Re-checked 2026-11-06, still unresolved. | 2026-11-04 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Waghbil (Thane) — open candidate since 2026-10-27, previously missing from `data/stores.json` | Local Reach (B) | Geocoded via WebSearch (two sources agreeing on the Suraj Water Park's exact coordinates) + haversine: 5.99km×1.3 = 7.8km from Thane store, well inside ceiling. Added to `data/stores.json` with hand-written blurb naming the real landmark (Suraj Water Park) and route. Regenerated, verified (JSON-LD, links, title/description length, NAP, llms.txt) | Site grows from 63 to 64 pages |
| Full technical/schema/AEO/E-E-A-T sweep after the Waghbil addition | All | Verified via a fresh programmatic sweep over all 64 pages and 1,262 internal links — **0 issues found** | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ/BreadcrumbList/SportingGoodsStore/openingHoursSpecification coverage, reviewRating-fabrication pattern all clean |
| Kamothe (Navi Mumbai) locality lead | Local Reach | Re-investigated via WebSearch for sector-level coordinates; found two new candidate points (Sector 18, unnamed road) both lower than the village-center figure, but no source confirms which sector borders CBD Belapur | Left in candidate table, note updated with new data points |
| Ghatkopar West, Prabhadevi, Uttan locality leads | Local Reach | Not re-searched — no new leads expected, re-litigating would repeat prior conclusions | Left in candidate table, unchanged |
| WebFetch blocked, 41st consecutive run — re-confirmed against Nominatim | Technical GEO/SEO / Local Reach | Re-tested; confirmed still blocked (`getaddrinfo ENOTFOUND`) despite this run's instructions claiming otherwise | WebSearch confirmed working and used for all research and geocoding this run |
| Detached HEAD / stale local `main` ref at run start | Housekeeping | Reconciled: `git checkout main` + `git merge --ff-only origin/main` (6 commits, no divergence, no lost work) | No action needed beyond reconciliation |

**This run's site/data changes:** one (B) new locality page (Waghbil, Thane) — see Action Plan above. No (A) mechanical fixes were needed; the technical/schema/AEO/E-E-A-T sweep found 0 issues after the addition. `data/stores.json`, all regenerated output, and this audit file were committed and pushed together.

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (session network-policy block) | Technical GEO/SEO / Local Reach | Open, now 41 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until the relevant hosts are added to the session's network allowlist. This run's instructions again claimed the block was lifted for WebFetch/WebSearch; WebSearch works, WebFetch does not (confirmed against Nominatim this run). | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, not re-searched this run — see candidate table above | 2026-10-22 |
| Ghatkopar West — candidate locality needing a real-route distance check or human call | Local Reach | Open, not re-searched this run — see candidate table above | 2026-10-24 |
| Prabhadevi (Santacruz) — candidate locality, borderline over the ~10km ceiling | Local Reach | Open, not re-searched this run — see candidate table above | 2026-10-27 |
| Kamothe (Navi Mumbai) — candidate locality, right at the ~10km ceiling with sector-boundary uncertainty | Local Reach | Open, re-checked this run with new data points — see candidate table above | 2026-11-04 |

*(Three items — "no press/backlinks" (first flagged 2026-09-15), "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18), and "MadDog brand not named verbatim in homepage's brand-description copy" (first flagged 2026-09-16, not a real entity-coverage gap since MadDog is already quotable on all 5 store pages) — remain open >30 days and continue to be trimmed from this table per the 30-day rule. All three remain unresolved/unchanged. None needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, the sitemap item needs a one-time human decision on approach, and the MadDog item is a non-issue under this audit's own entity-coverage criterion.)*
