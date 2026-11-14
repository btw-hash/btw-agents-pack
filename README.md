# btw-agents-pack

**37 Claude Code subagents + 17 skills.** Battle-tested in BTW Studio's production pipeline. MIT licensed. Copy-paste to install.

Studio that ships them: **[btwstudio.dev](https://btwstudio.dev)**

## What's inside

```
btw-agents-pack/
├─ agents/               37 × .md subagents (product-manager, architect, developer, debugger, …)
└─ skills/               17 × slash-commands (/waterfall, /log, /deploy, /audit, …)
```

All agents have explicit tool-allowlists; skills follow Anthropic's SKILL.md convention. Nothing here depends on our private workspace — files are sanitized (no paths, tokens, or personal refs).

## Install

### Option A — Bulk copy (takes 10 seconds)

```bash
git clone https://github.com/btw-hash/btw-agents-pack.git
cp btw-agents-pack/agents/*.md ~/.claude/agents/
cp -r btw-agents-pack/skills/* ~/.claude/skills/
```

Restart Claude Code. Agents become available to the `Agent` tool; skills are invokable via `/<name>`.

### Option B — Cherry-pick

Open `agents/` or `skills/`, pick a file and copy it into `~/.claude/agents/<name>.md` (or `~/.claude/skills/<name>/`).

## Agents (37)

**Planning & product**
`product-manager` · `business-analyst` · `architect` · `ux-designer`

**Design**
`brand-identity-designer` · `motion-designer` · `3d-scene-designer` · `image-prompt-engineer` · `visual-storyteller`

**Development**
`developer` · `debugger` · `refactoring-specialist` · `prompt-engineer` · `ollama-expert`

**Domain experts**
`prisma-expert` · `supabase-expert` · `chrome-extension-expert` · `telegram-bot-expert` · `n8n-editor` · `api-tester`

**Quality**
`reviewer` · `qa-engineer` · `test-engineer` · `tester` · `accessibility-tester` · `performance-engineer` · `security-engineer`

**Ops**
`devops-automator` · `dependency-manager` · `git-workflow-manager` · `seo-specialist` · `technical-writer`

**Content**
`content-creator` · `instagram-curator` · `carousel-growth-engine`

**Orchestration**
`boss` · `worker`

## Skills (17)

`/waterfall` · `/log` · `/reflect-session` · `/audit` · `/new-project` · `/onboard`
`/deploy` · `/check-types` · `/test-all` · `/lighthouse` · `/refactor` · `/bundle-analyze`
`/deps-audit` · `/git-pr` · `/security-scan` · `/accessibility-audit` · `/db-migrate`

## How we use them

BTW Studio's standard pipeline for shipping a new product:

```
Idea
  └─→ product-manager      → PRD
    └─→ business-analyst   → spec with REQ-N/TASK-N/SVC-N identifiers
      └─→ architect        → technical design
        └─→ ux-designer    → wireframes
          └─→ motion-designer + brand-identity-designer → polish
            └─→ developer  → implementation
              └─→ reviewer + test-engineer + tester → QA
                └─→ devops-automator → deploy
```

Invoked as one command via `/waterfall`.

## Contributing

This is a snapshot pack — not a monorepo with submissions. If you've improved an agent, open a PR with the diff + a 1-line rationale. We'll merge liberally.

## License

MIT. Use commercially. Fork freely. Attribution appreciated but not required.
