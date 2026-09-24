## 2026-09-23 — Automation tab → grouped card-per-build (grouped tree)
- **Automation filter now renders a card per build** (`.build-group` hairline border/radius): tinted `.build-hdr` header row (build title + `N workflows` amber pill + stack + optional engine badge) with `.flow-child` indented flow rows beneath (amber branch number, left tree rail via `.flow-child>div` border-left). 11 groups / 23 flow rows verified. Replaces the flat per-flow rows that repeated the parent build as a `.flow-parent` eyebrow.
- **Interactions:** header row hover→project preview / click→build drawer (`openDrawer(p)` → flow chips); flow rows keep per-flow preview + per-flow drawer (scoped `imgs[]` + P/S/O unchanged). Search still scopes to flows — a matching flow shows its whole group.
- **`render()` automation branch rewritten** (grouping + first-flow default preview); `.flow-parent` CSS rule removed (dead). `.th/.row` responsive column collapses reused — no count changes (chip stays **Automation 23**).
- **AGENTS.md:** work-panel row (781–803) + workbench render row (1124–1157) synced to grouped-tree description.
- **Verify:** 2 script blocks parse OK; grouping sim = 11 groups / 23 flow rows; no `.flow-parent` references remain; chip/tooltip/placeholder still 23.

## 2026-09-23 — FitCoach n05 per-flow images scoped to each automation
- **n05 flows now carry `imgs[]`** scoping the proof to the focused workflow: New Client Onboarding→`auto01.webp` (1 shot), Abandoned Checkout Recovery→`auto02/auto03.webp` (2), Payment Failed Alert→`auto04/auto05.webp` (2). All 5 screenshots allocated, zero duplicates.
- **Preview pane** (`setPreview`) + **drawer automation zoom** (`openDrawer`) now use `flow.imgs` when a flow is focused, falling back to `p.automation` otherwise (other builds unaffected). Drawer zoom-bar count/labels follow the scoped array; non-flow labels reuse `autoLabels`/defaults.
- **AGENTS.md:** flow item shape notes `imgs?` + n05 mapping; drawer/preview anchors unchanged.
- **Verify:** 2 script blocks parse OK; n05 flows 1/2/2 images, project-level still holds all 5.

## 2026-09-23 — FitCoach n05 expanded to 3 independent automation workflows (23 automations / 11 builds)
- **`n05.flows[]`: 1 → 3** (New Client Onboarding / Abandoned Checkout Recovery / Payment Failed Alert) — each flow now carries its own `problem`/`solution`/`outcome` in the empathetic marketing voice, plus flow-specific tags. Automation tab renders 3 independent rows (`05·1/05·2/05·3`), each with its own preview, drawer chips, and search.
- **Per-flow case-study rendering:** `openDrawer` case-study block now prefers the focused flow's P/S/O via `const cs=(flow&&flow.problem)?flow:p` (index.html:1452); builds without per-flow copy (n04/n22) fall back to project-level P/S/O — no regression.
- **`bullets[]` removed** from n05 (4 legacy enrollment-only technical bullets; unrendered search-hay, flows/tags carry the content now).
- **Counts:** Automation chip 21→**23** (tooltip "23 automations across 11 builds"); `#workSearch` placeholder "Search 21 automations…"→"Search 23 automations…". All 17 / Funnel 6 unchanged (builds, not flows).
- **AGENTS.md:** file-map + taxonomy/counts synced (n05:1→n05:3, 21→23, flow item shape notes per-flow P/S/O).
- **Verify:** 2 script blocks parse OK; n05 = 3 flows each with P/S/O+tags; TOTAL FLOWS = 23; no stale "21 automations"/"Search 21"/n05:1 references remain.

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

## 2026-09-23 — Session wrap-up: n04 emphasis + workbench polish (committed da1c0af, pushed)
- **n04 Conversation AI emphasis** shipped (engine badge on flow rows/preview/drawer) + **"Conversation AI" dropped from n04 `stack[]`** as redundant — details in the two entries above. AGENTS item shape synced with the optional `engine` field.
- **Type↔stack column breathing room**: `.stack-mini` gains `padding-left:14px` + a hairline left border so the type pill column and stack column aren't glued; **Stack** table header now centered to match **Type**.
- **Verify**: 2 script blocks parse OK, 16/16 markers, counts unchanged (17 projects / funnel 6 / automation 11 / 21 flows). Nothing in-flight; remote `main` is at da1c0af.

## 2026-09-23 — Session wrap-up: FitCoach 3 workflows + grouped Automation tab (committed cb6b81c, pushed)
- **FitCoach n05 → 3 independent automations** (Onboarding / Abandoned Checkout / Payment Failed) with per-flow P/S/O + scoped `imgs[]` (auto01 / auto02-03 / auto04-05); Automation count 21→23.
- **Automation tab → grouped card-per-build**: `.build-group` + `.build-hdr` header + `.flow-child` tree rows (11 groups / 23 flows); `.flow-parent` eyebrow/CSS removed; old single-row flattening gone.
- **AGENTS.md** file-map rows 21/29/30/32 + taxonomy/counts synced (n05:3, `imgs?` flow shape, grouped render). Nothing in-flight.
## 2026-09-24 — Real Estate automation expanded 2→4 + preview crop + counts
- **n07 expanded 2 → 4 flows** (Builder/Seller Lead Router / Hot Lead Instant Alert / Staggered Lead Re-engagement / Appointment Confirmation & Reminder), each with imgs proof + plain-language `short` + problem/solution/outcome; added `automation[]` + `autoLabels[]` so the drawer renders "Zoom — 4 workflow steps" with named labels (mirrors n05).
- **Proof images imported** to `assets/work/realestate-{router,hotalert,stalled,appointment}.png`; `img` repointed from the broken `realestate-ghl.png` to `realestate-router.png`.
- **Automation counts 23→25** (11 builds unchanged): toolbar chip 25, tooltip "25 automations across 11 builds", `#workSearch` placeholder "Search 25 automations…". All 17 / Funnel 6 unchanged.
- **Preview crop for tall screenshots**: added `.prev-crop` (16:9 cover crop); used for n07 + n22 so the preview pane shows a crisp top slice instead of a squished full-page image (full pages still open via lightbox).
- **Verify:** 2 JS script blocks parse OK (3rd = ld+json); n07 = 4 flows verified; AGENTS.md rows 21/29/46/48 + taxonomy list synced (n07:4, 25 total flows).
## 2026-09-24 — FlowFix Plumbing n08 rebuilt to 4 automations (flows 25→26)
- **n08 flows 3 → 4** (Intake & Triage / Missed-Call-Text-Back / Database Reactivation / Review & Referral Loop) — user copy kept verbatim as per-flow `problem/solution/outcome`; derived `short` + `tags` added (approved); inline double-quotes escaped as `\"` for JS validity.
- **Automation count 25→26** (n08:4); All 17 / Funnel 6 unchanged. Chip/tooltip/`#workSearch` placeholder updated; AGENTS.md rows 29/46/48 synced.
- **Images attached:** per-flow `imgs[]` → `assets/work/flowfix-{intake,missedcall,reactivation,review}.png` + project `automation[]`/`autoLabels[]` (build-level drawer zoom mirrors n07); n08 added to `.prev-crop` (tall screenshots); `img`/`flowfix-triage.png` preview untouched.