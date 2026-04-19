---
name: accessibility-audit
description: Run accessibility audit — WCAG 2.1 AA compliance check
allowed-tools: Bash, Read, Glob, Grep, Agent
---

Run accessibility audit on the current project:

1. Launch `accessibility-tester` agent to review components
2. Check all interactive elements for:
   - Keyboard accessibility
   - ARIA labels
   - Color contrast (4.5:1 minimum)
   - Alt text on images
   - Heading hierarchy
   - Form labels
3. If possible, run axe-core: `npx axe-cli $URL`
4. Generate WCAG 2.1 AA compliance report with fix priorities