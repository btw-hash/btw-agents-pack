---
name: reflect-session
description: End-of-session capillary reflection. Extract 0-3 candidate memory entries from the session (corrections, approvals of non-obvious choices, new project facts, external references) and write them to memory/ after per-entry approval. Invoke when user signals session end (phrases like "логируем", "спасибо", "до завтра", "пока", "хватит") or when a pending_reflections/*.json marker exists. OK to output "ничего нового" and exit silently.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, AskUserQuestion
---

Capillary reflection loop. Capture only what is **surprising or non-obvious** — do NOT save things already derivable from code/git/docs. If nothing warrants saving, say "ничего нового" and exit. Empty output is a valid success.

## Steps

1. **Locate source of reflection**
   - If called from pending marker: read `C:/Users/frost/.claude/projects/c--AI/memory/pending_reflections/*.json` (oldest first), extract `transcript_path`, read the tail of the transcript (last ~150 messages).
   - If called inline (no marker): use the current conversation context directly.

2. **Scan for signals** (classify by confidence):
   - **HIGH** → direct corrections: "не так", "no, don't", "stop", "переделай", "не мокай X". Feedback type.
   - **MEDIUM** → explicit approvals of non-obvious choices: "yes exactly", "perfect, keep doing that", "согласен" on a debatable approach. Feedback type.
   - **LOW** → new project facts: who/why/when, decisions, deadlines, incidents. Project type.
   - **EXTERNAL** → references to external systems (URLs, channels, dashboards, bot tokens). Reference type.

3. **Filter ruthlessly** — skip anything that:
   - Is already in an existing memory file (`Glob memory/*.md`, check names/descriptions).
   - Is derivable from code, git log, or CLAUDE.md.
   - Is ephemeral (current task state, "currently debugging X").
   - Is a generic programming fact.

4. **Draft ≤3 candidates** — use this exact frontmatter format:
   ```markdown
   ---
   name: {short-slug}
   description: {one-line, specific, <120 chars}
   type: {feedback|project|reference|user}
   ---

   {body}

   **Why:** {the reason — past incident, constraint, or explicit user preference}
   **How to apply:** {when/where this kicks in}
   ```
   `Why:` and `How to apply:` are MANDATORY for `feedback` and `project` types.

5. **Approve per entry via AskUserQuestion**
   - For each candidate, one question with options: `Save as-is` / `Edit first` / `Reject`.
   - Show the full proposed file content in the question description or as preview.
   - If user picks `Edit first`, ask for the change in free text, then re-confirm.

6. **Write approved entries**
   - Save to `C:/Users/frost/.claude/projects/c--AI/memory/{type}_{name}.md`.
   - Append ONE line to `MEMORY.md` under the correct section: `- [{name}.md](file.md) — {description}`.
   - Keep MEMORY.md entries alphabetical within each section.

7. **Record session metrics** — append one JSON line to `c:/AI/vault/metrics/sessions.jsonl`:
   ```json
   {"date":"YYYY-MM-DD","corrections":N,"tasks_completed":N,"tasks_reworked":N}
   ```
   - `corrections` = count of HIGH-confidence signals (user corrections/rejections in this session).
   - `tasks_completed` = distinct tasks worked on (estimate from conversation flow).
   - `tasks_reworked` = tasks where user said "не так" / rejected output and asked for redo.
   - If counts are uncertain, use best estimate — approximate data beats no data.

8. **Clean up pending markers** — delete any processed `pending_reflections/*.json` files.

9. **Final output** — 1-2 sentences: what was saved, what was skipped, plus metrics line. Example: "Сохранено 2: feedback_X, project_Y. Отклонено 1 (дубликат). Метрики: 1 коррекция, 3 задачи, 0 переделок."

## Rules (hard)

- **Max 3 candidates per session.** Ritual fatigue kills the loop.
- **Never auto-save.** Always approve per entry (first 2 weeks of loop).
- **Never duplicate** — before drafting, `Glob` existing memory filenames and check for overlap.
- **Never save ephemeral state.** "Currently working on X" belongs in HANDOFF.md, not memory.
- **If zero signals warrant saving** — output "ничего нового для памяти" and exit without asking anything.

## Anti-patterns (reject these at step 4)

- "User uses TypeScript in project X" — derivable from package.json.
- "Fixed bug Y in commit Z" — git log owns this.
- "User is currently debugging auth flow" — ephemeral, belongs in HANDOFF.
- "Always use async/await" — generic programming fact.
