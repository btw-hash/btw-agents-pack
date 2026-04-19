---
name: git-pr
description: Create a PR with conventional commit, description, and Notion link
allowed-tools: Bash, Read, Glob, Grep
---

Create a pull request for the current branch:

1. Check `git status` and `git diff` for changes
2. Generate conventional commit message (feat/fix/chore/refactor/docs)
3. Create commit with the message
4. Push branch to remote
5. Create PR via `gh pr create` with:
   - Title from commit message
   - Body with: Summary, Changes list, Test plan
6. If $ARGUMENTS contains a Notion task reference, include link in PR body

If no branch exists, create one from the commit message (e.g., `feat/add-auth`).