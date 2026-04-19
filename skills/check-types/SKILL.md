---
name: check-types
description: Run TypeScript type checking on current or all projects
allowed-tools: Bash, Read, Glob
---

Run TypeScript type checking.

If inside a specific project directory, check only that project.
If in c:\AI root or if $ARGUMENTS is "all", check all TypeScript projects:

1. courseai: `npx tsc --noEmit`
2. ai-cover-letter-ext: `npx tsc --noEmit`  
3. heroes-randomizer: `npx tsc --noEmit`

Report type errors grouped by file. Show total error count per project.
