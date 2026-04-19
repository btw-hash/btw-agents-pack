---
name: new-project
description: Bootstrap a new project in c:\AI — create folder, CLAUDE.md, vault/projects/<name>.md with frontmatter, register in notion-sync.
allowed-tools: Bash, Read, Edit, Write, Glob, Grep, AskUserQuestion
---

Bootstrap a new project under `c:\AI\`.

## Inputs

Name from $ARGUMENTS. If missing — AskUserQuestion for name, stack (Node/Python/Other), and short description.

## Steps

1. **Create folder:** `c:\AI\<name>\` (fail fast if exists).
2. **git init** + initial commit scaffold.
3. **Project CLAUDE.md** — minimal: purpose, stack, how to run, any project-specific rules.
4. **vault/projects/<name>.md** with YAML frontmatter:
   ```yaml
   ---
   name: <name>
   status: active
   version: v0.1
   stack: [...]
   created: YYYY-MM-DD
   ---
   ```
   Plus sections: `## Stack`, `## Recent`, `## Known Issues`, `## Next`, `## Architecture`.
5. **Register in notion-sync.js** — inspect `c:/AI/notion-sync.js`, if projects list is static — add new entry; if it scans vault/projects — no action needed.
6. **Run notion-sync** dry-run to verify the project picks up: `node c:/AI/notion-sync.js --dry-run --project <name>`.

Report: paths created, notion-sync dry-run result, next suggested action.
