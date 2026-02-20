# agent-nucleation

An agent is not a model. An agent is a process that produces a verified claim.

## `/V(T, B)`

The Agent Function. Model-agnostic. Takes a target and a basis, produces a verified claim or honestly reports it cannot.

```
/V  T: "what you want"
    B: "what you know / what inspires you"
```

## Three Grades

| Grade | Name | Role | Contents |
|---|---|---|---|
| 2 | **agent-nucleation** | The function — WHAT V produces | `skills/v/` |
| 1 | **formal-agents** | The template — HOW agents reason | `skills/dominos-reasoning/` |
| 0 | **V-protocol** | The tools — WITH WHAT | `skills/neuron-dynamics/`, `skills/explain-with-math/`, ... |

## Pool — Your Portable Knowledge Bank

```
pool/
├── llm_readme.md      ← instructions for the LLM (do not remove)
├── user_readme.md      ← instructions for you (read this)
└── ...                 ← drop your files here
```

The pool is μ_cont — the liquid part of the neuron pool. Drop your notes, papers, code, data — anything. Any language, any format, any level of polish. When V() hits a DEMAND and the built-in skills can't resolve it, it searches pool/ for material that can.

Your pool is the fuel. V() is the engine.

## Workspace — The Crystallization Surface

```
agent_workspace/
├── llm_readme.md                          ← instructions for sub-agents
├── 2026-02-20T15:30:00_slot_A_demand.md   ← (runtime)
├── 2026-02-20T15:30:45_slot_A_resolved.md ← (runtime)
└── ...
```

Sub-agents write here. One file per state change, timestamped, never overwritten. After V() completes, the workspace is the full record of the cascade — which slots fired DEMAND, what was tried, what resolved, how many rounds.

Read-only for humans. Ephemeral. Clear it anytime.

## How It Works

1. **Parse**: extract T (target) and B (basis) from user input
2. **Completeness check**: skills cover path B → T? If not, search pool/. If neither: DEMAND.
3. **Cascade**: run dominos reasoning (9 slots, 3 layers, COMMAND/DEMAND)
4. **Lazy tree**: sub-agents spawn ONLY on DEMAND, never speculatively
5. **Claim**: cascade verifies → `believe_it` → the process IS an agent

## Install

```bash
git clone https://github.com/JianghanZHang/agent-nucleation ~/.claude/plugins/local/agent-nucleation
```

Then enable in Claude Code settings.

## The Correspondence

This plugin implements [Neuron Dynamics](https://github.com/JianghanZHang/A-KIND-MOVIE/tree/main/REMEDY/PURE_MATH/NeuronDynamics) applied to agent management:

- **Neuron pool** → skill bank + pool/
- **μ_cont (liquid)** → pool/ (user's raw material)
- **Nucleation** → sub-agent spawns on DEMAND
- **Crystal surface** → agent_workspace/ (timestamped log)
- **Collapse** → sub-agent claims, output absorbed
- **Core number K\*** → minimum sub-agents needed
- **FPE** → dominos reasoning template
- **Temperature** → context budget remaining

You do not design agents. You let them nucleate.

## Author

Jianghan Zhang · Dartmouth College · 2026

## License

MIT
