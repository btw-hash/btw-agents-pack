---
name: log
description: Session wrap-up. Full "логируем" protocol (A7) — git commit + Obsidian daily/project update + HANDOFF/SESSION_STATE + notion-sync. Invoke on "/log", "логируем", "залогируй", "wrap up".
allowed-tools: Bash, Read, Edit, Write, Glob, Grep
---

Execute the 4-step logging protocol from CLAUDE.md A7.

## Step 1 — git commit (if there are changes)

In each affected project directory:
```bash
git status
```
If changes exist and user hasn't said "no commit" — stage, write Conventional Commit message, commit. Never use `--no-verify` or `--force`.

## Step 2 — Obsidian

- `c:/AI/vault/daily/YYYY-MM-DD.md` — append today's work (what was done, per project). Create file if missing.
- `c:/AI/vault/projects/<project>.md` — if status / version / recent changed, update YAML frontmatter (keep `version:` field — see feedback_version_badges) and Recent/Next sections.

## Step 3 — Claude memory

- `C:/Users/frost/.claude/projects/c--AI/memory/HANDOFF.md` — что начато/приостановлено, с чего продолжить.
- `C:/Users/frost/.claude/projects/c--AI/memory/SESSION_STATE.md` — живой статус всех проектов.

## Step 4 — Notion sync

```bash
node c:/AI/notion-sync.js
```

Report: what was committed, which vault/memory files touched, notion-sync result. State pass/fail per step.

If $ARGUMENTS contains project name — scope commit+vault updates to that project only.
