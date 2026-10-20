# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-20
**Status:** 🟢 Clean sweep. 0 real issues found, 0 new localities added. Site unchanged at **60 pages** (1 homepage + 5 store pages + 54 locality pages).

**Housekeeping:** Checkout was already on `main`, clean, and matched `origin/main` exactly — no detached HEAD, nothing to reconcile this run.

**Network access note — WebFetch still non-functional, 24th consecutive run:** Re-tested directly at run start against `https://helmetstorenearme.in/` and `https://nominatim.openstreetmap.org/search`. Both failed immediately with `getaddrinfo ENOTFOUND <host>` — the same failure mode reported every run since 2026-09-25. This again contradicts the task brief's claim that WebFetch runs outside the sandbox's egress block; the block appears to still apply to it in this sandbox. `WebSearch` continues to work fully and was used for all research this run. No live-site fetch and no precise Nominatim geocoding were possible.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 60/60 match exactly |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 60 pages |
| Broken internal links | ✅ 0 found |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 60 ≤60 chars, all unique |
| Meta description length/uniqueness | ✅ All 60 unique, all ≤140 chars |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch failed with `getaddrinfo ENOTFOUND` (see network note above) |

Verified with a fresh programmatic sweep script written this run (HTML-unescape-aware). `python3 generate.py` was **not** re-run this run since no data or template change was made (nothing to regenerate); the sweep ran directly against the committed HTML output, which matches `data/stores.json` and `generate.py` on `origin/main`.

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes. Still unresolved — needs a human call on approach (hash-based or data-driven lastmod), not a mechanical fix. First flagged 2026-09-18.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 59 store/locality pages; `Organization` + 5×`SportingGoodsStore` confirmed on the homepage.
- Re-scanned all 60 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds. No individual `Review` object anywhere carries a `reviewRating` field (source data has none).
- `AggregateRating` programmatically checked on all 5 store pages: present with correct `ratingValue`/`reviewCount` only where `reviews.rating` is a real, non-null value (Malad 4.7/2445, Thane 4.5/34); correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating` is null for all three, even though Santacruz and Mira Road carry a review *count*). No change from prior runs.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 categories and all 3 brands (LS2, Crank1, MadDog) appear verbatim on all 5 store pages (confirmed after accounting for `&amp;` HTML-entity escaping in "Touring Luggage & Bags" / "Bike Accessories & Electronics" — both present once correctly unescaped, no real gap). The EMI policy sentence and the 7-day return policy sentence both appear verbatim on all 5 store pages.
- `llms.txt` re-checked line-by-line against current `data/stores.json`: store count (5), every phone number, and all 54 locality names match exactly. No drift.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 59 store/locality pages: each store's phone number appears on every page belonging to that store.
- Authoritativeness (press/backlinks): still the human's active research track via `audits/backlink-citation-plan.md`, unchanged this run — not touched, not re-tabled below (see Carried-over note).

## 5. Platform Optimization

- FAQs unchanged this run; no new buying-decision gap surfaced.

## 6. Local Reach Gaps

**No new localities added this run.** No open candidates were carried in from 2026-10-19 (the candidate table was already empty).

- Checked Mira Road and Navi Mumbai (the two stores with thinner locality coverage — 7 each, vs. 13-14 for Malad/Santacruz/Thane) for genuinely new, well-known missing localities via WebSearch (Nominatim unreachable — see network note).
- Mira Road: search surfaced only thin real-estate-blog names already covered by rejected leads from prior runs — Shanti Nagar/Naya Nagar/Sheetal Nagar (Shanti Nagar and Naya Nagar already on site), Poonam Sagar (a complex/landmark inside Shanti Nagar, not a distinct destination locality), Kanakia Road (long-rejected, inside Mira Road itself), and a cluster of society/complex names (Shanti Park, Sanghavi Nagar, Hatkesh, Silver Park, Golden Nest, Jangid, Pleasant Park, Geeta Nagar, Beverly Park, Evershine Enclave) with no independent confirmation of distinct boundaries or a landmark specific enough to write an honest, non-generic blurb — same treatment as Shivar Garden and Bharti Nagar (rejected 2026-10-19). None actioned.
- Navi Mumbai: search confirmed the existing locality set (CBD Belapur, Nerul, Juinagar, Sanpada, Vashi, Kharghar, Turbhe) already covers the well-known neighbours of Seawoods; no new candidate surfaced beyond the already-rejected list (Koparkhairane, Ghansoli, Airoli, Ulwe, Panvel, Taloja).
- Coverage remains close to saturation for genuinely distinct, in-range localities across all 5 stores. `nominatim.openstreetmap.org` remains unreachable (see network note), so precise geocoding of any future candidate is still blocked pending an environment-level fix.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script — **0 real issues found**.
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness) — **0 real issues found**.
- Entity-coverage, NAP, and `llms.txt` drift checks — **0 real issues found** (one false-positive from the checker script's own `&amp;` handling, resolved and confirmed not a site defect).
- Git state reconciled at run start — already clean, on `main`, matching `origin/main`.
- WebFetch directly re-tested against two different hosts at run start — confirmed still non-functional (`getaddrinfo ENOTFOUND`), 24th consecutive run.

---

## Candidate localities awaiting human geocoding

*(none open)*

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 60 pages | All | Verified via a fresh programmatic sweep script, 0 real issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness all clean |
| No new candidate localities confidently resolved | Local Reach | Checked Mira Road and Navi Mumbai via WebSearch — all new leads read as thin real-estate names or sub-pockets of already-covered areas | Coverage remains near saturation for Mira Road and Navi Mumbai |
| WebFetch non-functional, 24th consecutive run | Technical GEO/SEO / Local Reach | Re-tested directly against 2 different hosts at run start — both failed with `getaddrinfo ENOTFOUND` | All research this run used WebSearch only; live-site check and precise geocoding both blocked |
| Git state at run start | Housekeeping | Already clean, on `main`, matching origin | No action needed |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (`getaddrinfo ENOTFOUND`) | Technical GEO/SEO / Local Reach | Open, now 24 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until this is fixed at the environment level | 2026-09-25 |

*(Two items — "no press/backlinks" (first flagged 2026-09-15) and "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18) — remain open >30 days and continue to be trimmed from this table per the 30-day rule. Both remain real and unresolved; see Category 1 and Category 4 notes above for current status. Neither needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, and the sitemap item needs a one-time human decision on approach, not a recurring mechanical check.)*
