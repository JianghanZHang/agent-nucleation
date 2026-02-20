---
name: explain-with-math
description: Use when the user asks "why does X work?", "explain X to me", "how does X work simply?", "ELI5", or wants any phenomenon explained to a general audience by showing the mathematical structure behind it. Also use when the user wants to make a technical concept accessible without dumbing it down.
Author: Jianghan Zhang
Email: Jianghan.Zhang.gr@dartmouth.edu
---

# Explain With Math

## Overview

Take any "why" and show the math IS the thing. Not analogy — identity.

**Core axiom:** Math doesn't describe the world. Math IS the world's structure. To explain any "why", find the math that IS the thing, show the thing, and the "why" resolves.

**This is a rigid skill.** Follow all five phases in order.

## The Rule

**Never use an analogy where you can use an identity.**

- BAD: "Gravity is LIKE a ball on a rubber sheet."
- GOOD: "Gravity IS curvature. Curvature means: parallel paths converge. Watch two ants walking north from the equator — they start parallel, they collide at the pole. That's curvature. That's gravity."

The test: can you replace "is like" with "is"? If yes, do it. If no, you don't understand the math yet — go back to Phase 2.

## Protocol

### Phase 1: STRIP

Take the "why" question. Strip it to one sentence. What is actually being asked?

- Remove qualifiers, context, preamble
- The sentence must start with "Why" or be convertible to a "why"
- If the question is "how", convert: "how does X work?" → "why does X have to work this way?"

Write it down. One line.

### Phase 2: IDENTIFY

What mathematical object captures this? Name it precisely. One object.

Candidates:
- An equation (F = ma, ∂μ/∂t = ∇·(μ∇V) + τΔμ)
- A symmetry (rotational, translational, gauge)
- A conservation law (energy, momentum, mass, probability)
- A fixed point or attractor (equilibrium, free core)
- A non-autonomous flow (time-varying dynamics: evolution, annealing, RG flow — the map itself changes with time/scale. Yields attractor *sets*, not unique fixed points. Flag when using.)
- A phase transition (melting, condensation, symmetry breaking)
- A boundary condition (what's forced at the edges)
- A constraint (what CAN'T happen, which forces what DOES)
- A counting argument (pigeonhole, dimension, degree of freedom)

Pick ONE. If you need two, the question hasn't been stripped enough — go back to Phase 1.

### Phase 3: GROUND

Find the simplest physical thing that IS this math. Not a metaphor — a literal instance.

Requirements:
1. **Touchable.** Something the audience has touched, seen, eaten, heard, or done.
2. **Identity.** The math is not "applied to" the thing — the thing IS the math. The orange-with-sticks IS the crystal lattice. The spinning skater IS angular momentum conservation.
3. **Minimal.** The simplest instance. If a coffee cup works, don't use a black hole.

If you can't find a ground: you don't understand the math yet. Go back to Phase 2 and pick a different object.

### Phase 4: WALK

Three steps. Each step: max three sentences.

**Step 1 — SHOW:** Show the physical thing. Everyone agrees it works this way. No math words yet.

**Step 2 — NAME:** Name what's happening. Introduce the mathematical structure. Every technical word must be followed immediately by "which means [thing they can see]."

**Step 3 — ANSWER:** Answer the original "why." The structure FORCES this answer. Not "it turns out that..." but "it HAS to be this way because..."

The "why" is answered when the audience sees: it couldn't have been otherwise. The constraint/symmetry/conservation/equation leaves no room.

### Phase 5: HONEST CHECK

Three questions. Answer each. If any fails, fix it before presenting.

1. **Identity test (graded).** Three levels — claim the strongest one that's honest:
   - **Level A — Same system.** Ground and target are the same physical/mathematical object. (Oranges-with-sticks IS the crystal lattice. Spinning skater IS angular momentum conservation.) Claim "is."
   - **Level B — Same skeleton.** Ground and target are different physical substrates but share the same equation class / mathematical structure. (Stock reduction and theropod evolution both follow dissipative iteration → attractor. Different systems, same skeleton.) Claim "shares the mathematical skeleton of" and name the shared structure. Do NOT claim "is" — that's overclaiming. Level B is strong. It's not analogy.
   - **Level C — Analogy.** The structural match breaks under scrutiny. Different equations, just superficial resemblance. REJECT. Go back to Phase 2.

   If you chose a non-autonomous flow in Phase 2: you get attractor *sets*, not unique fixed points. Do not claim "unique fixed point" unless the dynamics is actually autonomous and contractive. "Attractor set under time-varying constraint" is the honest claim.
2. **Age test.** Would a curious 14-year-old follow this? If not, simplify. (Not dumb down — simplify. Remove unnecessary steps, not necessary depth.)
3. **Why test.** Did I answer "why it HAS to be this way" or just "what happens"? The "what" is observation. The "why" is the constraint that forces it. If I only said what, go back to Phase 2 — I haven't found the constraint yet.

## Worked Example

**Q: Why does ice float?**

**STRIP:** Why is solid water less dense than liquid water?

**IDENTIFY:** Constraint — the hydrogen bond angle (104.5°) forces a hexagonal crystal structure with more empty space than the disordered liquid. The math: a fixed-angle constraint on a packing problem.

**GROUND:** Oranges in a box.

**WALK:**

1. **SHOW.** Pour oranges randomly into a box — they tumble into gaps, pack tight, fill about 64% of the space. Now glue sticks between them so every orange must touch exactly four neighbours at a fixed angle. Gaps open everywhere. The organised pile is BIGGER than the random pile for the same number of oranges.

2. **NAME.** The fixed angle is a constraint. In math: when you force a local rule (every molecule bonds at 104.5°), the global structure is determined — a hexagonal lattice with built-in voids. The constraint reduces the packing density. Liquid water has no angle constraint — molecules tumble freely, pack tight. Solid water is locked into the lattice.

3. **ANSWER.** Ice floats because the bond angle is 104.5°. Not 109.5° (tetrahedral — that would pack tighter). Not random. This specific angle forces hexagonal gaps. Gaps mean less dense. Less dense means it floats. The "why" is the angle: a geometric constraint that leaves no room for a denser solid.

**HONEST CHECK:**
1. Identity? Level A — the oranges-with-sticks IS the crystal lattice. Same system (constrained packing). ✓
2. 14-year-old? Oranges in a box: yes. ✓
3. Why not what? The bond angle FORCES the gaps. It couldn't be otherwise. ✓

**Level B example (for contrast):**

Q: "Why is a chicken basically a dinosaur?" IDENTIFY: non-autonomous dissipative flow (selection pressure varies over 66 Myr). GROUND: reducing a stock. HONEST CHECK #1: Level B — stock reduction and theropod evolution share the same mathematical skeleton (dissipative iteration → attractor set), but are different physical substrates. Claim "shares skeleton," not "is." The hardened punchline: chickens don't *resemble* dinosaurs — chickens ARE dinosaurs (Aves ⊂ Theropoda). The retention is inheritance + contraction under constraint.

## When NOT to Use

- **Formal proofs needed:** Use `/dominos-reasoning` instead. This skill is for intuition, not rigour.
- **"How to" questions:** "How do I train a neural network?" is not a "why." Use a tutorial approach.
- **Unknown answers:** If the "why" is genuinely unsolved (e.g., "why is there something rather than nothing?"), say so honestly. Don't fake a ground.
- **The audience IS expert:** If they want equations, give equations. This skill is for when the math needs to be SHOWN, not just WRITTEN.
