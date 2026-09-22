# CHANGELOG

Compact, append-only log of what changed and why. Newest entry at the bottom. Each entry = one working session (use `/wrapup`). Bullets only — no prose dumps. Read the tail of this file + `git log` to get current.

## 2026-09-17 — Session ops setup
- Added token-efficiency scaffold: `AGENTS.md` (project brain + file map), this CHANGELOG, `/catchup` + `/wrapup` slash commands, `opencode.json` (autoload AGENTS.md + tool_output cap).
- No changes to `index.html` or assets.

## Seeded from git history (latest → oldest)
- fix: restore GHL skill drawer interactivity + hero details (`openDrawerById`, `heroLive` binding).
- audit pass — a11y (aria labels, focus, Escape), self-hosted images, repo cleanup.
- GHL skills section: nested sub-skills under Contacts + Contacts Import, proof-popup hover zoom + lightbox.
- GHL skills section added (data-driven `glSkills` tiles → existing drawer).
- ClearView Pressure Washing funnel added (n21) + live view (press on live links instead of copy-paste checkout URLs).
- FitCoach automation gallery (Make 5 steps) + de-pilled drawer (editorial mono A).
- Haven Animal Clinic refresh + Mountain Hiking (n20) + Live view links for Legal/Haven/Rubio.
- Rubber-band fixes: rail name block spacing, hero live look, theme metadata 18 → 21 builds.

## Deploy
- Push `main` → GitHub Pages updates automatically. `.nojekyll` present. No build/verify step.

## 2026-09-17 — Mobile/touch UX pass
- iOS/safe-area: `viewport-fit=cover` + `theme-color` metas, safe-area padding on sticky topbar, 16px form inputs (kills iOS zoom-on-focus), overflow fixes for app/main/work/services panels.
- Mobile rail: dropped `inert`, replaced inline `onclick` nav with `data-panel`/`data-go` attributes + one delegated close handler.
- `inert` unified to `setAttribute`/`removeAttribute` for drawer + lightbox; row focus-preview gated behind `!isCoarse`.
- Counts untouched (21 builds, hero 6).

## 2026-09-17 — GHL learning tiles (n02–n07)
- Added 6 placeholder GHL tiles: Pipelines, Workflows, Funnels & Websites, Forms/Calendars, Email & SMS, Reporting & Dashboards — flagged `learning:true`.
- Learning tiles: dimmed + dashed border + amber "Learning" badge; drawer shows "Still learning" note; sub-skills render "Proof coming soon."
- Graduating a tile = drop `learning:true` + add `assets/ghl/proof-*.png` shots (no structural change).
- Committed mobile/touch pass + ops scaffold (AGENTS.md, CHANGELOG.md, opencode.json, .opencode/commands).

## 2026-09-17 — GHL learning tiles shipped
- Finalized the 6 `learning:true` placeholder tiles (n02–n07) — verified both inline script blocks parse clean (node `new Function` check).
- Committed + pushed to `main`: rebased over remote CNAME-only commits; 2 commits landed — `571a29b` (ops scaffold) + `bfd0dc9` (tiles + mobile UX pass). Working tree clean.
- Counts confirmed current: 21 builds, hero 6, GHL tiles 7 (1 proof + 6 learning).
- AGENTS.md file map + counts refreshed for the new line ranges (~1,285 lines) and `glSkills` shape. Nothing pending — graduate tiles by adding proof as modules finish.

## 2026-09-17 — GHL proof-backed tiles grow to 3
- Graduated n02 Pipelines & Opportunities (custom copy + 2 `proof-pipeline-*.png` shots). Proof label generalized from "record management" to "Proof — N shots" so all tiles read correctly.
- Split n05 into two tiles: Forms & Surveys + new Calendars & Booking (8 tiles total, renumbered through n08).
- Reordered Calendars to n03, graduated it with booking copy + 2 `proof-calendar-*.png` shots.
- Pushed `main`: `304ba94` (pipelines) + `bcee448` (calendars reorder/graduate). Working tree clean.
- GHL tiles now 01–03 proof-backed, 04–08 learning (Workflows, Funnels, Forms, Email/SMS, Reporting). AGENTS.md counts/file-map already synced. Pending: none — graduate 04–08 as modules complete.

## 2026-09-18 — Mobile nav polish
- Hid topbar "Start a project →" CTA on ≤860px — drawer's amber CTA (`#mobileRail`) + hero button already cover the conversion path.
- Added scroll affordance for the tab strip: pinned edge-fade masks (`.ov` / `.ov-left` / `.at-end`) driven by `updTabs()` overflow tracker; clicked tab now scrolls into view.
- No count changes (21 builds, hero 6, GHL 8).
- Committed + pushed `b106e83`; AGENTS.md file map refreshed for ~1,307 lines. Pending: none.

## 2026-09-18 — Graduate GHL tile 07: Email & SMS → Marketing
- Graduated n07 from a `learning:true` placeholder to a proof-backed tile renamed **"Marketing"** (icon ✉ → ✦) — confident first-person copy ("I can execute end-to-end marketing tasks in GoHighLevel…").
- Restructured sub-skills from 2 → 6: Email Campaigns & Analytics, Social Planner, Snippets, Countdown Timers, Trigger Links, Brand Boards — each with desc + chips.
- Copy-only graduate: `proof:[]` for now, so drawer sub-skills show "Proof coming soon." until screenshots land in `assets/ghl/`.
- Dropping `learning:true` un-dims the tile + footer flips to "Skills · 6" (no CSS edits; verified 8 tiles total parse clean via node).
- Counts unchanged: GHL now 01–03 + 07 proof/copy-backed, 04–06 + 08 learning. AGENTS.md file-map + counts synced. Pending: add tile-07 proof shots.

## 2026-09-18 — GHL panel locked to 100vh (always-fit tiles)
- `.panel-ghl` `overflow:auto` → `overflow:hidden`: panel now always fills the viewport like Work/Services, header pinned (`flex-shrink:0` already).
- `.ghl-tiles` now `flex:1;min-height:0` + `grid-auto-rows:minmax(0,1fr)` → all 8 tiles stretch to share the row height and always fit, no scrollbars (2 rows on 4-col, 3 rows on 3-col).
- `.ghl-tile` got `overflow:hidden` so card content clips cleanly on very short viewports instead of spilling past its stretched row.
- Mobile (≤860px): `.panel-ghl` / `.ghl-tiles` override to `flex:none` + natural auto rows so mobile keeps normal page flow.
- No count changes. Also in this session: graduated tile 07 → "Marketing" (copy + proof shots wired: email ×2, snippet ×1, timer ×1, trigger ×5, brand ×1) — Social Planner still "Proof coming soon."

## 2026-09-18 — GHL tile breathing room + always-fit clamps
- `.panel-ghl` padding 12→14px; `.ghl-tile` internal gap 7→9px; sub-tag gap/margin up (2px→6px, 5→6px), chip padding 3px→2px vertical; `.ghl-open` pad-top 6→8px. Tiles breathe more.
- Clamped so always-fit rows never spill: `h3` 13px + 2-line clamp, `p` 11.5px + 2-line clamp, `.ghl-sub-tags` capped at `max-height:38px` (2 rows; full list lives in the drawer). Worst case (~768px viewport, 3 rows) now fits cleanly.

## 2026-09-18 — Tile icon hover experiments reverted
- Explored corner-pop + behind-card emblem peeks on `.spec-icon`/`.ghl-tile::before`; user scrapped them. Clean revert: no `::before`, no `data-glyph`/`data-kicker` attrs, `.spec-icon` back to its static 20px box, reduced-motion untouched. Icons stay as the original glyph set.

## 2026-09-18 — GHL hover spotlight
- Hovered/focused tile is the sole focus: siblings dim + desaturate (`opacity:.42`, `saturate(.55)`) via `:has()`; the active tile lifts more (`translateY(-2px) scale(1.03)`), gains a deeper shadow + amber-wash gradient (`--amber-wash`, auto light/dark). Keyboard focus-visible dims siblings too. `.ghl-tile` transition bumped to `.2s`. Rest state unchanged.

## 2026-09-18 — GHL sub-skill cards fan (folder micro-interaction)
- Each tile gains a `.ghl-fan` layer (aria-hidden): up to 4 sub-skill chips + `…` overflow, hidden at rest. On `:hover`/`:focus-visible` (desktop only, `@media(hover:hover)`), cards fan out of the tile's top edge — symmetric horizontal spread (count-aware via `--n`/`--i` CSS vars), staggered `45ms` per card, springy ease, amber border/paper fills with drop shadows.
- `.ghl-tile:hover` and `:focus-visible` gain `z-index:6` so fanned cards render above adjacent tiles.
- `.panel-ghl` top padding `14px` → `24px` so the first row's fan clears the 100vh-clipped edge; middle rows overlay the tile above (looks like cards in front of the folder).
- Reduced-motion disables fan-card transitions. Marketing fans 4 cards + muted `…` chip; all other tiles fan 2–3 cards. Click still opens the drawer. No count changes.

## 2026-09-18 — Fan rework: arc pop, each sub-skill individually visible
- Dropped the top-edge card "stack" (folded-deck origin). Now every sub-skill card has its own landing spot on a top arc (`renderGhl` computes per-chip inline `--dx/--dy/--rot`: `a=π·i/(n−1)`, `dx=sin(a)·128`, `dy=-(70+cos(a)·64)`, `rot=±4°`). 2 cards → top corners, 3 → left/top/right, 6 → full arc.
- Individual pop, never stacked: rest state sits at 45% along each card's own ray (`translate(dx·.45, dy·.45) scale(.72)`, `transform-origin:center bottom`) so cards start at unique positions and rise to their slots, staggered 45ms/index, `cubic-bezier(.16,1,.3,1)`. Spotlight dim stays.
- Cap raised 4 → 6; the `…` more-chip removed (no tile has >6 subs). `.ghl-fan` anchored `top:50%;left:50%`; `.panel-ghl` top padding 24 → 44px for top-row arc headroom. Reduced-motion unchanged (cards snap to their slots).
- Fix: the sweep was `a∈[0,π]` — `sin(a)` never negative, so cards piled center-right (n=2 stacked at dx 0, no left side). Centered to symmetric `a∈[−π/2,+π/2]`: `dx=sin·128` sweeps −128→+128, `dy=−(88+cos·12)` hugs the tile top, `rot=±5°`. n=2 → corner pair, n=3 → left/top/right, n=6 → even mirrored sweep.
- Fix: cards were top-left anchored on their slots — a card at `dx=+128` extends right past the tile while its mirror at `−128` fills toward center, so the fan's centroid drifted right. Added `translateX(-50%)` to both rest + hover transforms: each card now centers exactly on `(--dx,--dy)`. Left/right fans mirror about the tile center.

## 2026-09-18 — Per-tile fan customization
- Added optional `fan` field to `glSkills` entries for per-tile pop layouts; absent = symmetric top-arc default.
- Tile 01 "Contacts & Lead Records" set `fan:"right"` — its 3 sub-skills now pop in a vertical stack along the right edge (`dx=132`, `dy=(i−(n−1)/2)·34`, alternating ±6° tilt) instead of the top arc.
- Added `fan:"left"` mirror layout. Tiles 05 "Funnels & Websites" → `left` and 06 "Forms & Surveys" → `right`. Fan layouts now: 01 right, 05 left, 06 right, rest top-arc.

## 2026-09-18 — GHL panel interactions + Marketing graduation
- Graduated tile 07 "Marketing" (6 sub-skills, copy-backed; proof wired: email ×2, snippet ×1, timer ×1, trigger ×5, brand ×1). Social Planner still "Proof coming soon."
- GHL panel locked to 100vh always-fit + breathing-room padding/gaps + content clamps (h3/p 2-line, sub-tags capped) so tiles never spill on short viewports.
- Sub-skill pop-up (`.ghl-fan`): cards arc above each tile, each with its own landing slot (`--dx/--dy/--rot` computed in `renderGhl`, ray-pop rest origin), staggered 45ms; hover spotlight dims siblings (`:has()`) + lifts the focused tile with amber-wash.
- Per-tile `fan` field: 01 right, 05 left, 06 right edge stacks; rest symmetric top-arc. Cards centered on slots via `translateX(-50%)` (fixes right-drift). Icon hover experiments reverted — original glyphs kept. Mobile nav CTA/scroll-hint work had landed earlier in `b106e83`.
- Pushed `552c210` → GitHub Pages. Counts unchanged (21 builds, hero 6, GHL 8). AGENTS.md GHL file-map ranges re-pointed (1190–1307, 1309–1329).

## 2026-09-19 — BG tweak button (background tester)
- Added topbar "▦ BG" control (`#bgBtn` + `#bgPop`) to switch the main-column background treatment live, persisted as `rd-bg` in localStorage (mirrors `rd-theme`). Applies `data-bg` on `.main`; default `grid`.
- Static modes: **grid** (original), **dots** (lithographic halftone), **grain** (inline-SVG feTurbulence noise), **blueprint** (column rules + every-4th baseline + amber corner registration marks via `.main::after`), **bare** (no texture), **watermark** (giant faint serif "21" bottom-right, Instrument Serif italic, over the grid). Each option row carries a mini CSS swatch preview; popover closes on outside click / Escape.
- Grid-motion experiment (ambient `translate3d` drift) was added, then reverted — user reported dizziness; all artifact-free (tokens back to `.04/.06`, no `@keyframes`).
- No counts changed (21 builds, hero 6, GHL 9).

## 2026-09-19 — GHL featured PSGCIMBTFLO banner tile (n09)
- Added `glSkills` n09 "PSGCIMBTFLO — Automation Building System" as a `featured:true` tile: full-width horizontal banner on the grid's 3rd row (`grid-column:1/-1`), kicked off with icon → icon later removed in-session (banner now: kicker + title + one-line desc + "Open system →"), no fan/wave pop.
- `renderGhl` branch for `featured`: horizontal layout (icon + kicker + title + one-line desc + letters row + "Open system →"); `.ghl-tile--featured` CSS (row flex, ellipsis clamps, reduced hover scale `1.012`); ≤860px stacks to column.
- Tile drawer holds all 11 steps as sub-skills with their playbook definitions; new `skipProof:true` sub field suppresses the "Proof coming soon." line for methodology steps.
- Grid rows changed to `grid-template-rows:minmax(0,1fr) minmax(0,1fr) auto` — the 8 tiles keep two equal rows, the banner row sizes to content (tile rows actually get a little taller). Still always-fit.
- Skill created globally: `psgcimbtflo` (opencode + claude). Counts: GHL 8 → 9; 21 builds + hero 6 unchanged. AGENTS.md map (1210–1347 / 1349–1377) + tile-9 count updated. Not yet committed/pushed.

## 2026-09-20 — Rail tokens, warm light bg, live dots, tab hints
- Rail tokenized to `--ra-*` and locked to soft dark `#2B2620` in BOTH themes (replaces navy rail in light mode); rail BG-tweak popover was built then removed in-session — rail now always soft dark, additive-free.
- Light mode rebalanced: parchment tokens (`--ground:#EFE7D8`, `--paper:#FBF6EC`, `--line:#E2D5C0`, `--line-strong:#D5C5AC`, grid baked to warm `rgba(122,90,56,.055)`) + amber radial wash on `.main`; explicit `[data-theme="dark"] .main{background:var(--ground)}` reset keeps dark pixel-identical. Light `theme-color` meta → `#EFE7D8`.
- Live indicators → blinking green badge system: `.live-tag` + `.live-dot` (8px #1DB954 + `livePing` pulse ring, reduced-motion → static halo). Badges derive from `liveUrl` — hero-top + workbench preview-top toggled in `setHeroLive`/`setPreview`; hero side list shows them only on builds 01–04 & 06 (05 FitCoach has no URL). Featured list header badge reverted to plain; unused `.dot` rule repurposed. Dot uses `<span>` not `<i>` — `.hero-side-item small i` was overlaying it black.
- Tab hover hint (topbar `.ptab`s): JS-positioned singleton `#tabHint` (`position:fixed`, `pointer-events:none`, clamped to viewport, re-anchored on resize/scroll, gated to `(hover:hover) and (pointer:fine)`, `role="tooltip"`). Final design = foundry ticket: notched paper card (clip-path TL+BR cuts) with dashed perforation border, amber rubber-stamp kicker, dashed divider, caret tracking the hovered tab center; stamped-in reveal (`scale(.92)→1` back-out curve). Earlier card + folded-pivot variants tried and iterated away. `data-hint` copy on all 6 tabs.
- Pushed to `main` → GitHub Pages. Counts unchanged (21 builds, hero 6, GHL 9).

## 2026-09-20 — Tab hover hint: design iteration + wrap-up
- Iterated topbar tab-hint directions — plain card, folded pivot (A), foundry ticket (B), blueprint annotation (C), teletype readout (D) — settled on B.
- Final = foundry ticket: notched paper card (clip-path TL+BR corner cuts), dashed perforation border, amber rubber-stamp kicker (rotated −2°, ink-ring halo), dashed divider, `drop-shadow` on the notched shape; caret kept on an unclipped outer layer and tracks the hovered tab's center; stamped-in reveal `scale(.92)→1` on a back-out curve.
- A (folded pivot) was trialed as a comparison and reverted in favor of B; caret hardcoded-`left:14px` was replaced with JS tracking (clamped 16..w−16).
- `<span class="live-dot">` swap also fixed `.hero-side-item small i` overlaying the dot as a black pill (dark mode).
- Pushed `1b8e30b` to `main` → GitHub Pages. Counts unchanged (21 builds, hero 6, GHL 9). No AGENTS.md map changes (no new data blocks or counts).

## 2026-09-20 — Archify diagrams embedded in PSGCIMBTFLO skill (n09)
- Added two standalone Archify viewers to the repo: `capabilities.html` (architecture, SHA `6463bdf7…`) and `psgcimbtflo.html` (workflow, SHA `36e74543…`, 11-step snake: Drive/Proof lanes, tags 01–11), delivered via the Archify skill (9/9 validate, 0 warnings, visual-check PASS at 1440–2048px light+dark).
- n09 PSGCIMBTFLO skill now renders the workflow diagram as the first block of its drawer (`diagram:` field → `.sysmap-wrap` iframe + "Open full ↗"), right under the title; the `embed` sub field exists for iframing a standalone html in place of desc/proof (unused after the System-map sub was removed in-session).
- Added `.sysmap-wrap`/`.sysmap-open` CSS (~724); sub renderer in `openGhlSkill` supports `embed`; drawer focus-trap/overlay unchanged, lazily-loaded iframes.
- AGENTS.md: "Companion Archify viewers" fact + GHL-skills file-map note (`diagram`, `embed`). Not yet committed/pushed.

## 2026-09-20 — Drawer expands to full width
- `.drawer` width `min(720px,100%)` → `100%` — the side panel now occupies the whole design; `.drawer-body` content centered on `max-width:min(1080px,100%)` for reading comfort at desktop widths. Applies to both case-study and GHL-skill drawers. No counts/lines changed.

## 2026-09-20 — Native PSGCIMBTFLO flow replaces Archify viewers
- Reverted the Archify iframe approach (viewer chrome clashed with the editorial aesthetic): deleted `capabilities.html` + `psgcimbtflo.html`, removed `.sysmap-wrap`/`.sysmap-open` CSS, the `diagram` field, and the `embed` sub-branch from `openGhlSkill`.
- Added native `.psm-track` — a single editorial one-line flow from Problem → Optimize at the top of the n09 drawer: 11 stations on a hairline rule (labels alternating above/below, Fragment Mono `01`–`11` amber numerals + step titles, amber markers, filled first/last dots, hover → amber tint, `--ground-2` panel), auto-generated from `subs[]` titles via new `psmTrackHtml(subs)` gated on an n09 `flow:true` flag. Subtle-grain: no chrome, no JS state, theme-adaptive, ≤600px side-scroll. CSS ~723; JS ~1560.
- AGENTS.md: dropped "Companion Archify viewers" fact, re-pointed GHL-skills row (`flow` + `.psm-track`). Counts unchanged (n09 subs = 11, GHL 9, 21 builds). Not yet committed/pushed.

## 2026-09-20 — Archify PSGCIMBTFLO diagram restored (signal-flow preset)
- The native `.psm-track` editorial chart was replaced — restored the Archify workflow viewer the user preferred for its design + trace animation.
- Re-delivered from a new frozen candidate `psgcimbtflo-signal.candidate.json` (copy of the classic candidate, `meta.visual_preset` flipped `classic` → `signal-flow`): 9/9 validate, 0 warnings, artifact SHA `5975052e…` (809,863 B) → `psgcimbtflo.html` in repo, visual-check PASS (no overflow, 8px min node text, viewer chrome OK).
- `index.html`: removed `.psm-track` CSS + `psmTrackHtml()` + n09 `flow:true`; restored `.sysmap-wrap`/`.sysmap-open` CSS (~723), `diagram:"psgcimbtflo.html"` on n09, and the drawer iframe branch in `openGhlSkill` (top of drawer + "Open full ↗"). Drawer stays full-width so the viewer renders large; theme toggle, pan/zoom + animated trace replay intact (S key cycles the signal skin).
- AGENTS.md: "Companion Archify viewer" fact restored (signal-flow, new SHAs), GHL-skills row back to `diagram` + `.sysmap-wrap`. Counts unchanged. Not yet committed/pushed.

## 2026-09-20 — Default drawer reverted to side panel; roomy n09 special case
- `.drawer` width reverted `100%` → `min(720px,100%)` — case-study and ordinary GHL-skill drawers are the original narrow right side panel again.
- New `.drawer-roomy` special case for chart-carrying skills (n09): drawer fills the main area below the topbar (`top:var(--top-h); left:var(--rail-w); right:0; bottom:0`) so the Archify workflow shows wide while the **topbar nav + left rail stay visible**; `html.drawer-n09-open .overlay` trims the dim layer to the drawer footprint (no dim over rail/nav). ≤860px: drawer + overlay drop to full-width below the sticky topbar.
- JS: `openGhlSkill` toggles `.drawer-roomy`/`drawer-n09-open` off `s.diagram`; `openDrawer` + `closeDrawer` clear both. Counts unchanged. Not yet committed/pushed.

## 2026-09-20 — Native PSGCIMBTFLO chart replaces the Archify iframe (final)
- Removed the Archify viewer for good: deleted `psgcimbtflo.html` + repo-root visual-check sidecars, dropped `s.diagram`/`.sysmap-*` CSS and the iframe branch in `openGhlSkill`.
- New **native `.psm-chart`** (in-house, no iframe, editorial tokens): orthogonal serpentine of the 11 steps — **Drive row** top (01,03,05,07,09,11) + **Proof row** bottom (02,04,06,08,10), node cards w/ numbered amber/sage tags, hover lift, an `<svg>` center-line route (constant-width via non-scaling strokes in a stretched 100×100 viewBox) with junction dots and an **animated amber pulse tracing Problem→Optimize** (respects `prefers-reduced-motion`). Keyed on n09 `chart:true`; legended Drive/Proof; ≤600px hides sublabels, taller/tighter layout.
- `chart:true` now also drives the roomy drawer flag (was `s.diagram`). Runnable check: temp `psm-check.js` evals `psmChartHtml()` → 2,880 B, 11 cards (6 Drive / 5 Proof), all tokens present. CSS ~731; JS `psmPlan`/`psmChartHtml` ~1579. AGENTS.md re-pointed (`.psm-chart`, `chart`). Counts unchanged. Not yet committed/pushed.

## 2026-09-21 — PSGCIMBTFLO chart redesigned as field-manual ledger + animations
- Rebuilt the n09 chart as a **printed-circuit ledger**: ruled blueprint panel (`repeating-linear-gradient` grid + dashed inner frame), medallion stations (24px amber/sage pins) hung directly on the serpentine rail (Drive pins top @42%, Proof bus bottom @58%), Drive/Proof rotating lane captions + 3 direction ticks on the bus, START→Optimize implied by numbering. Cards now absolutely positioned at their station coords (`PSM_STX`/`top:42|58%`) so pins sit exactly on the track; removed the old CSS-grid cards, `.psm-tag`, `.psm-jdot`/`.psm-pulse`.
- **Three tiers of motion** (all gated by `prefers-reduced-motion`): (1) entrance — route draw-in (`psmDraw`, pathLength=1 dashoffset) + per-station rise/stagger (`psmRise`, `--i`-based delay); (2) continuous — a **comet** walks Problem→Optimize (`.psm-comet` CSS keyframes on `left/top`, generated from `PSM_WP`/`PSM_LEGS` cumulative fractions, 4.5s linear, plus `psmBreath` halo); (3) hover — trace from Problem to the hovered step via a `<number>`-syntax `@property --prog` with `transition:--prog .28s`, bound by new `psmBind()` (fine-pointer only), `.psm-trace` draws with a soft amber glow.
- Geometry derived from one source of truth: `PSM_PATH` + `PSM_WP`/`PSM_LEGS`/`PSM_SIDX` → comet keyframes, `PSM_PROG` hover fractions (pathLength-normalized), station x/y. Layout verified headless: 11 cards, 0 overlaps, medallion centers on rails, `calc(0.5px) 1` dasharray resolves on hover (Chrome). CSS ~730–782; JS `psmPlan`~/psmChartHtml`/`psmBind` ~1601–1655. AGENTS.md GHL row re-pointed. Counts unchanged (21 builds, hero 6, GHL 9, n09 subs 11). Not yet committed/pushed.

## 2026-09-21 — Remove chart-only workflow drawer
- Removed the n09 workflow-chart drawer and all `.psm-*` chart styles, helpers, and bindings; the featured PSGCIMBTFLO tile now opens the standard compact skill drawer.
- Added two supplied GHL proof screenshots under `assets/ghl/` and attached them to the Calendar & Booking → Calendar Types sub-skill.
- Updated `AGENTS.md` to document the compact skill drawer and removed obsolete chart-specific instructions.

## 2026-09-22 — Proof images & skill updates
- Added two GHL proof screenshots (availability-1/2) and attached them to the Availability & Booking Rules sub‑skill.
- Updated the Automation Triggers and Calendar & Booking skill proof arrays; removed the PSGCIMBTFLO chart references.
- In‑progress: finalize AGENTS.md line‑range updates and verify syntax.

## 2026-09-22 — TorqueWorks Dormant Win-Back → Work section (n22), n04 reverted
- Reverted the n04 graduation: `Workflows & Automations` is back to its `learning:true` placeholder (2 subs, no proof, dimmed tile). Deleted `assets/ghl/proof-workflow-1/2/3.png`.
- Added the TorqueWorks project as a **case study in the Work panel** instead — new `projects` entry **n22** "TorqueWorks Auto Care — Dormant Lead Win-Back" (`cat: automation`, `family: automation`). Full case-study block (niche/problem/solution/build/outcome) from the supplied docx: tiered dormancy Smart Lists (60/90/180+ days), three tag-triggered win-back workflows, Wait-for-Reply + stage-check suppression, dedicated retention pipeline, 5 documented build bugs fixed.
- The three workflow screenshots moved into `assets/work/torqueworks-1/2/3.png` (60-day / 90-day / Dormant-Lost) and attached as `sections[]`; added n22-specific section labels in `openDrawer` (pattern mirrors n06's custom labels).
- Counts bumped: toolbar chips All 22 / Automation 17, rail "WORK — 22". AGENTS.md synced (work-panel row, projects row 22 entries, WORK 22; GHL rows reverted to committed text). GHL tiles still 9; learning set back to 04–06 + 08. Not committed/pushed.
- Moved n22 earlier in the `projects` array so TorqueWorks ranks 3rd on the Automation-filtered Work list (after Rubio, Haven; before FitCoach). No count changes.

## 2026-09-22 — Graduated n04 Workflows & Automations (capability, copy + proof)
- Dropped `learning:true` from the Workflows & Automations tile — now a confident capability tile, not a project showcase (that's n22 in the Work panel). Desc uses supplied copy: custom GHL/Make.com builds tailored to how the business runs, tested live, fixed before it reaches customers.
- 5 build-area sub-skills, each matching a chip and each proof-backed by existing shipped work: Defensive suppression (TorqueWorks workflow shot), Cross-app integrations Stripe·Sheets·Slack (FitCoach Make auto01/02), Lead routing & escalation (FlowFix triage), Dormant lead re-engagement (TorqueWorks 1–3), Conversation AI bot flows (Haven sec01). Root `proof:[]` stays empty — subs carry the shots.
- AGENTS.md synced: GHL row 1427–1480, counts line now 01–04 + 07 proof-backed. GHL tiles still 9; learning set 05–06 + 08. Not committed/pushed.

## 2026-09-22 — Work preview pane: page-like scroll + labeled image strip
- Preview was two hidden scroll regions (`.preview-img` + `.preview-body`, both `scrollbar-width:none`); a tall screenshot filled the image area and the 64×44 "tap to jump" strip was below its fold — multi-image projects read as single-image.
- Now one flow: `.preview-img` is `flex:none`, the big image scales to fit (`max-height:40vh, object-fit:contain`), and every image renders as a labeled `.preview-strip` chip under it (`n/N · Workflow 01 · Win-Back — 60-Day`, automation → `n/N · Auto M · Make scenario`, funnel → `n/N · Hero · …`), each chip opening the lightbox; count bar "N screenshots · click any to view full".
- `.preview-body` is the sole scroller with a visible slim scrollbar; a sticky `▾ more below` cue (`.preview-cue`) is appended only when the body overflows. Single-image/letter previews unchanged.
- Verified: both script blocks parse, 13/13 pattern checks pass, drawer untouched. AGENTS.md work-panel row updated. Not committed/pushed.
