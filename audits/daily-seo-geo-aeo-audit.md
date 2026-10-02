# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-02
**Status:** 🟢 Clean technical/schema/AEO/E-E-A-T sweep across all pages. Local Reach Gaps: added two new locality pages this run (Borivali East → Malad, Lokhandwala Complex → Santacruz), both geocoded and route-verified. Re-examined the open Ulwe candidate with fresh search data — corrected a factual error in the previous run's reasoning (the "Ulwe Coastal Road" project is for MTHL–airport connectivity, not a Seawoods–Ulwe link) but real driving-distance sources still range 7–13 km depending which part of Ulwe, so it stays a logged candidate rather than added. Logged one new candidate (Mira Road West) pending more precise geocoding. Rejected Uttan outright (clearly over the 10 km ceiling). **WebFetch is still blanket-blocked for every domain tried — 8th consecutive run**, despite this run's task prompt stating WebFetch should now bypass the sandbox egress block. WebSearch continues to work fully and was used for all geocoding and route verification this run.

Site: 55 pages (1 homepage + 5 store pages + 49 locality pages) generated from `data/stores.json` via `generate.py`. Up from 53 on 2026-09-30 — added `near/malad/borivali-east/` and `near/santacruz/lokhandwala-complex/`.

**Housekeeping:** checkout was on a detached HEAD matching `origin/main`'s tip (`f471857`) at run start, one commit behind the `main` branch ref itself. Ran `git checkout main && git merge --ff-only origin/main` to reattach — fast-forwarded cleanly, no divergent work, nothing lost.

**Network access note — 8th consecutive run:** WebFetch returned `EGRESS_BLOCKED` for both `nominatim.openstreetmap.org` and `helmetstorenearme.in` itself this run — the same blanket block observed every run since 2026-09-25, unchanged despite the task prompt's updated claim that WebFetch should work from this sandbox. Worked around entirely via WebSearch (coordinate lookups via Wikipedia/findlatitudeandlongitude.com/latlong.net results, and real driving-distance corroboration via indexed route/distance sites) exactly as the past several runs have done. Live-site verification was skipped again for the 8th run running.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 55/55 match exactly (programmatic diff of `sitemap.xml` `<loc>` entries vs every `index.html` on disk) |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 55 pages (programmatic parse of every `<script type="application/ld+json">` block) |
| Broken internal links | ✅ 0 found (every `href`/`src` resolves to a file on disk once fragments/external/tel/mailto/whatsapp are excluded) |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 55 ≤60 chars, all unique (new: "Helmet Store Near Borivali East \| Bikester Global", "Helmet Store Near Lokhandwala Complex \| Bikester Global") |
| Meta description length/uniqueness | ✅ All 55 unique, all ≤140 chars (decoded-entity length) |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch to the live domain returned `EGRESS_BLOCKED` this run (see network note above) |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 54 store/locality pages; `Organization` + 5×`SportingGoodsStore` on the homepage.
- Re-scanned all 55 pages' JSON-LD for any `Review` node carrying a fabricated `reviewRating` field (the pattern fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` correctly present only where `reviews.rating` is a real, non-null value (Malad 4.7, Thane 4.5); correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating: null` in source data).
- Both new pages' JSON-LD parses cleanly and inherits their store's standard schema block — no fabricated fields introduced.

## 3. AI Citability / AEO

- Entity-coverage re-check (HTML-entity-aware): all 6 categories, all 3 brands (LS2, Crank1, MadDog), the EMI policy sentence and the 7-day return policy sentence each appear verbatim on all 5 store pages. No gap.
- `llms.txt` regenerated and spot-checked: store count (5), brand list and every locality name across all 5 "Serves:" lines match current `data/stores.json`, including the two new entries (Borivali East on the Malad line, Lokhandwala Complex on the Santacruz line). No drift.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run — no changes made to any of these (bucket C).
- NAP consistency re-verified programmatically across all 55 pages: each store's phone number appears byte-for-byte on every page belonging to that store, including both new locality pages.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` not touched this run — still the human's active research doc.

## 5. Platform Optimization

- FAQs unchanged this run; both new locality pages inherit their store's full FAQ block (certification, try-before-buy, stock-check, EMI/returns, exact location), same as every other locality page.

## 6. Local Reach Gaps

**Added: Borivali East → Malad store.** Malad already had "Borivali West" (7.9 km, via Link Road/Kandivali). Checked whether Borivali East is a genuine, distinct-enough locality for its own page, the same way the site splits other suburbs into East/West pairs:
- Geocoded via WebSearch: 19.2298, 72.8609 (cross-checked against a second source, 19.231259/72.862393 — consistent). Straight-line 6.22 km from the Malad store (19.1786726, 72.8365407) → road-est 8.09 km, comfortably under the 10 km ceiling.
- Confirmed genuine route distinctness: Borivali East is served by the **Western Express Highway**, not the New Link Road corridor that Borivali West uses (confirmed via WebSearch — "Borivali East is well connected with Western Express Highway while Borivali West is linked to the New Link Road"), with its own landmarks (Sanjay Gandhi National Park gate, Dattapada Road) distinct from Borivali West's Link Road/Kandivali/IC Colony references.
- Wrote a hand-written blurb naming the WEH service road, the National Park gate and Dattapada Road, explicitly contrasting it with Borivali West's Link Road route, at km=8.1, minutes="22-25" (consistent with the store's existing km-to-minutes ratios — closest comparable entry is Borivali West itself at 7.9 km → 20-25 min; nudged slightly higher for the extra 0.2 km and WEH's own peak-hour profile).
- Added to `data/stores.json`, regenerated, verified: page builds clean, JSON-LD parses, title/description within limits, sitemap/llms.txt updated, NAP correct.

**Added: Lokhandwala Complex → Santacruz store.** General-knowledge check of areas between the existing Andheri West (3.4 km) and Mahim (7.0 km) entries:
- Geocoded via WebSearch: 19.130815, 72.82927 (findlatitudeandlongitude.com). Straight-line 4.97 km from the Santacruz store (19.086455, 72.8358556) → road-est 6.46 km, well within range.
- Confirmed genuine route distinctness from the existing Andheri West entry (which uses SV Road and references Vile Parle signal traffic): Lokhandwala Complex sits off **New Link Road**, near the Oshiwara flyover, Infinity Mall and Lokhandwala Market — a different, verifiable set of landmarks and road (confirmed via WebSearch, including the neighbourhood's origin as reclaimed Versova marshland developed by Lokhandwala Constructions).
- Wrote a hand-written blurb naming New Link Road, the Oshiwara flyover, Infinity Mall and Lokhandwala Market, at km=6.5, minutes="18-22" (interpolated between the store's existing Andheri East 4.9 km → 16-19 min and Mahim 7.0 km → 22-25 min entries).
- Added to `data/stores.json`, regenerated, verified: page builds clean, JSON-LD parses, title/description within limits, sitemap/llms.txt updated, NAP correct.

**Ulwe candidate (Navi Mumbai) — re-examined, kept as candidate, previous run's reasoning partly corrected.** The 2026-09-30 entry rejected-by-inaction based on the "Ulwe Coastal Road" project being unopened. This run's research found that project (a 5.8–7 km elevated six-lane corridor, 60% complete as of Nov 2025) actually connects the **Mumbai Trans Harbour Link (Atal Setu) to Navi Mumbai International Airport** — it is not a Seawoods–Ulwe local connector, so citing it as the reason Seawoods↔Ulwe is indirect was a factual error. Correcting that, however, does not resolve the underlying distance question: multiple independent driving-distance sources this run put Seawoods↔Ulwe anywhere from **7 km to 13 km** depending on which part of Ulwe is meant (Ulwe spans many sectors across several km) — straddling the site's 10 km ceiling with real ambiguity about which end of Ulwe a store-bound rider would be coming from. Given that spread, there isn't enough confidence to write a single "X km, Y minutes" entry honestly. **Kept as an open candidate**, reasoning corrected; still needs either a human call on which Ulwe sector to anchor the entry to, or a more precise geocode of its populated/accessible core (e.g. Ulwe Sector 19, the most commonly cited reference point in search results).

**New candidate logged: Mira Road West.** General-knowledge check of the store's own immediate surroundings (existing entries Naya Nagar, Kashimira and Bhayandar East/West all sit within 1.4–3.4 km but none is explicitly "Mira Road West," the area across the tracks from the store's own Mira Road East). WebSearch only returned a generic "Mira Road" coordinate (19.28, 72.86) rounded to two decimal places — effectively the same reference point that would describe Mira Road East, not precise enough to confirm a genuinely distinct sub-locality or route (e.g. which subway/overbridge crossing it would use). Logged rather than added — needs a sharper landmark-level geocode (a specific road, society or station-side reference in Mira Road West) before a distinct, non-generic blurb can be written honestly.

**Checked and rejected without logging:** Uttan (coastal village beyond Bhayandar West) — geocoded (19.280, 72.785), straight-line 9.67 km from the Mira Road store → road-est 12.57 km, over the 10 km ceiling; also independently described as "8 km away from Bhayandar" itself, which is already the farthest existing Mira Road entry before Uttan. Clearly over threshold, not logged (same treatment as Ghansoli on 2026-09-30).

### Verification performed before closing out this run

- `python3 generate.py` re-run: 55 pages generated (up from 53), 0 errors.
- Full technical checklist (titles/descriptions, JSON-LD, broken links, alt text, sitemap-vs-files parity, robots.txt, llms.txt, canonical tags) — all pass via a programmatic sweep script, including both new pages.
- Entity-coverage and NAP checks — both pass, including the two new pages.
- Confirmed the reviewRating-fabrication fix still holds across all 55 pages — 0 hits.
- Diffed `data/stores.json` and the generated output before committing to confirm the only substantive changes are the two new locality entries (and the resulting breadcrumb/"Serves" list updates on their stores' other pages, `index.html`, `sitemap.xml` and `llms.txt` — all expected side effects of `generate.py`, not hand-edits).

---

## Candidate localities awaiting human geocoding

| Locality | Candidate store | Note |
|---|---|---|
| Ulwe | Navi Mumbai | Real driving-distance sources range 7–13 km depending which part of Ulwe is meant (it spans many sectors). Previous run's "blocked by unopened coastal road" reasoning was a factual error (that project connects MTHL to the airport, not Seawoods to Ulwe) — corrected this run, but the underlying distance ambiguity remains. Needs a human call on which Ulwe sector to anchor to, or a sharper geocode of its accessible core (e.g. Sector 19). |
| Mira Road West | Mira Road | WebSearch only returns a generic "Mira Road" coordinate (19.28, 72.86), not precise enough to confirm a genuinely distinct route/landmark from the store's own Mira Road East side. Needs a sharper, landmark-level geocode before a non-generic blurb can be written. |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Malad store had Borivali West but not Borivali East, a genuinely distinct East-side locality on a different road corridor (WEH vs Link Road) | Local Reach | Geocoded, route-verified via WebSearch, wrote a distinct hand-written blurb, added to `data/stores.json`, regenerated and verified | New page: `near/malad/borivali-east/` |
| Santacruz store's coverage had a gap between Andheri West and Mahim; Lokhandwala Complex is a well-known, distinctly-routed locality in that gap | Local Reach | Geocoded, route-verified via WebSearch (New Link Road vs Andheri West's SV Road), wrote a distinct hand-written blurb, added to `data/stores.json`, regenerated and verified | New page: `near/santacruz/lokhandwala-complex/` |
| Open Ulwe candidate's prior rejection reasoning (blocked coastal road project) was found to be a factual error on re-check | Local Reach | Corrected the reasoning in the audit; distance ambiguity (7-13km) is the real open question, not the coastal road | Still a logged candidate, not added |
| Possible new Mira Road locality (Mira Road West) | Local Reach | Attempted geocode, got only a generic/imprecise coordinate | Logged as candidate rather than added |
| Possible new Mira Road locality (Uttan) | Local Reach | Geocoded and checked — 12.6 km road-est, clearly over the 10 km ceiling | Rejected, not logged as a standing candidate |
| Full technical/schema/AEO/E-E-A-T sweep across all 55 pages | All | Re-verified via programmatic sweep, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt all clean |
| WebFetch blocked for every domain tested, including the live site itself — 8th consecutive run, contradicting this run's task-prompt claim that it should now work | Technical GEO/SEO | Flagged again, not fixable from this session — environment-level egress proxy blocks WebFetch entirely | Adapted to WebSearch-only geocoding and route verification again; live-site verification skipped for the 8th run running |
| Git checkout was on a detached HEAD, one commit behind `main` branch ref, at run start | Housekeeping | Checked out `main` and fast-forward merged from `origin/main` | No divergent work, nothing lost; routine reconciliation |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| WebFetch returns `EGRESS_BLOCKED` for every external domain tried in this environment (Nominatim, live site, third-party lat/long sites), despite task-prompt claims it should work from this sandbox | Technical GEO/SEO / Local Reach | Open, now 8 consecutive runs — worked around via WebSearch each time; live-site checks remain unavailable until this is fixed at the environment level | 2026-09-25 |
