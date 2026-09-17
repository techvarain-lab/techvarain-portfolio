# Variant E — Portfolio (single-file)

Personal GHL Specialist / Funnel Builder portfolio. One self-contained page — no build step, no framework, deploys straight to GitHub Pages.

## Project facts

- **Single file:** `index.html` (~1,255 lines, ~122 KB) — CSS, panels, and JS all inline. All edits to the site happen here.
- **Assets:** `assets/` holds images only. `assets/funnel/<slug>/` = `thumb.webp`, `full.webp`, `secNN.webp` per case study; `assets/work/` = automation/funnel screenshots; `assets/ghl/` = GHL proof shots.
- **Deploy:** GitHub Pages from `main`. `.nojekyll` present. No build/verify script — sanity-check by opening `index.html` or the Pages URL.
- **No analytics/hard-coded Netlify forms here** (Rubio funnel has `fbq`/`gtag` hooks; this portfolio itself does not).

## File map (approximate line ranges — change-safe to drift)

| Range | Content |
| --- | --- |
| 2–49 | `<head>`, fonts, favicon, meta |
| 10 | Theme bootstrap `localStorage.getItem('rd-theme')` (dark/light) |
| 52–640 | CSS: tokens/vars, dark theme overrides (`[data-theme="dark"]`), panels, workbench, drawer, lightbox, ghl tiles / zoom, responsive rules |
| 648–699 | Shell markup: rail (links, socials), `themeBtn`, `menuBtn`, top tabs `.ptab[data-panel=*]`, CTA |
| 701–772 | Hero panel: `heroLive` carousel (driven by `projects`), `heroSideList`, CTA buttons — "21" count |
| 773–795 | Work panel: `.work-toolbar` filters (All 21 / Funnel 11 / Automation 16 / Hybrid 6), `#rows` bench, `#preview` pane |
| 797–813 | Services panel |
| 815–823 | GHL panel — `#ghlTiles` (rendered by `renderGhl()`) |
| 827–847 | About panel — timeline cards |
| 850–869 | Contact panel — `handleSubmit(event)` form (mailto fallback), links: `techva.rain@gmail.com`, `0995 146 2765`, LinkedIn |
| 874–897 | Mobile rail drawer (`toggleMobileRail()`) |
| 899–901 | `#overlay`, `#drawer` (case-study), `#lightbox` markup |
| 904–926 | **`const projects=[...]`** — 21 entries. Item shape: `n` ("01".."21"), `cat` (`funnel`/`automation`), `tags[]`, `family` (`funnel`/`hybrid`/`automation`), `title`, `desc`, `img`, `full`, `sections[]`, `stack[]`, `bullets[]`, `niche/problem/solution/build`, optional `loom`, `automation[]`, `letter`, `liveUrl`. Items without `img` use `letter` fallback. |
| 928–960 | Workbench render/filter: `render(filter)`, row builder, family pill logic |
| 974–1006 | Zoom/lightbox/drawer helpers: `drawerZoom`, `openLightbox`, `prevUpdater`/preview body, `famLabel`, tag label mapping |
| 1007 | `openDrawerById(n)` |
| 1032–1085 | Hero carousel: `heroProjectNs` (ns "01".."06"), `setHeroLive(i)`, `heroLive**` element binding |
| 1061–1075 | Theme toggle wiring |
| 1086–1158 | `openDrawer(p)` / `closeDrawer()` / Escape-key handler |
| 1160–1222 | **GHL skills**: `const glSkills=[...]` (tile shape: `n, icon, title, short, desc, chips[], proof[], subs[]`), `ghlChip`, `ghlZoom*` hover peek, `ghlProof`, `renderGhl()`, `openGhlSkill(s)` |
| 1224–1255 | `handleSubmit(e)` (mailto compose), mobile rail toggling, menu/rail listeners |

## Conventions

- **Aesthetic:** editorial-mono. Fonts: Instrument Serif (display) + Fragment Mono (labels) + Cormorant Garamond accents. Ink on paper, amber accent, hairline `var(--line)` borders.
- **Tags/taxonomy:** `funnel` / `automation` / `hybrid` (funnel + automation). Filter chips derive counts from `projects` — keep the span count and the `family`/`tags` fields in sync.
- **Hero carousel** shows the 6 most recent/notable builds via `heroProjectNs` at line 1032.
- **Counts to keep current:** rail "WORK — 21", toolbar chips, `heroProjectNs` length, CONTACT reads "24h reply".
- **Images:** add sections as `sec01..secNN.webp` under `assets/funnel/<slug>/`; never hotlink. GHL proof under `assets/ghl/proof-*.png`.
- New case study = new `projects` entry (number = next `n`). Update: toolbar chips, rail count, hero list if notable, this file's "File map" + CHANGELOG.md.

## Working agreements (token efficiency)

Do NOT re-read all of `index.html` to "catch up". Orienting to recent work is cheap:

1. Start of session: run `/catchup` (git log oneline + `git diff --stat` + CHANGELOG tail).
2. Target reads — use `grep` or `Read` with a line window from the File map above, not the whole file.
3. For "what changed since last week," use `git log` / `git diff`; commit messages carry the summary.
4. Long project entries (Rubio/ClearView/Haven/Legal) have single-line JSON — `Read` truncates at 2000 chars; use `Read` with `offset` at the entry, or `grep` for the field you need.
5. After finishing work, run `/wrapup` to append today's entry to `CHANGELOG.md` (or the user will run it). Keep each entry to a few bullet lines.