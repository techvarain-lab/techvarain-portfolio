---
description: Get fully oriented at session start — git history, working-tree delta, and the CHANGELOG tail, without re-reading index.html.
---

Quickly orient me to the current state of this project before we start working. Do the following in one pass, keeping total output compact:

1. Run `git log --oneline -15` and `git status`.
2. Run `git diff --stat` (unstaged) and, if present, `git diff --cached --stat`.
3. Read the last ~40 lines of `CHANGELOG.md` (the tail is the newest session entries).
4. If `index.html` has uncommitted changes, run `git diff -- index.html` and summarize what changed and why in a few lines — do NOT dump the whole diff.

Then report back in this shape:

- **HEAD:** <subject> — days since last commit
- **Working tree:** clean / N changed files (list them + one-line nature of change)
- **Latest session:** <first bullet of the newest CHANGELOG entry>
- **Since last session:** <what the last CHANGELOG entry changed>
- **Counts check:** if any UI count (work items, chips, hero list) looks stale vs the CHANGELOG, flag it.

Do not start any file edits — this is orientation only. $ARGUMENTS