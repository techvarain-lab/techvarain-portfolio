# Variant E — Portfolio (single-file)

Personal GHL Specialist / Funnel Builder portfolio. One self-contained page — no build step, no framework, deploys straight to GitHub Pages.

## Project facts

- **Single file:** `index.html` (~1,640 lines, ~161 KB) — CSS, panels, and JS all inline. All edits to the site happen here.
- **Assets:** `assets/` holds images only. `assets/funnel/<slug>/` = `thumb.webp`, `full.webp`, `secNN.webp` per case study; `assets/work/` = automation/funnel screenshots; `assets/ghl/` = GHL proof shots.
- **Deploy:** GitHub Pages from `main`. `.nojekyll` present. No build/verify script — sanity-check by opening `index.html` or the Pages URL.
- **No analytics/hard-coded Netlify forms here** (Rubio funnel has `fbq`/`gtag` hooks; this portfolio itself does not).

## File map (approximate line ranges — change-safe to drift)

| Range | Content |
| --- | --- |
| 2–49 | `<head>`, fonts, favicon, meta |
| 10 | Theme bootstrap `localStorage.getItem('rd-theme')` (dark/light) |
| 52–700 | CSS: tokens/vars, dark theme overrides (`[data-theme="dark"]`), panels, workbench, drawer, lightbox, ghl tiles / zoom / learning-tile variants, **BG-tweak modes** (`.main[data-bg=*]` overrides of `.main::before`/`::after`: grid/dots/grain/blueprint/bare/watermark) + `.bg-btn`/`.bg-pop` control styling, responsive rules (incl. mobile `.ptabs` edge-fade scroll hint) |
| 704–757 | Shell markup: rail (links, socials), `themeBtn`, `menuBtn`, top tabs `.ptab[data-panel=*]` (`#ptabs`), CTA (hidden ≤1024px), **BG test button `#bgBtn` + popover `#bgPop` (.bg-opt[data-bgopt=*])** |
| 709–780 | Hero panel: `heroLive` carousel (driven by `projects`), `heroSideList`, CTA buttons — "17" count |
| 781–803 | Work panel: `.work-toolbar` filters (All 17 / Funnel 6 / Automation 25) + `#workSearch` box, `#rows` bench, `#preview` pane. Under the `automation` filter builds render as **grouped cards** (`.build-group`, hairline border/radius): each build has a tinted header row (`.build-hdr`, `data-id` = `p.n`, title + `N workflows` pill + stack + optional engine badge; hover → project preview, click → build drawer) with its flows as indented child rows beneath (`.flow-child`, `data-id` = `p.n·idx`, amber branch number, left tree rail; hover → per-flow preview, click → per-flow drawer). Search matches a flow → its whole group shows; no matching flow → group hidden. All/Funnel stay project-level. Preview column: pinned `.preview-top`, then `.preview-body` is the single page-scroller housing the media + typography. Tall full-page screenshots preview via `.prev-crop` (16:9 cover crop) for n07/n22, else `.prev-full`/`.prev-hero`; click → lightbox.|
| 805–821 | Services panel |
| 823–833 | GHL panel — `#ghlTiles` (rendered by `renderGhl()`) |
| 835–856 | About panel — timeline cards |
| 858–877 | Contact panel — `handleSubmit(event)` form (mailto fallback), links: `techva.rain@gmail.com`, `0995 146 2765`, LinkedIn |
| 882–905 | Mobile rail drawer (`toggleMobileRail()`) |
| 907–909 | `#overlay`, `#drawer` (case-study), `#lightbox` markup |

| 1098 | **`const projects=[...]`** — 17 entries (n "01".."16" + n22 + n23 + n24 = TorqueWorks Dormant Win-Back + FitCoach Funnel Copy + Haven Funnel Copy, GHL automation case study w/ 3 workflow screenshots under `assets/work/torqueworks-*.png` and `assets/funnel/fitcoach/`; letter-fallback placeholders n11/n15/n17–n21 removed 2026-09-22; n23 FitCoach funnel copy added 2026-09-22; n24 Haven Animal Clinic funnel copy added 2026-09-23). Item shape: `n`, `cat` (`funnel`/`automation`), `tags[]`, `family` (`funnel`/`automation` — hybrid removed), `title`, `desc`, `img`, `full`, `sections[]`, `stack[]`, `bullets[]`, `niche/problem/solution/build/outcome`, optional `loom`, `automation[]`, `automations` (workflow count — TorqueWorks:3), `engine` (opt-in amber "Conversation AI agent" badge on flow rows/preview/drawer — n04 only), `letter`, `liveUrl`, and automation items carry `flows[]` (29 flows across 11 builds — n04:3 n22:3 n05:3 n07:4 n08:4 n09:5 n10:3 n12:1 n13:1 n14:1 n16:1; each flow = `{name,short,tags[],imgs?,video?,poster?,problem/solution/outcome}`
— n05 flows carry per-flow `imgs[]` (New Client Onboarding→auto01 + make-onboarding.png; Abandoned Checkout Recovery→auto02/03 + make-abandoned.png; Payment Failed Alert→auto04/05 + make-paymentfailed.png) that scope both the preview pane and drawer automation zoom to the focused flow, plus per-flow `problem/solution/outcome` rendered when a flow is focused in the drawer). Items without `img` use `letter` fallback. |

| 1124–1157 | Workbench render/filter: `render(filter, q)` — under `automation` builds group into **card sections** (`.build-group` → `.build-hdr` header row + `.flow-child` indented flow rows, tree rail via `.flow-child>div` border-left); `data-id` = `p.n` (header) / `p.n·idx` (flows); no `.flow-parent` eyebrow (removed 2026-09-23). All/Funnel stay project-level. `rowEl`/`wireRow` helpers; active highlight tracked by `data-id` (not the visible number). `#workSearch` filters the current filter. Type pills (Funnel/Automation — hybrid removed 2026-09-22) |
| 1189–1233 | Zoom/lightbox/panel helpers + **preview pane** `setPreview(p, flow)` (single page-scroller in `.preview-body` via `mediaHtml` — multi-image shows the full-page shot at natural size `.prev-full`, single-image uses scale-to-fit `.prev-hero`, letter placeholder pinned in `#prevImg`; flow rows preview the flow name/short with a parent kicker (`Preview — p.n·idx · Automation · flow name`) and a CTA that opens the parent drawer on that flow; no zoom bar in the preview, `.zoom-bar` survives for the drawer only; `drawerZoom`, `autoZoom`, `openLightbox`, `famLabel`, tag label mapping), `switchPanel` |
| 1235 | `openDrawerById(n)` |
| 1208–1281 | Panel switching wiring + `.ptab` strip overflow tracker `updTabs()` (`ov`/`ov-left`/`at-end` masks) |
| 1282–1316 | Hero carousel: `heroProjectNs` (ns "01".."06"), `setHeroLive(i)`, heroLive** element binding |
| 1333–1346 | Theme toggle wiring |
| 1414–1495 | `openDrawer(p, fi)` / `closeDrawer()` / Escape-key handler — when `p.flows.length>1` renders `.wf-chip` workflow jump chips (highlighting the focused flow, `fi`), plus an amber flow intro block when a flow is in focus; metaLine derives workflow count from `flows[]` |
| 1440–1584 | **GHL skills**: `const glSkills=[...]` — 9 tiles (01–04 + 07 proof-backed/copy-backed — n04 `Workflows & Automations` graduated, subs stripped 2026-09-23 to keep it title/desc + "See actual work" CTA (subs:[], chips:[]); 05–06, 08 `learning:true` placeholders; 09 `featured:true` full-width PSGCIMBTFLO banner). Tile shape: `n, icon, title, short, desc, chips[], proof[], subs[]`, optional `learning`, `fan` (`"left"`/`"right"` = vertical pop stack on that edge; absent = top-arc), `featured` (horizontal banner: kicker + title + one-line desc, no icon, no fan). Subs honor `skipProof:true` to hide "Proof coming soon". `ghlChip`, `ghlZoom*` hover peek, `ghlProof`, `renderGhl()`, `openGhlSkill(s)` render the tiles and drawer; no embedded workflow chart remains. |
| 1642– | `handleSubmit(e)` (mailto compose), mobile rail toggling, menu/rail listeners |

## Conventions

- **Aesthetic:** editorial-mono. Fonts: Instrument Serif (display) + Fragment Mono (labels) + Cormorant Garamond accents. Ink on paper, amber accent, hairline `var(--line)` borders.
- **BG tweak:** topbar "▦ BG" button tests background treatments live (`.main[data-bg=*]` switcher, persists `rd-bg` in localStorage, mirrors theme pattern). Default `grid`. Mode list in `#bgPop`; keep `.bg-opt` rows in sync with `BG_OPTS` + `data-bgopt` + mode CSS + swatch classes.
- **Tags/taxonomy:** `funnel` / `automation` only — the Hybrid category was removed 2026-09-22 (old hybrids 01 Rubio → funnel, 04 Haven → automation, 05 FitCoach → automation, 06 Legal → funnel). Filter chips derive counts from `projects` — keep the span count and the `family`/`tags`/`flows[]` fields in sync. The Automation chip counts *automations*, not builds: 29 automations across 11 automation builds, derived from `flows[]` totals (n04:3 n22:3 n05:3 n07:4 n08:4 n09:5 n10:3 n12:1 n13:1 n14:1 n16:1), not the legacy `automations` field.
- **Hero carousel** shows the 6 most recent/notable builds via `heroProjectNs` at line 1282.
- **Counts to keep current:** rail "WORK — 17", toolbar chips (All 17 / Funnel 6 / Automation 29), `heroProjectNs` length (6, at line 1352), CONTACT reads "24h reply". GHL tiles = `glSkills` length (9: 01–04 + 07 proof-backed/copy-backed, 05–06 + 08 `learning` placeholders, 09 `featured` PSGCIMBTFLO banner). n09 subs = 11 steps; the banner remains, but no embedded workflow chart or roomy drawer behavior remains.
- **Images:** add sections as `sec01..secNN.webp` under `assets/funnel/<slug>/`; never hotlink. GHL proof under `assets/ghl/proof-*.png`.
- New case study = new `projects` entry (number = next `n`). Update: toolbar chips, rail count, hero list if notable, this file's "File map" + CHANGELOG.md.

## Working agreements (token efficiency)

Do NOT re-read all of `index.html` to "catch up". Orienting to recent work is cheap:

1. Start of session: run `/catchup` (git log oneline + `git diff --stat` + CHANGELOG tail).
2. Target reads — use `grep` or `Read` with a line window from the File map above, not the whole file.
3. For "what changed since last week," use `git log` / `git diff`; commit messages carry the summary.
4. Long project entries (Rubio/ClearView/Haven/Legal) have single-line JSON — `Read` truncates at 2000 chars; use `Read` with `offset` at the entry, or `grep` for the field you need.
5. After finishing work, run `/wrapup` to append today's entry to `CHANGELOG.md` (or the user will run it). Keep each entry to a few bullet lines.