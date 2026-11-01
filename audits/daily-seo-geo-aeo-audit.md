# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-11-01
**Status:** 🟢 Clean sweep, no changes needed. Full programmatic re-sweep of all 62 pages (technical, schema, entity-coverage, NAP, llms.txt, AggregateRating correctness) found 0 issues. No new locality pages added this run — the four already-open candidates (Uttan, Ghatkopar West, Waghbil, Prabhadevi) were re-checked via WebSearch and haversine distance recomputation; none resolved, reasoning unchanged. One new candidate (Shilphata, Thane) was investigated and rejected outright (clearly over threshold), not added to the candidate table. Site stays at **62 pages** (1 homepage + 5 store pages + 56 locality pages).

**Housekeeping:** Session started on a detached HEAD at the same commit as `origin/main` (no divergence, no lost work) — reconciled with `git checkout -B main origin/main`. Working tree was clean throughout.

**Network access note — WebFetch still blocked at the session network-policy level, 35th consecutive run:** This run's instructions stated WebFetch/WebSearch now bypass the sandbox VM's network block since they run on Anthropic's infrastructure. Tested directly: `WebSearch` works fully and was used for all research this run. `WebFetch`, however, still fails with `getaddrinfo ENOTFOUND <host>` against every host tried this run — the live site (`helmetstorenearme.in`), Nominatim (`nominatim.openstreetmap.org`), and even a neutral control host (`example.com`) — with the tool's own error confirming the host is outside this session's allowed network domains. So the block is a session-level allowlist restriction on WebFetch specifically, not fixed by this run's claim, and not host-specific (all three tested hosts failed identically, including a host with no plausible reason to be blocked). Precise Nominatim JSON geocoding and a live-site fetch remain unavailable; all geocoding this run used WebSearch's synthesized answers (which cite Wikipedia/latlong.net/Rome2Rio/etc.) plus manual haversine computation against `data/stores.json` coordinates — the same workaround used for the prior 34 runs.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 62/62 match exactly, 0 missing, 0 extra |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /`, sitemap referenced |
| JSON-LD parses | ✅ 0 errors across all 62 pages |
| Broken internal links | ✅ 0 found (fresh link-checker sweep) |
| Image alt text | ✅ All `<img>` tags have non-empty, descriptive alt text |
| Title tag length | ✅ All 62 ≤60 chars (post-entity-decode), all unique |
| Meta description length/uniqueness | ✅ All 62 unique, all ≤140 chars (post-entity-decode) |
| Canonical tags | ✅ Present and correct on every page |
| Live-site check (helmetstorenearme.in) | ⚠️ Not performed — WebFetch failed, session-level network block (see network note above) |

**Housekeeping note:** `python3 generate.py` was run to confirm output matches current `data/stores.json` — it regenerated identically except for `sitemap.xml`'s `lastmod` dates bumping to today (the known issue below). Since no real content changed, that no-op diff was reverted with `git checkout -- sitemap.xml` rather than committed.

**Known open issue (not re-tabled below, see Carried-over note):** `generate.py` stamps every page's sitemap `lastmod` to the run date on every invocation rather than tracking real per-page content changes (`generate.py` — `TODAY = datetime.date.today().isoformat()`). Still needs a human call on approach (hash-based or data-driven lastmod). First flagged 2026-09-18.

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` present on all 61 store/locality pages, verified programmatically this run — 0 missing.
- Re-scanned all 62 pages' JSON-LD for the reviewRating-fabrication pattern (fixed 2026-09-16) — **0 found**, fix holds. No individual `Review` object anywhere on the site carries a `reviewRating`.
- `AggregateRating` programmatically re-verified against source `reviews.rating`/`reviews.count`: Malad (4.7/2445) and Thane (4.5/34) carry correct values; Santacruz, Mira Road and Navi Mumbai correctly carry no `AggregateRating` (source `reviews.rating` is `null` for all three). 0 mismatches.

## 3. AI Citability / AEO

- Entity-coverage re-check: all 6 brand-wide categories, all 3 brands (LS2, Crank1, MadDog), and both brand-wide policy sentences (EMI, 7-day return) appear verbatim (post-`html.unescape()`) somewhere on the site. 0 gaps.
- `llms.txt` re-checked programmatically against current `data/stores.json` — every store name, every phone number, and all 56 locality names found verbatim. No drift.
- No new entity-coverage or FAQ gaps surfaced this run.

## 4. Content E-E-A-T / Brand Authority

- Reviews, ratings, gallery photos and `youtube_id`s untouched this run (bucket C, no changes).
- NAP consistency re-verified programmatically across all 61 store/locality pages: each store's phone number appears repeatedly on every page belonging to that store, 0 mismatches.
- Authoritativeness (press/backlinks): still the human's active research track via `audits/backlink-citation-plan.md`; no change to that file this run, not touched.

## 5. Platform Optimization

- Spot-checked FAQ coverage across all 5 stores (certification, try-on, location, stock-check — 4 FAQs each, identical pattern per store). No new buying-decision gap surfaced.

## 6. Local Reach Gaps

**No new locality pages added this run.** All four previously-logged candidates (Waghbil, Prabhadevi, Uttan, Ghatkopar West) were re-checked; none resolved. One new candidate (Shilphata, Thane) was investigated for the first time and rejected (clearly over the ~10km ceiling, not borderline enough to warrant a candidate-table entry).

- **Prabhadevi (nominal nearest: Santacruz store) — re-checked, conclusion unchanged.** Used Wikipedia's Prabhadevi area-centre coordinates (19.0166°N, 72.8295°E) against the Santacruz store's actual lat/lng (19.086455, 72.8358556): haversine straight-line = 7.8km, ×1.3 = **10.14km**, confirming the standing just-over-threshold conclusion. Rome2Rio again gives a lower, non-comparable station-to-station road figure (~8.5-8.9km) that doesn't use the store's own coordinates. Stays in the candidate table, unchanged.
- **Ghatkopar West (nominal nearest: Santacruz store) — re-checked, conclusion unchanged.** Fresh Rome2Rio figures this run: 9-10.3km depending on exact Ghatkopar/Ghatkopar West endpoint, still straddling the ~10km ceiling with the same cross-city (JVLR/SCLR, over the hills) routing ambiguity that makes the ×1.3 multiplier unreliable for this specific hop. Stays in the candidate table, unchanged.
- **Waghbil (Thane) — re-checked via WebSearch, conclusion unchanged.** Still no source gives coordinates for "Waghbil Naka" specifically — only the wider village/area (Wikipedia ~19.266°N/72.985°E vs a mirror's ~19.253°N/72.978°E, ~1.5km apart). Not confident enough to add. Stays in the candidate table, unchanged.
- **Uttan (Mira Road) — re-checked via WebSearch, conclusion unchanged.** No direct Uttan-to-Mira-Road-store figure exists; closest proxy (Uttan-to-Bhayandar, Rome2Rio) gives ~8-9.1km, but Uttan itself sits roughly 10.3km straight-line (~13.4km ×1.3) from the Mira Road store's own coordinates — clearly over threshold. Stays in the candidate table, unchanged.
- **Shilphata (nominal nearest: Thane store) — new candidate investigated, rejected.** Shilphata is a well-known Thane-Belapur Road / NH4 junction popular with riders, so it was worth checking. Wikipedia coordinates (19.147°N, 73.041°E) against the Thane store's lat/lng (19.201555, 72.9749461) give a haversine straight-line of 9.2km, ×1.3 = **11.98km** — clearly over the ~10km ceiling, and the route crosses the Mumbra/Diva creek corridor (routing ambiguity similar to the Ghatkopar case, but with a larger, non-borderline margin). Rejected outright; not added to the candidate table since it isn't close enough to be a genuine borderline case.
- No other genuinely new, confidently-resolvable candidate surfaced this run. Checked and ruled out as already-saturated or already-rejected in prior runs: remaining Malad-area infill (Thakur Village — overlaps existing Kandivali East coverage), Navi Mumbai infill beyond Turbhe (Koparkhairane/Ghansoli/Airoli — all previously rejected, confirmed still over threshold against Turbhe's own 9.3km baseline), and the long-standing previously-examined-and-rejected list (Kasarvadavali, Aarey Colony, Ulwe, Mira Road West, Dahisar West, Balkum, Kanakia, Nerul East/West, Panvel, Taloja, Poonam Sagar, Hiranandani Estate, Bandra Kurla Complex, Teen Hath Naka/Khopat/Kopri, Golden Nest, Naigaon, Oshiwara cluster, Dindoshi, Powai, Rai, Kalina, Seawoods, "Upper Thane", Chincholi Bunder, Louiswadi, Liberty Garden) was not re-litigated — their reasoning stands.

Coverage remains close to saturation for genuinely distinct, in-range localities across all 5 stores. Precise geocoding (Nominatim via WebFetch) remains blocked at the session network-policy level, so the four open candidates stay stuck on the same ambiguity until either that block lifts or a human supplies tighter coordinates/a real-route distance check.

### Verification performed before closing out this run

- Full technical sweep via a fresh programmatic script covering sitemap-vs-pages, robots.txt bot coverage, JSON-LD parsing, internal links, image alt text, title/description length and uniqueness, and canonical tags — **0 issues found** across all 62 pages.
- Schema sweep (reviewRating fabrication pattern, AggregateRating correctness against source `reviews.rating`, FAQPage/BreadcrumbList/SportingGoodsStore completeness) — **0 issues found**.
- Entity-coverage, NAP, and `llms.txt` drift checks, all re-verified programmatically against current `data/stores.json` — **0 issues found**.
- `python3 generate.py` re-run to confirm output matches current data; only the known `lastmod`-bump no-op diff appeared, reverted without committing.
- Git state checked and reconciled at run start (detached HEAD → `main`, matching `origin/main`).
- WebFetch re-tested against 3 hosts (live site, Nominatim, a neutral control) — confirmed still blocked session-wide for WebFetch specifically; WebSearch confirmed working and used for all research. 35th consecutive run with the WebFetch block.
- All four open candidates re-checked via WebSearch + manual haversine distance computation against actual store coordinates — reasoning reconfirmed on all four, none resolved, none re-logged with duplicate reasoning.
- One new candidate (Shilphata) investigated and rejected with a clear over-threshold margin.

---

## Candidate localities awaiting human geocoding

| Locality | Assigned store | Why uncertain | First logged |
|---|---|---|---|
| Uttan | Mira Road | Own coordinates (19.2810°N, 72.7790°E approx.) put it at ~10.3km straight-line / ~13.4km ×1.3 from the Mira Road store — over the ~10km threshold; no direct Uttan-to-store route figure exists to double-check against. Re-checked 2026-11-01, conclusion unchanged. Needs a tighter geocode (Nominatim, once reachable) or a human call before adding. | 2026-10-22 |
| Ghatkopar West | Santacruz (nominal nearest) | Road-estimate to Santacruz sits right at the ~10km ceiling (9-12km depending on which endpoint/source is used), but the ×1.3 multiplier is unreliable for this cross-city, opposite-side-of-Mumbai hop (no direct road — via JVLR/SCLR across the hills), and Ghatkopar isn't a natural "near me" catchment for a Santacruz-area search. Needs a human call or a real-route (not straight-line) distance check before adding. Re-checked 2026-11-01, unchanged. | 2026-10-24 |
| Waghbil | Thane | Already named as a landmark in the existing Patlipada blurb, so a real place, but its own coordinates vary ~1.5km between sources and no source gives coordinates for "Waghbil Naka" specifically (only the wider village). Road-distance estimates range 6-11km depending on endpoint. Needs a tighter geocode or a human call before adding. Re-checked 2026-11-01, unchanged. | 2026-10-27 |
| Prabhadevi | Santacruz (nominal nearest) | Coordinates are consistent across sources; the site's own straight-line×1.3 methodology (from the store's actual lat/lng) puts it at 10.1-10.2km, just over the ~10km ceiling, and farther from the store than the existing Mahim entry (7.0km) which already covers the same southward corridor. Needs a human call on whether to extend the ceiling for this specific locality, or leave as-is. Re-checked 2026-11-01 with a fresh haversine calc (10.14km), unchanged. | 2026-10-27 |

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| Full technical/schema/AEO/E-E-A-T sweep across all 62 pages | All | Verified via a fresh programmatic sweep — **0 issues found** | Titles/descriptions, JSON-LD, links, alt text, canonicals, robots.txt, entity coverage, NAP, llms.txt, AggregateRating correctness, FAQ/BreadcrumbList/SportingGoodsStore coverage, reviewRating-fabrication pattern all clean. No code or data changes made this run. |
| Waghbil (Thane) locality lead | Local Reach | Re-investigated via WebSearch; coordinate/distance spread persists, no Waghbil-Naka-specific coordinates found | Left in candidate table, no duplicate re-log |
| Prabhadevi (Santacruz) locality lead | Local Reach | Re-investigated with fresh haversine calc against store's own coordinates (10.14km) | Left in candidate table, no duplicate re-log |
| Uttan (Mira Road) locality lead | Local Reach | Re-investigated with fresh haversine calc against store's own coordinates (~13.4km) | Left in candidate table, no duplicate re-log |
| Ghatkopar West (Santacruz) locality lead | Local Reach | Re-checked via WebSearch with fresh sources; estimate spread (9-12km) still straddles the ~10km ceiling | Left in candidate table, unchanged |
| Shilphata (Thane) — new candidate | Local Reach | Investigated via WebSearch + haversine calc (11.98km) | Rejected outright, not added to candidate table — clearly over threshold, not borderline |
| WebFetch blocked for all hosts, 35th consecutive run | Technical GEO/SEO / Local Reach | Re-tested against 3 hosts including a neutral control; confirmed still blocked despite this run's instructions claiming otherwise | WebSearch confirmed working and used for all research this run |
| Detached HEAD at run start | Housekeeping | Reconciled: `git checkout -B main origin/main` (no divergence, no lost work) | No action needed beyond reconciliation |

**No commit this run** — no (A) fixes or (B) new localities; everything checked clean or stayed in the candidate queue unchanged.

## Carried over from previous runs

| Finding | Category | Status | First flagged |
|---|---|---|---|
| WebFetch cannot reach any external host from this session (session network-policy block) | Technical GEO/SEO / Local Reach | Open, now 35 consecutive runs — worked around via WebSearch each time; live-site checks and precise Nominatim geocoding remain unavailable until the relevant hosts are added to the session's network allowlist. This run's instructions claimed the block was lifted for WebFetch/WebSearch; WebSearch works, WebFetch does not (re-tested against 3 hosts including a neutral control). | 2026-09-25 |
| Uttan (Mira Road) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-22 |
| Ghatkopar West — candidate locality needing a real-route distance check or human call | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-24 |
| Waghbil (Thane) — candidate locality needing tighter geocode | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-27 |
| Prabhadevi (Santacruz) — candidate locality, borderline over the ~10km ceiling | Local Reach | Open, re-checked this run — see candidate table above | 2026-10-27 |

*(Three items — "no press/backlinks" (first flagged 2026-09-15), "sitemap `lastmod` stamped to run date, not content-driven" (first flagged 2026-09-18), and "MadDog brand not named verbatim in homepage's brand-description copy" (first flagged 2026-09-16, not a real entity-coverage gap since MadDog is already quotable on all 5 store pages) — remain open >30 days and continue to be trimmed from this table per the 30-day rule. All three remain unresolved/unchanged. None needs re-litigating daily — the backlink item is the human's own active track via `audits/backlink-citation-plan.md`, the sitemap item needs a one-time human decision on approach, and the MadDog item is a non-issue under this audit's own entity-coverage criterion.)*
