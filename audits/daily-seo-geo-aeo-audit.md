# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-13
**Status:** 🟢 One locality page added (Nerul, Navi Mumbai store) — a genuine gap where the store's own containing suburb had no locality page. Full technical/schema/AEO/E-E-A-T sweep otherwise clean, zero issues.

Site: **59 pages** (1 homepage + 5 store pages + 53 locality pages), up from 58 — **Nerul** added for the Navi Mumbai store, geocoded and verified this run.

**Housekeeping:** Git checkout started on a detached `HEAD` sitting exactly at `origin/main`'s tip (`af9f034`), with the local `main` branch ref itself 7 commits behind. Reset `main` to the detached tip (`git checkout -B main af9f034`) — no conflicts, no stash needed, nothing lost, no commits discarded (the local `main` ref was simply stale, not ahead).

**Network access note — WebFetch still non-functional, 18th consecutive run:** Directly re-tested at run start against both `https://nominatim.openstreetmap.org/search` and `https://helmetstorenearme.in/` — **both failed immediately with `getaddrinfo ENOTFOUND <host>`**, the same failure mode reported every run since 2026-10-08. WebSearch continues to work normally and was used for all research this run, same as every prior run back to 2026-09-25.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 59/59 match exactly |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 59 pages |
| Broken internal links | ✅ 0 found |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 59 ≤60 chars, all unique |
| Meta description length/uniqueness | ✅ All 59 unique, all ≤140 chars |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch to the live domain failed with `getaddrinfo ENOTFOUND` (see network note above) |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 58 store/locality pages; `Organization` + 5×`SportingGoodsStore` confirmed on the homepage.
- Re-scanned all 59 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` programmatically checked on all 5 store pages: present with correct `ratingValue`/`reviewCount` only where `reviews.rating` is a real, non-null value (Malad 4.7/2445, Thane 4.5/34); correctly absent for Santacruz, Mira Road and Navi Mumbai even though Santacruz (count 434) and Mira Road (count 317) carry a review *count* — `rating` is null for all three in source data, and the generator correctly withholds `AggregateRating` without a rating value rather than guessing one. No change from prior runs.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 categories (`Touring Luggage & Bags`, `Bike Accessories & Electronics` included, correctly HTML-entity-escaped) and all 3 brands (LS2, Crank1, MadDog) appear verbatim on all 5 store pages; the EMI policy sentence and the 7-day return policy sentence both appear on all 5 store pages. No gap.
- `llms.txt` re-checked line-by-line against current `data/stores.json`: store count (5), every phone number, every maps link, and all 53 locality names (including the new Nerul entry) match exactly. No drift — confirmed the generator's own `llms.txt` regeneration picked up the new locality without manual editing.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 58 store/locality pages: each store's phone number appears byte-for-byte on every page belonging to that store, including the new Nerul page.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` not touched this run — still the human's active research doc.

## 5. Platform Optimization

- FAQs unchanged this run; no new buying-decision gap surfaced.

## 6. Local Reach Gaps

**One locality page added this run: Nerul, for the Navi Mumbai store.**

- **Nerul (Navi Mumbai) — added.** The Navi Mumbai store's own address places it in "Nerul, Navi Mumbai" (`Sector 50 E, Seawoods West, Nerul`), yet neither "Nerul" nor "Seawoods" had its own locality page before this run — a genuine gap, directly analogous to how the Malad store already has a "Malad East" locality page for its own containing suburb. Geocoded via WebSearch (Wikipedia-sourced Nerul railway station coordinates, 19.0336, 73.0181) → straight-line 2.47 km from the store → **road-est 3.2 km**, comfortably inside the 10 km ceiling and placed correctly in distance order (just past CBD Belapur at 1.8 km, before Juinagar at 4.9 km). Minutes range (10-12) interpolated from the existing CBD Belapur (1.8 km → 7-9 min) and Juinagar (4.9 km → 15-18 min) ratios for the same store. Blurb names two real, WebSearch-confirmed landmarks distinct from the store's own immediate area (DY Patil Stadium, Nerul railway station/Sector 19-20) and a concrete reason to visit (station commuters, stadium match-day crowds) rather than a templated swap. Added to `data/stores.json`, regenerated, verified (JSON-LD valid, titles/descriptions within limits, internal links resolve, llms.txt picked it up automatically).
- **Rai (Mira-Bhayandar) — re-checked, still open, no new facts found.** Re-ran WebSearch for coordinates, road distance, and a corroborated landmark inside Rai village itself. Confirmed again it's a genuine East Indian village under Mira-Bhayandar Municipal Corporation (postal code 401101, on Uttan Road) with nearby Tembha Hospital/shopping cited at ~2 km, but still no distance figure to the Mira Road store and no landmark beyond the single uncorroborated "Walchand Palace" mention already in the candidate table. Left unchanged — same reasoning as 2026-10-11/2026-10-12, no new information this run.
- **Poonam Sagar (Mira Road) — new candidate considered, ruled out as already-covered ground.** WebSearch places it in Mira Road East, pincode 401107, with a listing citing "Shanti Nagar Garden nearby" as a landmark. The existing **Shanti Nagar** locality entry already explicitly describes "the older, numbered-sector stretch (Sector 1 through 11... the separate, west-side part of Mira Road East)" — the same ground Poonam Sagar sits in. Same duplicate-ground reasoning as the Hiranandani Estate/BKC precedent (2026-10-12). Not added, not logged.
- **Teen Hath Naka, Khopat, Kopri (Thane) — checked, already covered as landmarks inside existing blurbs**, not standalone gaps. No action.

### Verification performed before closing out this run

- Full technical checklist re-run via a programmatic sweep script (titles/descriptions, JSON-LD validity, broken links, alt text, sitemap-vs-files parity, canonical correctness) across all 59 pages, before and after the Nerul addition — 0 issues both times.
- `llms.txt` cross-checked line-by-line against `data/stores.json` after regeneration — no drift, Nerul picked up automatically.
- Entity-coverage and NAP checks (programmatic, across all pages) — both pass.
- reviewRating-fabrication fix re-confirmed holding across all 59 pages — 0 hits.
- `AggregateRating` presence/absence and values spot-checked against `reviews.rating`/`reviews.count` for all 5 stores — correct in all cases.
- Git fast-forward/reconciliation completed before any work began; working tree otherwise clean.
- WebFetch directly re-tested against Nominatim and the live domain at run start — confirmed still non-functional (`getaddrinfo ENOTFOUND`) for both, 18th consecutive run.
- Haversine distance computed in Python for Nerul (2.47 km straight-line → 3.2 km road-est), consistent with the methodology used on all prior successful additions.

---

## Candidate localities awaiting human geocoding

| Locality | Nearest store | Notes |
|---|---|---|
| Rai | Mira Road | Genuine, distinct East Indian village in Mira-Bhayandar (separate postal code 401101), but no confirmed coordinates, distance, or corroborated landmark found via WebSearch across three runs now — Nominatim unreachable (WebFetch still down). Needs either working geocoding access or a human-supplied landmark/distance to resolve safely. First logged 2026-10-11, re-checked 2026-10-12 and 2026-10-13 with no new information.

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Nerul (Navi Mumbai) — the store's own containing suburb had no locality page | Local Reach | Geocoded via WebSearch (road-est 3.2 km), hand-written blurb, added to `data/stores.json`, regenerated, verified | New page at `/near/navi-mumbai/nerul/`; llms.txt updated automatically |
| Full technical/schema/AEO/E-E-A-T sweep across all 59 pages | All | Re-verified via programmatic sweep, 0 issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness all clean |
| Rai (Mira-Bhayandar) — re-checked this run | Local Reach | No new coordinates, distance, or corroborated landmark found | Left in candidate table unchanged, no new reasoning to add |
| Poonam Sagar (Mira Road) — new candidate considered this run | Local Reach | Overlaps the existing "Shanti Nagar" locality's described numbered-sector area | Not added, not logged — duplicate-ground precedent |
| WebFetch non-functional, 18th consecutive run | Technical GEO/SEO / Local Reach | Re-tested directly against Nominatim and the live site at run start — both failed with `getaddrinfo ENOTFOUND` | All research this run used WebSearch only |
| Git state at run start (detached HEAD at `origin/main`'s tip, local `main` ref 7 commits stale) | Housekeeping | Reset local `main` to the detached tip, now tracking `origin/main` cleanly | No conflicts, no stash needed, nothing discarded |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| WebFetch cannot reach any external host from this session (`getaddrinfo ENOTFOUND`) | Technical GEO/SEO / Local Reach | Open, now 18 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until this is fixed at the environment level | 2026-09-25 |
