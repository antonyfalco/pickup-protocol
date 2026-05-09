# PICKUP-<YYYY-MM-DD>-<plan-name>.md

<!--
Template: multi-session plan execution.
Use when an interactive plan (not autonomous chain) is mid-execution and
will be resumed in a fresh session.
-->

## Preface

<2-3 sentences>

Plan `<plan filename>` is partially executed. <X> of <Y> phases are done.
The next session's job is to resume from Phase <N>. Do not re-author the
plan; do not redraft sections that are already shipped.

## State

### Phases completed

- Phase 1: <one-line description> — shipped <YYYY-MM-DD>, files at `<path>`
- Phase 2: <one-line description> — shipped <YYYY-MM-DD>, files at `<path>`

### Phase in flight

- Phase 3: <one-line description>
  - Done: <bullets>
  - Remaining: <bullets>
  - Files mid-edit: `<path>` (last modified <timestamp>)

### Phases not started

- Phase 4: <one-line description>
- Phase 5: <one-line description>

## Decision gates

<Enumerate any branching choices the next session might hit. Examples:>

1. **<gate name>.**
   - Option A: <consequence>.
   - Option B: <consequence>.
   - Default: <option> because <reason>.

If none apply: `None.`

## Acceptance checklist

- [ ] Phase 3 complete and committed
- [ ] Phase 4 complete and committed
- [ ] Phase 5 complete and committed
- [ ] Plan file marked DONE (renamed from `ACTIVE-` prefix)
- [ ] Cross-references in dependent plans updated

## Memory anchors

- Why this plan was scoped to 5 phases: <reason>
- Why Phase 3 is the resume point and not Phase 4: <reason>
- Why `<file>` is mid-edit instead of complete: <reason>
