# pickup-protocol

Context-handoff artifacts for multi-session Claude Code work.

Plans tell future-you *what to do*. PICKUPs tell future-you *what not to redo*. That asymmetry is the whole value, and it's the reason fresh sessions waste thirty minutes re-authoring work that's already staged.

This repo ships:

- `REF_pickup-shape.md` — the canonical structure (preface, state, decision gates, acceptance checklist, memory anchors).
- `/pickup` — a slash command that drafts a PICKUP file from current chat state.
- `pickup-parse` — a skill that the receiving session uses to ingest a PICKUP deterministically and acknowledge its constraints in one line.
- Three templates: autonomous-run handoff, multi-session plan execution, doctrine refactor.

See [PITCH.md](PITCH.md) for the full pitch. See [REF_pickup-shape.md](REF_pickup-shape.md) for the canonical structure.

## Status

Early. v0.1 scaffolding lands via PR #1.

## License

MIT
