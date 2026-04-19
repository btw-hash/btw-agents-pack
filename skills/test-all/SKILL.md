---
name: test-all
description: Run tests across all projects in c:\AI
allowed-tools: Bash, Read, Glob
---

Run tests for all projects and report results:

1. agent-dashboard (c:\AI\agent-dashboard): `npm run test:e2e`
2. courseai (c:\AI\courseai): `npm run lint && npm run build`
3. ai-cover-letter-ext (c:\AI\ai-cover-letter-ext): `npm run lint && npm run build`
4. heroes-randomizer (c:\AI\heroes-randomizer): `npm run build`

For each project:
- cd into the directory
- Run the test/build command
- Report PASS or FAIL with error details

At the end, show a summary table of all results.
