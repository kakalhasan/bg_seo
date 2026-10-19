# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-19
**Status:** 🟢 Clean sweep. 0 real issues found, 0 new localities added. Site unchanged at **60 pages** (1 homepage + 5 store pages + 54 locality pages).

**Housekeeping:** Checkout was already on `main`, clean, and matched `origin/main` exactly — no detached HEAD, nothing to reconcile this run.

**Network access note — WebFetch still non-functional, 23rd consecutive run:** Re-tested directly at run start against `https://helmetstorenearme.in/` and `https://nominatim.openstreetmap.org/search`. Both failed immediately with `getaddrinfo ENOTFOUND <host>` — the same failure mode reported every run since 2026-09-25. This again contradicts the task brief's claim that WebFetch runs outside the sandbox's egress block; the block appears to still apply to it in this sandbox. `WebSearch` continues to work fully and was used for all research this run, including a `site:helmetstorenearme.in` query — Google did not appear to honor the `site:` operator for this domain (returned unrelated generic results), so the live site's indexing status could not be confirmed this way either. No live-site fetch was possible.

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

Verified with a fresh programmatic sweep script (rewritten this run, `html.unescape()`-aware per the 2026-10-17 fix). `python3 generate.py` re-run first to confirm idempotency — only `sitemap.xml`'s `lastmod` dates changed (known carried-over generator issue, see below); reverted since no real content changed. 0 real issues on the sweep.

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes. Still unresolved — needs a human call on approach (hash-based or data-driven lastmod), not a mechanical fix. First flagged 2026-09-18.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 59 store/locality pages; `Organization` + 5×`SportingGoodsStore` confirmed on the homepage.
- Re-scanned all 60 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds. No individual `Review` object anywhere carries a `reviewRating` field (source data has none).
- `AggregateRating` programmatically checked on all 5 store pages: present with correct `ratingValue`/`reviewCount` only where `reviews.rating` is a real, non-null value (Malad 4.7/2445, Thane 4.5/34); correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating` is null for all three, even though Santacruz and Mira Road carry a review *count*). No change from prior runs.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 categories and all 3 brands (LS2, Crank1, MadDog) appear verbatim on all 5 store pages. The EMI policy sentence and the 7-day return policy sentence both appear verbatim on all 5 store pages. No gap.
- `llms.txt` re-checked line-by-line against current `data/stores.json`: store count (5), every phone number, and all 54 locality names match exactly. No drift.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 59 store/locality pages: each store's phone number appears on every page belonging to that store.
- Authoritativeness (press/backlinks): still the human's active research track via `audits/backlink-citation-plan.md`, unchanged this run — not touched, not re-tabled below (see Carried-over note).

## 5. Platform Optimization

- FAQs unchanged this run; no new buying-decision gap surfaced.

## 6. Local Reach Gaps

**No new localities added this run.** No open candidates were carried in from 2026-10-17 (the candidate table was already empty).

- Checked whether any genuinely new, well-known locality near Mira Road or Navi Mumbai (the two stores with thinner locality coverage — 7 each, vs. 13-14 for Malad/Santacruz/Thane) was missing, via WebSearch (Nominatim unreachable — see network note).
- Two new leads surfaced for Mira Road and were **not** added or formally logged:
  - **Shivar Garden** — a park/landmark on Mira Bhayander Road inside Mira Road East itself, per a builder listing and a property-portal page. Reads as a sub-pocket of the store's own immediate area, not a distinct destination locality — same overlap issue as Sai Baba Nagar (rejected 2026-10-17) and the long-rejected Mira Road West/Kanakia leads.
  - **Bharti Nagar** — also inside Mira Road East per thin, auto-generated-looking listing copy; no independent confirmation of its boundaries or any landmark distinct enough to write an honest, non-generic blurb. Not confident enough to action; not logged as a formal candidate since the lead is too thin to pursue (same treatment as Sai Baba Nagar).
- No new candidates surfaced for Navi Mumbai beyond the already-rejected list (Koparkhairane, Ghansoli, Airoli, Ulwe, Panvel, Taloja and similar — all either over the ~10km threshold or thin real-estate-listing names with no distinct landmark).
- Coverage remains close to saturation for genuinely distinct, in-range localities across all 5 stores. `nominatim.openstreetmap.org` remains unreachable (see network note), so precise geocoding of any future candidate is still blocked pending an environment-level fix.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script — **0 real issues found**.
- `generate.py` re-run to confirm idempotency — only `sitemap.xml` `lastmod` dates changed (known issue), reverted.
- Git state reconciled at run start — already clean, on `main`, matching `origin/main`.
- WebFetch directly re-tested against two different hosts at run start — confirmed still non-functional (`getaddrinfo ENOTFOUND`), 23rd consecutive run.

---

## Candidate localities awaiting human geocoding

*(none open)*

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 60 pages | All | Verified via a fresh programmatic sweep script, 0 real issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness all clean |
| No new candidate localities confidently resolved | Local Reach | Checked 2 new weak leads for Mira Road (Shivar Garden, Bharti Nagar) via WebSearch — both read as sub-pockets of the store's own area, not actionable | Coverage remains near saturation for Mira Road and Navi Mumbai |
| WebFetch non-functional, 23rd consecutive run | Technical GEO/SEO / Local Reach | Re-tested directly against 2 different hosts at run start — both failed with `getaddrinfo ENOTFOUND` | All research this run used WebSearch only; live-site check and precise geocoding both blocked |
| Git state at run start | Housekeeping | Already clean, on `main`, matching origin | No action needed |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (`getaddrinfo ENOTFOUND`) | Technical GEO/SEO / Local Reach | Open, now 23 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until this is fixed at the environment level | 2026-09-25 |

*(Two items — "no press/backlinks" (first flagged 2026-09-15) and "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18) — have now been open >30 days and are trimmed from this table per the 30-day rule. Both remain real and unresolved; see Category 1 and Category 4 notes above for current status. Neither needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, and the sitemap item needs a one-time human decision on approach, not a recurring mechanical check.)*
