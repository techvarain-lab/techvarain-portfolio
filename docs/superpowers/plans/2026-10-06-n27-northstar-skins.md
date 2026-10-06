# n27 Northstar Skins Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add build n27 (one self-directed funnel rendered in four design systems) and extend the funnel folder deck with a third tab unit, `kind:'skin'`.

**Architecture:** `p.sections[]` becomes the flat concatenation of every skin's bands, in skin order. `deckUnits` gains a `kind:'skin'` branch whose accumulation produces exactly the right ranges, so the existing pane loop in `foldersMedia` stacks them unchanged. Captions move onto each skin object (`labels[]`) because the four skins do not share content. Seven additive renderer edits; no CSS; no deletions.

**Tech Stack:** Single self-contained `index.html` (vanilla JS, no framework, no build step). Verification via headless Microsoft Edge over CDP — **there is no test framework and no `package.json` in this repo.** Asset pipeline via Python 3.11 + Pillow 12.3.0 (WebP encode confirmed; no `cwebp`, no ImageMagick, no ffmpeg — and note `C:\Windows\system32\convert.exe` is the FAT→NTFS tool, **not** ImageMagick).

**Spec:** `docs/superpowers/specs/2026-10-06-n27-northstar-skins-design.md` — read it before starting; this plan argues from it and both travel together.

## Task Order

Data before rendering, so rendering is tested against the real entry rather than a throwaway probe: **1 assets → 2 `deckUnits` → 3 n27 data → 4 `foldersMedia` → 5 n26 fix → 6 copy → 7 counts → 8 resume → 9 sweep → 10 docs.**

## Amendments (2026-10-06, after asset handover)

1. **Task 1 is a hand-over, not a capture.** The user supplied four full-page desktop PNGs; CDP capture and the render-styled gate are dropped. Verify/slice/encode all remain.
2. **Full-page captures are downscaled to 1280 wide.** Bands stay at the captured 1920 (the reading surface); the four fulls are only ever a lightbox target and a heavily-downscaled preview, so 1280 keeps n27 near the house weight. ~2.6 MB rather than ~3.63 MB.
3. **v3 is a rebrand, not a re-skin.** It brands as *Julian Sterling* (personal brand) with its own copy and 5 sections, where v2/v4/v5 brand as *North Star Executive* with 4. The build is retitled brand-neutral and every skin's tab label carries its brand, so no tab implies all four are one firm.
4. **All four skins carry a `liveUrl`**, plus a project-level `p.liveUrl` pointing at the lead skin (Advisory) so the five existing `liveUrl` sites work untouched.
5. **Per-skin live link in the deck.** Task 4 adds a `↗ Live` button to the zoom bar, rendered only when the active unit has a `liveUrl`.


## Global Constraints

- **Never write `index.html` with a shell command.** The repo is UTF-8 with LF in git and `core.autocrlf=true`; `[System.IO.File]::WriteAllText` / `Out-File` round-trips silently mojibake every non-ASCII character. Use the edit tool only, then read `git diff` back and check `git diff --numstat` is plausible.
- **Verification is CDP, not a test runner.** Launch `C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe --headless --remote-debugging-port=<port>`, then drive `http://127.0.0.1:<port>/json/list`. There is no `pytest`, no `npm test`.
- **CDP traps that have all bitten this repo** (from AGENTS.md): `/json/list` returns every tab in the profile — always match by URL, never `list.find(t=>t.type==='page')`. `--dump-dom` and `--headless=old` are no-ops in this Edge build. A URL containing spaces must be percent-encoded or the page never loads. `visibilityState:hidden` freezes CSS transitions, so call `el.getAnimations().forEach(a=>a.finish())` before measuring geometry. `Page.captureScreenshot` with `fromSurface:false` returns blank frames — leave the default. Screenshots hang while any transition or animation is live; inject `*,*::before,*::after{transition:none !important;animation:none !important}` first. A hash-only `Page.navigate` is a same-document no-op — give each load a unique query string.
- **Assets are WebP only**, calibrated to **29–44 KB per megapixel**. Never ship PNGs to `assets/`. `**/source-*.png` is gitignored — that is where raw captures go.
- **Screenshot the result, don't measure it by eye.** Assert programmatically.
- Every funnel on this site is a self-directed build for a fictional client: `practice:true` is load-bearing and drives two marks (bench pill + sticky drawer-head note). Never write an achieved-result claim into `outcome`.
- **`outcome` uses the targets shape**, opening exactly: `This is a self-directed build for a sample client, so there are no client results to report. The targets it was designed around:`
- Do not add `flows[]`, `automation[]`, `bullets[]`, `build[]` or `niche` to n27 — the first two hit the n22 trap (the automation branch silently takes over); the last three are dead fields with zero render sites.

## Review Focus

Five failure modes the spec implies that a naive per-task test will miss.

1. **A clipped capture ships.** All four existing PNGs are exactly 1600px tall — viewport-height, not full-page — so the intake form is cut off in every one. A capture that looks right at a glance passes a file-exists test while missing the conversion point. → Task 1
2. **A caption array shorter than its skin's `count`.** Falls back to a bare "Section 4" on that one tab, invisible in the other three, and `deckCoversSections` still passes. → Task 2, Task 9
3. **A global index leaking into a per-skin caption.** Prints `Section 1 / 17` on a 4-band pane. Structurally valid, visibly wrong. → Task 4
4. **`⤢ Full` opening the wrong capture.** `pg.full || p.full` does **not** fix n26, because `p.pages[]` entries carry no `full` field and every unit falls through to `p.full`. → Task 2, Task 5
5. **Count drift on a surface nobody listed.** This repo has fallen into stale counts three times already, including a resume PDF and both meta descriptions. → Task 7, Task 8

---

### Task 1: Capture, slice and encode the four skins

**Files:**
- Read: `C:\Users\raini\Desktop\Opencode New Designs\Northstar Coaching\v{2,3,4,5}\code.html` (read-only; do not modify)
- Create: `assets/funnel/northstar/source-<slug>.png` (transient, gitignored)
- Create: `assets/funnel/northstar/<slug>-full.webp` × 4
- Create: `assets/funnel/northstar/<slug>-sec01.webp` … `-secNN.webp` — 4 for `advisory`/`obsidian`/`vermilion`, 5 for `editorial`
- Create: `assets/funnel/northstar/thumb.webp`

**Interfaces:**
- Consumes: four full-page desktop PNGs supplied by the user (verified 2026-10-06 — 1920 wide, 5907/7255/7071/6767 tall, each confirmed to carry its own canvas palette and the intake form at the bottom).
- Produces: the 23 asset files Task 3's `projects` entry references by path. Slugs are fixed by spec §5: `advisory` (v2), `editorial` (v3), `obsidian` (v4), `vermilion` (v5).

- [ ] **Step 1: Verify each capture is full-page and correctly labelled**

Assert width is desktop (>=1440) and height **strictly greater than 1600** for all four — that inequality is what the four original PNGs failed. Then confirm each capture carries its own variant's canvas palette and brand, so a mislabelled handover is caught:

```python
from PIL import Image
# v2 #08080A obsidian · v3 alternating #111317 / #f8f8f9 · v4 #121317 · v5 #fafafa
# v2/v4/v5 brand "North Star Executive"; v3 brands "Julian Sterling"
```

If two captures share an identical height and palette, they are the same variant — stop and ask.

- [ ] **Step 2: Confirm the intake form is present in every capture**

The bottom of each page is the 8-field strategy-call application. The original 1600px clips cut it off in all four. Assert the bottom 700px of each capture is non-uniform (a form, not a flat fill) — visually confirm the `Select timeline` dropdown, `APPLY FOR YOUR STRATEGY CALL` button and consent line.

- [ ] **Step 3: Slice each capture into bands on real section boundaries**

Band counts are fixed by the spec and come from the source's own structure — never infer them from image height: `advisory` 4, `editorial` 5, `obsidian` 4, `vermilion` 4.

Cut each capture at the boundaries of its own id-bearing sections. Since the captures are static, derive the offsets by locating each section's heading text block, or cut on proportional boundaries verified against the source DOM offsets measured with headless Edge. Assert the boundaries are strictly increasing and that the final band reaches the image foot — a dropped band silently shortens the case study.

- [ ] **Step 4: Encode bands to WebP at 1920, calibrating quality by bisection**

For every band, encode with Pillow and bisect `quality` until `29 <= bytes/1024/(w*h/1e6) <= 44`. Do not pick a fixed quality blind. Bands are the reading surface, so they keep the full captured width.

- [ ] **Step 5: Downscale the four fulls to 1280 wide, then encode**

The fulls are only ever a `⤢ Full` lightbox target and the preview pane's heavily-downscaled `prev-full`. Encode the 1280px-wide downscale at the same 29–44 KB/MPix band. This is what keeps n27 near the house weight instead of ~3.63 MB.

- [ ] **Step 6: Write `thumb.webp` from the Advisory full**

640px wide, per the house `thumb.webp` convention. Advisory is the lead skin (spec §5).

- [ ] **Step 7: Measure the ratios and confirm `prev-crop` stays unchanged**

Print `w/h` for all four `<slug>-full.webp`. Measured at capture time: 0.325 / 0.265 / 0.272 / 0.284 — the same family as n01 (0.313) and n26 (0.192), both of which render through `prev-full` inside the scrolling preview body. **No `prev-crop` allowlist change.** Re-measure after the 1280 downscale and confirm the ratio is unchanged (downscaling preserves `w/h`).

- [ ] **Step 8: Commit**

```bash
git add assets/funnel/northstar/
git status --short          # confirm no source-*.png is staged
git commit -m "feat(variant-E): n27 Northstar assets - 4 directions, bands 1920 + fulls 1280, sliced 4/5/4/4"
```

---

### Task 2: `deckUnits` gains `kind:'skin'`, and every unit carries `full`

**Files:**
- Modify: `index.html:1793-1801` (`deckUnits`)
- Test: ad hoc CDP assertion on `file://…/index.html`

**Interfaces:**
- Consumes: nothing.
- Produces: `deckUnits(p) -> Unit[]` where `Unit = { kind:'page'|'band'|'skin', label, count, from, to, full, labels? }`. `labels` is present only on `skin`; `full` on **all three** kinds. Task 4 consumes `labels`, Task 5 relies on `full`.

- [ ] **Step 1: Write the failing assertion**

Evaluate against a probe object, since n27 does not exist yet:

```js
const probe = { sections: new Array(17).fill('x'), skins:[
  {label:'Advisory',count:4,full:'a.webp',labels:['a','b','c','d']},
  {label:'Editorial',count:5,full:'e.webp',labels:['a','b','c','d','e']},
  {label:'Obsidian',count:4,full:'o.webp',labels:['a','b','c','d']},
  {label:'Vermilion',count:4,full:'v.webp',labels:['a','b','c','d']}]};
const u = deckUnits(probe);
JSON.stringify({ kinds:u.map(x=>x.kind), ranges:u.map(x=>[x.from,x.to]),
  counts:u.map(x=>x.count), fulls:u.map(x=>x.full), labels:u.map(x=>!!x.labels),
  sum:u.reduce((a,x)=>a+x.count,0), covers:deckCoversSections(probe) })
```

Expected **after**: `kinds` `["skin","skin","skin","skin"]`; ranges `[[0,4],[4,9],[9,13],[13,17]]`; counts `[4,5,4,4]`; four distinct `fulls`; `labels` all `true`; `sum` 17; `covers` true.
Expected **before**: `kinds` is 17 `band` units — the `skins` array is ignored entirely.

- [ ] **Step 2: Run it and confirm it fails**

- [ ] **Step 3: Implement the skins branch**

Insert as the **first** branch of `deckUnits`, before the `p.pages` check — a build has skins *or* pages, never both. Document the precedence in the comment block above the function:

```js
if(p.skins && p.skins.length>1 && n){
  let i=0; return p.skins.map(sk=>{ const from=i; i+=sk.count;
    return {kind:'skin', label:sk.label, count:sk.count, from, to:i, full:sk.full, labels:sk.labels}; });
}
```

Then add `full` to the two existing branches so every kind carries it (this is what unblocks Task 5): the `page` branch returns `full:(pg.full || p.full)`, the `band` branch returns `full:p.full`.

- [ ] **Step 4: Re-run, then confirm no regression on the existing seven**

Assertion passes. Then assert unit kinds are unchanged for every existing build: n26 `["page","page","page"]`, n01 and n03 five `band` units each, n02 and n24 `[]`, and `deckCoversSections` true for all 19.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat(variant-E): deckUnits gains kind:'skin'; every unit kind carries full"
```

---

### Task 3: The n27 data entry and the `metaRight` case

**Files:**
- Create: one line in `index.html`, appended after n26's entry and before the `];` at `:1696`
- Modify: `index.html:2256-2259` (`metaRight`)
- Consumes: asset paths from Task 1

**Interfaces:**
- Consumes: `kind:'skin'` units from Task 2.
- Produces: build n27 on the funnel bench. Task 4 renders it; Task 6 writes its copy.

- [ ] **Step 1: Append the entry as a single line**

It must be **one line**: the `projects` array is literally one-line-per-entry, which is why the previous session could not split its commit at a hunk boundary. Use spec §6's exact values — `n:"27"`, `cat:"funnel"`, `tags:["funnel"]`, `family:"funnel"`, `practice:true`, `img:"assets/funnel/northstar/thumb.webp"`, `full:"assets/funnel/northstar/advisory-full.webp"`, the four `skins` with exact `label`/`slug`/`count`/`full`/`labels`, `sections[]` as 17 paths in skin order, `stack:["Custom HTML/CSS/JS","Tailwind CSS","Responsive","Forms"]`.

`sections[]` order is `advisory-sec01..04`, `editorial-sec01..05`, `obsidian-sec01..04`, `vermilion-sec01..04` — it must match the skin order and counts exactly, or Task 2's ranges land on the wrong images.

Write placeholder `problem`/`solution`/`outcome` in this commit; Task 6 replaces them. **Do not** add `flows[]`, `automation[]`, `bullets[]`, `build[]` or `niche`.

- [ ] **Step 2: Add the `metaRight` skins case**

At `:2256-2259`, add a case ahead of the `p.pages` case: `p.skins && p.skins.length>1` → `` `${p.skins.length} design systems · ${p.sections.length} sections` ``. It must derive from the data so it cannot go stale. Leave the `flows`, `pages` and plain-sections branches intact.

- [ ] **Step 3: Assert counts and both invariants**

In-page: `projects.length === 20`; funnels 8; automation builds 12; total `flows` across automation builds 38. `deckCoversSections(p)` true for all 20. **`sk.labels.length === sk.count` for all four n27 skins** (spec §8.2) — and explicitly assert `projects.find(p=>p.n==='27').sections.length === 17`.

- [ ] **Step 4: Assert the bench row renders with its practice marks**

Switch to the funnel filter; assert exactly one row carries `data-id="27"`, the amber `.practice-badge` span is present, and its computed `font-family`/`font-size` match the other funnel rows — a presence assertion cannot see a legibility defect, which is how the badge once shipped at 1.37:1 contrast.

- [ ] **Step 5: Assert bench order and that the lead did not move**

Funnel bench reads `26 01 02 03 06 23 24 27`; automation order unchanged at `04 22 05 25 07 08 09 10 12 13 14 16`. `leadProjectN` stays `'26'`, so n26 remains the default preview.

- [ ] **Step 6: Assert the preview pane needs no edit**

Select n27; the preview pane's image `src` must be `advisory-full.webp` — the lead skin — proving `fullSrc` reading `p.full` is sufficient.

- [ ] **Step 7: Commit**

```bash
git add index.html
git commit -m "feat(variant-E): n27 Northstar Executive - one funnel, four design systems"
```

---

### Task 4: `foldersMedia` — per-unit captions, local indices, per-unit `⤢ Full`, aria

**Files:**
- Modify: `index.html:1802` (`capHtml`), `:1813` and `:1814` (label resolution and the pane loop), `:1816` (`⤢ Full`), `:1819` (tablist `aria-label`)

**Interfaces:**
- Consumes: `Unit.full` and `Unit.labels` from Task 2; n27's entry from Task 3.
- Produces: the rendered 4-tab deck.

- [ ] **Step 1: Write the failing assertion**

Open the n27 drawer, then evaluate against the live DOM:

```js
const tabs=[...document.querySelectorAll('.cs-tab')];
JSON.stringify({ n:tabs.length,
  labels:tabs.map(t=>t.textContent.replace(/[▸▾]/g,'').trim()),
  aria:document.querySelector('.cs-folders').getAttribute('aria-label'),
  counters:[...document.querySelectorAll('#csPane div div')]
    .map(d=>d.textContent.trim()).filter(t=>/^Section/.test(t)),
  fullHref:[...document.querySelectorAll('.zoom-bar button')].pop().getAttribute('onclick'),
  dupIds:(a=>a.length-new Set(a).size)([...document.querySelectorAll('[id]')].map(e=>e.id)) })
```

Expected **after**: 4 tabs reading `Advisory 4`, `Editorial 5`, `Obsidian 4`, `Vermilion 4`; aria `"Design systems"`; counters `Section 1 / 4 … Section 4 / 4` on the Advisory pane; `fullHref` containing `advisory-full.webp`; `dupIds` 0.
Expected **before**: 17 band tabs, counters reading `/ 17`, aria `"Page sections"`.

- [ ] **Step 2: Run it and confirm it fails**

- [ ] **Step 3: Resolve captions off the active unit, with a safe fallback**

Replace `const labels=secLabelsFor(p)` at `:1813` with:

```js
const labels = (pg && pg.labels) ? pg.labels : secLabelsFor(p);
```

The fallback is what keeps the other seven funnels untouched.

- [ ] **Step 4: Index captions locally**

In the pane loop at `:1814`, both the `alt` attribute and the `capHtml` call currently index `labels[i]` where `i` is a **global** index into `p.sections`. Change both to `labels[i - pg.from]`, keeping the existing `|| 'section '+(i+1)` fallback.

- [ ] **Step 5: Make the counter local**

`capHtml(txt, i, total)` at `:1802` is called with the global `i` and global `total` (`p.sections.length` = 17 for n27). Change the call site to pass local values so the strip reads `Section 1 / 4`. **Band and page units must produce byte-identical output to before** — assert that on n01 and n26.

- [ ] **Step 6: Resolve `⤢ Full` from the active unit**

At `:1816`, change `openLightbox('${p.full||p.sections[pg.from]}')` to `openLightbox('${pg.full||p.full||p.sections[pg.from]}')`.

- [ ] **Step 7: Add the third tablist aria-label**

At `:1819` the label is a two-way ternary on `u[0].kind` (`'Funnel pages'` / `'Page sections'`). Extend to three cases, adding `'Design systems'` for `skin`.

- [ ] **Step 8: Re-run, then assert the DOM-id invariant after a full tab cycle**

Click all four tabs, then re-assert `dupIds` is 0 and that exactly one `#csPane` and one `#drawerZoomImg` exist document-wide. `foldersMedia` resolves those **by id**, so a second mounted pane silently breaks zoom — this is why only the active pane may exist.

- [ ] **Step 9: Assert every skin's `⤢ Full` resolves to its own capture**

Tab through all four and read `fullHref` each time: expect `advisory-full.webp`, `editorial-full.webp`, `obsidian-full.webp`, `vermilion-full.webp` in turn.

- [ ] **Step 10: Commit**

```bash
git add index.html
git commit -m "feat(variant-E): per-unit captions, local counters, per-unit full-page lightbox"
```

---

### Task 5: n26 data fix — `full` on its Booking and Confirmation pages

**Files:**
- Modify: `index.html:1695` (n26's entry, the `pages:[…]` array)

**Interfaces:**
- Consumes: `Unit.full` from Task 2.
- Produces: a correctness fix to an existing build. Task 9 verifies it.

- [ ] **Step 1: Write the failing assertion**

Open n26's drawer, click the **Booking page** tab, read the `⤢ Full` button:

```js
document.querySelector('.cs-tab.on').textContent.trim() + ' :: ' +
  [...document.querySelectorAll('.zoom-bar button')].pop().getAttribute('onclick')
```

Expected **after**: the argument is `bright-minds/sec07.webp`.
Expected **before**: `bright-minds/full.webp` — the landing capture. That is the bug.

- [ ] **Step 2: Run it and confirm it fails**

- [ ] **Step 3: Add `full` to the two single-section pages**

Both are `count:1`, so their one section *is* the whole page. Add `full` to the **Booking page** and **Confirmation page** entries only. Leave **Landing page** alone — its six slices are not the page, so it keeps the `p.full` fallback.

- [ ] **Step 4: Re-run, and confirm the Landing tab is unaffected**

Landing's `⤢ Full` must still resolve to `bright-minds/full.webp`.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "fix(variant-E): n26 booking and confirmation tabs open their own full-page capture"
```

---

### Task 6: n27 copy, with honesty assertions

**Files:**
- Modify: `index.html` — `problem`, `solution`, `outcome` on n27's entry

**Interfaces:**
- Consumes: n27's entry from Task 3.
- Produces: copy satisfying the practice-disclosure convention. Task 9 re-checks it.

- [ ] **Step 1: Write the failing assertion — the banned-phrase list**

This is the n23 trap: `bullets[]` once claimed "UTM + promo-code capture on hidden fields" on a page with zero `<input>`s. Assert on **rendered drawer text**, case-insensitively — `innerText` returns UPPERCASE for `.btn-p` and the drawer kicker, which carry `text-transform:uppercase`:

```js
const t = document.querySelector('.drawer-body').innerText.toLowerCase();
const banned = ['captured lead','captures leads','lead capture','submits to','sent to your',
  'gohighlevel','ghl','crm','webhook','calendar booking','booked call','enrolled students','revenue increased'];
JSON.stringify({ hits: banned.filter(b => t.includes(b)) })
```

Expected `hits` `[]`. The source has **zero** GHL/calendar references and its form is `preventDefault()` plus a success card reading "Application Received", so every one of those phrases would be false.

- [ ] **Step 2: Run it and confirm it fails**

- [ ] **Step 3: Write `problem`, `solution`, `outcome`**

- `problem` — the operator-bottleneck situation, and why a 12-week high-ticket programme needs a qualifier rather than a generic lead form. Name the sample client plainly.
- `solution` — what was built: hero with a single promise, the programme pillars, the for-you / not-for-you criteria matrix as the qualifying device, and the 8-field strategy-call application (name, business, challenge, revenue, budget, timeline). Fold build detail in as `<br><br>` + `<b>`/`<i>` blocks, the existing n03/n06 convention.
- `outcome` — the **targets shape**, opening exactly the Global Constraints sentence, then `<br><br>`-separated bullets describing what it was *designed* to achieve. Describe the form as **built front-end only**; never claim capture, delivery or routing.

- [ ] **Step 4: Re-run and confirm `hits` is `[]`**

Also assert the targets prefix **is** present and that `bullets`, `build` and `niche` keys are absent from n27's object.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "docs(variant-E): n27 case-study copy - practice disclosure, no capture claims"
```

---

### Task 7: Counts sweep — 19 → 20 builds, 7 → 8 funnels

**Files:**
- Modify: `index.html:9`, `:19`, `:1224`, `:1326`, `:1431`

**Interfaces:**
- Consumes: n27 from Task 3.
- Produces: every count surface consistent. Task 8 is the resume, a separate toolchain.

- [ ] **Step 1: Sweep for stale counts before editing**

```bash
rg -n '19 builds|>19<|cnt">19|Funnel <span class="chip">7|PORTFOLIO BUILDS' index.html
```

Expected: exactly the five known lines. **A sixth hit is an unlisted surface** — stop and add it to this task rather than leaving it stale.

- [ ] **Step 2: Edit the five surfaces with the edit tool**

`:9` and `:19` `"19 builds."` → `"20 builds."` · `:1224` `.cnt` `19` → `20` · `:1326` `Funnel <span class="chip">7</span>` → `8` · `:1431` `PORTFOLIO BUILDS — 19` → `20`. Do **not** touch the Automation chip or the hero's 7 slots.

- [ ] **Step 3: Assert in the DOM**

Nav `.cnt` reads 20, mobile nav 20, funnel chip 8, automation chip still 12, `heroLiveDots` still exactly 7 buttons, `heroProjectNs` unchanged at `["25","01","08","22","04","05","06"]`.

- [ ] **Step 4: Confirm no encoding damage**

```bash
git diff --numstat index.html
```

Expected: a small plausible count. A count in the dozens or hundreds means a shell write mangled the file — restore and redo with the edit tool.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "chore(variant-E): counts 20 builds / 8 funnels across nav, chips and meta"
```

---

### Task 8: Regenerate the resume PDF

**Files:**
- Modify: `resume/index.html` (its hardcoded counts)
- Modify: `resume/rainier-dimasacat-jr-gohighlevel-specialist.pdf` (regenerated, tracked)

**Interfaces:**
- Consumes: Task 7's counts.
- Produces: a PDF that agrees with the site. The content box to measure against is **7.5in wide, not 8.5in** (0.5in margins); the page overflows to 2 if content grows.

- [ ] **Step 1: Assert the resume's current numbers**

```bash
rg -n '19|funnels' resume/index.html
```

Expected: hardcoded counts that must become 20 builds / 8 funnels. Automation figures (12 systems, 38 workflows) and 4 roles / 9 GHL skills do not change.

- [ ] **Step 2: Edit `resume/index.html` with the edit tool**

Change only the counts. Read `git diff` back and check `git diff --numstat`.

- [ ] **Step 3: Re-render the PDF with headless Edge**

No pandoc, wkhtmltopdf or libreoffice on this machine:

```
& "C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" --headless --print-to-pdf-no-header --print-to-pdf="resume\rainier-dimasacat-jr-gohighlevel-specialist.pdf" "file:///<percent-encoded path>/resume/index.html"
```

- [ ] **Step 4: Assert the PDF agrees and still fits one page**

Extract the text; assert it contains 20 builds and 8 funnels. Assert page count is still **1** — if it overflows to 2, tighten the resume copy rather than shipping a two-page resume.

- [ ] **Step 5: Commit**

```bash
git add resume/
git commit -m "chore(variant-E): regenerate resume PDF for 20 builds / 8 funnels"
```

---

### Task 9: Full verification sweep

**Files:**
- Test only — no source changes unless a check fails, in which case fix and amend the owning task's commit.

**Interfaces:**
- Consumes: everything from Tasks 1-8.
- Produces: the go/no-go evidence. Per AGENTS.md this earns a **full** sweep, not a tiered check, because Tasks 2-5 edited renderer code all seven existing funnels depend on.

- [ ] **Step 1: Parse and asset integrity**

All 4 script blocks parse; every asset reference resolves on disk (expect the two `yt-*.jpg` posters as false positives — built by template); 0 console errors, 0 uncaught exceptions, 0 failed `file://` requests.

- [ ] **Step 2: Both invariants across all 20 builds**

`deckCoversSections(p)` true for all 20; `sk.labels.length === sk.count` for all four n27 skins.

- [ ] **Step 3: n27 in the drawer**

4 tabs with exact labels and counts `Advisory 4 / Editorial 5 / Obsidian 4 / Vermilion 4`; `aria-label="Design systems"`; counters `1/4…4/4` and `1/5…5/5`, **never** `/17`; `⤢ Full` resolves to the active skin's own capture for all four; `metaRight` reads `4 design systems · 17 sections`; sticky head reads `FUNNEL - 27 SAMPLE CLIENT - NO CLIENT RESULTS`.

- [ ] **Step 4: Duplicate-id and single-pane hygiene**

0 duplicate ids document-wide **before and after** clicking all four tabs and closing/reopening the drawer. Exactly one `#csPane` and one `#drawerZoomImg` at any moment.

- [ ] **Step 5: Controls — the existing seven funnels**

- n26: 3 page tabs; `⤢ Full` on Booking → `sec07.webp`, Confirmation → `sec08.webp`, Landing → `full.webp`
- n01 and n03: band tabs still positional `Section 1…N`, counters unchanged
- n02 and n24: still no tab strip, still stacking `full`
- preview pane unchanged for every build; n27 shows `advisory-full.webp`

- [ ] **Step 6: Both themes, two viewports**

Light and dark at 1440 and 390. At 390 assert the folder tab strip satisfies `scrollWidth <= clientWidth` **and** every tab's `right <= strip.right` — the strip wraps rather than scrolls, so a wrap regression clips a tab before it can scroll. Assert 0 document overflow, and `main.clientWidth` fills the viewport.

- [ ] **Step 7: Counts and copy**

20 / 8 / 12 / 38 everywhere; 7 hero dots; Task 6's banned-phrase list returns `[]` on the rendered drawer.

- [ ] **Step 8: Screenshot both themes**

Inject the killswitch before capturing. Visually confirm the 4-tab strip, the manila notch filling correctly (`getComputedStyle(el,'::after').backgroundColor === getComputedStyle(el).backgroundColor`), and the band captions.

- [ ] **Step 9: Record results**

Do not commit unless a check failed and you fixed it. Report pass/fail per step with the measured numbers.

---

### Task 10: Update AGENTS.md and CHANGELOG.md

**Files:**
- Modify: `AGENTS.md` — the `projects` row, the folder-deck convention, the dead-fields and counts notes, the counts-to-keep-current list
- Modify: `CHANGELOG.md` — append today's entry

**Interfaces:**
- Consumes: measured results from Task 9.
- Produces: documentation matching the code.

- [ ] **Step 1: Update AGENTS.md's file map and conventions**

Add n27 to the `projects` row (20 entries, 8 funnels; `practice:true` now 9 flagged). Document the `kind:'skin'` unit: the flat-`sections` trick, per-skin `labels[]`, the local-index rule, the new `labels.length === count` invariant, and per-unit `⤢ Full` resolution including the n26 fix. Record the n22 trap warning — a funnel carrying `flows[]`/`automation[]` has its deck silently taken over, and n27 deliberately carries neither.

- [ ] **Step 2: Re-derive the line anchors**

AGENTS.md's file-map anchors are labelled historical and drift ~200 lines per session. Re-derive the ones Tasks 2-4 moved (`deckUnits`, `foldersMedia`, `capHtml`, `metaRight`, `projects`, the array close, `SEC_LABELS`) and update the staleness banner with today's date and the new drift figure.

- [ ] **Step 3: Update counts and append the CHANGELOG entry**

CHANGELOG entry covers: n27 as one build with four design systems, the `kind:'skin'` unit, the `⤢ Full` per-unit fix and its n26 consequence, counts 20/8/12/38, the resume regeneration, and Task 9's verification numbers. Record the capture pipeline (Edge CDP → `source-*.png` → Pillow → WebP at 29-44 KB/MPix) so the next session can repeat it.

- [ ] **Step 4: Final encoding check and commit**

```bash
git diff --numstat
git status --short
```

Expected: only `AGENTS.md` and `CHANGELOG.md`, small counts, and **no** `assets/funnel/northstar/source-*.png` staged.

```bash
git add AGENTS.md CHANGELOG.md
git commit -m "docs(variant-E): n27 design-system skins, kind:'skin' deck unit, 20 builds / 8 funnels"
```
