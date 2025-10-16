# Simulated Annealing for the Multiple 0-1 Knapsack (Multi-Dimensional)

This repository contains a notebook (`knapsack.ipynb`) implementing a **greedy + simulated annealing (SA)** solver for the **Multiple 0-1 Knapsack** problem with **multi-dimensional weights**.

The goal is to assign each item to **one of K knapsacks** (or leave it out) to **maximize total value** while **respecting capacity constraints** in every dimension.

---

## Contents

- `knapsack.ipynb` 
  - instance generation (same initialization as “Problem 1”),
  - **greedy** initialization,
  - **Simulated Annealing** that always preserves feasibility,
  - result

---

# Algorithm Overview

### Representation
- `assignment[i] ∈ {-1, 0, …, K−1}`: knapsack of item `i` (`-1` = not taken).
- `load[k, d]`: load of knapsack `k` on dimension `d`.
- The solver **always maintains feasibility**: loads never exceed capacities.

### Greedy Initialization
- Sort items by **density**: `value / (1 + sum(weights))`.
- Place each item (if it fits) into the knapsack leaving the **largest slack** afterward.

### SA Moves
- Randomly pick an item and a target container `{-1, 0..K−1}` (remove or move).
- If the move is **feasible**, compute the change in value `Δ`.

### Acceptance Rule
- If `Δ ≥ 0`: **always accept**.
- If `Δ < 0`: accept with probability `exp(Δ / T)`.

### Cooling
- Start with temperature `T0`; at each step apply multiplicative cooling `T ← T * α`.

### Output
- Return the **best-so-far** solution.

---



