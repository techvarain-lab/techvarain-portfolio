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
