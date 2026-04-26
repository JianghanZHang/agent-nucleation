---
name: library
description: >
  Isomorphism library — persistent structural knowledge that grows across tasks.
  Use when: recalling past insights before starting a task, recording a new insight
  after completing one, or checking if a current problem matches a known pattern.
  Automatically invoked by hooks on task completion.
license: MIT
metadata:
  author: Jianghan Zhang
  email: Jianghan.Zhang.gr@dartmouth.edu
  version: "0.1"
  grade: "0"
  role: tool
---

# Isomorphism Library

## Overview

A persistent, append-only store of structural correspondences learned from experience.
Each entry records: what pattern was seen, what solution component worked (or didn't),
and which perspective discovered it.

**Core principle:** Knowledge lives in the library. Not in the model weights.
The library only grows. No forgetting. Ever.

## Location

The library lives at `library/iso_library.json` in the repo root.
If absent, it starts empty. It is NEVER deleted — only appended to.

## Entry Format

```json
{
  "analogy": "A:B ≅ C:D",
  "transition": "M₀(what failed) → M₁(what worked)",
  "frame": "which perspective found this",
  "task_id": "where discovered",
  "spin": 1,
  "sigma_level": 2,
  "scope": "global"
}
```

Fields:
- **analogy**: the structural correspondence in "A:B ≅ C:D" format
- **transition**: which component of solution space was reached
- **frame**: which thinking perspective led to the insight
- **task_id**: which task produced this entry
- **spin**: +1 (confirmed works) or -1 (confirmed doesn't work)
- **sigma_level**: 1-4 (complexity of the task that produced this)
- **scope**: "global" (transfers across repos) or "repo:<name>" (specific)

## When to Use

### RECALL (before starting a task)

At the start of V(T, B), check if the library has relevant entries:

```
Read library/iso_library.json.
For each entry, check: is this problem structurally similar?
If match found:
  - Inject as context: "[LIBRARY] Past insight: {analogy}"
  - Use the transition as initial direction
  - This converts O(|π₀|) search into O(1) lookup
```

### LEARN (after completing a task)

After V(T, B) produces a claim:

```
If spin = +1 (success):
  Extract: what was the structural insight?
  Write entry with spin=+1 to library/iso_library.json

If spin = -1 (failure):
  Extract: what approach was tried and failed?
  Write entry with spin=-1 to library/iso_library.json (negative evidence)
```

### COMPOSE (reasoning about entries)

When two entries can be combined:
```
If entry1: A ≅ B (spin=+1)
And entry2: B ≅ C (spin=+1)
Then suggest: A ≅ C (transitivity)
```

### PRUNE (avoid repeated failures)

```
If 3+ entries for same pattern have spin=-1:
  Stop suggesting this pattern.
  Flag: "pattern X has failed 3+ times, consider fundamentally different approach"
```

## Hook Integration

The library is automatically consulted and updated by hooks:

1. **On task start (Stop hook)**: Guardian checks if library was consulted
2. **On file write to agent_workspace (PostToolUse)**: Check if result should be recorded
3. **On task completion (Stop hook)**: Guardian ensures new insight was appended

## Example Session

```
[TASK] Fix merge ordering in django

[LIBRARY RECALL] Found 2 relevant entries:
  1. [+] "overclaimed exactness ≅ DPI bound" (Σ₂, global)
  2. [-] "merge : expression fix ≅ wrong approach" (Σ₄, repo:django)

[DIRECTION] Entry 2 says local patching FAILED before.
  Try: search for existing utilities (entry 2 was Σ₄ = needs restructure)

... (task execution) ...

[TASK RESOLVED]

[LIBRARY LEARN] Appending:
  analogy: "N-way merge ordering ≅ topological sort utility"
  transition: "M₀(patch merge) → M₁(import topo_sort + rewrite)"
  frame: "Archaeologist: search codebase for existing algorithms"
  spin: +1, sigma: 4, scope: "repo:django"
```
