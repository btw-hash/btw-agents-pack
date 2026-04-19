---
name: deploy
description: Deploy a project to production (test → build → push → verify)
disable-model-invocation: true
allowed-tools: Bash, Read, Glob, Grep
---

Deploy the current project to production. Steps:

1. Run tests: `npm test` or `npm run test:e2e`
2. Build: `npm run build`
3. If git has uncommitted changes, ask user before proceeding
4. Push to remote: `git push origin main`
5. Check deployment status

If $ARGUMENTS is provided, use it as the target (e.g., "staging", "production").
If no target specified, deploy to production.

Project-specific deploy commands:
- agent-dashboard: `git push origin main` (Railway auto-deploys)
- courseai: `git push origin main` (Vercel auto-deploys)
- heroes-randomizer: just push, no auto-deploy
