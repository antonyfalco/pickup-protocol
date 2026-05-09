# pickup-protocol — PITCH

## Problem

Plans tell future-you *what to do*. PICKUPs tell future-you *what not to redo*.

Context handoffs across Claude Code sessions are fragile. A new session, presented with in-flight work, defaults to re-authoring: "let me draft a plan," "let me check the structure," "let me think through the approach." That instinct burns thirty minutes per handoff before the new session realizes everything is already staged.

The solution is not "better plans." Plans are forward-looking; they don't address the redo problem. The solution is a separate artifact whose entire purpose is to constrain what the next session is allowed to do.

A working pattern has emerged across multiple real PICKUP files (autonomous run handoffs, multi-session plan execution, doctrine refactors). It has a consistent shape: a "do not re-author" preface, decision gates with context, post-run acceptance checklists, memory anchors. Nobody else has codified it.

## What ships

- **`REF_pickup-shape.md`** — the canonical structure. Preface, state, decision gates, acceptance checklist, memory anchors. Short, opinionated.
- **`/pickup` slash command** — drafts a PICKUP file from the current chat state. Detects what was decided versus in flight. Names what files have been staged. Calls out what the next session must not re-author.
- **`pickup-parse` skill** — the inverse. The receiving session reads a PICKUP file and ingests its constraints deterministically. Outputs a one-line acknowledgment: "I have read PICKUP-2026-05-04. I will not re-author plans, briefs, or operator-inputs. Decision gates: <list>."
- **Three templates** — autonomous-run handoff, multi-session plan execution, doctrine refactor. Each is a working starting point with the structure pre-shaped.

## Distinctive angle

Plans and PICKUPs are dual artifacts. Plans tell future-you what to do. PICKUPs tell future-you what not to redo. The asymmetry is the value, and nobody has named it. Pairs naturally with `auto-mode-guardrails` — autonomous runs need PICKUPs more than interactive ones do, because there's no operator at the keyboard to catch the redo instinct in real time.

## Surface

Tiny. One slash command, one parse skill, one REF, three templates. Ships as a Claude Code plugin (or a directory you copy into `~/.claude/commands/`).

## First users beyond Tony

- Anyone running multi-session work in Claude Code.
- Anyone whose conversations span a context-window reset.
- Teams handing work between humans through Claude Code (one engineer kicks off a long-running task, another picks it up the next day).
- Plausibly the Claude Code team themselves — `/pickup` could become a built-in.

## Status

v0.1 scaffolding lands via PR #1. Next work: a real test where one Claude session writes a PICKUP file via `/pickup`, a fresh Claude session reads it via `pickup-parse`, and the redo instinct measurably stays suppressed for the duration of the resumed work.
