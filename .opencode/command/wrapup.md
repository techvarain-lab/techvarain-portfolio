---
description: Append today's working-session entry to CHANGELOG.md. Run after finishing work.
---

Append a compact entry for this working session to `CHANGELOG.md`. Follow the existing format exactly — date heading, `-` bullets, no prose dumps, newest at the bottom of the file. Keep it to 3–6 bullet lines.

Before writing:
1. Read the CHANGELOG head (first ~15 lines) to match the format, then read the last entry to see where to append.
2. If anything went into `index.html`, confirm the actual current file state before describing it (e.g., project counts, hero list, new `projects` entries).
3. If changes touch the file map in `AGENTS.md` (new sections / moved data blocks / new count fields), update the affected line ranges there too, in the same session.

Entry must answer: what changed, why (one short clause), anything in-flight or pending. Example shape:

```
## 2026-09-17 — Session ops setup
- Added token-efficiency scaffold: AGENTS.md, CHANGELOG.md, /catchup + /wrapup commands, opencode.json.
- No changes to index.html or assets.
```

Do NOT commit anything — changelog only. $ARGUMENTS