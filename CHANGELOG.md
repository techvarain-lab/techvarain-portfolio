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
