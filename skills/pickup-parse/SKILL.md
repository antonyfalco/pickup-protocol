---
name: pickup-parse
description: Read a PICKUP file at session start and acknowledge its constraints in one line. Suppress the redo instinct.
---

## When to use

The receiving session in a multi-session handoff. The operator opens a fresh chat and points to a PICKUP file (e.g., "we're resuming the work in `~/.claude/plans/PICKUP-2026-05-04-prolexic-dashboard-autonomous-run.md`"). This skill reads the file and produces a structured acknowledgment.

The point of this skill is not to summarize the PICKUP. The operator can read the file. The point is to make the receiving Claude session **commit explicitly to its constraints** before starting work.

## Behavior

1. Read the PICKUP file.
2. Verify it matches `REF_pickup-shape.md` structure (Preface, State, Decision gates, Acceptance checklist, optional Memory anchors). If sections are missing or malformed, surface that as the first thing — do not silently fill in.
3. Emit a one-paragraph acknowledgment in the chat:

```
I have read PICKUP-2026-05-04-prolexic-dashboard-autonomous-run.md.

I will not: re-author plans, briefs, or operator-inputs. The chain is staged.
My job: launch the chain via `podium run preset:from-scratch ...` and monitor for halt-on-decision-gate.

Open decision gates: 1 (chain duration --max-hours, default 9).
Acceptance checklist: 4 items, none verified yet.
```

4. Do not start the work yet. The acknowledgment is a checkpoint. The operator says "go" before any tools run.

## What it does not do

- Does not modify the PICKUP file. Read-only.
- Does not auto-launch the staged work. The acknowledgment is explicit; the operator unblocks.
- Does not compress or paraphrase the PICKUP's "do not re-author" line. That line is quoted verbatim.
- Does not infer state not stated in the file. If the file marks a piece of state `<unknown — operator should fill in>`, the acknowledgment surfaces that gap.

## Failure-mode notes

- If the PICKUP file is older than 14 days, the acknowledgment surfaces that explicitly: "This PICKUP is N days old. Confirm it is still load-bearing before proceeding." Stale PICKUPs are dangerous; they describe state that may have changed.
- If the PICKUP references files that no longer exist, surface that as a structural failure. The PICKUP cannot be valid if its referenced state is gone.
- If the PICKUP is malformed (missing required sections), refuse to acknowledge. Ask the operator to repair the PICKUP first. Acknowledging a malformed PICKUP is the same as guessing.
