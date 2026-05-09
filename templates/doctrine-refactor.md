# PICKUP-<YYYY-MM-DD>-<refactor-name>.md

<!--
Template: doctrine refactor.
Use when refactoring rules, conventions, or governance docs (CLAUDE.md
splits, evaluator-family contract migrations, plan-naming convention
changes). The work is mostly editorial; the risk is dropping rules
silently.
-->

## Preface

<2-3 sentences>

Doctrine refactor `<short name>` is partially complete. <N> of <M> rules
have been migrated; <K> rules are still in their old location. The next
session's job is to finish the migration without losing or duplicating
rules. Do not re-derive the rules from scratch; the audit table below maps
old → new for every rule.

## State

### Audit table

| Rule | Original location | New location | Status |
|------|-------------------|--------------|--------|
| <rule name> | <path:line> | <path:line> | DONE |
| <rule name> | <path:line> | <path:line> | DONE |
| <rule name> | <path:line> | <new path TBD> | IN FLIGHT |
| <rule name> | <path:line> | <new path TBD> | NOT STARTED |
| <rule name> | <path:line> | DELETE (superseded by <rule>) | NOT STARTED |

### Files modified

- `<path>` — N rules added, M rules removed
- `<path>` — N rules added

### Files not yet modified

- `<path>` — K rules pending migration

## Decision gates

1. **Rule scope ambiguity: <rule name>.**
   - Option A: scope it to the global file (`~/.claude/CLAUDE.md`).
   - Option B: scope it to the project file (`<project>/CLAUDE.md`).
   - Default: <option> because <reason>.

If none apply: `None.`

## Acceptance checklist

- [ ] Audit table marks every rule DONE or DELETE
- [ ] No rule appears in both the original and new locations (no duplication)
- [ ] No rule is dropped silently (every removed rule has a successor or is explicitly DELETE)
- [ ] Diff between old and new file states reviewed by operator
- [ ] Cross-references from other docs updated

## Memory anchors

- Why this refactor: <reason>
- Why this scope split: <reason>
- Why rules `<X>` and `<Y>` are merging: <reason>
