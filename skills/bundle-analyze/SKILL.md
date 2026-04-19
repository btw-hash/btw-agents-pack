---
name: bundle-analyze
description: Analyze JS bundle size — large deps, code splitting opportunities
allowed-tools: Bash, Read, Glob, Grep
---

Analyze JavaScript bundle size:

1. For Next.js: `ANALYZE=true npm run build` or `npx @next/bundle-analyzer`
2. For Vite: `npx vite-bundle-visualizer`
3. Parse output and identify:
   - Total bundle size
   - Top 10 largest dependencies
   - Dependencies > 100KB (flag as warnings)
   - Code splitting opportunities
   - Unused exports

Show results as a table sorted by size. Suggest optimizations.