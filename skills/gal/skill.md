---
name: gal
description: >
  Generative Adversarial Library — the framework for online self-supervised
  learning without weight updates. Use when reasoning about: adversarial games
  with exact oracles, library-based learning, filtration graphs, A* on evidence
  spaces, token complexity, creativity as phase transition, or the skill-knowledge
  separation. Provides the mathematical vocabulary for the GAL paper.
license: MIT
metadata:
  author: Jianghan Zhang
  email: Jianghan.Zhang.gr@dartmouth.edu
  version: "0.1"
  grade: "0"
  role: tool
---

# GAL: Generative Adversarial Library

## Core Objects

### 1. The Filtration Graph G = (V, E)
- V = {F ⊆ Evidence : F reachable from F₀}
- E = {(F, F') : ∃ tool u, F' = F ∪ ΔF(u), ΔF(u) ≠ ∅}
- G is a DAG (F grows strictly on each edge)
- A* ordering: f(F_t) = g(F_t) + h(F_t) = tokens_spent + V(F_t)

### 2. Three Players
- Builder (∃loise): generates candidates (patches, proofs)
- Adversary (∀belard): generates counterexamples
- Oracle: exact verifier (Lean checker, pytest, cargo test)
- σ ∈ {+1, -1, 0}: spin (oracle's verdict)

### 3. Isomorphism Library I
- Entry: (analogy, transition, spin, sigma_level, scope)
- analogy: "A:B ≅ C:D" (structural correspondence)
- transition: "M₀ → M₁" (which component to which)
- Append-only: I_t ⊆ I_{t+1} (no forgetting)
- Query: LLM is the semantic matcher (inject into context)

### 4. Three-Level Claims
- Level 2 CONJECTURE: direction (persists in library, across tasks)
- Level 1 HYPOTHESIS: testable claim (per-task, one experiment decides)
- Level 0 HEURISTIC: framework approximation (hardcoded, validated long-term)

### 5. Token Complexity
- T_GAL(τ) = O(m^Σ) where m = mass gap, Σ = quantifier depth
- Compression ratio: ρ = T_null / T_GAL
- Information efficiency: η = K(gold) / T_actual

## Key Theorems

1. **No forgetting**: I is monotone → past insights never lost
2. **Regret**: R_T ≤ Hρ√T (OMD convergence)
3. **Reachability**: connected + acyclic prereqs + budget ≥ d·m + A* → reaches target
4. **Token complexity**: Σ_k → T = O(m^k), AND decomposition: 2^m → km
5. **Creativity**: t* = inf{t : posterior mode jumps between π₀(P) components}
6. **RLHF barrier**: g* = Fisher(π_ref · e^{r/β}) is FIXED; framework provides metric freedom

## The Skill-Knowledge Separation

- KNOWLEDGE (library): structural correspondences, domain-specific, no gradient, no forgetting
- SKILL (protocol): how to use library + tools, domain-general, small finetune (~1M tokens)
- STP needs 51.3B tokens (knowledge + skill). GAL needs ~1M (skill only). 50,000x less.

## When to use this tool

- Formalizing any game-theoretic learning framework
- Reasoning about adversarial generation with exact oracles
- Analyzing token complexity and search efficiency
- Designing library-based learning systems
- Connecting gauge theory to learning theory
