# Daily SEO / AEO / GEO Audit — helmetstorenearme.in

**Date:** 2026-09-13
**Status:** 🟢 Healthy — 3 small mechanical fixes auto-applied and pushed; no new locality page this run (network to nominatim/site blocked); a handful of content-judgment items flagged for human review.

Site: 26 pages (1 homepage + 5 store pages + 20 locality pages) generated from `data/stores.json` via `generate.py`. Live network access to `helmetstorenearme.in` and `nominatim.openstreetmap.org` was blocked by the sandbox's egress policy this run (403 at the proxy/gateway) — audit performed against the local generated output and source data instead.

**Housekeeping note:** a previous run had produced a verified but unpushed commit ("Shorten meta descriptions to fit under 160 chars") that couldn't reach GitHub due to a connector write-permission issue at the time. Its content was re-verified in full today (JSON-LD, sitemap, links, description lengths) and pushed to `main` before this run's own audit began.

---

## 1. Technical GEO/SEO

| Check | Result |
|---|---|
| Sitemap vs actual pages | ✅ 26/26 match exactly, no drift |
| robots.txt bot coverage | ✅ `*`, GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended all `Allow: /` |
| JSON-LD parses | ✅ 0 errors across all 26 pages |
| Broken internal links | ✅ 0 found |
| Image alt text | ⚠️ 3 gallery images on the Thane store page used a generic "...at a Bikester Global store" alt instead of naming the store, unlike every other store's photos — **fixed** |
| Meta description length/uniqueness | ✅ All 26 unique, all under 160 chars (fix from prior run, re-verified after today's regenerate) |
| Canonical tags | ✅ Correct, self-referencing on every page |
| Social preview images | ⚠️ Every page's `og:image`/`twitter:image` pointed at the generic brand icon instead of the store's own real photo, weakening how link previews and AI-Overview-style summaries represent each store — **fixed**: store and locality pages now use that store's first gallery photo; homepage keeps the brand icon (no single store fits there) |

## 2. Schema & Structured Data

- `SportingGoodsStore` + `FAQPage` + `BreadcrumbList` present on every store and locality page.
- `aggregateRating`/`review` fields correctly mirror `data/stores.json` per store — checked all 5:
  - Malad: rating 4.7 / 2445 reviews + 4 quotes ✅
  - Thane: rating 4.5 / 34 reviews, no quotes ✅ (page correctly shows the "individual review text not pulled through yet" note)
  - Santacruz / Mira Road: review **count** only, no rating in source data → schema correctly omits `aggregateRating` (schema.org requires `ratingValue`; emitting one with just a count would be invalid) ✅
  - Navi Mumbai: 6 real named quotes, no rating/count in source data → schema correctly omits `aggregateRating` ✅
  - No mismatches between what's in `data/stores.json` and what's surfaced.
- ⚠️ `postalCode` was missing from every store's `PostalAddress` schema despite a valid 6-digit PIN being present in `address_lines` for all 5 stores — **fixed**: extracted and added.
- Gap (needs human): no `openingHours` anywhere in the schema or on-page, because `data/stores.json` has no hours field at all — there's no data to surface. Needs a human to supply each store's actual hours before this can be added.

## 3. AI Citability / AEO

- Every store and locality page states a real, specific address, phone number, named landmark, and a real distance/ride-time — spot-checked across all 26 pages, no generic filler found.
- FAQs (4 per store, identical question set, per-store-specific answers) cover certification (ISI/DOT), try-before-buy, exact location, and stock-check — genuinely useful buying-decision questions, not filler.
- `llms.txt` cross-checked field-by-field against current `data/stores.json` (every address, phone number, Maps link, and locality list) — 100% accurate, no drift.
- Gap (needs human/brand voice): the FAQ set doesn't include the two most "ask an AI assistant" shaped questions this business would benefit from — "what's the nearest Bikester Global to [X]?" and a brand-carried question ("does Bikester sell LS2/Crank1/MadDog helmets?"). Writing new FAQ copy is a content/brand-voice call, not mechanical — flagged, not auto-added.

## 4. Content E-E-A-T / Brand Authority

- Reviews are real, sourced (Google, Justdial, Magicpin, each with a `source_url`), and rendered only where the underlying data has them — no fabrication or embellishment found or introduced.
- Real store photos: 17 total across 5 stores (4/4/3/3/3), every file referenced in `data/stores.json` exists on disk.
- Real videos: a distinct YouTube store-tour `youtube_id` present and embedded for all 5 stores.
- NAP consistency: footer store list (name/address/phone for all 5 stores) is byte-for-byte identical across all 26 pages — single source of truth, no drift possible by construction.

## 5. Platform Optimization

- FAQs cover certification, try-before-buy, and stock-check well.
- Gap (needs human/brand voice): no FAQ-style, quotable answer names the specific brands carried (LS2/Crank1/MadDog) — that fact only lives in the homepage description and the store page's "Brands" info row, not as an answer an AI assistant could lift directly for "does this store sell LS2 helmets."
- Gap (needs human): no mention anywhere of price range, EMI, or warranty/exchange policy — can't add without a human confirming actual store policy.

## 6. Local Reach Gaps

- Network egress to `nominatim.openstreetmap.org` and `helmetstorenearme.in` was blocked this run (403 at the proxy), so **no new locality page was added** — per instructions, this is noted as blocked rather than guessed at.
- Candidate localities worth geocoding-checking on a future run when network access is available (mentioned only in passing in existing blurb text, not yet given their own page): Charkop (near Malad), Juhu (near Santacruz), Bhayandar West (near Mira Road), Ghodbunder Road corridor (near Thane).

---

## Action Plan

| Finding | Category | Action Taken | Notes |
|---|---|---|---|
| All 26 pages' meta descriptions exceeded 160 chars | Technical | Auto-fixed (prior run, pushed today) | Verified again after today's regenerate — still under 160 everywhere |
| Thane gallery alt text was generic ("...at a Bikester Global store") | Technical | Auto-fixed | Now names the store, matching every other store's pattern |
| `og:image`/`twitter:image` used the generic brand icon on every page | Technical / AI Citability | Auto-fixed | Store and locality pages now use that store's own real photo; homepage unchanged |
| `postalCode` missing from `PostalAddress` schema on all 5 stores | Schema | Auto-fixed | Extracted from existing `address_lines`, no new data invented |
| No `openingHours` in schema anywhere | Schema | Needs human | No hours data exists in `data/stores.json` at all — needs the actual hours from the user |
| FAQ set doesn't cover "nearest store to me" / brand-named questions | AEO / Platform Optimization | Needs human | New FAQ copy is a brand-voice/content decision, not mechanical |
| No price range / EMI / warranty policy content | Platform Optimization | Needs human | Requires the user to confirm actual store policy |
| No new locality page added this run | Local Reach | Blocked | Network access to nominatim/site blocked by sandbox policy (403); candidates noted above for a future run |

## Carried over from previous runs

_None — this is the first run of this living audit file._
