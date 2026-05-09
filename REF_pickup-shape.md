# REF: PICKUP file shape

A PICKUP file is a context-handoff artifact for multi-session Claude Code work. Its purpose is to constrain what the next session is allowed to do, so the next session does not waste time re-authoring work that is already staged.

## Filename convention

```
PICKUP-<YYYY-MM-DD>-<short-scope>.md
```

Examples:

- `PICKUP-2026-05-04-prolexic-dashboard-autonomous-run.md`
- `PICKUP-2026-05-05-execute-followup-plans.md`
- `PICKUP-2026-05-06-claude-md-memory-split.md`

PICKUP files live wherever the host project keeps plans (e.g., `~/.claude/plans/`).

## Required sections, in order

### 1. Preface (mandatory)

Two to four sentences. The single most important content in the file. Establishes:

- What was in flight at the moment the PICKUP was written.
- What is NOT the next session's job (the "do not re-author" line).
- The one or two things the next session is supposed to do.

Example:

> "Autonomous chain run for the Prolexic dashboard product is staged and ready to launch. The next session's job is to launch the chain and monitor for halt-on-decision-gate. Do not re-author plans, briefs, or operator-inputs. Everything is staged."

The "do not re-author" line is load-bearing. New Claude sessions, presented with plans and briefs, instinctively want to draft. The preface preempts that instinct explicitly.

### 2. State (mandatory)

A snapshot of where things are. What's done, what's in flight, what's not started. One-line bullets, not paragraphs. The next session reads this to orient.

Recommended sub-sections:

- **Completed:** what has shipped.
- **In flight:** what's mid-execution. For autonomous runs, the chain runner's last reported state.
- **Staged but not yet executed:** files written, fixtures placed, ready to consume.
- **Not started:** explicit, so the next session knows what's still ahead.

### 3. Decision gates (mandatory if any)

Branching choices the next session might encounter. Each gate names:

- The decision.
- Two to four options, with one-line consequences.
- The recommended default (if there is a defensible one) and the reason.
- Who decides (operator only, or operator + chain runner).

If no decision gates apply, write `None.` Do not omit the section.

### 4. Acceptance checklist (mandatory for autonomous runs and long-running work)

A short, explicit checklist the next session uses to verify the work is actually done. Bullets with checkbox shape:

```
- [ ] Chain run completed without crash
- [ ] All eight skills produced expected artifacts
- [ ] EVAL.json files all PASS or NEEDS-FIX (no BLOCK)
- [ ] Operator briefing note generated and reviewed
```

Acceptance checklists do double duty: they prevent premature "done" claims, and they tell the next session what the contract was.

### 5. Memory anchors (optional but recommended)

Bullets explaining why specific decisions were made, why specific files exist, why specific paths are the right ones. The next session reads these instead of re-deriving the reasoning from scratch.

Example:

> "Why `--max-hours 9`: chain has eight research lanes plus economics. Empirical runs took 6.5 hours; 9 gives margin without burning budget on a stuck lane."

## What a PICKUP file is NOT

- It is not a plan. Plans are forward-looking authoring guides; PICKUPs are constraint snapshots.
- It is not a status report. Status reports are descriptive; PICKUPs are prescriptive about what the next session may and may not do.
- It is not a CHANGELOG. CHANGELOGs are post-shipment; PICKUPs are mid-flight.

## Anti-patterns

- **Buried preface.** If the "do not re-author" line is not in the first paragraph, the next session will start drafting before reading it.
- **Vague acceptance checklists.** "Verify the work is done" is not actionable. Each checkbox must be machine-checkable or operator-checkable in seconds.
- **Stale PICKUPs.** A PICKUP from three weeks ago is no longer load-bearing. PICKUPs decay; if the work paused for long, write a new PICKUP rather than recycling the old one.
- **Missing decision gates.** If the work has branching choices and the PICKUP doesn't enumerate them, the next session will guess. PICKUPs must list the gates explicitly.
