---
name: audit
description: Full-system audit — settings hygiene, dependencies, secrets, types, tests, memory. Returns a prioritized action list. Use monthly or before major releases.
allowed-tools: Read, Glob, Grep, Bash, Agent
---

Run a comprehensive audit across the workspace and report issues with severity.

## Steps

1. **Settings hygiene**
   - `cat C:/Users/frost/.claude/settings.json | jq '.permissions.allow | length'` — flag if >80
   - grep for hardcoded one-shot rules (`rm <specific file>`, `grep -n "<specific string>"`) — these are cruft
   - check hooks are present: SessionStart, PreToolUse (Edit/Write protect + secrets-scan + Bash danger), PostToolUse (prettier)

2. **Dependencies**
   - for each of agent-dashboard, courseai, my-assistant: run `npm outdated` and `npm audit --audit-level=high`
   - flag high/critical vulnerabilities

3. **Secrets scan**
   - `grep -rnE "sk-ant-|sk-proj-|ntn_[A-Za-z0-9]{40}|AKIA[0-9A-Z]{16}|ghp_[A-Za-z0-9]{36}|-----BEGIN.*PRIVATE KEY-----" c:/AI --include="*.ts" --include="*.js" --include="*.json" --include="*.md"`
   - must return zero results

4. **Memory health**
   - delegate to `general-purpose` agent: `Agent({ subagent_type: "general-purpose", description: "Audit memory dir", prompt: "Audit C:/Users/frost/.claude/projects/c--AI/memory/ read-only. Check MEMORY.md drift, duplicates, stale project facts (>30d old or dead paths), frontmatter integrity (name/description/type), Why/How structure on feedback/project entries. Report issues + proposed DELETE/MERGE/UPDATE/FIX-INDEX actions. Do not edit." })`
   - or invoke `/prune-memory` skill directly

5. **Types & tests**
   - for each project with tsconfig.json: `npx tsc --noEmit` (list errors)
   - for each project with vitest: `npm test -- --run` (pass/fail count)

6. **Agent/skill inventory**
   - `ls C:/Users/frost/.claude/agents/*.md | wc -l` — current count
   - `grep -L "^model:" C:/Users/frost/.claude/agents/*.md` — agents without explicit model (cost optimization opportunity)

## Output

Return a structured report:

### Summary
- Overall health: 🟢 / 🟡 / 🔴
- Critical issues: N
- Warnings: M

### Critical (fix now)
- [severity] issue + file:line + fix

### Warnings (fix this week)
- ...

### Optimizations (nice to have)
- ...

Keep under 500 words. Actionable, not descriptive.
