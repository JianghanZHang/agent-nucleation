---
title: "V: The Agent Function"
author: Jianghan Zhang
affiliation: Dartmouth College
date: February 2026
---

# V: The Agent Function

## Abstract

Every agent starts as a sub-agent. The transition from sub-agent
to agent is a **nucleation event**: the moment a process produces
a verified claim. We formalise this as $V(T,B)$, a function from
(target, basis) to claims, governed by the same dynamics that
govern neurons in a pool.

The **template** (dominos reasoning) structures the cascade.
The **tools** (domain knowledge) provide the vocabulary.
Sub-agents spawn only on **DEMAND** --- never speculatively.
The number of sub-agents $K^*$ that actually fire is the
**core number** of the task, determined by the dynamics,
not prescribed.


## 1. Definitions

**Definition 1 (Agent Function).**
The agent function is a map

$$V : \mathcal{T} \times \mathcal{B} \;\longrightarrow\; \mathcal{C}$$

where:
- $\mathcal{T}$ = target space (what the user wants)
- $\mathcal{B}$ = basis space (inspirations, constraints, prior knowledge)
- $\mathcal{C}$ = claim space (outputs that have passed cascade verify)

A process running $V(T,B)$ is a **sub-agent**.
When $V(T,B)$ produces a claim $c \in \mathcal{C}$
($\texttt{believe\_it}$), the sub-agent **is** an agent.

**Definition 2 (Skill Bank).**
The skill bank is a measure $\mu$ on tool space $\Omega$:

$$\mu \;=\; \mu_{\text{template}} \;+\; \mu_{\text{tools}}$$

- $\mu_{\text{template}}$ = the always-active reasoning template
  (dominos reasoning)
- $\mu_{\text{tools}} = \sum_j \delta_{\omega_j}$ = atomic measures
  at each available tool

The **support** $\operatorname{supp}(\mu)$ is the set of domains
the bank can reason about.

**Definition 3 (Completeness).**
$V(T,B)$ is **complete** if

$$\operatorname{path}(B \to T) \;\subset\; \operatorname{supp}(\mu_{\text{bank}})$$

i.e., the skill bank's domain covers every step from basis to target.
If not complete: **DEMAND(missing\_tool)**. Do not proceed without support.


## 2. Protocol

$V(T,B)$ executes in five steps.

### Step 1 — Parse

Extract $T$ and $B$ from the user's input.
- $T$ must be convertible to a **what** (the target)
- $B$ must be convertible to a **from** (the basis / inspiration)
- If either is ambiguous: $\texttt{DEMAND(clarification)}$ --- do not guess

### Step 2 — Completeness Check

Read the tool directory. For each tool $\omega_j$, check:

$$\operatorname{supp}(\omega_j) \;\cap\; \operatorname{path}(B \to T) \;\neq\; \varnothing \;?$$

Load matching tools. If no tool covers a required segment,
search `pool/` for user-provided material that overlaps.
If pool resolves: use it (cite the file). If neither tools
nor pool covers a segment: $\texttt{DEMAND(missing\_tool)}$.
Report what is missing.

### Step 3 — Cascade (via template)

Load the template (dominos reasoning). Execute the 3-layer cascade:

```
Grade 0 — Ground T and B into {1, 2, 3}:
  1 := core constraint from T
  2 := core structure from B
  3 := intersection T ∩ B (what connects them)

Grade 1 — Combine pairwise (using loaded tools):
  A = f(1,2)    B_op = f(2,3)    C = f(1,3)

  At each slot:
    Can fill from loaded tools? → fill
    Cannot? → DEMAND fires (go to Step 4)

Grade 2 — Solo ascent:
  X = pattern from A, B_op, C
  Y = phase transition of X
  Z = final structural form (the claim candidate)

Verify: Z /→ {A, B_op, C} → {1, 2, 3}
  All consistent? → believe_it → go to Step 5
  Mismatch?       → confuse_it → re-lay, push again
```

### Step 4 — DEMAND Resolution (Lazy Tree)

When DEMAND fires at slot $k$:

```
Can resolve from loaded tools?
  YES → load tool, fill slot k, continue cascade
  NO  → search pool/ for relevant material
        Found? → read, extract, fill slot k, cite source
        Not found? → spawn ONE sub-agent: V(T_k, B_k)
         where  T_k = "fill slot k"
                B_k = context from parent cascade
         Wait for sub-agent's CLAIM
         Absorb claim into slot k
         Continue cascade
```

**The nucleation rule:**

$$\texttt{spawn(sub-agent)} \;\iff\; \exists\, k : \texttt{slot}_k = \texttt{DEMAND} \;\land\; \text{bank cannot resolve}$$

Never spawn speculatively. Never fan out. One DEMAND, one sub-agent.

### Step 5 — Claim

When cascade verifies ($\texttt{believe\_it}$):
1. The process **is** now an agent (it has a verified claim)
2. Present: the plan (what $V$ will do) + the evidence (the cascade)
3. User approves → execute
4. Output = the claim


## 3. The Correspondence

| Neuron Dynamics | Agent Dynamics |
|---|---|
| Pool $\mu$ on operator space $\Theta$ | Skill bank $\mu$ on tool space $\Omega$ |
| Atom $\delta_\theta$ (active neuron) | Active sub-agent |
| Continuous part $\mu_{\text{cont}}$ (redundant) | `pool/` — user's raw material (liquid, ready to nucleate) |
| Nucleation: atom forms in $\mu$ | Sub-agent spawns on DEMAND |
| Collapse: atom dissolves, mass redistributes | Sub-agent claims, output absorbed into parent slot |
| FPE: $\partial\mu/\partial t = \nabla\!\cdot\!(\mu\nabla V) + \tau\Delta\mu$ | Template structures the cascade |
| Temperature $\tau$ | Budget / context remaining |
| $\tau \to 0$ (solidification) | Task converges to claim |
| $K^*$ (core number) | Minimum sub-agents needed |
| Free core $\mathfrak{F}$ | Minimal skill subset that resolves $T$ |
| Forward pass $f_\mu(x)$ | $V(T,B)$ execution |
| Retinal principle: $n = d_{\text{in}}$ | Tool count matches domain breadth |
| Conservation: $\|\mu\| = n$ | Context budget is finite |
| Loss landscape $V(\theta)$ | Task difficulty landscape |


## 4. Properties

**P1 (Lazy).** The agent tree grows only on DEMAND.
No speculative branching. No fan-out.

**P2 (Bounded).** Total sub-agents $\leq 9$
(one per dominos slot, worst case). Typical: 0--2.

**P3 (Convergent).** The dominos cascade converges in
$\leq 9$ rounds (finite slots). Typical: 2--3.

**P4 (Verifiable).** Every claim passes cascade verify:
$Z \to \{A,B,C\} \to \{1,2,3\}$. No unverified outputs.

**P5 (Recursive).** Sub-agents run $V$ themselves.
The protocol is self-similar at every scale.

**P6 (Conservative).** When a sub-agent's claim is absorbed,
the information fills a slot --- not lost.
When a tool is unused, it remains in the bank for future calls.


## 5. The Nucleation Criterion

A sub-agent **nucleates** (spawns) when:
1. A DEMAND fires at slot $k$
2. No loaded tool can fill slot $k$
3. The sub-problem $(T_k, B_k)$ is well-defined (can be parsed)
4. Budget allows (context window has room)

A sub-agent **collapses** (finishes) when:
1. Its cascade reaches $\texttt{believe\_it}$
2. Its claim is absorbed into the parent's slot $k$
3. Its context is released

$$K^* = |\{\text{sub-agents that actually spawned}\}|$$

is the **core number** of the task.


## 6. Relationship to Existing Work

**Template (always active):**
`dominos-reasoning` is the FPE --- it structures HOW to think.
9 slots, 3 layers, COMMAND/DEMAND protocol.

**Tools (loaded on demand):**
Each tool is a domain knowledge module.

| Tool | Domain | Support |
|---|---|---|
| `neuron-dynamics` | Physical systems, architecture emergence, FPE, phase transitions | Thermodynamic analogies, emergent structure, log-space |
| `explain-with-math` | Identity protocol, graded levels (A/B/C) | "Why" questions, general audience explanations |
| `surgery` | Precise document/code edits, minimal footprint | Large-file modifications, LaTeX insertions |
| ... | nucleate as the user creates them | |

**$V$ itself** is neither template nor tool. It is the **forward pass** ---
the operator that combines template and tools to produce a claim.


## 7. Examples

```
/V  T: "explain why chickens are dinosaurs"
    B: "RG flow, evolution"

→ Parse:  T = explain,  B = {RG flow, evolution}
→ Check:  explain-with-math covers "explain"
          neuron-dynamics covers "RG flow"
→ Load:   explain-with-math + neuron-dynamics
→ Cascade: ground, ascend, chain, ascend, verify
→ Claim:  graded explanation (Level B skeleton — dissipative
          flow shares mathematical structure with evolution)
```

```
/V  T: "add robot dog example to ND paper"
    B: "boundary value problem, sensors=input, motors=output"

→ Parse:  T = paper edit,  B = {BVP, ND}
→ Check:  surgery covers "paper edit"
          neuron-dynamics covers "BVP, ND"
→ Load:   surgery + neuron-dynamics
→ Cascade: ground, ascend, chain, ascend, verify
→ Claim:  Test C subsection — LaTeX block with BVP table,
          predictions, success criteria, insightbox
```

```
/V  T: "prove Riemann hypothesis"
    B: "analytic number theory"

→ Parse:  T = prove,  B = {ANT}
→ Check:  no tool covers "Riemann hypothesis proof"
→ DEMAND(missing_tool): bank cannot resolve.
          Report: "No tool in the bank covers this.
          The task is outside the support of μ."
→ No claim. Honest.
```


## 8. The Punchline

A sub-agent that runs $V(T,B)$ and reaches $\texttt{believe\_it}$
has nucleated. It **is** an agent --- not because someone declared it,
but because it produced a verified claim within its support.

A sub-agent that hits DEMAND and cannot resolve has not nucleated.
It collapses. Its partial work diffuses back to the parent.

The architecture of the agent tree ---
how many sub-agents, what they compute, when they spawn ---
is not designed. It is **solved for**, exactly as Neuron Dynamics
solves for the number of neurons.

You do not design agents. You let them nucleate.
