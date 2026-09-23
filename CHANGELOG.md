## 2026-09-23 — Manage the automation: flows + search (21 automations / 11 builds)
- **`flows[]` authored** on the 11 automation projects (21 automations: n04:3 n22:3 n05:1 n07:2 n08:3 n09:2 n10:3 n12:1 n13:1 n14:1 n16:1; each `{name,short,tags[]}`). No new images — flows reuse existing proof/section assets.
- **Automation filter flattens into per-flow rows** (`render(filter, q)`): `data-id` = `p.n·idx` (e.g. `04·2`), parent build as `.flow-parent` eyebrow, flow tag pills, `rowEl`/`wireRow` helpers; All/Funnel stay project-level. Active highlight now tracks `data-id` (not the visible number).
- **`#workSearch` box** added to the work toolbar — filters the current filter (flow name/short/tags/parent build on the Automation tab; title/desc/stack/tags otherwise); placeholder adapts ("Search 21 automations…" / "Search builds…").
- **Preview + drawer flow context:** `setPreview(p, flow)` shows the flow name/short with a parent kicker and an "Open case study" CTA that opens the drawer on that flow; `openDrawer(p, fi)` renders `.wf-chip` workflow jump chips (highlighting the focused flow) + an amber flow intro block when `flows.length>1`; metaLine derives the workflow count from `flows[]`.
- **Counts updated:** toolbar Automation chip 13→**21** (tooltip "21 automations across 11 builds"); rail `WORK — 17`, All 17 / Funnel 6 unchanged (builds, not flows).
- **AGENTS.md:** file-map rows + taxonomy/counts synced (`flows[]` item shape, 21 count, render/setPreview/openDrawer anchors).
- **Verify:** 2 script blocks parse OK (1,672 lines); 17 projects (funnel 6 / automation 11); 21 automation flows; n23 (FitCoach funnel copy) carries no `flows` — the earlier accidental duplicate was removed.

## 2026-09-23 — Haven funnel copy on Funnels tab (n24)
- **Haven Animal Clinic funnel copy added** as `n:"24"` at the end of the `projects` array (before `];`), mirroring the n23 FitCoach funnel-copy pattern: same `assets/funnel/haven/` thumb/full/sec01 + `liveUrl` (funnelbuild-haven_animal_clinic), `family` flipped to `funnel`. Title "Haven Animal Clinic — New Patient Checkup Funnel"; desc + bullets grounded in the live page — ₱1,999 Overall Checkup anchored vs ₱3,500 (saves ₱1,501), Today/Tomorrow slot picker with live availability, "Open Conversation Assistant →" hand-off to the Conversation AI, trust stack (1,200+ families, 4.9★), no upfront payment. Original n04 automation entry untouched.
- **Counts updated:** All 16→**17**, Funnel 5→**6**, Automation **13 unchanged** (still 11 automation builds). Meta/og "17 builds", ptab hint + WORK cnt 17, toolbar All 17 / Funnel 6, rail `WORK — 17`, hero CTA "Explore all 17" (was stale "21" leftover from removed letter placeholders).
- **AGENTS.md:** rows 20/21/29/47 synced (`All 17 / Funnel 6 / Automation 13`, "17 entries" with n24 note).
- **Parse verified:** 2 script blocks OK, 1,617 lines; 17 projects (fam funnel 6 / automation 11 / hybrid 0); n24 keys n/cat/tags/family/title/desc/img/full/sections/stack/bullets/liveUrl.

## 2026-09-23 — FitCoach funnel copy + counts update
- **FitCoach funnel copy added** as `n:"23"` at the end of the `projects` array (before `];`). Title reframed to "FitCoach - 12-Week Program Checkout Funnel"; bullets rewritten from a funnel-page angle; `automation[]` kept so the drawer shows both the 6 page sections and the 5-step Make flow below. All other copy (loom, stack, sections, img/full) unchanged from the original n05 entry.
- **Counts updated:** All 15→**16**, Funnel 4→**5**, Automation **13 unchanged** (same 11 automation builds + TorqueWorks×3). Chip titles/tooltips reflect 13 automations. Toolbar All chip 16, Funnel chip 5. Meta/og "16 builds", ptab hint "16 builds", rail `WORK — 16`.
- **AGENTS.md:** hero CTA count 16; chips `All 16 / Funnel 5 / Automation 13`; entries "16 entries" with n23 note; anchors shifted +1 (render 1114, setPreview 1159, openDrawerById 1197, switchPanel 1208, hero 1282, openDrawer 1371, glSkills 1440, handleSubmit 1585); row 47 `WORK — 16` and `heroProjectNs length (6, at line 1282)`.
- **Parse verified:** 2 script blocks OK, 1617 lines (array insertion added 1 line before `];`); fam funnel 5 / automation 11 / hybrid 0; no hybrid refs.

## 2026-09-23 — Session wrap-up
- Verified final state: 16 projects (fam funnel 5 / automation 11), 2 script blocks parse OK (1,617 lines), 0 `Hybrid` refs, single `n:"23"` in `projects` only — a stray copy that landed inside `glSkills` (broke parse) was caught and removed mid-session.
- All count touchpoints confirmed at All 16 / Funnel 5 / Automation 13; AGENTS.md file map + counts synced (rows 20/21/29/46/47, anchors shifted +1).
- Nothing pending; no commits pushed.
## 2026-09-23 - n04 Haven: one agent, three automations + flow walkthrough videos
- **n04 reworked to "one agent, three automations"** (via script) - flows renamed Emergency Escalation Automation / Lead Qualification & Data Capture / Booking Automation, each with dedicated shorts/tags; bullets, desc and solution rewritten to match.
- **n04 automation proof wired**: 2-step zoom stack `assets/work/haven-emergency.png` (483 KB, from Downloads) + `assets/work/haven-cai-config.png` (345 KB, from Screenshots) with matching `autoLabels` ("Emergency escalation - intent gate + hours-aware routing", "Conversation AI agent - bot configuration").
- **Automation-first preview/drawer**: `setPreview` shows proof only for automation items (`automation[0] || p.img`; funnel `sections` excluded from strip items, letter placeholder if no images); drawer primary zoom becomes the "Zoom - N workflow steps" stack and the "Funnel - the page" secondary block was removed entirely (`funnelMedia` deleted).
- **YouTube walkthrough embeds** on all three n04 flows (`video` field on flow objects): Emergency Escalation `0n5a-mSrghk`, Lead Qualification + Booking shared `NNA_A_6O6sU`. `ytCard(f)` renders a reusable `.loom-wrap` card (poster + play button, `playLoom` reuse); `ytThumb(img)` keeps a remote fallback chain (hqdefault->sddefault->mqdefault->default->maxresdefault) and hides the img on total failure. Preview shows the video card above the image; drawer shows it under the flow intro; `closeDrawer` tears down youtube iframes too.
- **Bundled local posters** `assets/work/yt-NNA_A_6O6sU.jpg` + `assets/work/yt-0n5a-mSrghk.jpg` (hqdefault frames, ~15 KB each) are the primary poster src - no `i.ytimg.com` dependency (fixes blank-thumbnail on local: cached 404 / client-side block). AGENTS flow shape now `{name,short,tags[],video?,poster?}`.
- **Flow previews are video-only**: when the focused flow has a `video`, the automation image is suppressed in the preview pane ("too much"), keeping proof on the main views (project preview + drawer zoom stack). Flow #1 (no video originally) keeps its image until it got its video.
- **Verify**: 2 script blocks parse OK; 17 projects (funnel 6 / automation 11); 21 flows; n04 carried 3 `video` fields after this batch.

## 2026-09-23 - n04 Conversation AI emphasis (4-point)
- **Opt-in `engine` field** added to n04 ("Conversation AI agent"); absent elsewhere so no other project changes. AGENTS item shape synced.
- **3 amber touchpoints on the Haven surfaces**: (1) flow rows on the Automation tab get an amber pill prefix on the `.flow-parent` eyebrow line; (2) flow preview kicker leads with "Conversation AI agent - title - n"; (3) drawer workflow-jump intro header suffixes "Conversation AI agent" (`Automation 04:2 - of 3 - Conversation AI agent`). All single-line edits, zero draft.
- **Verify**: 2 script blocks parse OK; 16/16 markers; 17 projects / 21 flows unchanged; `engine` decl 1x, `p.engine` refs 3x.

## 2026-09-23 - n04 stack de-dup
- **"Conversation AI" dropped from n04's `stack[]`** ("GoHighLevel","GHL Workflows","GHL Calendar") - now redundant with the amber `engine` badge on rows/preview/drawer. Removes the gray repeat from the flow-row `.stack-mini`, preview stack pills, drawer metaLine and stackPills. n24 (funnel copy) keeps it - no badge there, and it is a legit build tag in that context.
