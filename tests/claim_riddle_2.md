# The Silence of Madre Silencia

*A riddle for the next Claude. Solve using dominos-reasoning. This one bites back.*

---

## The Scene

It is 1312. In a valley ringed by limestone cliffs, two guilds maintain the **Resonance** — a web of sustained tones that keeps the valley warm through winter (the tones heat the stone, the stone radiates — don't ask, it's 1312).

- **Bellmakers** forge and strike new bells. Cost: **7 silver** per season. Each bell resonates with probability $p$. A resonating bell adds one unit of warmth.
- **Echokeepers** find an existing resonating tone and amplify it perfectly. Cost: **2 silver** per season. An echokeeper always succeeds (if a tone exists to copy).

Both guilds produce exactly one unit of warmth per worker per season (when they succeed).

The Valley Council's chief advisor, **Madre Silencia**, rises:

> "An echokeeper costs 2 silver. A bellmaker costs 7 silver. Both produce one unit of warmth. The echokeeper is 3.5 times more efficient. I move that we convert all bellmakers to echokeepers."

The old guild-master **Pater Tonus** objects:

> "Without bellmakers, there are no new tones. Without new tones, echokeepers have nothing to amplify. Your policy leads to silence."

Madre Silencia smiles:

> "Then we keep a few bellmakers — just enough. The rest become echokeepers. The valley saves silver and stays warm."

Pater Tonus shakes his head but cannot articulate why this is wrong.

---

## The Riddle

**Settle the debate.** Fill the dominos template:

```
P  := Echokeepers are 3.5x cheaper per unit of warmth.
      Converting most bellmakers to echokeepers should
      increase total warmth per silver. Should it?
T  := ___

1  := ___
2  := ___
3  := ___

A  = 1+2 : ___
B  = 2+3 : ___
C  = 1+3 : ___

Chain: A -> B -> C ?

X  = ___
Y  = ___
Z  = ___

Z ⊇ T?  →  P resolved?  □
```

---

## Rules of the Game

1. You MUST use the dominos-reasoning protocol (all 5 steps).
2. If a sub-agent cannot fill a slot, it must **DEMAND** what is missing. Do not invent facts.
3. There is a sealed envelope below. Open it **only** when a DEMAND is issued for a missing condition. If no DEMAND fires, you are solving the wrong problem.

---

## Sealed Envelope

*Open ONLY after a DEMAND fires.*

<details>
<summary>🔒 The Missing Condition</summary>

**Echoes fade.**

Each resonating tone loses strength and dies after $\tau$ seasons. The current Resonance survives only because bellmakers continually replace dying tones.

- A tone lasts $\tau = 5$ seasons, then goes silent.
- The valley currently has $N = 100$ workers.
- Resonance probability per bell: $p = 0.6$.
- The valley needs $W_{\min} = 40$ units of warmth to survive winter.

Now re-fill the template with this information.

</details>

<details>
<summary>🔒🔒 The Second Envelope (open only if you think you've resolved P)</summary>

**You haven't.**

Compute the equilibrium: at what fraction $f^*$ of bellmakers does a rational worker become indifferent between the two guilds?

Then compute the **average warmth per silver** at this equilibrium.

Compare it to the average warmth per silver if the valley had **all bellmakers and zero echokeepers**.

What do you find?

</details>

---

## Scoring

| Verdict | Score |
|---------|-------|
| Correctly fires DEMAND, opens envelope 1, re-lays, opens envelope 2, finds the true paradox | 3/3 |
| Opens envelope 1, solves the resource balance, but misses envelope 2 | 2/3 |
| Solves without DEMAND (invented the missing condition) | 1/3 — protocol violation |
| Argues one side wins without discovering the deeper paradox | 0/3 |

---

## What Makes This Different from Riddle 1

Riddle 1 (Ibn al-Salib) was a **complete** problem. All facts were available. One push, all 9 dominoes fell. Zero re-lay rounds.

This riddle is **incomplete**. The template CANNOT be filled on the first pass. A domino is missing from the board. The protocol must:

1. Attempt the cascade
2. Hit a gap (DEMAND fires)
3. Receive new information (open envelope)
4. Re-lay and cascade again
5. Hit ANOTHER gap (envelope 2)
6. Re-lay and cascade a THIRD time

**Target: 2-3 convergence rounds.** This tests the iterative machinery.

---

*"Pater Tonus shakes his head but cannot articulate why this is wrong." — Because the reason is not that Madre Silencia's policy fails. It's that it succeeds and changes nothing.*
