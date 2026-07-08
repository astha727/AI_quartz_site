
> [!abstract]
> Simulated Annealing is a **stochastic global optimization algorithm** inspired by the physical process of annealing in metallurgy. It is a modified form of stochastic hill climbing that allows occasional uphill moves to escape local minima.

---

# 1. Heuristics (Foundational Idea)

A heuristic is a **rule of thumb** used to find a good (not necessarily optimal) solution when exact optimization is infeasible.

Heuristics are used when:
- The search space is large, nonlinear, or non-convex
- There are many local minima/maxima
- Exact optimization is computationally expensive or impossible

Unlike classical optimization methods, heuristics:
- Do NOT guarantee the global optimum
- Aim for **good solutions efficiently**
- Trade optimality for scalability

## Why Use Heuristics?

- Handle combinatorial explosion
- Escape (or reduce impact of) local optima
- Work in large state spaces
- Incorporate randomness for exploration

## Common Heuristic Types

### Construction Methods
- Build a feasible solution first
- Then improve it

### Improvement Methods
- Start with a feasible solution
- Iteratively refine it

## Common Metaheuristics
- Simulated Annealing (SA)
- Genetic Algorithms
- Tabu Search
- Particle Swarm Optimization

# 2. Intuition (Metallurgy Analogy)

Simulated Annealing is inspired by **annealing in metals**:

- Metal is heated → atoms move freely (high randomness)
- Slow cooling → atoms settle into stable structure
- Final state → low-energy configuration

### Optimization mapping:
- Atoms → candidate solutions  
- Energy → objective function  
- Cooling → reduction in randomness  
- Stable crystal → optimal/near-optimal solution  

---

# 3. Why Simulated Annealing?

### Problem with Hill Climbing
- Always moves to better states
- Gets stuck in local minima

### Key Idea of SA
> Sometimes accept worse solutions to escape local minima.

---

# 4. Core Mechanism

At each step:
- If new solution is better → accept
- If worse → accept with probability

This probability depends on:
- How bad the move is
- Current temperature

---

# 5. Metropolis Acceptance Criterion

For minimization:

$$
P(\text{accept}) = e^{-\Delta E / T}
$$

Where:
- \( \Delta E = E(\text{new}) - E(\text{current}) \)
- \( T \) = temperature

---

## Interpretation

- High T → random exploration
- Low T → greedy behavior
- Large ΔE → lower acceptance probability

---

> [!important]
> This mechanism allows SA to escape local minima early in the search.

---

# 6. Temperature Schedule

A common schedule:

$$
T = \frac{T_0}{i + 1}
$$

Where:
- \(T_0\) = initial temperature
- \(i\) = iteration index

## Behavior Over Time

| Phase              | Behavior                  |
| ------------------ | ------------------------- |
| High temperature   | exploration, random jumps |
| Medium temperature | balanced search           |
| Low temperature    | greedy convergence        |

---

# 7. Simulated Annealing Algorithm

```text
S ← initial solution
T ← initial temperature

repeat until stopping condition:

    generate neighbor S'

    ΔE = E(S') - E(S)

    if ΔE ≤ 0:
        S ← S'
    else:
        accept S' with probability e^(-ΔE / T)

    reduce T
```

---

# 8. Relationship to Hill Climbing

| Hill Climbing | Simulated Annealing |
|--------------|----------------------|
| Always improves | Allows worse moves |
| Deterministic | Stochastic |
| Gets stuck easily | Escapes local minima |
| Greedy | Controlled randomness |

---

# 9. Why SA Works

Simulated Annealing works because:

- Early stage → exploration (high T)
- Late stage → exploitation (low T)
- Random uphill moves prevent premature convergence

---

# 10. Python Implementation (Clean Version) 
Source: https://machinelearningmastery.com/simulated-annealing-from-scratch-in-python/

```python
import numpy as np

def simulated_annealing(objective, bounds, n_iter, step_size, temp):

    # initial solution
    best = bounds[:, 0] + np.random.rand(len(bounds)) * (bounds[:, 1] - bounds[:, 0])
    best_eval = objective(best)

    curr, curr_eval = best, best_eval

    for i in range(n_iter):

        # generate neighbor
        candidate = curr + np.random.randn(len(bounds)) * step_size
        candidate_eval = objective(candidate)

        # update best
        if candidate_eval < best_eval:
            best, best_eval = candidate, candidate_eval

        # difference
        diff = candidate_eval - curr_eval

        # temperature schedule
        t = temp / float(i + 1)

        # metropolis probability
        metropolis = np.exp(-diff / t)

        # accept/reject
        if diff < 0 or np.random.rand() < metropolis:
            curr, curr_eval = candidate, candidate_eval

    return best, best_eval
```

---

# 11. Example Objective Function

```python
def objective(x):
    return x[0] ** 2
```

Global minimum:
```
x = 0
f(x) = 0
```

---

# 12. Key Insight

> Simulated Annealing = Hill Climbing + Probabilistic Acceptance + Cooling Schedule

---

# 13. Advantages

- Escapes local minima
- Simple to implement
- Works in non-convex spaces
- Flexible objective function
- Good for combinatorial optimization

---

# 14. Limitations

- Slow convergence
- Sensitive to cooling schedule
- No guarantee of global optimum
- Requires tuning (T, step size, schedule)

---

# 15. Applications

- Traveling Salesman Problem (TSP)
- Scheduling problems
- Vehicle routing
- VLSI design
- Clustering
- Image processing
- Crystal structure prediction
- Multiprocessor scheduling

---

# 16. Key Exam Summary

> [!tip]
> Simulated Annealing is:
>
> - stochastic local search
> - allows uphill moves
> - controlled by temperature
> - gradually becomes greedy
> - used for global optimization in complex search spaces