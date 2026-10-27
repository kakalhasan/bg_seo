# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-10-27
**Status:** 🟢 Clean sweep + 1 new locality page added. Full programmatic re-sweep of all pages found 0 real technical/schema/AEO/E-E-A-T issues. **1 new locality page added: Brahmand (Thane store, 5.0 km, off Ghodbunder Road near Kapurbawdi)** — geocoded and verified this run. Two new leads (Waghbil, Prabhadevi) were investigated and logged as candidates rather than added — see Local Reach Gaps. The two already-open candidates (Uttan, Ghatkopar West) remain open with unchanged reasoning. Site grew from **61 to 62 pages** (1 homepage + 5 store pages + 56 locality pages).

**Housekeeping:** Repo was already clean and up to date with `origin/main` (`0e8d6f2`) at run start — no detached HEAD, no divergence, nothing to reconcile.

**Network access note — WebFetch still non-functional to arbitrary hosts, 31st consecutive run:** Re-tested directly at run start against two hosts — `https://helmetstorenearme.in/` and `https://nominatim.openstreetmap.org/search`. Both failed immediately with `getaddrinfo ENOTFOUND <host>`, with the harness itself stating the host is outside this session's allowed network domains. This run's task brief again claimed WebFetch runs on Anthropic's infrastructure and should be unaffected by the sandbox's `curl`/Bash egress block — not borne out here for the 31st run in a row (neither the live site nor Nominatim is reachable via WebFetch). `WebSearch` continues to work fully and was used for all geocoding research this run. No live-site fetch and no direct Nominatim JSON geocoding were possible; all distance estimates below use WebSearch-sourced reference coordinates and haversine calculation (via local Python), consistent with every run since this was first flagged.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 62/62 match exactly, 0 missing, 0 extra (re-verified after adding Brahmand) |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 62 pages |
| Broken internal links | ✅ 0 found (fresh sweep via a new link-checker script this run, handles relative hrefs + fragments/query strings) |
| Image alt text | ✅ Every `<img>` has non-empty, descriptive alt text |
| Title tag length | ✅ All 62 ≤60 chars (post-entity-decode), all unique, including new Brahmand page's title |
| Meta description length/uniqueness | ✅ All 62 unique, all ≤140 chars (post-entity-decode), including new Brahmand page |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch failed with `getaddrinfo ENOTFOUND` (see network note above) |

Ran a fresh broken-link sweep across all 62 pages — 0 broken links, including the new `near/thane/brahmand/` page and the 14 other Thane-store pages whose "other areas near" grid now links to it.

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes (`generate.py:26` — `TODAY = datetime.date.today().isoformat()`). This run's `lastmod` bump to 2026-10-27 across all 62 pages is legitimate (real content changed — a new locality was added and 15 Thane-store pages' "other areas" grids changed), not a spurious stamp. Still needs a human call on approach (hash-based or data-driven lastmod) for days when nothing actually changes. First flagged 2026-09-18.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` present on all 61 store/locality pages, verified programmatically this run — 0 missing, including the new Brahmand page.
- Re-scanned all 62 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds.
- `AggregateRating` programmatically re-verified against source `reviews.rating`/`reviews.count`: Malad (4.7/2445) and Thane (4.5/34) carry correct values; Santacruz, Mira Road and Navi Mumbai correctly carry no `AggregateRating` (source `reviews.rating` is `null` for all three). 0 mismatches.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 brand-wide categories, all 3 brands (LS2, Crank1, MadDog), and both brand-wide policy sentences (EMI, 7-day return) appear verbatim (post-`html.unescape()`) somewhere on the site. 0 gaps.
- `llms.txt` re-checked programmatically against current `data/stores.json` after the Brahmand addition: every store name, phone number and Maps link, and all 56 locality names (including the new Brahmand), found verbatim in `llms.txt`. No drift — confirmed it picked up the new locality automatically on regeneration.
- No new entity-coverage or FAQ gaps surfaced this run; see Carried-over note for the standing MadDog-on-homepage non-issue (unchanged).

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 61 store/locality pages (including the new Brahmand page): each store's phone number appears on every page belonging to that store, 0 mismatches.
- Authoritativeness (press/backlinks): still the human's active research track via `audits/backlink-citation-plan.md`; not touched this run (see Carried-over note).

## 5. Platform Optimization

- FAQs unchanged this run; no new buying-decision gap surfaced beyond what's noted in Category 3.

## 6. Local Reach Gaps

**1 new locality page added this run: Brahmand (Thane store).** Two new leads (Waghbil, Prabhadevi) were investigated and logged as candidates rather than added. The two already-open candidates (Uttan, Ghatkopar West) were re-checked; both unchanged.

- **Brahmand (Thane store) — ADDED.** Geocoded via WebSearch (two independent real-estate-listing coordinate pins for addresses in the locality, 19.2466°N/72.9805°E and 19.2458°N/72.9800°E — [Square Yards: Brahmand overview](https://www.squareyards.com/brahmand-in-thane-overview-4627), consistent to within ~150m); haversine straight-line distance from the Thane store (19.201555, 72.9749461) is ~4.95-5.05 km → road estimate (×1.3) ≈ 6.4-6.6 km, comfortably inside the ~10 km ceiling. Set to **5.0 km / 15-18 min**, interpolated between the existing Patlipada (4.9 km → 14-17 min) and Kolshet Road (6.1 km → 16-20 min) entries. Wrote a hand-written blurb naming Brahmand's real, verified older local name "Dharmacha Pada" (confirmed across multiple independent real-estate sources, not fabricated) and its real position — a cooperative-housing belt about 1 km off Ghodbunder Road near the Kapurbawdi stretch — rather than inventing a landmark I couldn't confirm (a WebSearch for a specific "Brahmand Temple"/Yeoor/lake landmark came up empty, so the blurb deliberately doesn't claim one). Added to `data/stores.json`, regenerated with `python3 generate.py`, verified: JSON-LD parses, title/description within length limits, canonical correct, page links resolve, `llms.txt` and sitemap picked it up automatically, phone/NAP present, 0 broken links.
- **Waghbil (Thane store) — investigated, NOT added, logged as a new candidate.** Already referenced as a landmark in the existing Patlipada blurb ("between Manpada and Waghbil"), so a real place, but its own coordinates are inconsistent across sources: Wikipedia's current figure (19.266°N, 72.985°E) gives a haversine of 7.24 km → road-est 9.42 km from the Thane store, while an older Wikipedia mirror (19.253°N, 72.978°E) gives 5.73 km → road-est 7.45 km, a ~2 km swing between sources. A dedicated routing site ([distancesfrom.com: Thane Station to Waghbil Naka GB via Waghbil Naka Flyover](https://www.distancesfrom.com/distance-from-Thane-Station-to-Waghbil--Naka-GB--Thane-W-via-Waghbil-Naka-Flyover/DistanceHistory/9216685.aspx)) separately gives an actual 9 km road route, measured from Thane Station rather than our exact store coordinates. All estimates land close to or under the ~10 km ceiling, but with too much spread between sources to be "genuinely confident" per this run's own bar. Logged to the candidate table rather than added.
- **Prabhadevi (nominal nearest: Santacruz store) — investigated, NOT added, logged as a new candidate.** Coordinates consistent across sources (Wikipedia 19.0166°N/72.8295°E; latlong.net 19.016439°N/72.829422°E); haversine from the Santacruz store (19.086455, 72.8358556) is 7.80-7.81 km → road-estimate 10.14-10.16 km, just over the ~10 km ceiling (and farther than the existing Mahim entry at 7.0 km/22-25 min, which already covers the same southward corridor). Logged to the candidate table rather than added.
- **Uttan (Mira Road store) — re-checked via WebSearch, conclusion unchanged.** Same town-level coordinates as prior runs (≈19.280°N, 72.785°E, [Uttan, Wikipedia](https://en.wikipedia.org/wiki/Uttan)); this run's search also surfaced the lighthouse operator's own figure of ~12 km by road from Bhayandar station, reinforcing rather than contradicting the over-threshold conclusion. Stays in the candidate table, reasoning unchanged.
- **Ghatkopar West (nominal nearest: Santacruz store) — re-checked via WebSearch, conclusion unchanged.** Re-ran the geocode with four independent sources this run (post office point, latlong.net, a travel-distance site, and the railway station); haversine from the Santacruz store (19.086455, 72.8358556) ranges 7.23-7.60 km → road-estimate 9.4-9.9 km, still right at the ~10 km ceiling, and the cross-city routing concern (no direct road — via JVLR/SCLR across the hills) from prior runs is unchanged. Stays in the candidate table, unchanged.
- No other genuinely new, confidently-resolvable candidate surfaced this run. The extensive list of previously-examined and rejected/already-covered names (Kasarvadavali, Aarey Colony, Airoli, Ulwe, Mira Road West, Koparkhairane, Ghansoli, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Taloja, Poonam Sagar, Hiranandani Estate, Bandra Kurla Complex, Teen Hath Naka/Khopat/Kopri, Golden Nest, Naigaon, Oshiwara cluster, Dindoshi, Powai, Rai, Kalina, Seawoods, "Upper Thane") was not re-litigated — their reasoning stands.

Coverage remains close to saturation for genuinely distinct, in-range localities across all 5 stores; Brahmand was a genuine gap on the Kapurbawdi/Ghodbunder Road side of Thane, distinct from the already-covered Majiwada, Kapurbawdi, Manpada and Patlipada entries on that same corridor.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script covering sitemap-vs-pages, robots.txt bot coverage, JSON-LD parsing, internal links, image alt text, title/description length and uniqueness, and canonical tags — **0 real issues found**, re-run after the Brahmand addition.
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness against source `reviews.rating`, FAQPage/BreadcrumbList/SportingGoodsStore completeness) — **0 real issues found**.
- Entity-coverage, NAP, and `llms.txt` drift checks, all re-verified programmatically against current `data/stores.json` — **0 real issues found**, confirmed `llms.txt` auto-picked up the new Brahmand locality.
- Git state reconciled at run start — already clean and matching `origin/main`, nothing to do.
- WebFetch directly re-tested against 2 hosts at run start — confirmed still non-functional (`getaddrinfo ENOTFOUND`), 31st consecutive run.
- Both open candidates (Uttan, Ghatkopar West) re-checked via WebSearch — reasoning reconfirmed on both, neither resolved, neither re-logged with duplicate reasoning.
- Two new leads (Waghbil, Prabhadevi) investigated via WebSearch, found genuinely uncertain/borderline, logged as new candidates rather than added or force-fit.
- One new locality (Brahmand) geocoded, distance/ride-time calibrated against existing nearby entries, blurb written using a verified real local name (Dharmacha Pada) and position rather than an unconfirmed landmark, added, regenerated, and fully re-verified.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Only town-level coordinates available (not a pinpoint for the actual beach/lighthouse visitor area); road-distance estimate from those coordinates (~12.6km, and the lighthouse operator's own ~12km-from-Bhayandar-station figure) exceeds the ~10km threshold. Re-checked 2026-10-27 via WebSearch, conclusion unchanged. Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. | 2026-10-22 |
| Ghatkopar West | Santacruz (nominal nearest) | Road-estimate to Santacruz sits right at the ~10km ceiling (9.4-9.9km depending on which of 4 sources' coordinates are used), but the ×1.3 multiplier is unreliable for this cross-city, opposite-side-of-Mumbai hop (no direct road — via JVLR/SCLR across the hills), and Ghatkopar isn't a natural "near me" catchment for a Santacruz-area search. Needs a human call or a real-route (not straight-line) distance check before adding. Re-checked 2026-10-27, unchanged. | 2026-10-24 |
| Waghbil | Thane | Already named as a landmark in the existing Patlipada blurb, so a real place, but its own coordinates vary ~2km between sources (7.45-9.42km road-estimate depending on source), and a dedicated routing site's actual 9km road figure is measured from Thane Station rather than the store's exact coordinates. Needs a tighter geocode or a human call before adding. | 2026-10-27 |
| Prabhadevi | Santacruz (nominal nearest) | Coordinates are consistent across sources, but the resulting road-estimate (10.14-10.16km) sits just over the ~10km ceiling, and it's farther from the store than the existing Mahim entry (7.0km) which already covers the same southward corridor. Needs a human call on whether to extend the ceiling for this specific locality, or leave as-is. | 2026-10-27 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 62 pages | All | Verified via a fresh programmatic sweep, 0 real issues found | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ/BreadcrumbList/SportingGoodsStore coverage all clean |
| Brahmand (Thane) — new locality | Local Reach | Geocoded via WebSearch (2 independent listing pins, ~5.0km straight-line → ~6.5km road-est), calibrated ride-time against existing Patlipada/Kolshet Road entries, wrote a hand-written blurb naming the verified local name "Dharmacha Pada" rather than an unconfirmed landmark, added to `data/stores.json`, regenerated, fully re-verified | New page: `near/thane/brahmand/`. Site now 62 pages |
| Waghbil (Thane) locality lead | Local Reach | Investigated via WebSearch; coordinates inconsistent ~2km between sources, not confident enough to add | Logged as new candidate, not added |
| Prabhadevi (Santacruz) locality lead | Local Reach | Investigated via WebSearch; consistent coordinates but road-estimate (10.1-10.2km) just over the ~10km ceiling | Logged as new candidate, not added |
| Uttan (Mira Road) locality lead | Local Reach | Re-investigated via WebSearch; reconfirms prior over-threshold estimate | Left in candidate table, no duplicate re-log |
| Ghatkopar West (Santacruz) locality lead | Local Reach | Re-checked via WebSearch with fresh coordinate sources; estimate sits right at the ~10km ceiling either way, reasoning on cross-city routing unchanged | Left in candidate table, unchanged |
| WebFetch non-functional to arbitrary hosts, 31st consecutive run | Technical GEO/SEO / Local Reach | Re-tested directly against 2 hosts at run start — both failed with `getaddrinfo ENOTFOUND` | Confirms sandbox-wide block persists despite this run's brief again claiming otherwise; all geocoding research this run used WebSearch only |
| sitemap `lastmod` bumped to run date on all 62 pages | Technical GEO/SEO | No action — this run's bump is legitimate (real content change: new locality page + 15 Thane pages' nav grids changed) | Not a spurious stamp this run; underlying mechanical-vs-content-driven issue (see Carried-over) is unchanged |

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (`getaddrinfo ENOTFOUND`) | Technical GEO/SEO / Local Reach | Open, now 31 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until this is fixed at the environment level | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-22 |
| Ghatkopar West — candidate locality needing a real-route distance check or human call | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-24 |
| Waghbil (Thane) — candidate locality needing tighter geocode | Local Reach | Open, newly logged this run — see candidate table above | 2026-10-27 |
| Prabhadevi (Santacruz) — candidate locality, borderline over the ~10km ceiling | Local Reach | Open, newly logged this run — see candidate table above | 2026-10-27 |
| MadDog brand not named verbatim in homepage's brand-description copy | AI Citability/AEO | Open but not a real gap — MadDog is already quotable on all 5 store pages, so this is not an entity-coverage failure under this audit's own criterion. Editing the homepage's deliberately-phrased marketing copy is bucket-C brand-voice territory, not a mechanical fix. Unchanged this run. | 2026-09-16 |

*(Two items — "no press/backlinks" (first flagged 2026-09-15) and "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18) — remain open >30 days and continue to be trimmed from this table per the 30-day rule. Both remain real and unresolved; see Category 4 (reviews/backlinks) and Category 1 (sitemap `lastmod`) history for current status. Neither needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, and the sitemap item needs a one-time human decision on approach, not a recurring mechanical check.)*
