# PICKUP-<YYYY-MM-DD>-<run-name>.md

<!--
Template: autonomous-run handoff.
Use when handing off a long-running autonomous chain to a future session
(or a future operator) for monitoring and verification.
-->

## Preface

<2-3 sentences>

The autonomous chain `<chain name>` for `<product slug>` is staged and ready
to launch. The next session's job is to <launch and monitor / verify
acceptance / handle halt-on-decision-gate>. Do not re-author plans, briefs,
or operator-inputs. Everything is staged.

## State

### Completed

- Plan: `<path to plan file>`
- Brief: `<path to brief>` (locked, do not edit)
- Operator inputs: `<path>` (locked)
- Fixtures: `<count>` files staged at `<path>`, frontmatter verified

### Staged but not yet executed

- Chain command: `<exact shell invocation>`
- Output directory: `<expected output path>`
- Budget: `--max-hours <N> --max-usd <N>`

### Not started

- Acceptance checklist verification (post-run)
- Operator briefing note (post-run)

## Decision gates

1. **Halt on NEEDS-FIX evaluator verdict.**
   - Option A: pause and surface the verdict to the operator.
   - Option B: proceed with `--override-prior-gate` if the verdict's recommended-override prose applies.
   - Default: A. Operator decides per-halt.

2. **Budget tripwire fires.**
   - Option A: accept partial result, run housekeeping skills only.
   - Option B: raise threshold and resume.
   - Default: A unless the operator pre-authorized B.

## Acceptance checklist

- [ ] Chain run completed without crash
- [ ] All declared skills produced expected artifacts
- [ ] EVAL.json files all PASS or NEEDS-FIX (no BLOCK)
- [ ] Output directory has expected file shape (cross-reference plan)
- [ ] Operator briefing note drafted

## Memory anchors

- Why `--max-hours <N>`: <reason>
- Why this preset: <reason>
- Why fixtures live at `<path>`: <reason>
