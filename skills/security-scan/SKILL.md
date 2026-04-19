---
name: security-scan
description: Run security scan — dependency audit + secret detection + code analysis
allowed-tools: Bash, Read, Glob, Grep, Agent
---

Run a comprehensive security scan on the current project (or all if $ARGUMENTS is "all"):

1. **Dependencies**: `npm audit` for known vulnerabilities
2. **Secrets**: grep for API keys, tokens, passwords in source code (not .env)
3. **Code analysis**: launch `security-engineer` agent to review auth, input validation, XSS, injection
4. **HTTPS**: check for hardcoded HTTP URLs

Output a security report with severity ratings and fix recommendations.