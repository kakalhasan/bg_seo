# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-16
**Status:** 🟢 One locality resolved and published — **Rai** (Mira Road store), closing an item open since 2026-10-11. Full technical/schema/AEO/E-E-A-T sweep otherwise clean, 0 issues.

Site: **60 pages** (1 homepage + 5 store pages + 54 locality pages), up from 59. One page added this run: `near/mira-road/rai/`.

**Housekeeping:** Git checkout started on a detached `HEAD` at `d4a7d71` (the 2026-10-15 audit commit), matching `origin/main` exactly — just not on a branch ref. Checked out `main` and fast-forwarded; no conflicts, nothing lost, nothing ahead of origin.

**Network access note — WebFetch still non-functional, 21st consecutive run:** Re-tested directly at run start against `https://nominatim.openstreetmap.org/search` and `https://helmetstorenearme.in/`. Both failed immediately with `getaddrinfo ENOTFOUND <host>` — the same failure mode reported every run since 2026-10-08 (and `EGRESS_BLOCKED` before that, since 2026-09-13). This directly contradicts this run's task brief, which asserts WebFetch runs on Anthropic infrastructure outside the sandbox's egress block. It does not, in this sandbox, for any host tried. All research this run (including the Rai resolution below) used WebSearch only, same workaround as the last 20 runs.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 60/60 match exactly (incl. new Rai page) |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 60 pages |
| Broken internal links | ✅ 0 found |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 60 ≤60 chars, all unique (new Rai page: "Helmet Store Near Rai \| Bikester Global") |
| Meta description length/uniqueness | ✅ All 60 unique, all ≤140 chars |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch failed with `getaddrinfo ENOTFOUND` (see network note above) |

Verified via a programmatic sweep script (written this run, parses every generated HTML file against `data/stores.json`). `python3 generate.py` re-run first to confirm idempotency before the Rai edit (only `sitemap.xml`'s `lastmod` dates changed — known carried-over issue — reverted since no real content had changed yet at that point); re-run again after adding Rai to `data/stores.json`, this time a real regen (60 pages, new page + updated `areaServed`/locality-card links on the other 6 Mira Road pages + `llms.txt` + homepage + sitemap).

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 59 store/locality pages; `Organization` + 5×`SportingGoodsStore` confirmed on the homepage.
- Re-scanned all 60 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds. Confirmed no per-review `reviewRating` value is emitted anywhere (source data has none) and `AggregateRating` is correctly present only where `reviews.rating` is non-null.
- `AggregateRating` programmatically checked on all 5 store pages: present with correct `ratingValue`/`reviewCount` only where `reviews.rating` is a real, non-null value (Malad 4.7/2445, Thane 4.5/34); correctly absent for Santacruz, Mira Road and Navi Mumbai, since `rating` is null for all three even though Santacruz (count 434) and Mira Road (count 317) carry a review *count*. No change from prior runs.
- New Rai page's `SportingGoodsStore`/`FAQPage`/`BreadcrumbList` JSON-LD generated correctly via the standard template — no hand-edited HTML.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 categories and all 3 brands (LS2, Crank1, MadDog) appear verbatim on all 5 store pages; the EMI policy sentence and the 7-day return policy sentence both appear on all 5 store pages. No gap.
- `llms.txt` re-checked line-by-line against current `data/stores.json`: store count (5), every phone number, and all 54 locality names match exactly, including the new "Rai" entry under Mira Road's "Serves" line (auto-regenerated, not hand-edited).

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 59 store/locality pages: each store's phone number appears byte-for-byte on every page belonging to that store, including the new Rai page.
- Authoritativeness (press/backlinks): `audits/backlink-citation-plan.md` unchanged since 2026-09-17 — still the human's active research doc, not touched this run.

## 5. Platform Optimization

- FAQs unchanged this run; no new buying-decision gap surfaced.

## 6. Local Reach Gaps

**One locality page added this run: Rai (Mira Road store).**

- **Rai — resolved.** Open since 2026-10-11, re-checked every run since with no resolution (prior blocker: two postal coordinate sources disagreeing by ~1 km, no confirmed landmark). This run's WebSearch turned up a materially better data point: a postal directory entry specifically for the **Rai Branch Office** itself (not the shared, disagreeing Bhayander West Sub Office figures used in prior runs) at 19.298223, 72.824575 — a single, non-disagreeing source specific to Rai. Straight-line distance from this point to the Mira Road store (19.2843751, 72.8772246) is 5.74 km; applying the site's established ×1.3 road-distance convention (cross-checked against the existing Dahisar entry, where the same method reproduces its recorded 5.6 km almost exactly) gives **7.5 km — within the ~10 km bar**. Separately corroborated via a MahaRERA project listing address ("Uttan Road, Rai Village, Bhayandar, Thane 401101") that **Uttan Road is Rai's real, documented access road**, and via multiple general sources that Rai is a genuine East Indian coastal village in the Mira-Bhayandar belt (alongside Murdha, Morva, Dongri, Uttan, Pali Chowk, Tarodi). Did **not** use the previously-found "Rai Custom House" bus stop name (still unverified what/where it is) or invent any specific church/landmark beyond what was corroborated — kept the blurb honest about what's actually confirmed (the road, the village's real character, and the connection to nearby Uttan as a coastal-ride destination) rather than reaching for unverified specifics.
  - Minutes range (26-30) derived by interpolating from the existing Mira Road ratios (2.2 km→8-10 min, 3.4 km→10-12 min, 5.6 km→18-22 min), consistent with the slightly higher per-km ratio the longer, more rural Dahisar entry already uses.
  - Blurb, schema, sitemap, llms.txt, homepage and the other 6 Mira Road locality pages' cross-links all regenerated via `python3 generate.py` and verified (see Section 1).
- **No new candidate localities surfaced.** Checked Navi Mumbai (store's own area is Seawoods/Nerul — any "Seawoods" entry would overlap the store's own immediate address, consistent with the standing overlap rule) and did not find grounds to revisit any of the extensive list of previously-rejected names (Kasarvadavali, Aarey Colony, Airoli, Ulwe, Mira Road West, Koparkhairane, Ghansoli, Uttan, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Poonam Sagar, Hiranandani Estate, BKC, Teen Hath Naka/Khopat/Kopri, Golden Nest). Coverage across all 5 stores remains close to saturation for genuinely distinct, in-range localities.

### Verification performed before closing out this run

- Full technical sweep via a new programmatic script (`python3 generate.py` re-run first to confirm idempotency, then again after the Rai edit): titles/descriptions length and uniqueness, JSON-LD validity and reviewRating-fabrication scan, broken internal links, alt text, sitemap-vs-files parity, canonical correctness, llms.txt drift, entity coverage, NAP consistency, AggregateRating correctness — **0 issues found** on either pass.
- Rai's distance figure cross-checked against the site's existing ×1.3 haversine convention using the Dahisar entry as a known-good reference point before being written to `data/stores.json`.
- Git state reconciled at run start (see Housekeeping above) — detached HEAD exactly matching `origin/main`, checked out cleanly.
- WebFetch directly re-tested against two different hosts at run start — confirmed still non-functional (`getaddrinfo ENOTFOUND`), 21st consecutive run.

---

## Candidate localities awaiting human geocoding

*(none open — Rai resolved this run)*

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Rai (Mira Road) — open candidate since 2026-10-11 | Local Reach | **Added** `near/mira-road/rai/`: km=7.5, minutes="26-30", hand-written blurb citing Uttan Road and Rai's East Indian coastal-village character | Resolved via a Rai-specific postal coordinate (not the previously disagreeing shared office figures) + a corroborated real access road (Uttan Road via MahaRERA listing). Regenerated and verified, 0 issues |
| Full technical/schema/AEO/E-E-A-T sweep across all 60 pages | All | Verified via a new programmatic sweep script, 0 real issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness all clean, before and after the Rai edit |
| No new candidate localities found beyond Rai | Local Reach | Checked Navi Mumbai's own area (Seawoods) against the overlap rule; no grounds to revisit the long previously-rejected list | Coverage remains close to saturation |
| WebFetch non-functional, 21st consecutive run, despite this run's brief asserting it should work | Technical GEO/SEO / Local Reach | Re-tested directly against 2 different hosts at run start — both failed with `getaddrinfo ENOTFOUND` | All research this run used WebSearch only; did not block the Rai resolution |
| Git state at run start | Housekeeping | Detached HEAD exactly matching `origin/main`; checked out cleanly | No conflicts, nothing lost |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| No third-party press/citations/backlinks (Authoritativeness) | E-E-A-T / Brand Authority | Strategic, not mechanical — human actively working this via `audits/backlink-citation-plan.md` (unchanged since 2026-09-17) | 2026-09-15 |
| `generate.py`'s sitemap `lastmod` is stamped to the run date on every invocation rather than tracking real per-page content changes | Technical GEO/SEO | Noted, not fixed — needs a human call on the right approach (e.g. hash-based or data-driven lastmod) since it changes generator behavior, not just data | 2026-09-18 |
| WebFetch cannot reach any external host from this session (`getaddrinfo ENOTFOUND`) | Technical GEO/SEO / Local Reach | Open, now 21 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until this is fixed at the environment level | 2026-09-25 |
