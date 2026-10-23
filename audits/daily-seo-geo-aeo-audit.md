# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-23
**Status:** 🟢 Clean sweep. 0 real issues found, 0 new localities added (no new candidates confidently resolvable; the one open candidate from 2026-10-22, Uttan, remains open). Site unchanged at **60 pages** (1 homepage + 5 store pages + 54 locality pages).

**Housekeeping:** Session started on a clean, up-to-date `main` (`748aad2`) — no detached HEAD, no divergence from origin this run. Nothing to reconcile.

**Network access note — WebFetch still non-functional, 27th consecutive run:** Re-tested directly at run start against two unrelated hosts — `https://helmetstorenearme.in/` and `https://nominatim.openstreetmap.org/search`. Both failed immediately with `getaddrinfo ENOTFOUND <host>`, same as the prior 26 runs — this run's task brief again claims WebFetch runs outside the sandbox's egress block, but that is not borne out here. `WebSearch` continues to work fully and was used for all research this run. No live-site fetch and no precise Nominatim geocoding were possible.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 60/60 match exactly |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 60 pages |
| Broken internal links | ✅ 0 found |
| Image alt text | ✅ Every `<img>` has non-empty alt text |
| Title tag length | ✅ All 60 ≤60 chars (post-entity-decode), all unique |
| Meta description length/uniqueness | ✅ All 60 unique, all ≤140 chars (post-entity-decode) |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch failed with `getaddrinfo ENOTFOUND` (see network note above) |

Verified with a fresh programmatic sweep script written this run (sitemap vs. filesystem diff, title/description length + uniqueness, canonical-vs-expected-URL match, alt-text, JSON-LD `json.loads()` parse, internal-link resolution). One false positive surfaced and was investigated before being dismissed: the raw (HTML-entity-encoded) meta description on `/stores/mira-road/` measured 141 characters because of a literal `&amp;`, but decodes to 137 characters (`&` = 1 char) — within the 140-char limit once properly decoded. The sweep script was fixed to `html.unescape()` before measuring length, consistent with how a real search engine or AI crawler would read the text; confirmed 0 real length violations after the fix. `python3 generate.py` was **not** re-run since no data or template change was made this run — the sweep ran directly against the committed HTML output, which matches `data/stores.json` and `generate.py` on `origin/main`.

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes (confirmed again this run by reading `generate.py:26,370,502,584` — `TODAY = datetime.date.today().isoformat()` is used unconditionally). Still unresolved — needs a human call on approach (hash-based or data-driven lastmod), not a mechanical fix. First flagged 2026-09-18.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` + `openingHoursSpecification` present on all 59 store/locality pages; `Organization` + 5×`SportingGoodsStore` confirmed on the homepage.
- Re-scanned all 60 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds. No individual `Review` object anywhere carries a `reviewRating` field (source data has none).
- `AggregateRating` programmatically checked on all 5 store pages and propagated correctly to every locality page under that store: present with correct `ratingValue`/`reviewCount` only where `reviews.rating` is a real, non-null value (Malad 4.7/2445 on all 15 Malad pages, Thane 4.5/34 on all 14 Thane pages); correctly absent for Santacruz, Mira Road and Navi Mumbai (`rating` is null for all three, even though Santacruz and Mira Road carry a review *count*). No change from prior runs.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 categories and all 3 brands (LS2, Crank1, MadDog) appear verbatim (post-`html.unescape()`) on all 5 store pages.
- The EMI policy sentence and the 7-day return policy sentence both appear verbatim on all 5 store pages. No gap.
- `llms.txt` re-checked line-by-line against current `data/stores.json`: store count (5), every phone number, every Maps link, and all 54 locality names match exactly. No drift.
- FAQ coverage spot-checked: each store carries 4 store-specific FAQs (certification, try-on/fit, location, stock-check) plus 2 brand-wide FAQs (EMI/returns, brands carried) in the rendered `FAQPage` block — 6 total, consistent across all 5 stores. No fabricated or missing facts found.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes). Confirmed all 5 stores still carry a non-empty `gallery` array and a `youtube_id`.
- NAP consistency re-verified programmatically across all 59 store/locality pages: each store's phone number appears on every page belonging to that store.
- Authoritativeness (press/backlinks): still the human's active research track via `audits/backlink-citation-plan.md` — checked git history, last touched 2026-09-17, unchanged this run — not touched, not re-tabled below (see Carried-over note).

## 5. Platform Optimization

- FAQs unchanged this run; no new buying-decision gap surfaced beyond what's noted in Category 3.

## 6. Local Reach Gaps

**No new localities added this run.** The one open candidate (Uttan, Mira Road store, logged 2026-10-22) was re-investigated but not resolved — see below. No other genuinely new, confidently-resolvable candidate surfaced.

- **Uttan (Mira Road store) — re-checked, still unresolved.** WebSearch this run turned up Mira-Bhayandar Municipal Corporation ward data confirming Uttan sits in the same coastal Ward Committee area as Rai, Murdha and Dongri, further out than Rai along Uttan Road — consistent with the existing Rai locality blurb on the site ("Riders continuing further out toward Uttan for a coastal run often stop at Rai first") and with the prior run's haversine estimate (~12.6km road distance, over the ~10km threshold). No tighter pinpoint coordinate for the beach/lighthouse visitor area was found via WebSearch, and Nominatim remains unreachable (WebFetch down). **Still not added** — stays in the candidate table pending a tighter geocode or a human call.
- **Dindoshi (near Malad) — checked, not a distinct candidate.** WebSearch confirms Dindoshi (Mumbai Metro Line 7 station) has its postal address "in Malad East," i.e. it's a sub-locality/landmark inside the already-listed Malad East locality, not a separate catchment area. Same pattern as prior sub-pocket rejections (Andheri West/Versova sub-localities, Kandivali/Borivali sub-localities, etc.) — not logged as a new candidate.
- **Mira Road society/park names — checked, not distinct candidates.** WebSearch surfaced a list of "nearby areas" to Mira Road (Shanti Park, Sanghavi Nagar, Silver Park, Golden Nest, Pleasant Park, Geeta Nagar, Beverly Park, Evershine Enclave). These are housing-society/complex names within Mira Road East itself — the same locality the store is already in — not distinct catchment localities. Golden Nest is already named inside the existing Bhayandar East blurb ("New Golden Nest"). Consistent with the already-rejected "society-name cluster for Mira Road" noted on prior runs — not re-logged.
- Navi Mumbai (Nerul/Seawoods) re-checked via WebSearch for any locality missed beyond the already-rejected list (Koparkhairane, Ghansoli, Airoli, Ulwe, Panvel, Taloja) — search results only reconfirmed the stores already listed (CBD Belapur, Nerul, Juinagar, Sanpada, Kharghar) as the standard "nearby localities" set for Seawoods/Nerul. Nothing new surfaced.

Coverage remains close to saturation for genuinely distinct, in-range localities across all 5 stores. `nominatim.openstreetmap.org` remains unreachable (see network note), so precise geocoding of the one open candidate (Uttan) is still blocked pending an environment-level fix.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script — **0 real issues found** (1 false positive investigated and dismissed — HTML-entity-encoding artifact in length measurement, fixed in the sweep script itself).
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness) — **0 real issues found**.
- Entity-coverage, NAP, and `llms.txt` drift checks — **0 real issues found**.
- Git state reconciled at run start — already clean and up to date with origin, nothing to reconcile.
- WebFetch directly re-tested against two different hosts at run start — confirmed still non-functional (`getaddrinfo ENOTFOUND`), 27th consecutive run.
- Open candidate (Uttan, Mira Road store) re-investigated via WebSearch (ward-boundary data) — reasoning reconfirmed, not resolved, no new candidate logged with duplicate reasoning.
- Two potential new leads (Dindoshi; Mira Road society names) investigated via WebSearch and conclusively found to be sub-localities of areas already on the site, not logged as candidates.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Only town-level Wikipedia coordinates available (not a pinpoint for the actual beach/lighthouse visitor area); road-distance estimate from those coordinates (~12.6km) already exceeds the ~10km threshold. Re-checked 2026-10-23 via ward-boundary WebSearch — confirms Uttan is farther out than the already-listed Rai (7.5km), consistent with the over-threshold estimate. Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. | 2026-10-22 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 60 pages | All | Verified via a fresh programmatic sweep script, 0 real issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ coverage all clean |
| Sweep script false positive on Mira Road meta description length (141 vs 140 chars) | Technical GEO/SEO | Investigated — raw HTML-entity-encoded `&amp;` inflated the count; decodes to 137 chars, within limit. Fixed the sweep script to decode entities before measuring. | No change to the site itself; this was a measurement bug in this run's own tooling, not a site defect |
| Uttan (Mira Road) locality lead | Local Reach | Re-investigated via WebSearch (ward-boundary data); reconfirms prior over-threshold estimate | Left in candidate table, no duplicate re-log; needs tighter geocode or human call |
| Dindoshi (Malad) and Mira Road society/park names | Local Reach | Investigated via WebSearch, found to be sub-localities of areas already on the site | Not logged as new candidates — consistent with prior sub-pocket rejection pattern |
| WebFetch non-functional, 27th consecutive run | Technical GEO/SEO / Local Reach | Re-tested directly against 2 hosts at run start — both failed with `getaddrinfo ENOTFOUND` | Confirms sandbox-wide block persists despite this run's brief claiming otherwise; all research this run used WebSearch only |
| Git state at run start | Housekeeping | Already clean and up to date with `origin/main` | Nothing to reconcile |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (`getaddrinfo ENOTFOUND`) | Technical GEO/SEO / Local Reach | Open, now 27 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until this is fixed at the environment level | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-22 |

*(Two items — "no press/backlinks" (first flagged 2026-09-15) and "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18) — remain open >30 days and continue to be trimmed from this table per the 30-day rule. Both remain real and unresolved; see Category 1 and Category 4 notes above for current status. Neither needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, and the sitemap item needs a one-time human decision on approach, not a recurring mechanical check.)*
