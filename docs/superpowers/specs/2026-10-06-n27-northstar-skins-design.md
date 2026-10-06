# n27 "Northstar Coaching" — a funnel presented as four design systems

Date: 2026-10-06
Status: design approved, ready for implementation plan
Affects: `index.html` (single file), `assets/funnel/northstar/` (new), `resume/` (regen)

---

## 1. Goal

Add build **n27** — one self-directed funnel, rendered in **four different design
systems** — and extend the funnel folder deck with a third tab unit, `kind:'skin'`,
so a build can be presented as "one page, four systems" instead of "one page, N bands".

## 2. Why this needs a renderer change

The folder deck (`deckUnits` / `foldersMedia`) has exactly two unit kinds today:

- `kind:'page'` — a genuinely separate captured page (only n26)
- `kind:'band'` — one slice of ONE page, so a band tab is only a position

Both are **ordered contiguous partitions** of a flat `p.sections[]`, computed by the
accumulation loop at `index.html:1796`. The tab strip therefore reads left-to-right as a
single visitor journey.

n27's real axis is **parallel, not sequential**: four skins of the same content, where a
reader never sees more than one. There is no existing vocabulary for that, so a third
unit kind is required. This is the `niche`/`build[]` dead-field trap's inverse — a *live*
shape the renderer cannot yet express.

## 3. The fit that makes this cheap

`p.sections[]` does not have to be a slice of one page. If it is the **flat concatenation
of every skin's bands, in skin order**, then:

- `deckUnits`' existing accumulation loop produces exactly the right ranges, unchanged
- `foldersMedia`'s existing `for(let i=pg.from;i<pg.to …)` pane loop stacks them, unchanged
- `deckCoversSections`' invariant `sum(count) === sections.length` still holds

Six additive renderer edits. No deletions, no CSS, and `SEC_LABELS` keeps serving the
other seven funnels untouched.

## 4. Source analysis (read 2026-10-06)

Source: `C:\Users\raini\Desktop\Opencode New Designs\Northstar Coaching\v{2,3,4,5}\`
Each holds `code.html` (Tailwind CDN, no build step) and a screenshot.
`v1` is excluded by explicit user decision. `v5` has **no** `DESIGN.md`.

| ver | DESIGN.md name | Fonts | Accent | Bands | id-bearing sections |
| --- | --- | --- | --- | --- | --- |
| v2 | Executive Advisory System | Inter 300–800 | emerald `#4edea3` | 4 | `overview` `framework` `criteria` `apply` |
| v3 | Executive Editorial Advisory | Cormorant Garamond + Plus Jakarta Sans | vermilion `#f2542d` | 5 | `hero` `about` `program` `selection` `apply` |
| v4 | Obsidian Architectural Executive | Playfair Display + Plus Jakarta Sans | gold `#e7c35a` | 4 | `overview` `framework` `criteria` `apply` |
| v5 | *(none)* | Inter + Playfair Display + Plus Jakarta Sans | vermilion | 4 | `overview` `framework` `criteria` `apply` |

All four: H1 "Stop being the bottleneck in your own business.", brand "NORTH STAR
EXECUTIVE", a 12-week executive coaching offer, a for/not-for selection matrix, and an
8-field strategy-call application (`fullName` `email` `phone` `businessName`
`biggestChallenge` `monthlyRevenue` `investmentBudget` `timeline`).

### 4.1 Content parity is 3 of 4, not 4 of 4

v2 / v4 / v5 share one structure and one copy. **v3 is a different funnel draft**: five
sections, different headlines ("Achieve Amazing Results Right Now"), reworded program
bullets, 616 words vs ~505.

Decision: **keep all four, with per-skin captions.** Band counts therefore differ
(4/5/4/4), which `skins[].count` handles natively — but it means captions can no longer
live in one global positional array, or v3's band 2 (`#about`) would silently inherit
v2's `#framework` caption. Captions move onto each skin object.

### 4.2 The existing screenshots are unusable

All four `screen.png` are narrow and clipped: 409x1600, 348x1600, 336x1600, 379x1600.
Four files at *identical* 1600px height means viewport-height captures, not full-page —
so the intake form (the conversion point) is cut off in all four. Only v2 and v5 have any
desktop shot and both are 1376x768 viewport, also clipped.

Decision: **re-capture all four at ~1440px wide, full page**, matching how n01
(1440x4607) and n26 (1440x10008) were captured, then slice into bands.

### 4.3 The intake form submits nothing

In all four, the submit handler is `e.preventDefault()` then hide-fields then reveal the
success card. No `action`, no `fetch`, no GHL, no calendar embed — zero GHL/calendar
references anywhere in any of the four files. The success states nonetheless read
"Application Received" / "Application Confirmed".

This is the n23 trap: `bullets[]` once claimed "UTM + promo-code capture on hidden
fields" on a page with zero `<input>`s. n27's copy must describe the form as **built
front-end only** and must never claim lead capture, submission, or CRM routing.

### 4.4 Minor defects in the source (not in scope for the portfolio work)

- v2 / v4 / v5 nav carries `href="#services"` but no `id="services"` exists in any of the
  three — a dead anchor. Worth fixing in source before re-capture.
- v3's `DESIGN.md` specifies Playfair Display while the code loads Cormorant Garamond.
  A doc/code drift. (This site's own aesthetic already uses Cormorant for accents.)

## 5. Decisions

| Decision | Choice | Rejected alternative |
| --- | --- | --- |
| Presentation | **A — skins are the deck** (4 tabs, each pane = that skin's bands) | B: journey primary + 4-up gallery below (demotes the differentiator); C: 4 tabs, one full capture each, no bands (thin against 6 captioned funnels) |
| Build count | **One build (n27)** | Four entries sharing a slug — the n05/n23 trap; reads as near-duplicate rows |
| Client | **Fictional, `practice:true`** | Real/anonymised |
| Tab labels | **Short**: Advisory, Editorial, Obsidian, Vermilion | Full `DESIGN.md` names (25–34 chars, wrap to 2–3 rows) |
| Lead skin | **v2 "Advisory"** | v4 (strongest thumb) / v3 (highest contrast) |
| Captions | **Per-skin `labels[]`** | One global `SEC_LABELS` entry (mislabels v3) |
| Captures | **Re-capture desktop full-page** | Ship the mobile clips (form cut off, design invisible) |
| Hero slot | **None** | 8th slot — see §9 |
| Bench position | **Last** (`leadProjectN` stays `'26'`) | Lead, which also displaces n26 from the default preview |

## 6. Data shape

Appended as **one line** after n26's entry, before the `];` at `index.html:1696`. It must
be one line: the array is literally one-line-per-entry, which is why the previous session
could not split its commit at a hunk boundary.

```js
{n:"27",cat:"funnel",tags:["funnel"],family:"funnel",practice:true,
 title:"Northstar Executive \u2014 Strategy Call Application Funnel",
 desc:"A high-ticket qualification funnel for a 12-week executive coaching programme \u2014 a sharp qualification matrix and an 8-field strategy-call application.",
 img:"assets/funnel/northstar/thumb.webp",
 full:"assets/funnel/northstar/advisory-full.webp",
 skins:[
  {label:"Advisory",  slug:"advisory",  count:4, full:"assets/funnel/northstar/advisory-full.webp",
   labels:["Hero \u00b7 the bottleneck","Program \u00b7 4 pillars","Criteria \u00b7 for / not for","Intake \u00b7 8-field application"]},
  {label:"Editorial", slug:"editorial", count:5, full:"assets/funnel/northstar/editorial-full.webp",
   labels:["Hero \u00b7 the bottleneck","About \u00b7 what it delivers","Program \u00b7 what you get in 12 weeks","Selection \u00b7 who it's for","Intake \u00b7 strategy call application"]},
  {label:"Obsidian",  slug:"obsidian",  count:4, full:"assets/funnel/northstar/obsidian-full.webp",
   labels:["Hero \u00b7 the bottleneck","Program \u00b7 4 pillars","Criteria \u00b7 for / not for","Intake \u00b7 8-field application"]},
  {label:"Vermilion", slug:"vermilion", count:4, full:"assets/funnel/northstar/vermilion-full.webp",
   labels:["Hero \u00b7 the bottleneck","Program \u00b7 4 pillars","Criteria \u00b7 for / not for","Intake \u00b7 8-field application"]}
 ],
 sections:[ /* advisory sec01..04, editorial sec01..05, obsidian sec01..04, vermilion sec01..04 */ ],
 stack:["Custom HTML/CSS/JS","Tailwind CSS","Responsive","Forms"],
 problem:"…", solution:"…", outcome:"…"}
```

`sections[]` is 17 entries in skin order: 4 + 5 + 4 + 4.

`p.full` points at the **Advisory** capture, which is what makes the preview pane correct
with zero edits (`fullSrc` reads `p.full`, and it wins over `stripItems[0].src`).

## 7. Renderer changes — seven additive edits

| # | Anchor | Change |
| --- | --- | --- |
| 1 | `deckUnits` `index.html:1795` | New `kind:'skin'` branch **before** the `p.pages` check — a build has skins *or* pages, never both. Unit carries `kind,label,count,from,to,full,labels`. |
| 2 | `foldersMedia` `:1813` | `const labels = pg.labels \|\| secLabelsFor(p)` — falls back safely for any unit without its own captions. |
| 3 | `foldersMedia` `:1814` | Index captions **locally**: `labels[i - pg.from]`, in both the `alt` and the `capHtml` call. |
| 4 | `capHtml` `:1802` | Counter becomes local: `Section {i-pg.from+1} / {pg.count}`. The existing global `Section {i+1} / {total}` would print `/17` on a 4-band pane. |
| 5 | `foldersMedia` `:1816` | `⤢ Full` resolves the **active unit's** own capture. See §7.1 — this needs two edits, not one. |
| 6 | `deckUnits` `:1796` | Every unit kind carries `full`, so §7.1's 5a is possible. |
| 7 | `foldersMedia` `:1819`, `metaRight` `:2258` | Third aria case `"Design systems"`; `metaRight` case `4 design systems · 17 sections`. |

### 7.1 Edit 5 is two edits, and it does change n26

`⤢ Full` currently hardcodes `openLightbox('${p.full||p.sections[pg.from]}')`. It
ignores which tab is active, so on n26 — whose `p.full` is the **landing** capture only —
clicking the **booking** tab's Full button opens the *landing* page. One funnel has
`pages[]`, so nobody has hit it.

`pg.full || p.full` alone would **not** fix n26, because `p.pages[]` entries carry no
`full` field at all (`{label,count,whole}`), so every n26 unit falls through to `p.full`
and the bug survives. The fix therefore needs:

- **5a (renderer)** — `deckUnits` carries `full` on **every** unit kind, not just skins:
  `skin -> sk.full`, `page -> pg.full || p.full`, `band -> p.full`. `foldersMedia` then
  opens `pg.full`.
- **5b (data, n26)** — add `full` to n26's *Booking page* and *Confirmation page*
  entries, each pointing at its own single section. Both are `count:1`, i.e. one whole
  page per section, so `p.sections[from]` is already the correct capture for them. The
  *Landing page* keeps the `p.full` fallback, since its six slices are not the page.

This is a **behaviour change to an existing build**, not a side effect of n27. It is
listed as an explicit control in §13 so it is verified rather than discovered.

### 7.2 Deliberately untouched

- `SEC_LABELS` `:1754` — still serves the other seven funnels
- `bandLabel` `:1792` — never reached; the skins branch returns first
- preview pane `:1919`/`:1922` — its `stripItems` labels are computed but never rendered
  (only `.length` and `stripItems[0].src` are read, and `fullSrc` wins)
- `leadProjectN` `:1708` — stays `'26'`
- all CSS — no new rules

## 8. Invariants to assert

1. `sum(count) === sections.length` for all 20 builds, via existing `deckCoversSections`
2. **NEW** — `skin.labels.length === skin.count` for all 4 skins. A short array falls
   back to a bare "Section 4" on that skin alone and is invisible in the other three.
   This is the n03-fallback trap scoped to one tab.
3. Only the active pane in the DOM; **0 duplicate ids** document-wide before and after a
   full drawer cycle.

## 9. Hero slot: none

Adding an 8th carousel slot means editing `heroProjectNs` `:2073`, the track `<img>`s,
the 7 side items `:1278-1308`, the 7 dots `:1266`, **and** the `%7` modulus at `:2097` —
five hardwired places that AGENTS.md documents as load-bearing together.

More importantly, 7 is a fixed **height budget**. Two stepped card-height tiers were
tried and both were wrong (non-monotonic slack); the shipped rule is
`grid-auto-rows:minmax(94px,max-content)` with `1fr` only at `min-height:960px`. At an
820px viewport an 8th card would vanish silently behind a hidden scrollbar — a bug that
already shipped and was missed by a first verification pass. n27 already gets a full bench
row and a 4-tab case study.

## 10. Assets — 23 files

`assets/funnel/northstar/`
- `<slug>-sec01.webp` … `<slug>-sec04.webp` for advisory / obsidian / vermilion
- `<slug>-sec01.webp` … `<slug>-sec05.webp` for editorial
- `<slug>-full.webp` × 4
- `thumb.webp`

18 slices + 4 fulls + 1 thumb. Calibrate WebP quality to the house band of **29–44
KB/megapixel**; never ship PNGs.

`prev-crop` allowlist: **no change.** Expect a tall `w/h` ratio, the same family as n26
(measured 0.192, deliberately excluded). Measure after capture before assuming.

## 11. Copy constraints

- `practice:true` → amber "Sample client" pill on the bench row, plus the outline
  "Sample client · no client results" badge in the **sticky** drawer head
- `outcome` in the **targets shape**, opening
  `This is a self-directed build for a sample client, so there are no client results to
  report. The targets it was designed around:` then `<br><br>`-separated bullets
- **The intake form is described as built front-end only.** No claim of lead capture,
  submission, email delivery, or CRM routing — see §4.3
- Assert the *absence* of the false claim forms, not just the presence of the new shape
- Deliberately carries **no** `bullets[]`, `build[]` or `niche`: all three are dead fields
  with zero render sites. Fold build detail into `solution` as `<br><br>` + `<b>`/`<i>`
- **No** `flows[]` and **no** `automation[]`: a funnel carrying either hits the n22 trap,
  where the automation branch silently takes over

## 12. Counts sweep — 19 → 20 builds, 7 → 8 funnels

| Surface | Line |
| --- | --- |
| `<meta name="description">` | `index.html:9` ("19 builds.") |
| `og:description` | `index.html:19` ("19 builds.") |
| nav tab `.cnt` | `index.html:1224` |
| toolbar chip | `index.html:1326` (`Funnel <span class="chip">7</span>`) |
| mobile nav | `index.html:1431` |
| resume PDF | `resume/` — regenerate; it hardcodes 19 builds / 7 funnels |

Automation counts do not move: still 12 builds / 38 automations. Hero slots stay 7.

## 13. Verification — full sweep

This edits renderer code all seven existing funnels depend on, so it earns the full
sweep, not a tiered check.

- Script blocks parse; 0 console errors; 0 failed `file://` requests
- Both invariants in §8 across **all 20** builds
- n27: 4 tabs with correct ranges; tablist `aria-label="Design systems"`; counters read
  `1/4`…`4/4` and `1/5`…`5/5`, **never** `/17`; `⤢ Full` resolves to the active skin's
  capture for all four
- 0 duplicate ids document-wide before and after a full drawer cycle
- `metaRight` reads `4 design systems · 17 sections`
- Both themes at 1440 and 390; tab strip `scrollWidth <= clientWidth` and every tab's
  `right <= strip.right`
- Counts read 20 / 8 / 12 / 38 in nav, mobile nav, chips, meta, og
- **Controls:** n26 pages deck unchanged in structure and its `⤢ Full` now *fixed*; n01 and
  n03 band tabs still positional `Section N`; n02 and n24 still emit no strip; preview
  pane unchanged
- Bench order renders `26 01 02 03 06 23 24 27`; automation order unchanged
  (`04 22 05 25 07 08 09 10 12 13 14 16`)

## 14. Risks

| Risk | Mitigation |
| --- | --- |
| `labels.length` mismatch on one skin | §8.2 invariant, asserted per skin |
| Per-skin `count` miscounts break `deckCoversSections` | Assert before slicing; derive counts from the band list actually produced |
| Global index leaking into captions | §7.3 local indexing; assert counters never read `/17` |
| n26's `⤢ Full` change is a behaviour change to an existing build, not just n27 | §7.1 spells out the required **5b data edit** to n26's `pages[]`; listed as an explicit control in §13 |
| Re-captured aspect ratio flips the `prev-crop` decision | Measure, do not assume (§10) |
| UTF-8/LF corruption from shell writes | Use the edit tool only; read `git diff` back; check `git diff --numstat` |
| Counts drift in an unlisted surface | `grep -n "19\b"` and `grep -n "Funnel <span"` as a sweep step |

## 15. Out of scope

- v1
- The dead `#services` nav anchor and the v3 DESIGN.md/code font drift — source-repo fixes
- GHL integration of the intake form (the build is deliberately static HTML, like every
  other practice funnel on the site)
- An 8th hero slot
- The file-map `Range` column in AGENTS.md (already labelled historical; a separate pass)
