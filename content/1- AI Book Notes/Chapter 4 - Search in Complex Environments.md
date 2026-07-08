>[!insight]
>[[Chapter 3 - Solving Problems by Searching]] studied search problems under several simplifying assumptions. The environment was assumed to be:
>
>**Fully observable**    : Agent always knows the complete current state
>**Deterministic**       : Every action has exactly one predictable outcome 
>**Static**              : Environment does not change while planning       
>**Known**               : Transition model is already known                
>**Sequential planning** : Goal is to find a sequence of actions 
>Under these assumptions, the solution is:
>A path from the initial state to the goal state.
>Examples include:
>- Romania Route Finding
>- 8-Puzzle
>- Grid Navigation


# Why Chapter 4 Exists

Many real-world problems violate one or more of the assumptions made in Chapter 3.

Instead of finding a path, we often only care about the final configuration.

Examples include:

- Integrated circuit design
- Factory floor layout
- Job-shop scheduling
- Automatic programming
- Telecommunications network optimization
- Crop planning
- Portfolio management

In these problems:

- The path taken is usually irrelevant.
- Only the final solution matters.

---

> [!important]
> If the final state is known, the sequence of moves that created it is often unnecessary.

Instead of asking

> "How do I get there?"

we ask

> "Which state is best?"

---

> [!tip] Exam Tip
>
> Always identify whether the problem requires
>
> - a path
>
> or
>
> - only the final state.
>
> That determines whether classical search or local search is appropriate.

# 4.1 Local Search and Optimization Problems

---

> [!note]
> Local search algorithms ignore paths and search only among neighboring states.
>
> They are designed primarily for optimization problems.

# Motivation

Chapter 3 algorithms searched for

```

Initial State
↓

Goal State

```

by constructing an entire path.

Local search changes the objective.

Instead of finding a path, we seek only

> the best final state.

---

# Example: 8-Queens

Suppose we are solving the 8-Queens problem.

We do **not** care how the queens were moved.

We only care about producing a board configuration where no queens attack one another.

---

> [!example]
> Once a valid board configuration has been found, reconstructing the moves that created it is trivial.
>
> Therefore the path itself is unnecessary.

# Local Search

## Definition

Local search algorithms search from one state to neighboring states without remembering

- the path
- previously visited states

Because of this, they are **not systematic.**

They may never explore parts of the search space where a solution exists.

---

# Advantages

Despite this limitation, local search has two major strengths.

## 1. Very little memory

Only the current state (or a small number of candidate states) must be stored, which makes memory usage dramatically lower than graph search.

## 2. Works in enormous state spaces

Many optimization problems contain millions, billions, or even infinitely many states, making systematic search infeasible. Local search can still operate effectively in such spaces and often finds good-quality solutions.

> [!important]
> Local search sacrifices completeness in exchange for scalability.

---

# Optimization Problems

Local search is naturally suited for optimization problems.

## Optimization Problem (Definition)

An optimization problem is the task of finding the **best state** according to a given objective function.

Unlike classical search problems, there may not be a single goal state; instead, every state is assigned a quality value.

# Objective Function

Every state is assigned a numerical value, and the objective function determines how good that state is.

Depending on the problem, higher values may represent better schedules, higher profits, or better layouts, while lower values may represent lower cost, fewer conflicts, or shorter delays.

---

# State-Space Landscape

The textbook visualizes the search space as a landscape, where each state corresponds to a point on that landscape. The height (or elevation) of each point represents the value returned by the objective function.

## Visualization

```

High Value

▲
│ Global Maximum
│
│ /\ /\

│ / \ Local Maximum
│ / \
│_/____\______________

```

---

# Two Perspectives

Depending on the objective, the landscape can be interpreted in different ways.

## Maximization

In a maximization problem, the goal is to find the highest peak in the landscape. This approach is commonly referred to as **hill climbing**.

## Minimization

In a minimization problem, the goal is to find the lowest valley in the landscape. This approach is commonly referred to as **gradient descent**.

> [!note]
> The underlying search algorithm is often identical. Only the interpretation of the objective function changes.

---

# Why Local Search Uses So Little Memory

Classical search algorithms store the frontier, the explored set, and the full search tree.

In contrast, local search typically stores only the current state.

As a result, memory usage is usually **O(1)**, or **O(k)** for algorithms that maintain a small set of candidate states.

---

# Typical Applications

The textbook lists several important optimization applications.

- Integrated circuit design
- Factory floor layout
- Job-shop scheduling
- Automatic programming
- Telecommunications network optimization
- Crop planning
- Portfolio management

---

# Comparing Classical Search vs Local Search

| Classical Search | Local Search |
|------------------|--------------|
| Searches for paths | Searches for best state |
| Stores frontier | Usually stores only current state |
| Complete (often) | Usually incomplete |
| High memory usage | Very low memory usage |
| Returns action sequence | Returns final configuration |

# Additional Example (for Intuition)

Imagine arranging desks inside an office. There may be millions of possible layouts, and no one cares which desks were moved first. The only thing that matters is the final arrangement.

This is exactly the kind of problem local search is designed for.

---

> [!tip] Exam Tip
> If a problem statement includes words like:
> - maximize  
> - minimize  
> - optimize  
> - best configuration  
> - best arrangement  
>
> then you should think **Local Search** before classical search.

---

# Key Takeaways

- Local search ignores paths.
- Only neighboring states are explored.
- Memory usage is very small.
- It is not systematic.
- It is useful for optimization problems.
- It represents problems as state-space landscapes.
- Maximization corresponds to hill climbing.
- Minimization corresponds to gradient descent.

---

# Related Notes

- [[Hill Climbing]]
- [[Simulated Annealing]]
- [[Local Beam Search]]
- [[Evolutionary Algorithms]]
- [[MIT 6.034 Lecture 4 - Search - Hill Climbing, Depth - First, Beam]]

---

# 4.1.1 Hill-Climbing Search

> [!abstract]
> Hill climbing is the simplest local search algorithm. Instead of searching for a path from a start state to a goal, it repeatedly moves from the current state to the best neighboring state until no better neighbor exists.

---

# Core Idea

Hill climbing maintains only one current state.

Instead of remembering the entire search tree, it repeatedly replaces the current state with its best neighboring state.

The search continues until no neighbor has a higher value.

---

> [!important]
> Hill climbing is a **local search algorithm**. It never considers the full search tree, only the immediate neighbors of the current state.
# Hill-Climbing Algorithm

The algorithm proceeds as follows:

1. Start at the initial state.
    
2. Examine all neighboring states.
    
3. Choose the neighbor with the highest value.
    
4. Move to that neighbor.
    
5. Repeat until no better neighbor exists.
    
6. Return the current state.
    

## Pseudocode (AIMA)

```text
function HILL-CLIMBING(problem) returns a state that is a local maximum

    current ← problem.INITIAL
    // Start from the initial state provided by the problem.
    // This is the algorithm's starting point in the search space.

    while true do
    // Repeat indefinitely until a stopping condition is reached.

        neighbor ← highest-valued successor of current
        // Generate all neighboring states of the current state.
        // Select the neighbor with the highest evaluation (best improvement).

        if VALUE(neighbor) ≤ VALUE(current) then
            return current
            // If no neighbor is better than the current state,
            // we have reached a local maximum, so terminate.

        current ← neighbor
        // Otherwise, move to the better neighbor and continue climbing.
```

---

# Algorithm Flow

```text
Initial State
      │
      ▼
Evaluate Neighbors
      │
      ▼
Choose Best Neighbor
      │
      ▼
Better?
 │
 ├── Yes → Move there
 │
 └── No → Stop
```

---

# Important Terminology

## Current State

The state currently occupied by the algorithm.

Only one state is stored.

---

## Neighbor

A state reachable by making one legal modification to the current state.

---

## Highest-Valued Neighbor

Among all neighboring states, the algorithm selects the one with the highest objective value. This strategy is called **steepest ascent**.

---

## Steepest Ascent

In hill climbing, the algorithm always chooses the neighbor that provides the greatest improvement in the objective function. It never intentionally moves downhill.

---

> [!note]  
> The algorithm **does not look ahead** beyond its immediate neighbors.

---

# Mountain Analogy

The textbook compares hill climbing to trying to find the top of Mount Everest in thick fog while suffering from amnesia. In this setting, you only know your immediate surroundings, you cannot remember where you have already been, and you always move uphill based only on local information.

---

# Using Heuristics

Sometimes the objective function is defined using a heuristic. In such cases, instead of directly maximizing a value, the algorithm minimizes heuristic cost by using the **negative of the heuristic cost** as the objective function.

As a result, hill climbing moves toward states with the **smallest heuristic distance to the goal**.

---

# Example: 8-Queens Problem

The textbook illustrates hill climbing using the 8-Queens problem.

---

## Complete-State Formulation

Unlike classical search problems, every state already contains all eight queens. However, some queens may be in incorrect positions.

---

> [!definition]  
> **Complete-State Formulation**  
> Every state contains a complete candidate solution, although it may violate constraints.

---

## Representation

Each column always contains exactly one queen, and only the row positions of the queens change.

---

## Initial State

The initial state is chosen randomly.

---

## Successor Function

A successor state is generated by moving one queen to another square within the same column.

---

### Number of Successors

There are 8 columns, and each queen can move to 7 other rows. Therefore, the total number of successors is:

```
8 × 7 = 56
```
---

> [!exam-tip]  
> The value **56 successors** for the 8-Queens hill-climbing formulation is frequently tested.

---

## Heuristic Function

The heuristic cost

```
h
```

equals

> the number of pairs of queens attacking each other.

Properties:

- Lower is better.
    
- Solution has
    

```
h = 0
```

---

> [!note]  
> Two queens are considered attacking even if another queen lies between them.

---

# Greedy Local Search

Hill climbing is sometimes called **greedy local search** because it always selects the best neighboring state immediately, without considering future consequences.

Although “greedy” is often used negatively, greedy algorithms frequently perform very well in practice.

---

# Why Hill Climbing Works Well Initially

In most problems, bad states tend to have many possible improvements. As a result, hill climbing often makes rapid progress at the beginning of the search.

For example, a state with:

```
h = 17
```

can often reach:

```
h = 1
```

in just **five moves**.

---

# Why Hill Climbing Fails

Hill climbing can terminate even when better solutions exist. The textbook identifies three main failure cases.

---

# 1. Local Maximum

> [!danger]  
> A **local maximum** is a state that is better than all its neighbors but still worse than the global maximum.

Once the algorithm reaches a local maximum, all neighboring states appear worse, so the search stops.

In the 8-Queens example, a state with:

```
h = 1
```

can be a local maximum (or equivalently a local minimum in a cost formulation). Any single move worsens the configuration.

---

# 2. Ridge

A ridge is a narrow region where improvement exists, but not in the direction chosen by greedy ascent.

As a result, the algorithm keeps making small or misleading moves and struggles to progress efficiently.

> [!important]  
> Greedy algorithms perform poorly on ridges because they only consider immediate steepest improvement.

---

# 3. Plateau

A plateau is a flat region of the search space where all neighboring states have the same value.

There are two types of plateaus:

## Flat Local Maximum

No exit leads upward, so the algorithm terminates.

## Shoulder

A flat region from which improvement is possible, but the algorithm may struggle to find the correct direction.

---

# Performance on 8-Queens

The textbook reports the following results:

| Result | Value |
|--------|------:|
| Success Rate | 14% |
| Failure Rate | 86% |
| Average steps (success) | 4 |
| Average steps (failure) | 3 |
| State space size | 8⁸ ≈ 17 million |

> [!exam-tip]  
> These values are commonly tested and are worth memorizing.

---

# Sideways Moves

Sideways moves allow the algorithm to move to a neighbor with the same value instead of stopping.

This helps determine whether a plateau is a shoulder rather than a flat local maximum.

However, excessive sideways moves can lead to infinite loops.

To prevent this, a limit is typically imposed (often **100 moves**).

---

## Effect of Sideways Moves

| Without Sideways | With Sideways |
|------------------|--------------:|
| Success rate | 14% |
| Average steps (success) | 4 |
| Average steps (failure) | 3 |

> [!important]  
> Sideways moves increase success rates but also increase runtime.

---

# Variants of Hill Climbing

## 1. Steepest-Ascent Hill Climbing

Evaluates all neighbors and selects the best one.

---

## 2. Stochastic Hill Climbing

Randomly selects among uphill moves, with probabilities influenced by improvement magnitude.

- Slower convergence  
- Sometimes finds better solutions  

---

## 3. First-Choice Hill Climbing

Generates random successors until it finds the first better state, then immediately moves there.

Useful when the number of neighbors is extremely large.

---

## 4. Random-Restart Hill Climbing

When stuck, the algorithm restarts from a random initial state and repeats the process until a solution is found.

> [!success]  
> Random-restart hill climbing is probabilistically complete because repeated restarts eventually explore a solution state.

---

# Expected Number of Restarts

If \( p \) is the probability that one run succeeds, then:

```
Expected restarts = 1 / p
```

---

## Example (8-Queens)

Given:

```
p ≈ 0.14
```

Then:

```
1 / 0.14 ≈ 7
```

So we expect about 6 failures before 1 success.

---

# Expected Number of Steps

```
Expected steps =
(success cost) +
((1 - p)/p) × failure cost
```

For the 8-Queens problem:

- Without sideways moves: ~22 steps  
- With sideways moves: ~25 steps  

---

# Success Depends on the Landscape

Hill climbing works well when the search space has few local maxima and few plateaus.

However, many NP-hard problems contain an exponential number of local maxima.

Even then, random-restart hill climbing often finds good local optima efficiently.

---

> [!quote]  
> The search landscape is described as:
>  
> *"a widely scattered family of balding porcupines on a flat floor, with miniature porcupines living on the tip of each porcupine needle."*

# Summary Table

|Variant|Main Idea|
|---|---|
|Steepest-Ascent|Choose best neighbor|
|Stochastic|Random uphill move|
|First-Choice|Randomly generate neighbors until improvement|
|Random-Restart|Restart from random states|

---

> [!summary] Key Takeaways
> 
> - Hill climbing stores only the current state.
>     
> - Chooses the highest-valued neighboring state.
>     
> - Uses steepest ascent.
>     
> - Can become trapped in local maxima, ridges, and plateaus.
>     
> - Sideways moves help escape some plateaus.
>     
> - Random restarts make hill climbing complete with probability 1.
>     
> - Performance depends heavily on the shape of the search landscape.
>     

---

# 4.1.2 Simulated Annealing

> [!info] Definition
> **Simulated Annealing** is a local search algorithm that combines **hill climbing** with **random exploration**.
>
> Unlike hill climbing, it occasionally accepts worse states to escape local optima.

---

# Motivation

Hill climbing has one major weakness:

- It never moves downhill.
- Therefore, it can become trapped in:
  - Local maxima
  - Plateaus
  - Ridges

At the opposite extreme is a **pure random walk**, where the algorithm moves to successor states without considering their value.

| Hill Climbing | Random Walk |
|---------------|-------------|
| Efficient | Complete (eventually) |
| Easily trapped in local maxima | Extremely inefficient |

The textbook proposes combining these two ideas to obtain both efficiency and completeness.

---

# Physical Inspiration

Simulated annealing is inspired by the physical process of **annealing** in metallurgy.

Annealing consists of:

1. Heating a metal to a high temperature.
2. Allowing atoms to move freely.
3. Gradually cooling the metal.
4. Allowing atoms to settle into a low-energy crystalline structure.

The slow cooling process helps the material avoid poor local configurations and reach a lower-energy state.

---

# Book Analogy

The textbook asks us to imagine a **ping-pong ball** on a rough landscape.

Goal:

Find the deepest valley (global minimum).

### Without shaking

- The ball rolls into the nearest valley.
- Once there, it cannot escape.

Result:

- Local minimum.

### With shaking

If the surface is shaken:

- The ball may escape a shallow valley.
- It may eventually fall into a deeper valley.
- If the shaking is gradually reduced, the ball eventually settles into the deepest valley.

This behavior motivates simulated annealing.

---

# Search Interpretation

Hill climbing:

- Always selects the best neighboring state.

Simulated annealing:

- Selects a random neighboring state.
- Then decides whether to accept it.

---

# Basic Idea

At every iteration:

1. Randomly choose a neighboring state.
2. If the new state is better:
   - Always accept it.
3. If the new state is worse:
   - Accept it with a certain probability.

The acceptance probability depends on:

- How much worse the move is.
- The current temperature.

---

# Temperature

Temperature controls the amount of randomness.

High temperature:

- High randomness.
- Encourages exploration.

Low temperature:

- Low randomness.
- Behaves increasingly like hill climbing.

---

# Acceptance Probability

Let

- `VALUE(current)` = value of current state
- `VALUE(next)` = value of proposed successor

The textbook defines

$$\Delta E = VALUE(current) - VALUE(next)$$

If

$$\Delta E > 0$$

the new state is better.

It is **always accepted**.

Otherwise, the new state is accepted with probability

$$P = e^{\Delta E / T}$$

where

- \(T\) = temperature
- $$\Delta E \le 0$$

# Effect of Temperature

## High Temperature

When

$$
T \rightarrow \infty
$$

then

$$
e^{\Delta E/T} \approx 1
$$

Almost every move is accepted, even poor ones.

Behavior:

- Random exploration.

## Medium Temperature

Some worse moves are accepted.

Some are rejected.

The search gradually shifts from exploration toward exploitation.

## Low Temperature

When
$$
T \rightarrow 0
$$

the probability of accepting worse moves becomes very small.

Behavior becomes almost identical to hill climbing.

---

# Cooling Schedule

Temperature is controlled by

```
schedule(t)
```

The cooling schedule determines how quickly the temperature decreases.

> [!important]
> The textbook emphasizes that the cooling schedule must lower the temperature **slowly enough**.
>
> If cooling occurs too quickly, the algorithm may become trapped in poor local optima.

---

# Algorithm (Figure 4.5)

```text
SIMULATED-ANNEALING(problem, schedule)

current ← INITIAL(problem)

for t = 1 to ∞ do

    T ← schedule(t)

    if T = 0 then
        return current

    next ← randomly selected successor of current

    ΔE ← VALUE(current) − VALUE(next)

    if ΔE > 0 then
        current ← next
    else
        current ← next with probability e^(ΔE/T)
```

---

# Why Simulated Annealing Works

Hill climbing fails because it never accepts worse states.

Simulated annealing allows temporary downhill moves.

These occasional downhill moves help the search escape:

- Local maxima
- Local minima (cost version)
- Plateaus
- Ridges

As the temperature decreases, exploration gradually gives way to exploitation.

---

# Advantages

- Escapes local maxima.
- Escapes plateaus.
- Uses very little memory.
- Combines exploration and exploitation.
- Can converge to the global optimum under an appropriate cooling schedule.

---

# Limitations

- Performance depends heavily on the cooling schedule.
- Cooling too quickly reduces performance.
- Cooling very slowly increases runtime.

---

# Applications (Book)

The textbook lists:

- VLSI layout problems
- Factory scheduling
- Large-scale optimization problems

---

# Hill Climbing vs Simulated Annealing

| Hill Climbing | Simulated Annealing |
|---------------|---------------------|
| Chooses best neighbor | Chooses random neighbor |
| Never accepts worse states | Sometimes accepts worse states |
| Easily trapped | Can escape local maxima |
| Deterministic | Probabilistic |

---

> [!tip] Lecture
> Lecture explains simulated annealing using the analogy of **shaking a box containing a ball**.
>
> - High temperature → vigorous shaking → exploration.
> - Low temperature → gentle shaking → convergence.

---

> [!example] Additional Example
> Imagine climbing mountains in dense fog.
>
> Hill climbing always walks uphill.
>
> If you reach a small hill, you become trapped.
>
> Simulated annealing occasionally allows walking downhill, making it possible to discover a much taller mountain.

---

> [!success] Exam Tips
>
> - High temperature = exploration.
> - Low temperature = exploitation.
> - Better states are always accepted.
> - Worse states are accepted with probability
>
> $$
> e^{\Delta E/T}
> $$
>
> - Cooling schedule is critical.
> - The theoretical guarantee of reaching the global optimum requires sufficiently slow cooling.


# 4.1.3 Local Beam Search

> [!info] Definition
> **Local Beam Search** is a local search algorithm that keeps track of **k states simultaneously** instead of only one.
>
> At every iteration, it generates the successors of all k states, keeps the best k successors, and repeats until a goal is found.

---

# Motivation

Hill climbing stores only **one current state**.

If that state becomes trapped in a:

- Local maximum
- Plateau
- Ridge

the search cannot continue.

Local Beam Search attempts to reduce this problem by searching from **multiple states simultaneously**.

Instead of committing to one search path, it explores several promising regions of the state space at the same time.

---

# Basic Idea

Instead of maintaining:

```
1 current state
```

Local Beam Search maintains:

```
k current states
```

where **k** is called the **beam width**.

Each iteration expands all current states simultaneously.

---

# Algorithm

The textbook describes the algorithm as follows:

1. Generate **k random initial states**.
2. Generate all successors of every current state.
3. If any successor is a goal state:
   - Terminate.
4. Otherwise:
   - Select the **best k successors** from the complete set of generated successors.
5. Repeat.

Unlike hill climbing, Local Beam Search always maintains multiple candidate solutions.

---

# Search Process

Suppose

```
k = 4
```

Initially:

```
State A
State B
State C
State D
```

Each state generates successors.

Suppose together they generate:

```
28 successor states
```

The algorithm compares **all 28 successors together**.

Only the **best 4 successors** survive.

Those four become the beam for the next iteration.

---

# Information Sharing

One of the key ideas emphasized by the textbook is that the searches are **not independent**.

Instead, all generated successors compete against one another.

The textbook summarizes this idea with the phrase:

> "Come over here, the grass is greener!"

If one search discovers a promising region, its successors dominate the next generation, causing more search effort to move toward that region.

---

# Difference from Random-Restart Hill Climbing

At first glance,

Local Beam Search appears similar to running multiple hill-climbing searches in parallel.

However, the textbook explicitly states that the two algorithms are **quite different**.

## Random-Restart Hill Climbing

- Each search runs independently.
- No information is shared.
- Success or failure of one search does not affect the others.

## Local Beam Search

- All successors compete together.
- Information is effectively shared.
- Search resources naturally move toward the most promising regions.

---

# Advantages

Compared with hill climbing:

- Explores multiple regions simultaneously.
- Less dependent on one initial state.
- Can abandon poor search directions.
- Concentrates effort where the best progress is being made.

Because the best successors are always retained, search effort continually shifts toward better regions of the landscape.

---

# Limitation

The textbook identifies an important weakness of Local Beam Search: the **k states may lose diversity**.

Instead of exploring different regions of the search space, all k states may gradually become clustered in the same area.

When this happens, Local Beam Search behaves similarly to hill climbing, but with higher computational cost and no significant gain in exploration.

---

# Stochastic Beam Search

To address the loss of diversity, the textbook introduces **Stochastic Beam Search**.

Instead of always selecting the top k successors, states are selected **probabilistically**, with probability proportional to their value.

Better successors still have a higher chance of being selected, but weaker successors also have a non-zero probability of surviving. This helps maintain diversity within the beam.

---

# Local Beam Search vs Stochastic Beam Search

| Local Beam Search | Stochastic Beam Search |
|-------------------|------------------------|
| Selects best k successors | Selects successors probabilistically |
| Purely greedy selection | Probabilistic selection |
| Diversity often decreases | Better preserves diversity |
| Can converge prematurely | Encourages broader exploration |

---

# Relationship to Hill Climbing

Hill climbing maintains a single current state, while Local Beam Search maintains k current states.

Both are local search methods, but Local Beam Search distributes its search effort across multiple candidate solutions instead of committing to a single trajectory.

---

# Relationship to Random Restart

Random Restart hill climbing performs multiple independent search runs from different initial states.

In contrast, Local Beam Search maintains multiple states simultaneously that share information during the search process.

Thus:

- Random Restart = independent searches  
- Local Beam Search = cooperative searches  

---

# Relationship to Evolutionary Algorithms

The textbook notes that evolutionary algorithms can be viewed as an extension of Stochastic Beam Search.

The key difference is that evolutionary algorithms introduce additional operators such as:

- Recombination (crossover)
- Mutation

Local Beam Search, in contrast, does not use recombination or mutation and relies only on selection among generated successors.

---

# Strengths

- Requires little memory.
- Explores multiple regions simultaneously.
- Shares useful information between searches.
- Often performs better than a single hill-climbing search.

---

# Weaknesses

- May lose diversity.
- Can converge prematurely.
- Performance depends on the choice of beam width (k).

---

> [!tip] Class Connection
> The lecture describes Local Beam Search as maintaining **multiple particles** simultaneously.
>
> Each iteration keeps the most promising particles while discarding weaker ones.
>
> Stochastic Beam Search introduces randomness during this selection step to improve exploration.

---

> [!example] Additional Example
> Imagine four hikers searching for the highest mountain.
>
> **Hill Climbing**
>
> - One hiker searches alone.
>
> **Random Restart**
>
> - Four hikers search independently.
>
> **Local Beam Search**
>
> - Four hikers communicate continuously.
> - Whenever one discovers a promising region, the others gradually move toward that area.
>
> This illustrates the information-sharing property emphasized in the textbook.

---

> [!success] Exam Tips
>
> - Maintains **k states**, not one.
> - Expands successors of **all** current states.
> - Keeps the **best k successors**.
> - Not equivalent to Random-Restart Hill Climbing.
> - Information is shared between search paths.
> - Main weakness: **loss of diversity**.
> - Stochastic Beam Search selects successors with probability proportional to their value to preserve diversity.
> - Evolutionary algorithms are closely related to Stochastic Beam Search.

---

# 4.1.4 Evolutionary Algorithms

> [!info] Definition
> **Evolutionary algorithms** are local search algorithms that are **explicitly motivated by the metaphor of natural selection in biology**.
>
> Instead of maintaining a single state (hill climbing) or multiple independent states (beam search), they maintain a **population** of individuals. The fittest individuals are more likely to produce offspring, which form the next generation.

---

# Motivation

The textbook introduces evolutionary algorithms as an extension of **Stochastic Beam Search**.

Instead of simply keeping the best successor states, evolutionary algorithms mimic biological evolution by allowing individuals to:

- Compete for survival.
- Produce offspring.
- Pass useful characteristics to future generations.
- Occasionally mutate.

The overall goal remains the same:

> Search for increasingly better solutions over successive generations.

---

# Biological Inspiration

Evolutionary algorithms are inspired by **natural selection**.

The basic biological analogy is:

| Biology | Search Algorithm |
|----------|------------------|
| Organism | State |
| Population | Collection of states |
| Fitness | Objective function value |
| Reproduction | Generate successors |
| Mutation | Random modification |
| Natural selection | Prefer higher-valued states |

The central idea is that **better individuals are more likely to reproduce**, causing the overall population to improve over time.

---

# Population

Unlike hill climbing, which maintains one current state, evolutionary algorithms maintain an entire **population**.

A population is simply a collection of candidate solutions.

Example:

```
Population

State A

State B

State C

State D
```

Each individual represents one possible solution to the problem.

Instead of improving one state repeatedly, the algorithm improves the quality of the **entire population** over multiple generations.

---

# Fitness

Each individual is evaluated using a **fitness function**.

> [!info] Fitness Function
> A **fitness function** measures how good a particular solution is.
>
> Individuals with higher fitness are more likely to become parents.

The fitness function plays the same role that the objective function played in hill climbing.

Higher fitness means:

- Better solution
- Greater probability of reproduction

The textbook emphasizes that selection is driven entirely by fitness.

---

# Representation

Different evolutionary algorithms represent individuals differently.

The representation depends on the problem being solved.

The textbook lists three major representations.

## 1. Genetic Algorithms

Each individual is represented as a **string over a finite alphabet**.

Most commonly:

- Binary strings

The textbook notes the biological analogy:

DNA is also a string,

using the alphabet

```
A C G T
```


## 2. Evolution Strategies

Instead of binary strings, an individual is represented by a **sequence of real numbers**.

## 3. Genetic Programming

Instead of strings or numbers, an individual is represented by an entire **computer program**.

# Mixing Number (ρ)

One important design choice is the **mixing number**, denoted by

$$
\rho
$$

It represents

> the number of parents that combine to produce offspring.


## Most Common Case
$$
\rho = 2
$$

Two parents combine their genetic material to create children.

This corresponds to sexual reproduction.

## Special Case

$$
\rho = 1
$$

Only one parent produces offspring.

The textbook notes that this is essentially

**Stochastic Beam Search**

and can be viewed as a form of asexual reproduction.

---

## Larger Values

The textbook also notes

$$  
\rho  >2
$$
is possible.

Although uncommon in nature, it is easy to simulate computationally.

---

# Selection

Selection determines which individuals become parents.

The textbook describes two common selection methods.

---

## Method 1

Select parents with probability proportional to their fitness.

Higher fitness

↓

Higher probability of selection.

## Method 2

Randomly choose

```
n
```

individuals,

Given that

$$
n > \rho
$$

select the top

$$
\rho
$$

most fit individuals as parents.

---

> [!important]
> Selection does **not** always choose the best individuals.
>
> It simply makes better individuals **more likely** to reproduce.

---

# Recombination

Recombination is the process of producing offspring from parents.

The textbook describes it as combining parts of parent representations.

This process is often called **Crossover**.

## Crossover Point

Assuming

$$
\rho =2
$$

choose a random position in both parent strings.

Example

Parent 1

```
ABCDEFGH
```

Parent 2

```
12345678
```

Suppose the crossover point occurs after the fourth position.

Children become

```
ABCD5678

1234EFGH
```

Each child inherits part of each parent.

---

> [!info]
> The crossover point is chosen **randomly**.

---

# Mutation

Mutation introduces small random changes into offspring. After offspring are created, each bit (or element) has a small probability of changing.

The textbook defines this probability as the **mutation rate**.

## Purpose

Mutation introduces new genetic material into the population. Without mutation, useful characteristics that disappear from the population can never return.

Mutation therefore helps maintain diversity.

---

# Mutation Rate

> [!info]
> The **mutation rate** determines how often random mutations occur.

For binary strings, every bit is flipped with probability equal to the mutation rate.

Most offspring experience few or no mutations.

---

# Elitism

Another design decision is how the next generation is formed. One approach is called **Elitism**.

> [!info]
> Elitism means keeping some of the highest-scoring parents in the next generation.

The textbook notes that elitism guarantees overall fitness will **never decrease** over time.

---

# Culling

The textbook also mentions **Culling**.

> [!info]
> Culling removes all individuals whose fitness falls below a specified threshold.

The purpose is to speed up the search by eliminating poor solutions early.

The textbook cites Baum et al. (1995) as discussing this approach.

---

# Components of Evolutionary Algorithms

The textbook identifies several design choices that define an evolutionary algorithm.

| Component | Purpose |
|------------|---------|
| Population Size | Number of individuals maintained |
| Representation | How individuals are encoded |
| Mixing Number (ρ) | Number of parents producing offspring |
| Selection | Choosing parents |
| Recombination | Combining parent representations |
| Mutation Rate | Frequency of random changes |
| Elitism | Preserve best parents |
| Culling | Remove poor individuals |

---

# Complete Terminology


<div class="fun-table">

| Term              | Definition                                            |
| ----------------- | ----------------------------------------------------- |
| Population        | Collection of candidate solutions                     |
| Individual        | One candidate solution                                |
| Fitness Function  | Measures solution quality                             |
| Selection         | Chooses parents                                       |
| Parent            | Individual selected for reproduction                  |
| Offspring         | Newly generated individual                            |
| Recombination     | Combining parent information                          |
| Crossover         | Specific recombination method using a crossover point |
| Mutation          | Random modification of offspring                      |
| Mutation Rate     | Probability of mutation                               |
| Mixing Number (ρ) | Number of parents producing offspring                 |
| Elitism           | Keep best parents in next generation                  |
| Culling           | Remove weak individuals                               |

</div>

# Relationship to Earlier Local Search Algorithms

| Algorithm | Number of States |
|------------|-----------------|
| Hill Climbing | 1 |
| Simulated Annealing | 1 |
| Local Beam Search | k |
| Evolutionary Algorithms | Population |

Evolutionary algorithms extend the ideas of Local Beam Search by introducing biological concepts such as:

- Selection
- Recombination
- Mutation

---

> [!tip] [[Lecture 2 - Simulated Annealing]]
> The lecture introduces Genetic Algorithms immediately after Local Beam Search and describes them as another method for escaping local optima by maintaining multiple candidate solutions and introducing controlled randomness through crossover and mutation.

---

> [!example] Additional Example
> Consider designing an aircraft wing.
>
> Instead of optimizing a single design, an evolutionary algorithm maintains hundreds of different designs.
>
> The best-performing designs are selected, combined, and slightly mutated to create improved designs over many generations.

---

> [!success] Exam Tips
>
> - Evolutionary Algorithms are inspired by **natural selection**.
> - Maintain a **population**, not a single state.
> - Fitness determines probability of reproduction.
> - Mixing number **ρ** = number of parents.
> - **ρ = 2** is the most common case.
> - **ρ = 1** corresponds to Stochastic Beam Search.
> - Mutation introduces diversity.
> - Elitism preserves the best solutions.
> - Culling removes weak solutions.
> - Representation depends on the algorithm (binary strings, real numbers, or programs).

---

# 4.1.4 Genetic Algorithm Walkthrough (8-Queens Example)

> [!abstract] Source
> Section 4.1.4 — Evolutionary Algorithms
>> Figures 4.6 & 4.7

---

# Genetic Algorithm Overview

Instead of improving a **single solution**, genetic algorithms maintain an entire **population** of candidate solutions.

Every generation consists of four major phases:

1. Evaluate fitness
2. Select parents
3. Crossover
4. Mutation

The process repeats until an acceptable solution is found.

---

# Figure 4.6 Overview

![[Pasted image 20260626141918.png]]

Figure 4.6 illustrates one complete generation of a Genetic Algorithm.

It contains five stages:

```
Population
      │
      ▼
Fitness Evaluation
      │
      ▼
Parent Selection
      │
      ▼
Crossover
      │
      ▼
Mutation
      │
      ▼
Next Generation
```

---

# Step 1 — Initial Population

The algorithm begins with several randomly generated candidate solutions.

For the 8-Queens problem each individual is represented by an **8-digit string**.

Example:

```
32752411
```

Each digit represents the **row position** of the queen in that column.

Example

| Column | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---------|---|---|---|---|---|---|---|---|
| Row     |3|2|7|5|2|4|1|1|

Each individual therefore represents one complete board.

## Why this representation?

The representation guarantees:

- exactly one queen per column

Only row positions change.

The algorithm never has to worry about placing multiple queens in one column.

---

> [!example] OMSCS Example
>
> This encoding reduces the search space dramatically.
>
> Instead of searching every possible board configuration,
> the algorithm searches only configurations with one queen per column.

---

# Figure 4.6(a)

Figure 4.6(a) shows

```
Population of four individuals
```

Each individual is simply another possible 8-Queens board.

Example

```
32752411

24748552

...

...
```

These are the **gene pool** for the current generation.

---

# Step 2 — Fitness Evaluation

Every individual receives a fitness score.

For the 8-Queens problem,

Fitness is defined as

```
Number of non-attacking queen pairs
```

NOT

```
Number of attacking pairs
```

Higher fitness is better.

---

## Maximum Fitness

Eight queens produce

```
8 choose 2
```

possible pairs.

$$
\binom{8}{2} = \frac{8!}{2!(8-2)!} = \frac{8!}{2!6!} = \frac{8 \cdot 7}{2 \cdot 1} = 28
$$

Therefore

Maximum possible fitness

```
28
```

---

## Fitness Formula

```
Fitness

=

28

−

(Number of attacking pairs)
```

---

# Figure 4.6(b)

The four individuals receive scores

```
24

23

20

11
```

The book explicitly states these values.

---

## Interpretation

Higher score

↓

Fewer attacking queens

↓

Better board

---

## Best Individual

```
Fitness = 24
```

Only

```
4 attacking pairs
```

because

```
28 − 4 = 24
```

---

## Worst Individual

```
Fitness = 11
```

Many queens attack one another.

---

# Why Fitness Matters

Fitness determines

```
Probability of reproduction
```

Not every individual gets to become a parent.

Better individuals are selected more frequently.

---

# Step 3 — Normalize Fitness

Raw fitness values

```
24

23

20

11
```

are converted into probabilities.

---

## Total Fitness

```
24 + 23 + 20 + 11 = 78
```

---

## Probability Formula

$$
P(i) = \frac{\text{Fitness}(i)}{\sum \text{Fitness}}
$$

## Individual 1

$$
\frac{24}{78} \approx 0.31 \; (31\%)
$$

## Individual 2

$$
\frac{23}{78} \approx 0.29 \; (29\%)
$$

## Individual 3

$$
\frac{20}{78} \approx 0.26 \; (26\%)
$$

## Individual 4

$$
\frac{11}{78} \approx 0.14 \; (14\%)
$$
---

# Figure 4.6(b)

The normalized probabilities become

| Fitness | Probability |
|----------|-------------|
|24|31%|
|23|29%|
|20|26%|
|11|14%|

---

> [!important]
> Fitness determines **likelihood** of reproduction.
>
> It does **not** guarantee reproduction.

---

# Step 4 — Parent Selection

Parents are selected

according to

their probabilities.

Selection is random,

but biased toward higher fitness.

---

Example

Imagine spinning a roulette wheel.

Large fitness

↓

larger slice of wheel

↓

higher probability.

## Figure 4.6(c)

The book notes:

- one individual is selected twice
- one individual is not selected at all

This is perfectly acceptable.

Selection occurs **with probability**, not fairness.

---

> [!note]
> Even weak individuals still have a chance of reproducing.
>
> This preserves diversity.

---

# Selected Parents

The selected parents are grouped into pairs.

Example

```
Parent A

Parent B
```

↓

produce offspring

---

# Step 5 — Crossover

Once parents are chosen, the algorithm performs crossover.

## Crossover Point

A random crossover point is selected.

Example

```
327|52411
```

```
247|48552
```

---

## Child 1

Take

left half of Parent 1

+

right half of Parent 2

```
327

+

48552

=

32748552
```

## Child 2

Take

left half of Parent 2

+

right half of Parent 1

```
247

+

52411

=

24752411
```


This produces two children.

# Figure 4.6(d)

The crossover operation is shown graphically.

Each child receives part of each parent's genome.

## Why Crossover?

The goal is to combine useful traits from different parents.

Instead of modifying a solution slightly, genetic algorithms can make large jumps through the search space.

![[Pasted image 20260626142159.png|449]]

Figure 4.7 illustrates crossover using actual chess boards, rather than strings.

The figure shows

- Parent 1 board
- Parent 2 board

↓

crossover

↓

Child board

This helps visualize how exchanging digits changes queen positions.

## Important Observation

The crossover occurs on the string, not directly on the chess board. Changing the string automatically changes the board.

# Step 6 — Mutation

After crossover, every child undergoes mutation.

Mutation is random.

## Mutation Rule

Each position has a small independent probability of changing.

---

For 8-Queens

Mutation means

```
Choose one queen

↓

Move it to another row

within the same column
```

---

# Figure 4.6(e)

The book states

One mutation occurred in

- Child 1
- Child 3
- Child 4

One child

received

no mutation.

## Why Mutation?

Mutation introduces new genetic material. Without mutation, once information disappears, it can never reappear.

## Diversity

Early generations

↓

high diversity

↓

crossover makes large jumps

---

Later generations

↓

population becomes similar

↓

crossover makes smaller changes

---

Mutation prevents

premature convergence.

---

> [!important]
> Mutation is **not** intended to improve every child.
>
> Its purpose is to preserve exploration of the search space.

---

# Complete Figure 4.6 Pipeline

```
Random Population

↓

Evaluate Fitness

↓

Normalize Fitness

↓

Select Parents

↓

Choose Random Crossover Point

↓

Create Children

↓

Mutate Children

↓

Next Generation
```

---

# Why This Works

Every generation tends to contain more high-fitness individuals than the previous one.

Over many generations the average fitness increases.

The search gradually moves toward

high-quality solutions.

---

# Relationship to Earlier Algorithms

The book notes that Genetic Algorithms are similar to Stochastic Beam Search, but add

```
Crossover
```

---

Instead of exploring independent solutions, the algorithm combines good partial solutions from different parents.

---

# Example Walkthrough

Suppose

```
Parent 1

32752411
```

```
Parent 2

24748552
```

Random crossover point

```
327|52411

247|48552
```

Children become

```
32748552

24752411
```

After mutation

```
32748552

↓

32748152
```

(one digit changes)

This mutated child becomes part of the next generation.

---

> [!tip] Exam Mnemonic
>
> **Genetic Algorithm Pipeline**
>
> **Population → Fitness → Selection → Crossover → Mutation → Repeat**
>
> Remember:
>
> **PFSCMR**
>
> **P**opulation
> **F**itness
> **S**election
> **C**rossover
> **M**utation
> **R**epeat

---

# Key Takeaways

> [!summary]
>
> - Genetic algorithms maintain a **population**, not a single state.
> - Every individual is evaluated using a **fitness function**.
> - Fitness values are converted into **selection probabilities**.
> - Better individuals are **more likely**, but not guaranteed, to reproduce.
> - Crossover combines parts of two parents to create offspring.
> - Mutation introduces random variation after crossover.
> - Figure 4.6 illustrates one complete generation from population to offspring.
> - Figure 4.7 visualizes crossover using actual 8-Queens boards instead of strings.

---

# 4.2 Local Search in Continuous Spaces

> [!abstract]
> In previous chapters, search problems assumed **discrete state spaces**, where each state has a finite number of successors. Many real-world optimization problems, however, involve **continuous variables**, creating an **infinite branching factor**. Because infinitely many successor states exist, most graph-search algorithms cannot be applied directly.
>
> This section introduces local search methods designed specifically for continuous optimization problems.


## Why Continuous Spaces are Different

In Chapter 2, the book distinguished between **discrete** and **continuous** environments. While discrete environments contain a finite set of states and actions, most real-world environments are continuous.

A continuous action space has an **infinite branching factor**, because every variable can change by infinitely many possible amounts.

As a result, algorithms such as:

- Breadth-First Search
- Uniform Cost Search
- A*
- Greedy Best-First Search

cannot enumerate every successor.

The only local search algorithms discussed previously that naturally extend to continuous spaces are:

- First-choice hill climbing
- Simulated annealing

---

> [!example] Example — Airport Placement Problem
>
> Suppose we want to build **three airports** anywhere in Romania.
>
> The objective is to minimize the total squared straight-line distance from every city to its nearest airport.
>
> Unlike graph search, we do **not** search over cities or roads.
>
> Instead, we search over the possible coordinates of the airports.

---

# State Representation

Each airport has two coordinates:

- x-coordinate
- y-coordinate

Therefore, three airports require six variables.

$$
(x_1,y_1),\ (x_2,y_2),\ (x_3,y_3)
$$

The search state is therefore represented as

$$
x =
(x_1,y_1,x_2,y_2,x_3,y_3)
$$

This is a **six-dimensional state space**.

In general, continuous optimization problems represent each state using an **n-dimensional vector** of variables.

---

> [!note]
> In continuous optimization, a **state** is no longer a node in a graph.
>
> Instead, it is simply one point in a multidimensional mathematical space.

---

# Objective Function

The objective function measures the quality of every airport configuration.

For each airport:

- determine which cities are closest to that airport,
- compute the squared Euclidean distance from the airport to each assigned city,
- sum all of those squared distances.

The objective function is

$$
f(x)
=
\sum_{i=1}^{3}
\sum_{c\in C_i}
\left[
(x_i-x_c)^2
+
(y_i-y_c)^2
\right]
$$

where:

- \(C_i\) is the set of cities closest to airport \(i\)
- \((x_c,y_c)\) is the coordinate of city \(c\)

A **smaller value** of \(f(x)\) indicates a better airport placement.

---

> [!important]
> The formula above is only locally correct.
>
> If an airport moves far enough, some cities may become closer to another airport. The sets \(C_i\) must then be recomputed before evaluating the objective function again.

---

# Discretization

One way to search a continuous space is to convert it into a discrete one.

Instead of allowing every coordinate to take infinitely many values, coordinates are restricted to a fixed grid with spacing

$$
\delta
$$

Each variable can then move only by

$$
+\delta
\quad\text{or}\quad
-\delta
$$

For six variables, every state has

$$
2 \times 6 = 12
$$

possible neighboring states.

Once discretized, ordinary local search algorithms such as hill climbing can be applied.

---

> [!tip]
> Smaller values of \( \delta \) produce more accurate solutions but also require many more search steps.

---

# Random Sampling

Instead of constructing a grid, another approach is to generate successor states randomly.

At every step:

1. choose a random direction,
2. move by a small distance \( \delta \),
3. evaluate the objective function.

This keeps the branching factor finite even though the underlying space remains continuous.

---

# Empirical Gradient Methods

Empirical gradient methods estimate which direction improves the objective function by comparing nearby points.

Rather than computing derivatives mathematically, they simply measure how the objective function changes after making small movements.

Conceptually, this is equivalent to performing **steepest-ascent hill climbing** on a finely discretized version of the continuous space.

Reducing \( \delta \) over time generally improves accuracy, although it does **not** guarantee convergence to the global optimum.

---

# Analytical Gradient Methods

When the objective function has a mathematical expression, calculus can be used directly.

Instead of estimating the best direction, the algorithm computes the **gradient**.

The gradient is written as

$$
\nabla f
$$

and is the vector pointing in the direction of **steepest increase** of the objective function.

For the airport example,

$$
\nabla f
=
\left(
\frac{\partial f}{\partial x_1},
\frac{\partial f}{\partial y_1},
\frac{\partial f}{\partial x_2},
\frac{\partial f}{\partial y_2},
\frac{\partial f}{\partial x_3},
\frac{\partial f}{\partial y_3}
\right)
$$

Each component tells how rapidly the objective function changes when one variable changes.

---

# Finding an Optimum

Sometimes the optimum can be found exactly by solving

$$
\nabla f = 0
$$

For example, if there is only **one airport**, the optimal position is simply the arithmetic mean (centroid) of all city coordinates.

For multiple airports, however, the gradient depends on which cities are closest to each airport, making a closed-form solution impossible.

---

# Partial Derivative Example

For airport 1,

$$
\frac{\partial f}{\partial x_1}
=
2
\sum_{c\in C_1}
(x_1-x_c)
$$

Similar equations exist for the remaining variables.

These derivatives are valid only while the assignment of cities to airports remains unchanged.

---

# Gradient Ascent Update Rule

After computing the gradient, hill climbing updates the current state using

$$
x
\leftarrow
x
+
\alpha
\nabla f(x)
$$

where

- \( \alpha \) is the **step size**
- \( \nabla f(x) \) is the gradient

---

> [!definition]
> **Step Size (\(\alpha\))**
>
> Determines how far the algorithm moves along the gradient during each iteration.

---

# Choosing the Step Size

The choice of \( \alpha \) is critical.

If the step size is too small:

- convergence is very slow.

If the step size is too large:

- the algorithm may overshoot the optimum.

---

# Line Search

Line search automatically adjusts the step size.

Instead of choosing a fixed value, the algorithm repeatedly increases the step length—often by doubling \( \alpha \)—while the objective function continues to improve.

Once improvement stops, the best point reached becomes the new current state.

---

# Newton–Raphson Method

One of the most important optimization methods is the **Newton–Raphson method**.

Originally developed for solving equations

$$
g(x)=0,
$$

the update rule is

$$
x
\leftarrow
x
-
\frac{g(x)}{g'(x)}
$$

For optimization problems, we let

$$
g(x)=\nabla f(x),
$$

leading to

$$
x
\leftarrow
x
-
H_f^{-1}(x)
\nabla f(x)
$$

where

$$
H_f(x)
$$

is the **Hessian matrix**.

---

# Hessian Matrix

The Hessian contains all second-order partial derivatives.

Its entries are

$$
H_{ij}
=
\frac{\partial^2 f}
{\partial x_i \partial x_j}
$$

The Hessian measures the curvature of the objective function.

For the airport example:

- off-diagonal entries are zero,
- diagonal entries equal twice the number of cities assigned to each airport.

One Newton step therefore moves each airport directly to the centroid of its assigned cities.

---

> [!important]
> Computing and inverting the Hessian can be expensive for high-dimensional problems because an \(n\)-variable problem requires an \(n \times n\) matrix.

---

# Challenges of Continuous Local Search

Continuous optimization suffers from the same problems as discrete hill climbing:

- Local maxima
- Local minima
- Plateaus
- Ridges

To reduce the chance of becoming trapped, the book recommends:

- Random restarts
- Simulated annealing

High-dimensional continuous spaces remain particularly difficult because they contain an enormous number of possible directions.

---

# Constrained Optimization

Many optimization problems require solutions to satisfy hard constraints.

For the airport example:

- airports must remain inside Romania,
- airports cannot be placed inside lakes.

Such problems are called **constrained optimization** problems.

---

# Linear Programming

One important class of constrained optimization is **linear programming**.

Requirements:

- constraints are linear inequalities,
- feasible region is a convex set,
- objective function is linear.

Linear programming problems are solvable in polynomial time.

---

# Convex Optimization

Linear programming is a special case of **convex optimization**.

Convex optimization allows:

- any convex feasible region,
- any convex objective function.

Under suitable conditions, these problems are also polynomially solvable and can handle thousands of variables.

The AI textbook notes that convex optimization plays a major role in:

- Machine Learning
- Control Theory

(covered later in Chapter 21).

---

> [!summary]
>
> - Continuous spaces have infinitely many successors.
> - States are represented as vectors of variables.
> - Objective functions measure solution quality.
> - Discretization converts continuous search into finite search.
> - Empirical gradients estimate improvements numerically.
> - Analytical gradients use calculus.
> - Gradient ascent follows the steepest improvement direction.
> - Step size controls movement.
> - Line search automatically adjusts step size.
> - Newton–Raphson uses the Hessian for faster convergence.
> - Continuous optimization still suffers from local maxima and plateaus.
> - Constrained optimization introduces hard restrictions on variables.
> - Linear programming and convex optimization solve important classes of constrained problems.

