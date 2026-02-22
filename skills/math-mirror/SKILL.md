---
name: math-mirror
description: Use when a DEMAND requires mathematical computation, symbolic verification, or translating a concept into its mathematical structure. Also use when the cascade needs a verified equation, identity, or derivation that cannot be resolved by reasoning alone.
---

# Math Mirror

## Overview

**Grade 0 tool.** Does math. Only math. Verifies its own output.

When a slot in the cascade DEMANDs a mathematical computation — an equation to check, an identity to verify, a structure to find — this tool nucleates, computes, verifies, and collapses back.

The mirror never advises. Never interprets. Reflects mathematical structure.

## When to Load

- A slot DEMANDs: "what is the equation for X?"
- A slot DEMANDs: "verify that A = B"
- A slot DEMANDs: "what mathematical structure IS this?"
- A slot DEMANDs: "compute derivative / determinant / roots / ..."
- Phase 2 needs a verified equation before ascending to structure

## Protocol

### 1. RECEIVE DEMAND

From parent cascade: what math is needed? Extract the precise question.

### 2. COMPUTE

Use the math-mirror-ai framework:

```bash
# If model is trained and available:
python -c "
from math_mirror.verifier import MathVerifier
V = MathVerifier()
print(V.check_identity('YOUR_EXPRESSION_HERE'))
"
```

If model is not yet trained: use SymPy directly as the computation engine. The verifier is always available (Phase 0 is standalone).

```python
from math_mirror.verifier import MathVerifier
V = MathVerifier()

# Check an identity
V.check_identity("sin(x)**2 + cos(x)**2 = 1")  # True

# Check if expression is valid math
V.is_valid_math("d/dx(x**3)")  # True

# Batch verify
V.check_batch(["2+2=4", "3*7=21", "1+1=3"])
# {'total': 3, 'valid': 2, 'invalid': 1}
```

### 3. VERIFY

Every output passes through the verifier gate. No exceptions.

- **ACCEPT(result)**: verifier confirms. Return result to parent slot.
- **DEMAND(what_missing)**: computation needs more input. Propagate DEMAND upward.
- **REJECT**: verifier says no. Report honestly: "computation failed verification."

### 4. COLLAPSE

File marker in agent_table/. Result absorbed into parent slot. Mirror goes dormant.

## What This Tool IS

- A symbolic computation engine (SymPy)
- A self-validated data generator (bootstrap)
- A byte-level transformer trained on pure math (when trained)
- A verification gate that rejects unverifiable outputs

## What This Tool IS NOT

- An advisor (it doesn't tell you what to do)
- A language model (it doesn't generate natural language)
- An online learner (it doesn't learn from your conversations)

## Location

```
/Users/zhangjianghan/Documents/GitHub/math-mirror-ai/
```

Install: `pip install -e /Users/zhangjianghan/Documents/GitHub/math-mirror-ai/`

## The Rule

The mirror does math. Only math. If the DEMAND is not math, this is the wrong tool.
