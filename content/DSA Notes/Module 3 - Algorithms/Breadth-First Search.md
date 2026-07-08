# Shortest Paths in Graphs (BFS → Dijkstra Framework)

> [!abstract]
> This section develops algorithms for computing **shortest paths in graphs**, starting from the limitations of DFS, moving through BFS, and culminating in **Dijkstra’s algorithm** for weighted graphs.

---

# 1. Why Shortest Paths?

Depth-first search (DFS) explores reachability, but it does **not guarantee optimal paths**.

### Key limitation of DFS
- Finds *a path*, not the *shortest path*
- Paths may be unnecessarily long
- Example: DFS may reach a node in 3 steps even if a 1-step path exists

> [!important]
> We need algorithms that optimize **path length**, not just connectivity.

# 2. Distance in Graphs

## Definition

> The **distance between two nodes** is the length of the shortest path between them.

Formally:
- If no path exists → distance = ∞
- Otherwise → minimum number of edges (or weighted cost)

## Physical intuition

Imagine:
- Nodes = balls
- Edges = strings

If you lift node **s**:
- Connected nodes rise depending on proximity
- Height corresponds to shortest-path distance

> [!intuition]
> Shortest paths behave like tension propagation in a physical network.

---

# 3. Breadth-First Structure of Shortest Paths

Shortest paths naturally form **layers**:

- Layer 0 → source node `s`
- Layer 1 → nodes 1 edge away
- Layer 2 → nodes 2 edges away
- …

> [!key insight]
> Shortest paths can be discovered **layer-by-layer outward from the source**.

---

# 4. Breadth-First Search (BFS)

BFS computes shortest paths in **unweighted graphs**.

## Core idea
Use a **queue** to explore nodes in increasing order of distance.

## BFS Algorithm

```text
procedure bfs(G, s)

for each vertex u:
    dist(u) = ∞

dist(s) = 0
Q = queue containing s

while Q not empty:
    u = dequeue(Q)

    for each edge (u, v):
        if dist(v) == ∞:
            dist(v) = dist(u) + 1
            enqueue(Q, v)
```

## Correctness invariant

At any time:

> [!theorem]
> For each layer d:
> 1. All nodes with distance ≤ d are correctly labeled  
> 2. All others are ∞  
> 3. Queue contains exactly nodes at distance d  

## Complexity

- Each node enqueued once → O(|V|)
- Each edge processed once → O(|E|)

> [!summary]
> BFS runs in **O(|V| + |E|)** time.

---

# 5. BFS vs DFS (Conceptual Difference)

| Feature | DFS | BFS |
|--------|-----|-----|
| Strategy | Deep exploration | Layer-by-layer |
| Data structure | Stack | Queue |
| Guarantees shortest path | ❌ No | ✅ Yes (unweighted) |
| Behavior | Goes deep fast | Expands uniformly |

---

# 6. Weighted Graphs: The Problem

BFS assumes:
- All edges have equal cost (1)

But real-world graphs have:
- Road distances
- Travel times
- Costs
- Latencies

So edges have weights:

$$
l(u, v) > 0
$$

---

> [!question]
> How do we compute shortest paths when edges have different weights?

---

# 7. Reduction Idea: Convert to Unit Edges

Transform weighted graph into unweighted graph:

### Trick:
Replace each edge of length `l` with:
- `l` unit edges
- `l - 1` dummy nodes

## Problem

This makes graph size explode:
- Long edges → many dummy nodes
- BFS becomes inefficient

# 8. Alarm Clock Intuition (Key Insight)

Instead of simulating dummy nodes, we:

> [!idea]
> Jump directly to the next *important event* (real node arrival)


## Mechanism

For each node:
- Maintain an “alarm time” = best known distance

When exploring:
- Set alarms for neighbors
- Update if shorter path found

## Rule

- Next node processed = smallest alarm time

# 9. Dijkstra’s Algorithm

Dijkstra = BFS + priority ordering

## Data structure required

> [!important]
> Priority Queue (Min-Heap)

Supports:
- Insert
- Decrease-key
- Delete-min

## Algorithm

```text
procedure dijkstra(G, l, s)

for each vertex u:
    dist(u) = ∞
    prev(u) = nil

dist(s) = 0

H = make priority queue with all vertices

while H not empty:
    u = extract-min(H)

    for each edge (u, v):
        if dist(v) > dist(u) + l(u, v):
            dist(v) = dist(u) + l(u, v)
            prev(v) = u
            decrease-key(H, v)
```


## Output

- dist(u) → shortest distance from s
- prev(u) → reconstruct shortest path tree


# 10. Alternative View: Growing Region R

We maintain a set:

$$
R = \text{nodes whose shortest paths are known}
$$

## Algorithm idea

At each step:
- Choose closest node outside R
- Add it to R
- Relax edges from it

## Key property

> [!theorem]
> The next chosen node is always the closest node outside R.


# 11. Correctness Invariant (Dijkstra)

At every iteration:

> [!theorem]
> 1. Nodes in R have correct shortest distances  
> 2. Nodes outside R are not finalized  
> 3. dist(v) represents shortest known path through R  


## Why it works

Because:
- All edge weights are positive
- Any alternate path must go through already processed nodes first

# 12. Complexity Analysis

Let:
- |V| = vertices
- |E| = edges

Operations:
- |V| extract-min
- |E| decrease-key

## Running time depends on heap:

| Implementation | Complexity |
|---------------|------------|
| Binary heap | O((V + E) log V) |
| Fibonacci heap | O(E + V log V) |

---

> [!summary]
> Dijkstra is efficient due to structured greedy expansion + priority queue optimization.

---

# 13. BFS vs Dijkstra (Key Insight)

| Feature | BFS | Dijkstra |
|--------|-----|----------|
| Edge weights | Unit | Positive weights |
| Data structure | Queue | Priority queue |
| Expansion order | Distance layers | Minimum cost |
| Correctness basis | Uniform cost | Greedy optimality |

---

# 14. Big Picture Insight

> [!important]
> All shortest-path algorithms are about **controlling exploration order**.

- BFS → by hops
- Dijkstra → by weighted distance

---

# 15. Final Intuition

> [!tip]
> Think of shortest path search as:
>
> - BFS: wave spreading uniformly
> - Dijkstra: wave moving faster through low-cost edges

---
# Priority Queues, Dijkstra Extensions, and Negative Edge Shortest Paths

> [!abstract]
> This note connects **data structures (priority queues)** with **shortest path algorithms**, and extends shortest-path methods from:
> - non-negative weights (Dijkstra)
> - to general graphs with negative edges (Bellman–Ford)
>
> It also explains why negative cycles make shortest paths **ill-defined**.

---

# 1. Priority Queue Implementations

Priority queues are the **core data structure behind Dijkstra’s algorithm**. They maintain a dynamic set of elements with associated keys (distances), supporting efficient retrieval of the minimum.

Refer: [[Arrays]], [[Queues]]
## 1.1 Array-Based Priority Queue

> [!definition]
> A priority queue can be implemented as an **unordered array of key-value pairs**.

### Structure
- Each vertex stores a key: `dist[v]`
- Initially:
  $$
  dist(v) = \infty
  $$

## Operations

### Insert / Decrease-Key
- Simply update the key value in the array
- Complexity:
$$
O(1)
$$

### Delete-Min
- Scan entire array to find minimum key
- Complexity:
$$
O(|V|)
$$

## Summary

| Operation | Time Complexity |
|----------|----------------|
| Insert | O(1) |
| Decrease-key | O(1) |
| Delete-min | O(V) |

> [!warning]
> Simple but inefficient for large graphs due to expensive delete-min.

---

# 2. Binary Heap (Standard Implementation)

> [!definition]
> A **binary heap** is a complete binary tree satisfying the heap property:
>
> The key of each node ≤ keys of its children.

## 2.1 Structure

- Complete binary tree:
  - Filled level by level
  - Left to right
- Root always contains minimum element

## 2.2 Array Representation

Heap stored in array:

| Node relation | Formula |
|--------------|--------|
| Parent(j) | ⌊j / 2⌋ |
| Left child | 2j |
| Right child | 2j + 1 |


# 2.3 Heap Operations

## Insert

1. Insert element at end
2. “Bubble up”

### Complexity:
$$
O(\log n)
$$

## Decrease-Key

- Update value
- Bubble upward

$$
O(\log n)
$$

## Delete-Min

1. Remove root
2. Replace with last element
3. “Sift down”

$$
O(\log n)
$$

---

> [!intuition]
> Operations cost logarithmic time because the heap height is:
> $$
> O(\log n)
> $$

# 3. d-ary Heap

> [!definition]
> A **d-ary heap** generalizes binary heaps: each node has d children.


## 3.1 Height Reduction

Heap height:
$$
O(\log_d n) = O\left(\frac{\log n}{\log d}\right)
$$

## 3.2 Performance Trade-off

### Insert / Decrease-Key
Faster:
$$
O(\log_d n)
$$

### Delete-Min
Slower:
- Must check all d children
$$
O(d \cdot \log_d n)
$$

---

## 3.3 Insight

> [!important]
> Increasing `d` makes insertion faster but deletion more expensive.


# 4. Shortest Paths with Negative Edges

Dijkstra’s algorithm assumes:

> [!important]
> All edge weights are **non-negative**

This assumption breaks with negative edges.

## 4.1 Why Dijkstra Fails

Dijkstra relies on:

> “Once a node is closest, it is finalized.”

This is false when:
- A longer path may later become cheaper due to negative edges

### Key failure case

A node further away may later provide a **shorter path**.

# 5. Relaxation: The Core Operation

All shortest path algorithms rely on:

## Update (Relaxation)

$$
dist(v) = \min(dist(v), dist(u) + l(u, v))
$$

## Properties

### 1. Correctness property
If:
- dist(u) is correct
- (u, v) is on shortest path

Then update gives correct dist(v)

### 2. Safety property
Never underestimates true shortest path:

\[
dist(v) \geq \text{true shortest distance}
\]

> [!important]
> Relaxation is always safe, even if applied repeatedly.

---

# 6. Key Insight Behind Bellman-Ford

Consider shortest path:

$$
s \rightarrow u_1 \rightarrow u_2 \rightarrow ... \rightarrow t
$$

It has at most:

$$
|V| - 1 \text{ edges}
$$

## Requirement

If we apply relaxations in correct order, distances become correct.

But we do NOT know the order.

# 7. Bellman-Ford Algorithm

> [!definition]
> Repeatedly relax all edges to propagate shortest-path information.

## Algorithm

```text
procedure bellman_ford(G, s)

for each vertex v:
    dist(v) = ∞
    prev(v) = nil

dist(s) = 0

repeat |V| - 1 times:
    for each edge (u, v):
        dist(v) = min(dist(v), dist(u) + l(u, v))
```

## Complexity

$$
O(|V| \cdot |E|)
$$

## Intuition

> [!idea]
> Each iteration allows shortest paths with one more edge to be discovered.


# 8. Early Termination Optimization

> [!tip]
> If no updates occur in an iteration, algorithm can stop early.

This improves average-case performance significantly.

---

# 9. Negative Cycles

## 9.1 What is a negative cycle?

A cycle whose total weight is negative:

$$
A \rightarrow B \rightarrow C \rightarrow A < 0
$$


## 9.2 Why it breaks shortest paths

You can loop infinitely:

- Path cost keeps decreasing
- No minimum exists

---

> [!warning]
> Shortest path becomes **undefined** in presence of negative cycles.

## 9.3 Example behavior

- 2 → 1 → 0 → -1 → -2 → ...

No lower bound exists.

# 10. Detecting Negative Cycles

Key idea:

> [!important]
> Bellman-Ford performs exactly |V| − 1 passes for valid graphs.

So:

### Detection step
Run **one extra iteration**

- If any dist value changes → negative cycle exists

## Condition

$$
\text{If update occurs on } |V|^{th} \text{ iteration → negative cycle}
$$

# 11. Algorithm Summary

| Algorithm | Works with | Complexity | Key Idea |
|----------|------------|-----------|----------|
| BFS | Unweighted graphs | O(V + E) | Layer expansion |
| Dijkstra | Non-negative weights | O(E log V) | Greedy + heap |
| Bellman-Ford | Negative edges allowed | O(VE) | Repeated relaxation |

---

# 12. Conceptual Unification

> [!big idea]
> All shortest-path algorithms are variations of:
>
> **“Repeatedly improving distance estimates until convergence”**

- BFS → uniform propagation
- Dijkstra → greedy propagation
- Bellman-Ford → exhaustive propagation

---

# 13. Final Insight

> [!tip]
> The only reason shortest-path algorithms work is:
>
> - Relaxation is safe
> - Order of relaxation determines efficiency
> - Negative cycles destroy convergence

---
# 16. Summary

Shortest path algorithms evolve as:

1. DFS → reachability only  
2. BFS → shortest path in unweighted graphs  
3. Edge-weight problem → need generalization  
4. Dijkstra → BFS + priority queue  
5. Region-growing interpretation → greedy expansion  
