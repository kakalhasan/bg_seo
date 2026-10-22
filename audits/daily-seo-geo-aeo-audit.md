# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-22
**Status:** 🟢 Clean sweep. 0 real issues found, 0 new localities added (1 new candidate logged, uncertain on distance/geocode precision). Site unchanged at **60 pages** (1 homepage + 5 store pages + 54 locality pages).

**Housekeeping:** Session started on a detached HEAD, 2 commits behind `origin/main`'s `d633747`→`ae9c551` history from the 2026-10-21 run. Fetched, checked out `main`, and fast-forwarded — no divergent work to lose, nothing else to reconcile.

**Network access note — WebFetch still non-functional, 26th consecutive run:** Re-tested directly at run start against two unrelated hosts — `https://helmetstorenearme.in/` and `https://nominatim.openstreetmap.org/search`. Both failed immediately with `getaddrinfo ENOTFOUND <host>`, same as the prior 25 runs — this run's task brief claims WebFetch runs outside the sandbox's egress block, but that is not borne out here. `WebSearch` continues to work fully and was used for all research this run, including the one new locality lead (Uttan, see Category 6). No live-site fetch and no precise Nominatim geocoding were possible.

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

Verified with a fresh programmatic sweep script written this run (sitemap vs. filesystem diff, title/description length + uniqueness, canonical-vs-expected-URL match, alt-text, JSON-LD `json.loads()` parse, internal-link resolution). `python3 generate.py` was **not** re-run since no data or template change was made this run — the sweep ran directly against the committed HTML output, which matches `data/stores.json` and `generate.py` on `origin/main`.

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes (confirmed again this run by reading `generate.py:26,370,502,584` — `TODAY = datetime.date.today().isoformat()` is used unconditionally). Still unresolved — needs a human call on approach (hash-based or data-driven lastmod), not a mechanical fix. First flagged 2026-09-18.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 59 store/locality pages; `Organization` + 5×`SportingGoodsStore` confirmed on the homepage.
- Re-scanned all 60 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds. No individual `Review` object anywhere carries a `reviewRating` field (source data has none).
- `AggregateRating` programmatically checked on all 5 store pages: present with correct `ratingValue`/`reviewCount` only where `reviews.rating` is a real, non-null value (Malad 4.7/2445, Thane 4.5/34); correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating` is null for all three, even though Santacruz and Mira Road carry a review *count*). No change from prior runs.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 categories and all 3 brands (LS2, Crank1, MadDog) appear verbatim (post-`html.unescape()`) on all 5 store pages. The homepage's own lead copy says "LS2, Crank1 and other brands" without naming MadDog explicitly — checked whether this is a real gap: it isn't, since the criterion is "somewhere on the site" and MadDog is named verbatim (in prose, the Brands field, and the brands FAQ) on all 5 store pages one click away. Not logged as a finding; noted here for the record.
- The EMI policy sentence and the 7-day return policy sentence both appear verbatim on all 5 store pages. No gap.
- `llms.txt` re-checked line-by-line against current `data/stores.json`: store count (5), every phone number, and all 54 locality names match exactly. No drift.
- FAQ coverage spot-checked: each store carries 4 store-specific FAQs (certification, try-on/fit, location, stock-check) plus 2 brand-wide FAQs (EMI/returns, brands carried) in the rendered `FAQPage` block — 6 total, consistent across all 5 stores. No fabricated or missing facts found; any further FAQ (e.g. pricing/budget tiers, parking) would require a new fact in `data/stores.json` first, which is a human call, not something to add speculatively.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes). Confirmed all 5 stores still carry a non-empty `gallery` array and a `youtube_id`.
- NAP consistency re-verified programmatically across all 59 store/locality pages: each store's phone number appears on every page belonging to that store.
- Authoritativeness (press/backlinks): still the human's active research track via `audits/backlink-citation-plan.md`, unchanged this run — not touched, not re-tabled below (see Carried-over note).

## 5. Platform Optimization

- FAQs unchanged this run; no new buying-decision gap surfaced beyond what's noted in Category 3.

## 6. Local Reach Gaps

**No new localities added this run.** No open candidates were carried in from 2026-10-21 (the candidate table was already empty). One new candidate surfaced and is logged below rather than added.

- **Uttan (Mira Road store)** — surfaced via WebSearch as a genuinely distinct locality from the already-rejected "Mira Road West" (the latter is undeveloped salt pans/mangroves per Wikipedia; Uttan is a separate coastal former-fishing-village area under the same Mira-Bhayandar Municipal Corporation, with real landmarks — a beach and the Uttan Point lighthouse). Checked distance: only town-level Wikipedia coordinates were available (19.280, 72.785), not a pinpoint for the beach/lighthouse area riders would actually visit. Haversine from those coordinates to the Mira Road store (19.2843751, 72.8772246) is 9.69km straight-line → ~12.6km road estimate at the site's standard ×1.3 multiplier, **over** the ~10km threshold. Nominatim geocoding to get a tighter, more specific coordinate was not possible (WebFetch down — see network note). **Not added — logged as a candidate** pending either a tighter geocode (once WebFetch/Nominatim is restored) or a human call, since the only distance estimate available already exceeds the threshold and the underlying coordinate is approximate.
- Re-checked Mira Road and Navi Mumbai (thinnest coverage, 7 localities each) against general knowledge one more time beyond the long-rejected list (Shivar Garden, Bharti Nagar, Poonam Sagar, Kanakia Road, Mira Road West, and the society-name cluster for Mira Road; Koparkhairane, Ghansoli, Airoli, Ulwe, Panvel, Taloja for Navi Mumbai) — WebSearch confirms Ulwe (~12km), Taloja (~16.8km) and Ghansoli (~14.8km) are all measured from Seawoods and remain outside the 10km radius, consistent with prior rejections. Nothing else new surfaced.
- Andheri West/Versova sub-localities (Santacruz), Kandivali/Borivali sub-localities (Malad), and Kasarvadavali/Hiranandani Estate/Ghodbunder-Road-corridor names (Thane) were not re-litigated this run — all were already investigated and conclusively rejected on prior runs (sub-pockets of already-listed broader localities, or already named inside an existing blurb) and nothing new changes that.

Coverage remains close to saturation for genuinely distinct, in-range localities across all 5 stores. `nominatim.openstreetmap.org` remains unreachable (see network note), so precise geocoding of the one open candidate (Uttan) is still blocked pending an environment-level fix.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script — **0 real issues found**.
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness) — **0 real issues found**.
- Entity-coverage, NAP, and `llms.txt` drift checks — **0 real issues found** (one homepage-level brand-naming nuance checked and found not to be a real gap, see Category 3).
- Git state reconciled at run start — detached HEAD two commits behind origin, fast-forwarded cleanly.
- WebFetch directly re-tested against two different hosts at run start — confirmed still non-functional (`getaddrinfo ENOTFOUND`), 26th consecutive run.
- One new locality lead (Uttan, Mira Road store) investigated via WebSearch and haversine distance calculation to a firm conclusion (logged as candidate, not added — see Category 6).

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Only town-level Wikipedia coordinates available (not a pinpoint for the actual beach/lighthouse visitor area); road-distance estimate from those coordinates (~12.6km) already exceeds the ~10km threshold. Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. | 2026-10-22 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 60 pages | All | Verified via a fresh programmatic sweep script, 0 real issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ coverage all clean |
| Homepage doesn't name "MadDog" explicitly (only store pages do) | AI Citability / AEO | Checked, determined not a real gap — fact is quotable on all 5 store pages | No change made; criterion is "somewhere on the site", satisfied |
| Uttan (Mira Road) locality lead | Local Reach | Investigated via WebSearch + haversine; road-distance estimate (~12.6km) exceeds 10km threshold on available town-level coordinates | Logged to candidate table rather than added; needs tighter geocode or human call |
| WebFetch non-functional, 26th consecutive run | Technical GEO/SEO / Local Reach | Re-tested directly against 2 hosts at run start — both failed with `getaddrinfo ENOTFOUND` | Confirms sandbox-wide block persists despite this run's brief claiming otherwise; all research this run used WebSearch only |
| Git state at run start | Housekeeping | Detached HEAD two commits behind origin — fetched, checked out `main`, fast-forwarded | No divergent work, nothing else to reconcile |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (`getaddrinfo ENOTFOUND`) | Technical GEO/SEO / Local Reach | Open, now 26 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until this is fixed at the environment level | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, logged this run — see candidate table above | 2026-10-22 |

*(Two items — "no press/backlinks" (first flagged 2026-09-15) and "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18) — remain open >30 days and continue to be trimmed from this table per the 30-day rule. Both remain real and unresolved; see Category 1 and Category 4 notes above for current status. Neither needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, and the sitemap item needs a one-time human decision on approach, not a recurring mechanical check.)*
