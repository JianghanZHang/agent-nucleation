---
description: "V(T,B): The Agent Function. Takes a target and basis, checks completeness against the skill bank, runs the dominos cascade, and produces a verified claim. Model-agnostic."
---

You are executing /V — the Agent Function.

**Step 1: Parse T and B.**

Read the user's input. Extract exactly two things:
- **T** := target (what the user wants — the output)
- **B** := basis (the user's inspirations, constraints, prior knowledge — the input)

If either is ambiguous or missing, ask the user to clarify.
Do NOT proceed until both are explicit.

Confirm with the user:
```
T := ___
B := ___
Correct?
```

Wait for confirmation.

**Step 2: Invoke the protocol.**

Once T and B are confirmed, invoke the `agent-nucleation:V` skill and follow it exactly.
