---
name: onboard
description: Generate project overview for a new context — stack, structure, patterns, tasks
allowed-tools: Read, Glob, Grep, Bash
---

Generate a comprehensive project overview for the current directory:

1. **Tech stack** — detect from package.json, tsconfig, etc.
2. **Folder structure** — tree of important directories
3. **Key patterns** — how routing, auth, state management work
4. **Recent changes** — last 10 commits
5. **Open tasks** — from TODO comments, Notion, ROADMAP
6. **Known issues** — from Known Issues in Obsidian vault
7. **How to run** — dev, build, test commands

Output as a concise briefing document that lets a new agent (or human) understand the project in 2 minutes.