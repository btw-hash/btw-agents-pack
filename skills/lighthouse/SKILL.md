---
name: lighthouse
description: Run Lighthouse audit on a URL or local dev server
allowed-tools: Bash, Read, Glob
---

Run Lighthouse performance audit:

1. If $ARGUMENTS is a URL, audit that URL
2. If no URL, start local dev server and audit localhost
3. Run: `npx lighthouse $URL --output=json --chrome-flags="--headless"`
4. Parse scores: Performance, Accessibility, Best Practices, SEO
5. Flag any score below 90
6. List top 5 improvement opportunities with estimated savings

Show results as a scorecard with color indicators.