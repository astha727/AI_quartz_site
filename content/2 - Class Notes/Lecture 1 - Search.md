Refer: [[Chapter 3 - Solving Problems by Searching]], [[MIT 6.034 Lecture 4 - Search - Hill Climbing, Depth - First, Beam]]
## Search as Problem Solving

> [!info]+ Core Idea  
> Problem solving occurs when an agent cannot immediately determine the correct action.
> 
> Instead of acting reflexively, the agent must reason about future possibilities and search for a sequence of actions that achieves a goal.

AI search problems arise when:

- many possible states exist,
- many action sequences are possible,
- choosing the wrong action early can lead to failure later.

## Two Sources of Complexity

### 1. Search Complexity

The complexity comes from:

- many possible states,
- many possible actions,
- long sequences of decisions.

Example:

![[Pasted image 20260621115112.png|459]]

```
Arad 
├── Sibiu 
├── Zerind 
└── Timisoara
```

The challenge is deciding which branch to follow.

> [!example]+ Route Finding  
> Driving from Arad to Bucharest requires choosing the correct sequence of roads.
> 
> The difficulty comes from planning ahead through many possible routes.

---

### 2. Uncertainty Complexity

Another type of difficulty occurs when:

- the environment is partially observable,
- outcomes are uncertain,
- actions may have unknown effects.

Example:

```
Driving in fog
```

The agent may not know:

- where roads lead,
- what obstacles exist,
- whether actions will succeed.

> [!note]+ Important Distinction  
> Search problems assume the environment is known.
> 
> Later AI topics deal with uncertainty, probability, and incomplete information.

---

# What is a Problem?

A search problem consists of five components.

## 1. Initial State

The starting point.

Example:

```
Agent is in Arad
```

## 2. Actions Function

```
Actions(s)
```

Returns all legal actions available in state `s`.

Example:

```
Actions(Arad)
	→ Go to Sibiu
	→ Go to Zerind
	→ Go to Timisoara
```

> [!tip]  
> Different states may have different action sets.

## 3. Result Function

```
Result(state, action)
```

Returns the state produced by performing an action.

Example:

```
Result(Arad, Go To Timisoara)= Timisoara
```

## 4. Goal Test

```
GoalTest(state)
```

Determines whether the current state satisfies the goal.

Example:

```
GoalTest(Bucharest)= True
```

```
GoalTest(Arad)= False
```

## 5. Path Cost Function

Measures the cost of a complete solution.

```
Path Cost = Sum of Step Costs
```

Example:

```
Arad
	→ Sibiu
	→ Rimnicu Vilcea
	→ Pitesti
	→ Bucharest
```

Total cost:

```
140 + 80 + 97 + 101
```

> [!important]  
> Many solutions may reach the goal.
> 
> Cost allows us to compare which solution is better.

# State Space

## Definition

The state space is the set of all states reachable from the initial state.

For Romania:

```
States = All cities
```

Examples:

- Arad
- Sibiu
- Bucharest
- Timisoara
- Zerind

---

## Navigating the State Space

Search algorithms explore the state space by applying actions.

```
State
↓ 
Action
New State
↓ 
Action
New State
```

This generates paths.

---

# Frontier, Explored, and Unexplored Regions

During search, the state space naturally divides into three regions.

![[Pasted image 20260621132720.png|450]]

```
Explored | Frontier | Unexplored
```

## Explored Region

States already expanded.

```
✓ Already processed
```

## Frontier

States discovered but not yet expanded.

```
? Waiting to be explored
```

## Unexplored Region

States not yet discovered.

```
Unknown territory
```

> [!important]+ Frontier  
> The frontier is the most important data structure in search.
> 
> Different search algorithms differ primarily in how they choose which frontier node to expand next.

# Tree Search

## Core Idea

Tree Search overlays a search tree onto the state space.

```
State Space
```

becomes

```
Search Tree
```

by recording every path explored.

## Generic Tree Search Algorithm

```
Initialize FrontierLoop:    
If Frontier Empty:        
	Failure    
Select Path    

If Goal:       
	 Return Solution    

Expand Path    
Add New Paths to Frontier
```

> [!note]  
> Tree Search is not one algorithm.
> 
> It is a framework.
> 
> Different search algorithms differ only in how they select paths from the frontier.


# Breadth-First Search (BFS)

## Principle

Always expand the shortest path first.

```
Level 0  Level 1  Level 2  Level 3
```

The search spreads outward uniformly.

### Example

```
Arad
├── Sibiu
├── Zerind
└── Timisoara
```

Expand all depth-1 nodes before any depth-2 node.

## Why BFS Works

The first goal discovered must be the shallowest goal.

> [!important]  
> BFS guarantees the minimum number of actions when all actions have equal cost.


## Characteristics

|Property|BFS|
|---|---|
|Complete|Yes|
|Optimal|Yes (equal costs)|
|Memory Usage|Very High|
|Speed|Slow on large spaces|
# Graph Search

## Problem with Tree Search

Tree Search repeatedly revisits states.

Example:

```
Arad→ Sibiu→ Arad
```

This creates redundant work.

## Solution

Maintain an explored set.

```
Explored Set
```

When a state has already been expanded:

```
Ignore it
```

> [!important]+ Graph Search  
> Graph Search = Tree Search
> 
> - Explored Set
> 
> This eliminates repeated exploration and dramatically improves efficiency.

# Uniform Cost Search (UCS)

## Principle

Always expand the path with the lowest cumulative cost.

Not:

```
Shortest Path
```

but

```
Cheapest Path
```

## Frontier Ordering

BFS orders by:

```
Depth
```

UCS orders by:

```
Total Cost
```

---

### Example

```
Path A Cost = 75
Path B Cost = 140 
Path C Cost = 118
```

UCS expands:

```
Path A
```

first.

## Key Insight

A goal found early may not be optimal.

Therefore UCS does **not stop** when it first discovers a goal.

Instead it stops when:

```
Goal Path is removed from frontier
```

because only then can it guarantee no cheaper path exists.

---

> [!warning]+ Common Exam Trap  
> UCS does NOT terminate when a goal is added to the frontier.
> 
> UCS terminates when a goal path is removed from the frontier.

---
# Search Algorithm Properties

After learning how BFS, DFS, and Uniform-Cost Search operate, we need a way to evaluate and compare them.

The most important criteria are:

1. **Optimality**
2. **Space Complexity**
3. **Completeness**

These properties determine whether an algorithm is practical for large AI problems.

---

# Optimality

An algorithm is **optimal** if it always returns the best solution according to the problem's objective.

Depending on the problem, "best" may mean:

- shortest path,
- lowest cost path,
- highest reward,
- least risk.

## Breadth-First Search

Breadth-First Search expands paths in order of increasing depth.

```
Level 0
│
├── Level 1
│
├── Level 2
│
├── Level 3
│
└── ...
```

Because BFS examines every path of length `d` before considering paths of length `d+1`, the first goal discovered is guaranteed to have the fewest number of steps.

Also Refer: [[Breadth-First Search]], [[Chapter 3 - Solving Problems by Searching]]

> [!success]+ BFS Optimality  
> BFS is optimal when all step costs are identical.
> 
> Example:
> 
> If every road costs 1 unit to traverse, BFS finds the shortest path.

## Uniform-Cost Search

Uniform-Cost Search expands the cheapest path first.

```
Expand path with smallest g(n)
```

where:

```
g(n) = path cost so far
```

Because every cheaper path is explored before more expensive paths, UCS is guaranteed to find the minimum-cost solution.

> [!success]+ UCS Optimality  
> Uniform-Cost Search is optimal whenever all step costs are non-negative.

## Depth-First Search

DFS simply follows one branch as deeply as possible.

```
Start 
│
▼ 
A 
│ 
▼ 
B 
│ 
▼ 
C
```

It may find a goal quickly.

It may also find a terrible solution while a much better one exists nearby.

> [!warning]+ DFS Is Not Optimal  
> DFS returns the first solution it encounters.
> 
> A shorter or cheaper solution may exist elsewhere.

---

# Why Use DFS If It Isn't Optimal?

At first glance DFS seems inferior.

- Not optimal.
- Not complete in infinite spaces.
- Can get lost.

Yet DFS remains extremely useful.

The reason is memory.

---

# Space Complexity

Memory often becomes a bigger problem than time.

Suppose we have a binary tree:

```
            Root           
            /    \         
		    /      \        
		    /        \     
	    Level 1      
	    Level 2      
	    Level 3      
	    ...      
	    Level n
```

Each node generates two children.

## BFS Memory Usage

At depth `n`:

```
Number of nodes ≈ 2^n
```

The frontier contains an entire level.

Example:

|Depth|Frontier Size|
|---|---|
|10|1,024|
|20|1,048,576|
|30|1,073,741,824|

The memory requirement explodes exponentially.

> [!danger]+ BFS Weakness  
> BFS frequently runs out of memory before it runs out of time.

## UCS Memory Usage

Uniform-Cost Search behaves similarly.

Instead of storing a full level:

```
It stores a cost contour.
```

Conceptually it still accumulates huge numbers of frontier nodes.

Memory growth remains exponential.

## DFS Memory Usage

DFS stores only the current path plus a small number of alternatives.

```
Root 
│ 
├─ Alternative 
│ 
▼ Current Path 
│ 
▼ Node
```

At depth `n`:

```
Memory ≈ O(n)
```

instead of

```
O(2^n)
```

> [!tip]+ DFS Advantage  
> DFS uses dramatically less memory than BFS or UCS.
> 
> This is often the primary reason to choose DFS.

---

# Completeness

Completeness asks:

> If a solution exists, will the algorithm eventually find it?

## BFS Completeness

BFS explores level by level.

```
Depth 0
Depth 1
Depth 2
Depth 3
...
```

If the goal exists at any finite depth:

```
Eventually BFS reaches it.
```

> [!success]+ BFS Is Complete  
> BFS always finds a solution if one exists at a finite depth.

## UCS Completeness

Uniform-Cost Search expands paths by increasing cost.

```
Cost 1
Cost 2
Cost 3
Cost 4
...
```

If the goal has finite cost:

```
Eventually UCS reaches it.
```

> [!success]+ UCS Is Complete  
> UCS always finds a solution with finite cost.

## DFS Completeness

Consider this tree:

```
Start 
│ 
├── Goal 
│ 
└── Infinite Branch        
		│        
		▼        
		▼        
		▼        
		▼        
		▼        
		...
```

DFS might choose the infinite branch.

```
Down
Down
Down
Down
Down
...
```

forever.

It never comes back.

The goal is never reached.

> [!danger]+ DFS Is Not Complete  
> In infinite search spaces DFS can fail even when a solution exists.

---

# Understanding Uniform-Cost Search Geometrically

Uniform-Cost Search expands outward like a growing wave.

Imagine dropping a stone into water.

```
     Goal   (     ) (         )(    S      )
```

Expansion occurs in increasing cost contours.

First:

```
Cost = 1
```

Then:

```
Cost = 2
```

Then:

```
Cost = 3
```

and so on.

## The Problem

Uniform-Cost Search does not know where the goal is.

It expands equally in all directions.

```
        ↖  ↑  ↗
    ←   Start   →   
        ↙  ↓  ↘      
```

Even if the goal lies to the east:

```
UCS still explores north,south,west,and east.
```

> [!important]+ Key Insight  
> Uniform-Cost Search is optimal because it is unbiased.
> 
> Unfortunately, that same lack of bias makes it inefficient.

---

# Motivation for Heuristic Search

Suppose we know something about the goal.

For example:

```
Straight-line distance to Bucharest
```

or

```
Estimated distance remaining
```

Instead of searching everywhere equally, we can prefer states that appear closer to the goal.

This idea leads to:

- Greedy Best-First Search
- A* Search

which are the next major search algorithms in AI.

# The Limitation of Uniform Cost Search

Although UCS is optimal, it has no idea where the goal is.

> [!warning]+ Main Weakness  
> UCS spends substantial effort exploring states that clearly move away from the goal.
> 
> It uses cost information but ignores direction.

# Heuristics

## What Is a Heuristic?

> [!definition]+ Heuristic Function  
> A heuristic is a function:
> 
> ```
> h(n)
> ```
> 
> that estimates the remaining cost from node:
> 
> ```
> n
> ```
> 
> to the goal.

### Example

Romania Route Problem

```
h(Arad) = 366
```

Straight-line distance to Bucharest.

```
h(Sibiu) = 253
```

```
h(Fagaras) = 176
```

> [!tip]+ Intuition  
> Heuristics provide directional guidance.
> 
> They answer:
> 
> "Which state appears closer to the goal?"

# Greedy Best-First Search

## Basic Idea

Always expand the node with the smallest:

```
h(n)
```

### Evaluation Function

```
f(n) = h(n)
```

### Example

|City|h(n)|
|---|---|
|Sibiu|253|
|Zerind|374|
|Timisoara|329|

Greedy Search chooses:

```
Sibiu
```

because:

```
253 is smallest
```

### Advantage

> [!success]+ Fast Goal Direction  
> Greedy Search often reaches the goal using far fewer expansions than UCS.

### Problem

> [!danger]+ Greedy Is Not Optimal  
> Greedy ignores the cost already spent.
> 
> A node may appear close to the goal while actually requiring a very expensive route.

# A* Search

## Combining UCS and Greedy

> [!abstract]+ Key Insight  
> UCS considers:
> 
> ```
> cost so far
> ```
> 
> Greedy considers:
> 
> ```
> estimated cost remaining
> ```
> 
> A* combines both.

## Evaluation Function

```
f(n) = g(n) + h(n)
```

Where:

```
g(n = cost from start to node
```

and

```
h(n) = estimated cost from node to goal
```

### Interpretation

|Component|Meaning|
|---|---|
|g(n)|Cost already paid|
|h(n)|Estimated remaining cost|
|f(n)|Estimated total solution cost|

## Romania Example

|Path|g(n)|h(n)|f(n)|
|---|---|---|---|
|Arad → Sibiu|140|253|393|
|Arad → Timisoara|118|329|447|
|Arad → Zerind|75|374|449|

A* chooses:

```
Arad → Sibiu
```

because:

```
393
```

is smallest.

---

> [!success]+ Why A* Works So Well  
> A* simultaneously:
> 
> - keeps paths cheap,
> - keeps search directed,
> - avoids excessive wandering.

# Admissible Heuristics

## Definition

> [!definition]+ Admissible Heuristic  
> A heuristic is admissible if:
> 
> ```
> h(n) ≤ true cost to goal
> ```
> 
> for every node.

It never overestimates.

### Alternative Names

- Optimistic heuristic
- Lower-bound heuristic
- Never-overestimating heuristic

## Romania Example

Straight-line distance:

```
Arad → Bucharest = 366 km
```

Actual road distance:

```
Arad → Bucharest = 418 km
```

Since:

```
366 ≤ 418
```

the heuristic is admissible.

---

# Why Admissibility Guarantees Optimality

> [!important]+ Core Proof Idea  
> Every frontier node has:
> 
> ```
> f(n) = g(n)+h(n)
> ```
> 
> If h(n) never overestimates:
> 
> ```
> f(n)
> ```
> 
> is a lower bound on any solution passing through that node.
> 
> Therefore when A* selects a goal node for expansion, no cheaper solution can still be hidden elsewhere.

---

# Search Beyond Maps

Search is a general framework.

Maps are only one example.

## State Space Examples

|Domain|State|
|---|---|
|Romania Map|Current city|
|Vacuum World|Robot + dirt locations|
|Chess|Board configuration|
|Sliding Puzzle|Tile arrangement|


> [!note]+ MIT Connection  
> Patrick Winston repeatedly emphasizes:
> 
> Search is not about maps.
> 
> Search is about **choice**.
> 
> Maps simply provide a convenient visualization.

# State-Space Explosion

## Vacuum World Example

Robot position:

```
2 possibilities
```

Dirty/Clean at A:

```
2 possibilities
```

Dirty/Clean at B:

```
2 possibilities
```

Total states:

```
2 × 2 × 2 = 8
```

![[Pasted image 20260621201054.png|568]]
## Larger Vacuum World

Suppose:

- 10 locations
- 3 power modes
- 2 camera modes
- 5 brush settings
- 2¹⁰ dirt configurations

Total:

```
3 × 2 × 5 × 10 × 2¹⁰ = 307,200 states
```

> [!danger]+ Combinatorial Explosion  
> State spaces often grow exponentially.
> 
> Search algorithms exist because brute-force enumeration quickly becomes impossible.

# Sliding Puzzle Heuristics

## Misplaced Tiles

### Definition

```
h₁ = number of tiles not in goal position
```

---

### Why Admissible?

Every misplaced tile must move at least once.

Therefore:

```
h₁ ≤ true solution cost
```

## Manhattan Distance

### Definition

```
h₂ =Σ distance of each tile to its goal square
```

### Why Admissible?

A tile can move only one square closer per move.

Therefore:

```
h₂ ≤ true solution cost
```

## Comparison

|Heuristic|Admissible|Stronger|
|---|---|---|
|Misplaced Tiles|Yes|No|
|Manhattan Distance|Yes|Usually|


> [!tip]+ Heuristic Dominance  
> If:
> 
> ```
> h₂(n) ≥ h₁(n)
> ```
> 
> for almost all nodes,
> 
> then A* with h₂ generally expands fewer nodes.

# Relaxed Problems

## Generating Heuristics Automatically

Instead of inventing heuristics manually:

Simplify the original problem.

### Example

Original rule:

```
A block may moveonly into a blank adjacent square
```

---

### Relaxation 1

Remove:

```
blank square requirement
```

---

### Relaxation 2

Remove:

```
adjacency requirement
```

> [!important]+ Relaxation Principle  
> Relaxing constraints creates an easier problem.
> 
> Easier problems always have solution costs less than or equal to the original problem.
> 
> Therefore their costs become admissible heuristics.

---

# Assumptions Behind Classical Search

Classical search assumes:

1. Fully observable
2. Deterministic
3. Static
4. Known
5. Discrete

---

If these assumptions hold:

> [!success]+ Open-Loop Planning  
> The agent can compute an entire solution before acting.

---

If they fail:

> [!warning]+ Need More Advanced AI  
> We move toward:
> 
> - probabilistic reasoning,
> - online search,
> - planning under uncertainty,
> - reinforcement learning,
> - POMDPs.

# Implementation Notes

## Node Structure

Each node stores:

```
State
Parent
Action
Path Cost
Depth
```

---

### Why Store Parent?

> [!tip]+ Path Reconstruction  
> When the goal is found:
> 
> Follow parent pointers backward.
> 
> Reverse the sequence.
> 
> Recover the complete solution path.

## Frontier

Typically implemented using:

- Queue (BFS)
- Stack (DFS)
- Priority Queue (UCS, A*)

## Explored Set

Typically implemented using:

```
Hash Set
```

Provides:

```
O(1)
```

membership checking.

# Big Picture

> [!summary]+ Connecting the Three Sources
> 
> **Norvig & Russell**
> 
> - Formal search framework
> - State spaces
> - Completeness
> - Optimality
> 
> **Georgia Tech OMSCS**
> 
> - Frontier mechanics
> - BFS/UCS implementation details
> - Goal-testing subtleties
> - Heuristic design
> 
> **MIT (Patrick Winston)**
> 
> - Search as a model of human deliberation
> - Search as choice
> - Heuristic reasoning as intelligent behavior
> 
> Together they form the foundation of classical AI search.

# Comparison Summary

## Search Algorithm Comparison

| **Property**          | **DFS**     | **BFS**             | **UCS**           | **Greedy Best-First** | **A***                  |
| --------------------- | ----------- | ------------------- | ----------------- | --------------------- | ----------------------- |
| Complete              | ❌ No        | ✅ Yes               | ✅ Yes             | ❌ Not always          | ✅ Yes*                  |
| Optimal               | ❌ No        | ✅ Yes*              | ✅ Yes             | ❌ No                  | ✅ Yes*                  |
| Space Usage           | Very Low    | Very High           | Very High         | High                  | High                    |
| Time Usage            | Can Be Fast | High                | High              | Often Fast            | Usually Better Than UCS |
| Finds Cheapest Path   | ❌           | Only if equal costs | ✅                 | ❌                     | ✅                       |
| Uses Cost Information | ❌           | ❌                   | ✅ g(n)            | ❌                     | ✅ g(n)                  |
| Uses Heuristic        | ❌           | ❌                   | ❌                 | ✅ h(n)                | ✅ h(n)                  |
| Infinite Trees        | May Fail    | Works               | Works             | May Fail              | Works*                  |
| Main Strength         | Low Memory  | Shortest Steps      | Cheapest Cost     | Goal Directed         | Optimal + Goal Directed |
| Main Weakness         | Not Optimal | Huge Memory         | Explores Too Much | Can Choose Bad Paths  | Requires Good Heuristic |

>[!note]+ Conditions for the Asterisks
>**BFS Optimal***  
>Only when every step cost is identical.
>**A* Complete and Optimal***  
When the heuristic is:
> - admissible (never overestimates),
> - and for graph search preferably consistent (monotonic).


> [!summary]+ Exam Takeaway
> 
> - DFS = memory efficient, not complete, not optimal.
> - BFS = complete and shortest-path optimal (equal costs).
> - UCS = complete and cost optimal.
> - UCS expands by **cost contours**.
> - BFS expands by **depth layers**.
> - DFS expands by **one branch at a time**.
> - The inefficiency of UCS motivates **heuristic search**, leading directly to **Greedy Best-First Search** and **A***.
> -  A* → Lowest cost + heuristic guidance
> 
> - Greedy → Fast but not necessarily optimal

### Frontier Ordering

|Algorithm|Expands Node With Lowest|
|---|---|
|DFS|Depth (deepest first)|
|BFS|Depth (shallowest first)|
|UCS|g(n)|
|Greedy|h(n)|
|A*|g(n) + h(n)|

Where:

```
g(n) = cost from start to node
h(n) = estimated cost to goal
f(n) = g(n) + h(n)
```

> [!tip]+ Exam Shortcut
> 
> **DFS** → Lowest memory
> 
> **BFS** → Shortest number of actions
> 
> **UCS** → Cheapest path
> 
> **Greedy** → Fastest goal-directed search
> 
> **A*** → Cheapest path while staying goal-directed
# Connections to MIT 6.034

Patrick Winston's search lectures emphasize:

> Search is not about maps.
> 
> Search is about choices.

Maps are merely visual examples.

The deeper principle is:

```
Current State
↓
Possible Choices
↓
Future Consequences
↓
Select Path
```

This same structure appears in:

- route finding,
- theorem proving,
- game playing,
- planning,
- diagnosis,
- scientific reasoning.

---

# Connection to Human Cognition

> [!tip]+ Cognitive Perspective  
> Search can be viewed as a computational model of deliberation.
> 
> Before acting, humans often mentally simulate future possibilities and evaluate outcomes.
> 
> Search algorithms formalize this process.

Examples:

- choosing a career,
- planning a trip,
- solving a math problem,
- deciding on a chess move.

The mind explores possible futures before committing to action.

## Related Notes

[[MIT 6.034 Lecture 4 - Search - Hill Climbing, Depth - First, Beam]]
[[Chapter 3 - Solving Problems by Searching]]

More
### Search (Part 2): Comparing Search Algorithms, A*, and Heuristics

Based on Georgia Tech OMSCS AI lectures 24–50

### Search Comparison: BFS vs UCS vs DFS

Three important uninformed search strategies:

### Breadth-First Search (BFS)

Optimal for equal-cost steps

Rule

Expand the shallowest path first (fewest actions).

Example expansion order

1 → 2 → 3 → 4 → 5 → 6 → 7

Moves level-by-level across the search tree.

Properties

Complete?

Yes

Optimal?

Yes (when all step costs are equal)

Memory usage

Very high (≈ 2^n frontier nodes)

### Uniform Cost Search (UCS)

Optimal for positive costs

Rule

Expand the path with the lowest total cost first.

Example expansion order

0 → 2 → 4 → 5 → 6 → 7 → 8

Ordered by cumulative path cost, not by depth.

Properties

Complete?

Yes

Optimal?

Yes (if all step costs are positive)

Memory usage

Very high

### Depth-First Search (DFS)

Low memory

Rule

Expand the deepest path first.

Example expansion order

1 → 2 → 3 → 4 → 5 → 6 → 7

Barrels down one branch before backing up.

Properties

Complete?

No (can get trapped in an infinite branch)

Optimal?

No

Memory usage

Very low (≈ n frontier nodes)

### Why DFS Is Still Used

DFS sacrifices optimality and completeness in exchange for dramatically lower memory usage.

Memory intuition

In a binary tree of depth n:

1. BFS: stores roughly 2^n frontier nodes.
    
2. DFS: stores roughly n nodes along the current branch.
    

This is a huge savings when the search depth is large.

### Completeness

|Algorithm|Complete?|
|---|---|
|BFS|Yes|
|UCS|Yes|
|DFS|No|

Why BFS and UCS are complete

They systematically explore all paths of increasing depth or cost, so any goal at finite depth or finite cost will eventually be reached.

Why DFS is not complete

If one branch is infinite, DFS may follow it forever and never return to explore other branches that contain the goal.

### The Limitation of Uniform Cost Search

UCS expands outward in cost contours, like ripples in a pond.

![Dijkstra vs. A* – Pathfinding | Baeldung on Computer Science](https://images.openai.com/static-rsc-4/9-ijTAP3I73Wg9TewO1TLtuttX5vDlSVAda_bY0wXy7Icgd65uTBla2DKBhNsH9zqUE5csWZ_9Tcj5gbHnSmRUpRRnFSYLNaZcpCq6mAKomkwtDk6DuJsccTg9lpmDmxJk4MVU9z4VFTKmSt6QOpMzAu6tFr6Izh0ceq1ivRMM7zY-MT3WNEuaN9JFHut_Gd?purpose=fullsize)

It guarantees the cheapest path, but it does not use any information about where the goal is. On average, it may need to explore a large portion of the state space before finding the goal.

### Greedy Best-First Search

To speed things up, introduce a heuristic estimate h(n) = estimated distance from state n to the goal.

Greedy rule

Always expand the node with the smallest h(n) (the one that appears closest to the goal).

This often explores far fewer nodes than UCS.

Example intuition

If the goal is to the east, Greedy search keeps moving east whenever possible.

Problem

Greedy search can get trapped by obstacles and choose a much longer route because it only cares about appearing close to the goal, not the actual total path cost.

### A* Search

### A* combines UCS and Greedy search

Best of both

Evaluation function

### f(n) = g(n) + h(n)

g(n) = cost so far from the start

h(n) = estimated remaining cost to the goal

Interpretation

1. g(n) keeps the path actually cheap.
    
2. h(n) keeps the search focused toward the goal.
    
3. f(n) estimates the total cost of a complete solution through n.
    

### Romania Example

From Arad:

|Path|g|h|f = g+h|
|---|---|---|---|
|Arad → Sibiu|140|253|393|
|Arad → Zerind|75|374|449|
|Arad → Timisoara|118|329|447|

A* expands Sibiu first because it has the lowest estimated total cost.

### When Is A* Optimal?

A* is guaranteed to find the lowest-cost path if the heuristic is admissible.

Admissible: h(n) never overestimates the true remaining cost.

Equivalent terms:

- Admissible heuristic
    
- Optimistic heuristic
    
- Never overestimates the distance to the goal
    

Why straight-line distance works in Romania

Roads are at least as long as the straight-line distance between cities, so straight-line distance is always ≤ the true road distance.

### Intuition for Admissibility

Suppose A* returns a path with cost c.

Every remaining path on the frontier has:

f(n) ≥ c

If h(n) never overestimates, then each frontier node's f(n) is a lower bound on the true solution cost through that node.

Therefore no unseen path can be cheaper than c, so the returned path must be optimal.

### State Spaces Beyond Maps

Search is not limited to geographic navigation.

Romania map

State = city.

Vacuum world

State = robot location + dirt configuration.

Sliding-block puzzle

State = arrangement of tiles.

### Vacuum World Example

Two locations: A and B.

Each location may be dirty or clean.

Total states:

robot position

### 2 × 2 × 2 = 8 states

(robot position × dirt at A × dirt at B)

State-space explosion

Adding a few independent variables multiplies the number of states.

For a larger vacuum world:

- 3 power modes
    
- 2 camera states
    
- 5 brush heights
    
- 10 positions
    
- 2^10 dirt configurations
    

Total states:

### 3 × 2 × 5 × 2^10 × 10 = 307,200

A seemingly tiny problem already creates hundreds of thousands of states.

### Sliding-Block Puzzle Heuristics

Goal: arrange tiles 1–15 in order.

### Heuristic h1: Misplaced Tiles

h₁ = number of tiles not in their goal position

Why admissible?

Each misplaced tile must be moved at least once.

### Heuristic h2: Manhattan Distance

h₂ = sum of distances each tile must move to reach its goal square

Why admissible?

A tile can get at most one square closer to its goal per move.

### Comparing h1 and h2

|Heuristic|Admissible?|Usually stronger?|
|---|---|---|
|h1 (misplaced tiles)|Yes|No|
|h2 (Manhattan distance)|Yes|Yes|

Because h2 ≥ h1 for almost all states, A* with h2 expands fewer nodes.

### Generating Heuristics Automatically

The lectures introduce relaxed problems.

Example rule:

A block can move from A to B if A is adjacent to B and B is blank.

Relaxation 1: remove the requirement that B is blank.

Relaxation 2: remove adjacency as well.

Each relaxation makes the problem easier, creating an admissible heuristic.

Key idea

Relaxing constraints adds new legal moves. Easier problems can be solved more cheaply, so their solution costs never overestimate the true problem cost.

### When Classical Search Works

Search-based planning assumes the environment is:

1. Fully observable – the current state is known.
    
2. Known – available actions are known.
    
3. Discrete – there are finitely many choices.
    
4. Deterministic – action outcomes are predictable.
    
5. Static – the world does not change while planning.
    

If all hold

The agent can compute a fixed sequence of actions and execute it without replanning.

If any fail

We need more advanced AI methods such as probabilistic reasoning, online planning, reinforcement learning, or partial-observability techniques.

### Implementation Notes

### Node Structure

A node represents one path in the search tree.

The parent pointer allows reconstruction of the full solution path.

### Data Structures

Frontier

Priority queue + membership set

Supports removing the best node and checking whether a state is already waiting on the frontier.

Explored Set

Hash set or tree

Supports fast membership tests to avoid revisiting states.

### Big Picture

What Norvig emphasizes

Formal problem definition, state spaces, optimality, completeness, and complexity.

What the OMSCS lectures add

Detailed frontier manipulation, BFS/UCS mechanics, why goal tests happen when nodes are removed, heuristic intuition, and practical implementation details.

What MIT adds

Search as a model of human choice and deliberation rather than merely graph traversal.

Together they form a very strong conceptual stack:

Problem formulation

State-space representation

Frontier-based search

Heuristic guidance

Optimal planning under assumptions

### Suggested Obsidian Links

Exam shortcut

BFS = shortest steps, UCS = cheapest cost, DFS = least memory, A* = cheapest cost + heuristic guidance.

Next: [[Lecture 2 - Simulated Annealing]]