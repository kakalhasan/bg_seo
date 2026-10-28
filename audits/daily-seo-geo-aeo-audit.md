# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-28
**Status:** 🟢 Clean sweep + 1 small technical fix. Full programmatic re-sweep of all pages found 0 real schema/AEO/E-E-A-T issues and 1 minor technical gap (missing `og:site_name` tag, now fixed). No new locality pages added this run — both new leads investigated (Waghbil re-checked, Chincholi Bunder newly investigated) were ruled out for solid reasons, not force-fit. The two already-open candidates (Uttan, Ghatkopar West, Prabhadevi, Waghbil) remain open with unchanged reasoning. Site stays at **62 pages** (1 homepage + 5 store pages + 56 locality pages).

**Housekeeping:** Repo was on a detached HEAD matching `origin/main` at run start (1 commit behind local `main` branch pointer) — checked out `main` and fast-forwarded cleanly, no divergence, no lost work.

**Network access note — WebFetch still non-functional to arbitrary hosts, 32nd consecutive run:** Re-tested directly at run start against `https://helmetstorenearme.in/` and `https://nominatim.openstreetmap.org/search`. Both failed immediately with `getaddrinfo ENOTFOUND <host>`. This run's task brief again claimed WebFetch runs on Anthropic's infrastructure and should be unaffected by the sandbox's `curl`/Bash egress block — not borne out for the 32nd run in a row. `WebSearch` continues to work fully and was used for all research this run. No live-site fetch and no direct Nominatim JSON geocoding were possible.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 62/62 match exactly, 0 missing, 0 extra |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 62 pages (re-verified after fix) |
| Broken internal links | ✅ 0 found (fresh link-checker sweep) |
| Image alt text | ✅ All 84 `<img>` tags have non-empty, descriptive alt text |
| Title tag length | ✅ All 62 ≤60 chars (post-entity-decode), all unique |
| Meta description length/uniqueness | ✅ All 62 unique, all ≤140 chars (post-entity-decode) |
| Canonical tags | ✅ Present and correct on every page |
| Open Graph `og:site_name` | ⚠️→✅ **Fixed this run** — `data/stores.json`'s `brand.site_name` ("Helmet Store Near Me") was never rendered anywhere on the site, not even as the standard `og:site_name` meta tag alongside the existing `og:title`/`og:description`/`og:type`/`og:url`/`og:image`. Added one line to `render_full_page()` in `generate.py` (`generate.py:399`, right after `og:type`), regenerated all 62 pages, re-verified JSON-LD/links/title-length/canonicals all still clean. |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch failed with `getaddrinfo ENOTFOUND` (see network note above) |

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes (`generate.py` — `TODAY = datetime.date.today().isoformat()`). This run's `lastmod` bump to 2026-10-28 across all 62 pages is legitimate (real content changed — the new `og:site_name` tag was added to every page). Still needs a human call on approach (hash-based or data-driven lastmod) for days when nothing actually changes. First flagged 2026-09-18.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` present on all 61 store/locality pages, verified programmatically this run — 0 missing.
- Re-scanned all 62 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds. No individual `Review` object anywhere on the site carries a `reviewRating`.
- `AggregateRating` programmatically re-verified against source `reviews.rating`/`reviews.count`: Malad (4.7/2445) and Thane (4.5/34) carry correct values; Santacruz, Mira Road and Navi Mumbai correctly carry no `AggregateRating` (source `reviews.rating` is `null` for all three). 0 mismatches.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 brand-wide categories, all 3 brands (LS2, Crank1, MadDog), and both brand-wide policy sentences (EMI, 7-day return) appear verbatim (post-`html.unescape()`) somewhere on the site. 0 gaps.
- Also checked `brand.site_name` and `brand.tagline` from `data/stores.json` specifically — neither appears anywhere on the site. Judged **not an entity-coverage gap**: this audit's own criterion (category 3) scopes entity coverage to "brands, categories, hours, policies, certifications" — factual claims an AI engine would quote — not internal branding/metadata fields like a site nickname or tagline. `site_name` is now at least machine-readable via the new `og:site_name` tag (see Category 1); `tagline` remains unused and is a brand-voice call, not a mechanical fix.
- `llms.txt` re-checked programmatically against current `data/stores.json` — every store name and phone number, and all 56 locality names, found verbatim. No drift.
- No new entity-coverage or FAQ gaps surfaced this run; see Carried-over note for the standing MadDog-on-homepage non-issue (unchanged).

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 61 store/locality pages: each store's phone number appears on every page belonging to that store, 0 mismatches.
- Authoritativeness (press/backlinks): still the human's active research track via `audits/backlink-citation-plan.md`; not touched this run.

## 5. Platform Optimization

- Spot-checked FAQ coverage across all 5 stores (certification, try-on, location, stock-check — 4 FAQs each, identical pattern per store). No new buying-decision gap surfaced; this matches the standing conclusion from prior runs that EMI/returns are covered elsewhere on each page (intro copy/policy blocks) even though not phrased as a dedicated FAQ.

## 6. Local Reach Gaps

**No new locality pages added this run.** One new lead (Chincholi Bunder, nominally Malad) was investigated and ruled out — not a gap at all, not even a candidate. One previously-logged candidate (Waghbil) was re-checked with fresh searches; conclusion unchanged. Prabhadevi, Uttan and Ghatkopar West were re-checked; all unchanged.

- **Chincholi Bunder (nominal: Malad) — investigated, NOT a gap, not logged.** Confirmed via WebSearch as a real, well-known Malad West locality (pincode 400064, near Inorbit Mall/Mindspace, Liberty Garden, Dahanukarwadi Metro). But cross-checking `data/stores.json`'s Malad store record shows the store's own address is **"Gala 4, Shakti Textile, Chincholi Bunder Road... Malad West"** — i.e. Chincholi Bunder is where the store itself sits, not a separate nearby locality a customer would search "near me" from. Correctly excluded; not added to the candidate table either, since this isn't an open question, it's a non-issue.
- **Louiswadi (nominal: Thane) — investigated, NOT added, not logged as candidate.** Real Thane West locality, but WebSearch results show its landmarks and boundaries heavily overlap already-covered Thane entries (Pokhran Road corridor shared with the existing Manpada/Cadbury Junction blurb, Kapurbawdi Metro Station shared with the existing Kapurbawdi entry) and sources themselves note "the exact boundaries are unclear." Not distinct enough from existing coverage to justify a dedicated page or add to the candidate queue.
- **Waghbil (Thane) — re-checked via WebSearch, conclusion unchanged.** Fresh search this run still shows a ~1.5km coordinate spread between Wikipedia's two listed figures, and road-distance estimates ranging 6-11km depending on source/endpoint (village centre vs. "Waghbil Naka" junction). Still not confident enough to add. Stays in the candidate table, reasoning unchanged.
- **Prabhadevi (nominal nearest: Santacruz store) — re-checked, conclusion unchanged.** Coordinates remain consistent across sources (~19.016°N/72.829°E); road-estimate still ~10.1-10.2km, just over the ~10km ceiling, and still farther than the existing Mahim entry (7.0km) covering the same corridor. Stays in the candidate table, unchanged.
- **Uttan (Mira Road) — re-checked via WebSearch, conclusion unchanged.** This run's search surfaced an Uttan-to-Bhayandar figure of ~9.1km road / 8km straight-line, consistent with (not contradicting) the prior over-threshold conclusion once the extra stretch from Bhayandar to the Mira Road store itself is added. Stays in the candidate table, unchanged.
- **Ghatkopar West (nominal nearest: Santacruz store) — re-checked via WebSearch, conclusion unchanged.** Fresh sources this run again give a spread (9-10.3km depending on source), still right at the ~10km ceiling, and the cross-city routing concern (via JVLR, 10.6km long in itself) from prior runs is unchanged. Stays in the candidate table, unchanged.
- No other genuinely new, confidently-resolvable candidate surfaced this run. The extensive previously-examined-and-rejected list (Kasarvadavali, Aarey Colony, Airoli, Ulwe, Mira Road West, Koparkhairane, Ghansoli, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Taloja, Poonam Sagar, Hiranandani Estate, Bandra Kurla Complex, Teen Hath Naka/Khopat/Kopri, Golden Nest, Naigaon, Oshiwara cluster, Dindoshi, Powai, Rai, Kalina, Seawoods, "Upper Thane") was not re-litigated — their reasoning stands.

Coverage remains close to saturation for genuinely distinct, in-range localities across all 5 stores.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script covering sitemap-vs-pages, robots.txt bot coverage, JSON-LD parsing, internal links, image alt text, title/description length and uniqueness, and canonical tags — **0 real issues found** (both before and after the `og:site_name` fix).
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness against source `reviews.rating`, FAQPage/BreadcrumbList/SportingGoodsStore completeness) — **0 real issues found**.
- Entity-coverage, NAP, and `llms.txt` drift checks, all re-verified programmatically against current `data/stores.json` — **0 real issues found**.
- Git state reconciled at run start — detached HEAD matching `origin/main`, fast-forwarded `main` to match, nothing lost.
- WebFetch directly re-tested against 2 hosts at run start — confirmed still non-functional (`getaddrinfo ENOTFOUND`), 32nd consecutive run.
- All four open candidates (Uttan, Ghatkopar West, Waghbil, Prabhadevi) re-checked via WebSearch — reasoning reconfirmed on all four, none resolved, none re-logged with duplicate reasoning.
- Two new leads (Chincholi Bunder, Louiswadi) investigated via WebSearch; both correctly excluded (one is the store's own address, not a nearby locality; the other overlaps existing coverage too much to be distinct) rather than force-fit or needlessly added to the candidate queue.
- `og:site_name` fix: added to `generate.py`, regenerated all 62 pages, re-ran the full technical sweep again post-fix — confirmed 0 regressions.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Only town-level coordinates available (not a pinpoint for the actual beach/lighthouse visitor area); road-distance estimate from those coordinates (~12.6km, and the lighthouse operator's own ~12km-from-Bhayandar-station figure) exceeds the ~10km threshold. Re-checked 2026-10-28 via WebSearch, conclusion unchanged. Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. | 2026-10-22 |
| Ghatkopar West | Santacruz (nominal nearest) | Road-estimate to Santacruz sits right at the ~10km ceiling (9-10.3km depending on which of several sources' coordinates are used), but the ×1.3 multiplier is unreliable for this cross-city, opposite-side-of-Mumbai hop (no direct road — via JVLR/SCLR across the hills), and Ghatkopar isn't a natural "near me" catchment for a Santacruz-area search. Needs a human call or a real-route (not straight-line) distance check before adding. Re-checked 2026-10-28, unchanged. | 2026-10-24 |
| Waghbil | Thane | Already named as a landmark in the existing Patlipada blurb, so a real place, but its own coordinates vary ~1.5km between sources and road-distance estimates range 6-11km depending on whether the source measures to the village centre or to "Waghbil Naka" junction. Needs a tighter geocode or a human call before adding. Re-checked 2026-10-28, unchanged. | 2026-10-27 |
| Prabhadevi | Santacruz (nominal nearest) | Coordinates are consistent across sources, but the resulting road-estimate (10.1-10.2km) sits just over the ~10km ceiling, and it's farther from the store than the existing Mahim entry (7.0km) which already covers the same southward corridor. Needs a human call on whether to extend the ceiling for this specific locality, or leave as-is. Re-checked 2026-10-28, unchanged. | 2026-10-27 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Missing `og:site_name` Open Graph tag | Technical GEO/SEO | Added one line to `render_full_page()` in `generate.py` using the existing (previously unused) `brand.site_name` field from `data/stores.json`; regenerated all 62 pages; re-verified full technical sweep clean | No fabricated data — `site_name` ("Helmet Store Near Me") was already present in source data, just never rendered |
| Full technical/schema/AEO/E-E-A-T sweep across all 62 pages | All | Verified via a fresh programmatic sweep, 0 real issues found besides the `og:site_name` gap above | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ/BreadcrumbList/SportingGoodsStore coverage all clean |
| Chincholi Bunder (Malad) locality lead | Local Reach | Investigated via WebSearch; found to be the Malad store's own street address, not a separate nearby locality | Correctly excluded — not a gap, not logged as a candidate |
| Louiswadi (Thane) locality lead | Local Reach | Investigated via WebSearch; landmarks/boundaries overlap existing Kapurbawdi/Manpada coverage too much to be distinct | Not added, not logged as a candidate |
| Waghbil (Thane) locality lead | Local Reach | Re-investigated via WebSearch; coordinate/distance spread persists | Left in candidate table, no duplicate re-log |
| Prabhadevi (Santacruz) locality lead | Local Reach | Re-investigated via WebSearch; road-estimate still just over the ~10km ceiling | Left in candidate table, no duplicate re-log |
| Uttan (Mira Road) locality lead | Local Reach | Re-investigated via WebSearch; reconfirms prior over-threshold estimate | Left in candidate table, no duplicate re-log |
| Ghatkopar West (Santacruz) locality lead | Local Reach | Re-checked via WebSearch with fresh sources; estimate sits right at the ~10km ceiling either way | Left in candidate table, unchanged |
| WebFetch non-functional to arbitrary hosts, 32nd consecutive run | Technical GEO/SEO / Local Reach | Re-tested directly against 2 hosts at run start — both failed with `getaddrinfo ENOTFOUND` | Confirms sandbox-wide block persists despite this run's brief again claiming otherwise; all geocoding research this run used WebSearch only |
| sitemap `lastmod` bumped to run date on all 62 pages | Technical GEO/SEO | No action — this run's bump is legitimate (real content change: `og:site_name` tag added to every page) | Not a spurious stamp this run; underlying mechanical-vs-content-driven issue (see Carried-over) is unchanged |
| Repo was on detached HEAD at run start | Housekeeping | Checked out `main`, fast-forwarded 1 commit to match `origin/main` | No divergence, nothing lost |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (`getaddrinfo ENOTFOUND`) | Technical GEO/SEO / Local Reach | Open, now 32 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until this is fixed at the environment level | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-22 |
| Ghatkopar West — candidate locality needing a real-route distance check or human call | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-24 |
| Waghbil (Thane) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-27 |
| Prabhadevi (Santacruz) — candidate locality, borderline over the ~10km ceiling | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-27 |

*(Three items — "no press/backlinks" (first flagged 2026-09-15), "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18), and "MadDog brand not named verbatim in homepage's brand-description copy" (first flagged 2026-09-16, not a real entity-coverage gap since MadDog is already quotable on all 5 store pages) — remain open >30 days and continue to be trimmed from this table per the 30-day rule. All three remain unresolved/unchanged; see Category 4 (reviews/backlinks), Category 1 (sitemap `lastmod`), and Category 3 (MadDog) history for current status. None needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, the sitemap item needs a one-time human decision on approach, and the MadDog item is a non-issue under this audit's own entity-coverage criterion.)*
