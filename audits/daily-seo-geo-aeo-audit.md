# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-30
**Status:** 🟢 Clean technical/schema/AEO/E-E-A-T sweep across all pages. Local Reach Gaps: added one new locality page this run (Mulund East, assigned to Thane), closed out the long-open Dahisar West candidate as **rejected** (not just deferred) with a confirmed reason, and logged one new candidate (Ulwe, Navi Mumbai) that looked promising on paper but fails a real-route distance check. WebFetch remains blanket-blocked for every domain tried (Nominatim, Wikipedia, the live site itself, third-party lat/long sites) — 6th consecutive run. WebSearch continues to work fully and was used for all geocoding, route verification and distance corroboration this run.

Site: 53 pages (1 homepage + 5 store pages + 47 locality pages) generated from `data/stores.json` via `generate.py`. Up from 52 on 2026-09-29 — added `near/thane/mulund-east/`.

**Housekeeping:** checkout was already clean and up to date with `origin/main` at run start — no reconciliation needed.

**Network access note — 6th consecutive run:** WebFetch returned `EGRESS_BLOCKED` for every domain tried this run, including `nominatim.openstreetmap.org`, `en.wikipedia.org`, `www.latlong.net`, and `helmetstorenearme.in` itself. This keeps contradicting the task prompt's assumption that WebFetch bypasses this sandbox's egress block — the block is blanket, not domain-specific, and unchanged since first observed 2026-09-25. WebSearch is unaffected and was used for all geocoding and route research this run, including pulling exact coordinates from indexed third-party sites (e.g. findlatitudeandlongitude.com results surfaced via search) as a substitute for direct Nominatim calls, and cross-checking haversine-derived distances against real driving-distance figures surfaced in search snippets — the latter caught a real problem (see Ulwe, Section 6) that a pure haversine estimate would have missed.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 53/53 match exactly, no drift, no missing/extra URLs either direction |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 53 pages (programmatic parse of every `<script type="application/ld+json">` block) |
| Broken internal links | ✅ 0 found (every `href`/`src` resolves to a file on disk once fragments/external/tel/mailto are excluded) |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 53 ≤60 chars, all unique (new Mulund East page: "Helmet Store Near Mulund East \| Bikester Global") |
| Meta description length/uniqueness | ✅ All 53 unique, all ≤140 chars (decoded-entity length) |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch to the live domain itself returned `EGRESS_BLOCKED` this run (see network note above) |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 52 store/locality pages; `Organization` + 5×`SportingGoodsStore` on the homepage.
- Re-scanned all 53 pages' JSON-LD for any `Review` node carrying a `reviewRating` field (the fabrication pattern fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` correctly present only where `reviews.rating` is a real, non-null value (Malad 4.7, Thane 4.5). Correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating: null` in source data). Verified directly against the generated HTML, not just source data.
- New Mulund East page's JSON-LD parses cleanly and carries no fabricated fields — it inherits Thane's standard store schema block like every other Thane locality page.

## 3. AI Citability / AEO

- Entity-coverage re-check (HTML-entity-aware): all 6 categories, all 3 brands (LS2, Crank1, MadDog), the EMI policy sentence and the 7-day return policy sentence each appear verbatim on all 5 store pages. No gap.
- `llms.txt` regenerated and spot-checked: store count (5), brand list (LS2, Crank1, MadDog) and every locality name across all 5 "Serves:" lines match current `data/stores.json`, including the new Mulund East entry on the Thane line. No drift.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run — no changes made to any of these (bucket C).
- NAP consistency re-verified programmatically across all 53 pages: all 5 stores' phone numbers appear byte-for-byte on every page belonging to that store, including every locality page (the new Mulund East page carries the correct Thane store phone number).
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` unchanged since 2026-09-17 — still the human's active research doc, not touched.

## 5. Platform Optimization

- FAQs unchanged this run; still cover the full natural buying-decision set (certification, try-before-buy, stock-check, EMI/returns, brands carried, exact location) on every page, including the new locality page (inherits the store's FAQ block, as all locality pages do).

## 6. Local Reach Gaps

**Dahisar West — closed out as REJECTED (previously an open candidate since 2026-09-28):** Last run identified a genuine West-side landmark (Kandarpada metro station) but deferred adding it, unsure whether the commute route from there is meaningfully distinct from the existing "Dahisar" entry's WEH-corridor route. This run found the deciding fact: the **Dahisar–Mira Bhayander Link Road** — the only road that would give Kandarpada/Dahisar West a direct, distinct route to the Mira-Bhayandar area (via Uttan Road to Subhash Chandra Bose Maidan) — is still under construction and has a documented history of delays (confirmed via WebSearch, incl. a Mumbai Live article on construction delays). A cited estimate for the corridor once open is "45 minutes down to 10," implying today's actual commute from that side is long and almost certainly routes through the same Western Express Highway corridor the existing "Dahisar" entry already describes. Adding a Kandarpada-based entry today would therefore describe the same route as the existing entry — a genuine near-duplicate. **Rejected, not re-logged as a candidate.** Revisit only if the link road opens (public project, would be news-searchable) or someone finds a genuinely distinct current route.

**Added: Mulund East → Thane store.** Thane already had "Mulund West" (5.2 km, via LBS Marg past "the old Mulund check naka"). Checked whether Mulund East is a genuine, distinct-enough locality to warrant its own page, the same way the site already splits Khar/Bandra/Vile Parle/Jogeshwari/Bhayandar/Santacruz into East/West pairs:
- Geocoded via WebSearch (findlatitudeandlongitude.com result, since Nominatim is unreachable): 19.157473, 72.956779. Straight-line 5.26 km from the Thane store (19.201555, 72.9749461) → road-est 6.84 km, comfortably under the 10 km ceiling.
- **Corroborated the estimate against real driving-distance data**, not just haversine: search results independently confirmed "Mulund Check Naka to Thane West: 7 km by road" — matching the estimate closely, so no hidden-barrier risk.
- Confirmed genuine route distinctness before writing the blurb: Mulund East sits on the Eastern Express Highway (EEH), not LBS Marg — a different physical corridor from Mulund West's route, with its own landmark (the EEH toll naka, also called Mulund Check Naka, distinct from "the old Mulund check naka" on LBS Marg that the existing Mulund West blurb references). EEH's northern end terminates at Thane via Teen Hath Naka, a well-known Thane junction.
- Wrote a hand-written blurb naming the EEH toll naka and Teen Hath Naka, explicitly contrasting it with the LBS Marg route Mulund West uses, at km=6.8, minutes="18-22" (consistent with the store's existing km-to-minutes ratios: Mulund West 5.2km→15-18, Kolshet Road 6.1km→16-20, Ghodbunder Road 7.5km→20-25).
- Added to `data/stores.json`, regenerated (`python3 generate.py`), verified: page builds clean, JSON-LD parses, title/description within limits, sitemap/llms.txt updated, NAP correct, phone number present.

**New candidate logged: Ulwe → Navi Mumbai store (NOT added — see reasoning).** General-knowledge check of areas south of Seawoods/Nerul. Geocoded via WebSearch (Wikipedia coordinates, 18.976063, 73.052294): straight-line 5.01 km from the Navi Mumbai store (19.0120102, 73.0235427) → naive road-est 6.51 km, which would look comfortably within range. **However**, a direct driving-distance search corroboration (the same cross-check that confirmed Mulund East was safe) contradicted the haversine estimate: multiple independent sources put the actual current driving distance at **9–12 km**, roughly 16–22 minutes — because Seawoods and Ulwe are separated by mangrove/creek terrain, and the only road that would shorten this (the "Ulwe Coastal Road," a ~5.8 km CIDCO project via Seawoods–Ulwe–Bamandongri–Targhar, including an elevated stretch over mangrove-sensitive area) was still targeting an October–November 2026 opening as of the most recent search results — i.e. not confirmed open as of this run. This is the same failure mode as Dahisar West: a straight-line estimate multiplied by a flat road-factor missed a real geographic barrier. Logged as a candidate rather than added or outright rejected, since 9-ish km real distance is borderline-plausible once/if the coastal road opens. Needs either confirmation the coastal road has opened (searchable, dated event) or a human call on whether the current ~10-12 min-longer route still justifies a page.

**Checked and rejected without logging:** Ghansoli (Navi Mumbai side) — geocoded (19.125362, 72.999199), straight-line 12.86 km from the Navi Mumbai store → road-est 16.72 km, clearly over the 10 km ceiling. Rejected, not logged (same treatment as Kopar Khairane on 2026-09-29 — unambiguously over threshold, not a borderline case).

### Verification performed before closing out this run

- `python3 generate.py` re-run: 53 pages generated (up from 52), 0 errors.
- Full technical checklist (titles/descriptions, JSON-LD, broken links, alt text, sitemap-vs-files parity, robots.txt, llms.txt, canonical tags) — all pass, see Section 1, re-run against the post-edit site including the new page.
- Entity-coverage and NAP checks — both pass, including the new Mulund East page.
- Confirmed the reviewRating-fabrication fix still holds across all 53 pages — 0 hits.
- `sitemap.xml`'s `lastmod` bump to today's date is a real content change this run (new page added), so it was committed as-is rather than reverted.
- Diffed `data/stores.json` and the generated output before committing to confirm the only substantive change is the one new Mulund East locality entry and its derived page.

---

## Candidate localities awaiting human geocoding

| Locality | Candidate store | Note |
|---|---|---|
| Ulwe | Navi Mumbai | Naive haversine×1.3 estimate (6.51 km) looked fine, but real driving-distance search corroboration puts it at 9–12 km / 16–22 min due to a mangrove/creek barrier between Seawoods and Ulwe. The direct-connecting "Ulwe Coastal Road" project was not confirmed open as of this run (targeting Oct–Nov 2026). Needs confirmation the coastal road has opened, or a human call on whether the current longer route still justifies a page. |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Dahisar West candidate open since 2026-09-28, route-distinctness from existing "Dahisar" entry unconfirmed | Local Reach | Found the deciding fact via WebSearch: the only road that would give it a distinct route (Dahisar–Mira Bhayander Link Road) is still under construction/delayed, so today's real route matches the existing entry's WEH corridor | Rejected outright, removed from candidate table (was previously just deferred) |
| Thane store's locality coverage had Mulund West but not Mulund East, a genuinely distinct East-side locality on a different road corridor (EEH vs LBS Marg) | Local Reach | Geocoded, route-verified, distance corroborated against real driving data, wrote a distinct hand-written blurb, added to `data/stores.json`, regenerated and verified | New page: `near/thane/mulund-east/` |
| Possible new Navi Mumbai locality (Ulwe) looked viable on a naive distance estimate | Local Reach | Cross-checked against real driving-distance search data, found a creek/mangrove barrier inflates the real route to 9–12 km, likely borderline once a coastal-road project opens (not yet confirmed open) | Logged as candidate rather than added or rejected outright |
| Possible new Navi Mumbai locality (Ghansoli) | Local Reach | Geocoded and checked — 16.7 km road-est, clearly over the 10 km ceiling | Rejected, not logged as a standing candidate |
| Full technical/schema/AEO/E-E-A-T sweep across all 53 pages | All | Re-verified, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt all clean |
| WebFetch blocked for every domain tested, including the live site itself and third-party lat/long lookup sites — 6th consecutive run | Technical GEO/SEO | Flagged again, not fixable from this session — environment-level egress proxy blocks WebFetch entirely, not just specific domains | Adapted to WebSearch-only geocoding and route verification again; live-site verification skipped for the 6th run running |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| WebFetch returns `EGRESS_BLOCKED` for every external domain tried in this environment (Nominatim, Wikipedia, live site, third-party lat/long sites), despite being expected to work per the task prompt | Technical GEO/SEO / Local Reach | Open, now 6 consecutive runs — worked around via WebSearch each time; live-site checks remain unavailable until this is fixed at the environment level | 2026-09-25 |
