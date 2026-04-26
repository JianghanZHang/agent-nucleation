# /library — Isomorphism Library

Persistent, append-only structural knowledge. Grows across tasks. Never deleted.

## Files

- `iso_library.json` — the main library (global + repo-scoped entries)
- Future: `domains/lean-math.json`, `domains/python-code.json` (domain-specific)

## Rules

1. **Append-only**: entries are NEVER modified or deleted
2. **Auto-collected**: the Stop hook checks every task completion
3. **Versioned**: git tracks the growth history
4. **Shareable**: JSON format, can be merged across users/repos

## Usage

```
/library recall  — show relevant entries for current task
/library learn   — record new insight from completed task
/library stats   — show library size and distribution
```
