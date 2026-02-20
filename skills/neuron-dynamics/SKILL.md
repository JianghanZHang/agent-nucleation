---
name: neuron-dynamics
description: >
  Domain knowledge for reasoning about physical systems,
  architecture emergence, phase transitions, and the
  Fokker-Planck equation on operator space.
  Load this tool when the task involves neural architecture,
  thermodynamic analogies, nucleation/collapse dynamics,
  log-space computation, or boundary value formulations
  of controller design.
license: MIT
metadata:
  author: Jianghan Zhang
  email: Jianghan.Zhang.gr@dartmouth.edu
  version: "0.1"
  grade: "0"
  role: tool
  source: "Neuron Dynamics: Log-Space Computation with Emergent Architecture (Zhang, 2026)"
---

# Neuron Dynamics — Tool

## Core Vocabulary

| Term | Definition | Equation |
|---|---|---|
| Operator space | $\Theta = \mathbb{R}^{n \times n} \times \mathbb{R}^n \times \mathbb{R}^n \times \mathbb{R}$ | Space of all possible neurons |
| Neuron pool | $\mu \in \mathcal{M}_+(\Theta)$, $\|\mu\| = n$ | Measure over operator space, total mass = input dim |
| Active set | $\mathcal{A}(\mu) = \{\theta_k : m_k > 0\}$ | The crystallised neurons (atoms of $\mu$) |
| Redundant part | $\mu_{\text{cont}}$ | Continuous part — liquid, ready to nucleate |
| Core number | $K^* = |\mathcal{A}(\mu_\infty)|$ | Number of survivors at $\tau \to 0$ |
| Free core | $\mathfrak{F} \subset \Theta$ | Minimal invariant set under the flow |


## Key Equations

### Log-space forward pass

$$y = \exp(W \cdot \log x + c)$$

In original space: power-law map $y_i = e^{c_i} \prod_j x_j^{W_{ij}}$.
Each $W_{ij}$ is an exponent — typically a small number ($0, \pm1, \pm2$).
This is what physicists mean by "counting powers."

### Relative gradient (No-Adam)

$$\nabla_\phi L = \theta \odot \nabla_\theta L \qquad \text{where } \phi = \log\theta$$

Updates proportional to parameter magnitude.
SGD in log-space = mirror descent with negentropy potential
$\psi(\theta) = \sum_i \theta_i \log \theta_i$.
Adam's $(\beta_1, \beta_2, \varepsilon)$ absorbed into representation.
Zero optimiser hyperparameters.

### Fokker-Planck on operator space

$$\frac{\partial \mu}{\partial t} = \nabla \cdot (\mu \,\nabla V) + \tau \,\Delta \mu$$

- **Drift** $\nabla \cdot (\mu \nabla V)$:
  operators flow downhill on loss.
  Useful concentrate, useless disperse.
- **Diffusion** $\tau \Delta \mu$:
  temperature spreads operators.
  High $\tau$ = liquid. Low $\tau$ = solid.

### Nucleation

Continuous part concentrates at $\theta^*$ where
score $s^*(\theta) = -\nabla V(\theta)/\tau$ is maximal.
A new atom forms. Mass conserved.

### Collapse

Atom dissolves back into $\mu_{\text{cont}}$.
Information diffuses to neighbours in $\Theta$.
Mass conserved. Energy released.


## The Iron ↔ NN Correspondence

| Iron | Neural network |
|---|---|
| Liquid (hot) | Pool: $\mu$ diffuse, no atoms |
| Nucleation (cooling) | Neuron appears: atom forms in $\mu$ |
| Crystal growth | Receptive field expands |
| Ostwald ripening | Pruning: large neurons absorb small |
| Solid (cold) | Fixed architecture: $K^*$ active neurons |
| Remelting (heating) | Retraining: neurons collapse back to pool |
| Grain count | $K^*$ (core number) |
| Cooling schedule | Temperature annealing $\tau_t \to 0$ |
| Crystal orientation | Weight vector (receptive field) |


## The Boundary Value Framing

For any input-output system:

| | |
|---|---|
| **Left boundary** (Dirichlet) | sensor dimension $d_{\text{in}}$ (hardware fact) |
| **Right boundary** (Dirichlet) | actuator dimension $d_{\text{out}}$ (hardware fact) |
| **Interior** | solved by FPE |
| **Architecture** | the interior solution, not a design choice |

Specification = $\{d_{\text{in}},\; d_{\text{out}},\; n,\; \tau_{\text{schedule}}\}$.
Four numbers.

### Example: Robot Dog

- Input: 12 joint positions + 12 velocities + 6 IMU = 30
- Output: 12 joint torques
- Pool capacity: $n = 30$
- Prediction: $K^* \approx 4$--$6$ (one operator per gait)


## The Two Theorems

**No-Adam [P]:**
Log-space parameterisation makes gradients scale-free.
Plain SGD = natural gradient = mirror descent with negentropy.
Zero optimiser hyperparameters.

**Core Number Emergence [P]:**
Pool with capacity $n \geq K$ under FPE with $\tau \to 0$
converges to $K^* \leq K$ atoms — the core number of the target.
Freedom Theorem on operator space.

**Duality:**
No-Adam solves optimisation (how to train).
Core Number solves architecture (how many neurons).
Both from: log-space + compact domain + Freedom Theorem.


## The Feeling Distinction

- **Fixed $W$ = camera** (inference):
  sees but does not feel. The sensor is not modified by the signal.
- **Updating $W$ = feeling** (training):
  the sensor is modified by what it senses. The neuron changes.
- **$W$ dissolves = melting** (phase transition):
  the neuron's identity ceases to exist.
  Its information diffuses into the pool.

The eye **is** the weight. The weight **is** the eye.
Manufacturing (annealing) is training. Using it is inference.


## When This Tool Applies

Load `neuron_dynamics` when reasoning about:

- Neural architecture (why this width / depth / $K$?)
- Physical analogies to computation (steel, crystals, phase transitions)
- Log-space / order-of-magnitude computation
- Emergent structure from dynamics (not prescribed)
- Boundary value problems (sensors → ? → actuators)
- The "feeling" distinction (inference vs training vs melting)
- Distillation / pruning / lottery ticket phenomena
- Why Adam is unnecessary (log-space absorbs it)


## When NOT to Use

- Pure symbolic/algebraic problems
  (use dominos reasoning template directly)
- Code-level implementation details
  (use surgery)
- Explaining to general audience without physical grounding
  (use explain\_with\_math — though ND may appear as a loaded tool within it)
