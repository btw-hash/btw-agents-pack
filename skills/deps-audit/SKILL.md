---
name: deps-audit
description: Audit dependencies across all projects — vulnerabilities, outdated, unused
allowed-tools: Bash, Read, Glob, Grep
---

Run dependency audit across all projects in c:\AI:

For each project with package.json:
1. `npm audit` — security vulnerabilities
2. `npm outdated` — outdated packages
3. Check for unused dependencies (installed but not imported)

Show results as a summary table:
| Project | Vulnerabilities | Outdated | Unused |

Flag critical/high vulnerabilities. Suggest upgrade plan if needed.