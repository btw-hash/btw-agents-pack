---
name: refactor
description: Launch refactoring-specialist on changed or specified files
allowed-tools: Agent, Bash, Read, Glob, Grep
---

Run a refactoring session:

1. If $ARGUMENTS specifies files — refactor those files
2. If no arguments — find recently changed files: `git diff --name-only HEAD~5`
3. Launch `refactoring-specialist` agent on the identified files
4. Review suggestions and apply approved changes
5. Run tests after refactoring to verify no behavior change