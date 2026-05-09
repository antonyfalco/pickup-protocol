---
name: pickup
description: Draft a PICKUP file from current chat state. Names what's done, what's staged, what the next session must not re-author.
---

## When to use

The operator types `/pickup` near the end of a session that has done substantive work and will be resumed later (different session, different operator, different time of day). The slash command produces a `PICKUP-<YYYY-MM-DD>-<scope>.md` file ready for the next session to consume.

## Behavior

1. Read the current conversation state. Identify:
   - Files written, staged, or modified during this session.
   - Decisions made (and decisions deferred).
   - Tools run successfully (and tools that failed).
   - In-flight work that has not yet completed.

2. Ask the operator (in chat) two questions:
   - **Scope name** — short kebab-case slug for the filename (e.g., `prolexic-dashboard-autonomous-run`).
   - **Output location** — where to write the PICKUP file. Default to `~/.claude/plans/` if Podium-style; otherwise the host project's plan directory.

   These two questions are the only operator-blocking interaction. Everything else is inferred.

3. Draft the file matching `REF_pickup-shape.md`. All five sections (Preface, State, Decision gates, Acceptance checklist, Memory anchors). Decision gates is `None.` if no branching choices are pending. Memory anchors is omitted if no non-obvious decisions were made.

4. Write the file. Do not commit. The operator decides whether to commit and where.

5. Print the path and a one-line summary. The operator can review and edit before handing off.

## What it must not do

- **Do not re-author plans.** If a plan exists for the work, the PICKUP references it; the PICKUP does not duplicate its content.
- **Do not editorialize.** Memory anchors are factual reasons, not opinions about whether the choices were right.
- **Do not hallucinate state.** If the conversation doesn't make a piece of state explicit, the PICKUP either omits it or marks it `<unknown — operator should fill in>`.
- **Do not over-broaden the "do not re-author" line.** Be specific: "do not re-author the plan at `~/.claude/plans/ACTIVE-foo.md`" beats "do not re-author anything."

## Example output

```markdown
# PICKUP-2026-05-09-evaluator-kit-bootstrap.md

## Preface

Three skill repos (`auto-mode-guardrails`, `evaluator-kit`, `pickup-protocol`)
have been scaffolded locally with main + add-initial-skills branches each.
Next session's job is to push the repos to GitHub and open PRs through the UI.
Do not re-author the SKILL.md files or PITCH.md files; they are committed.

## State

### Completed
- Three local repos initialized at ~/projects/{auto-mode-guardrails, evaluator-kit, pickup-protocol}
- Each has main with seed (README/LICENSE/.gitignore) and add-initial-skills with PITCH.md plus skill content

### Staged but not yet executed
- `gh repo create` for each, splitting between antonyfalco and TonyHDX accounts
- `git push -u origin main` and `git push -u origin add-initial-skills` for each
- PR open through the GitHub UI

### Not started
- v0.2 work on any of the three (runtime hooks, real test harnesses)

## Decision gates

1. Account routing per repo.
   - Default: auto-mode-guardrails and pickup-protocol → antonyfalco; evaluator-kit → TonyHDX.
   - Operator decides per repo.

## Acceptance checklist

- [ ] All three repos visible on GitHub under the chosen accounts
- [ ] PR #1 open on each repo with the add-initial-skills diff
- [ ] PR descriptions reference PITCH.md inline

## Memory anchors

- Why split across two GitHub accounts: evaluator-kit extracts Hydrolix-Podium IP, so it lives under TonyHDX. The other two have reach beyond Hydrolix.
- Why feature branch `add-initial-skills` instead of committing directly to main: the operator wanted PR-driven workflow on personal repos to build GitHub UI familiarity.
```

## Failure-mode notes

- If the conversation has not yet produced any concrete artifacts, refuse to draft. A PICKUP for a session that did nothing is noise.
- If the operator interrupts before the two questions are answered, leave the slash command in a re-runnable state. Do not write a partial file.
