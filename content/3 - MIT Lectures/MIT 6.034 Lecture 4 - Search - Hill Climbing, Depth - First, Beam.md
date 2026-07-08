![](https://www.youtube.com/watch?v=j1H3jAAGlEA&list=PLUl4u3cNGP63gFHB6xb-kVBiQHYe_4hSi&index=4)

## Key Terms

| Term                  | Meaning                                 |
| --------------------- | --------------------------------------- |
| Search                | Exploring possibilities to reach a goal |
| State                 | Current situation                       |
| Start State           | Initial position                        |
| Goal State            | Desired position                        |
| Path                  | Sequence of states                      |
| DFS                   | Explore deeply before alternatives      |
| BFS                   | Explore level by level                  |
| Backtracking          | Return to previous decision point       |
| Queue                 | Collection of candidate paths           |
| British Museum Search | Explore every possibility               |
| Lexical Order         | Alphabetical expansion order            |
# Search

## Definition

Search is one of the fundamental methods used in Artificial Intelligence.

The goal is to find a path from a **start state** to a **goal state** by exploring available choices.

Although search is often illustrated using maps, **search is not really about maps**.

> [!important] Gold Star Idea  
> **Search is about choice, not maps.**
> 
> Maps are only a convenient way to visualize decision making.
> 
> Every search algorithm represents a different strategy for choosing what to explore next.

## Example: Finding a Route

Imagine a taxi driver trying to find a route from a starting location **S** to a destination **G**.

Different drivers may produce different routes:

### Thief's Route

- Wanders inefficiently.
- Makes poor choices.
- Finds a route but wastes effort.

### Honest Beginner's Route

- Makes reasonable decisions.
- Finds a good route.
- Not necessarily optimal.

### Physics PhD Route

- Considers many possibilities mentally.
- Evaluates alternatives before moving.
- Produces the best route.

The lecture uses these examples to motivate different search strategies.

## Human vs AI Search

Humans often solve path-finding problems almost instantly.

Given a map, most people can visually identify a good route within seconds.

However:

- Humans use visual reasoning.
- AI programs usually do not have human-like visual systems.
- Therefore AI must rely on explicit search procedures.

> [!note]  
> Human vision contributes significantly to intelligence.
> 
> We can often "see" a good solution immediately.
> 
> AI search algorithms compensate for the absence of this visual intuition.

---
# Search Example Graph

The lecture uses a simplified graph:

![[Pasted image 20260621102148.png|241]]
The objective is to find a path from:

```
Start = S    Goal = G
```

# Search Conventions Used in the Course

## 1. Lexical Order

When multiple choices exist:

```
A before B   B before C    C before D
```

Nodes are expanded alphabetically.

### Example

If S connects to A and B:

```
S
├── A
└── B
```

Expand **A first**.

## 2. No Tail Biting

A path is never allowed to revisit a node already on that same path.

### Not Allowed

```
S → A → S
```

### Not Allowed

```
S → A → B → A
```

This prevents loops.

# British Museum Search

## Idea

Explore **every possible path**.

The name is a humorous criticism.

The strategy is:

> If you want the answer, look everywhere.

## Procedure

Generate all possible paths from the start node.

```
S
├── A
│   
├── B
│   
│   
└── C
│   
│       
└── E
│   
└── D
│       
└── G
└── B    
├── A    
│   
└── D    
│       
└── G    
└── C        
└── E
```

Every legal path is explored.

## Advantages

- Guaranteed to find every solution.
- Complete.

## Disadvantages

- Extremely expensive.
- Usually impractical.
- Performs enormous amounts of unnecessary work.

> [!example]  
> Searching for one route from New York to Boston by examining every possible route in North America would be a British Museum search.


# Depth-First Search (DFS)

## Core Idea

Follow one path as deeply as possible before trying alternatives.

Think:

> "Keep going until you hit a wall."

![[Pasted image 20260621102644.png|255]]

## Procedure

Start at S.

### Step 1

```
S → A
```

### Step 2

```
S → A → B
```

### Step 3

```
S → A → B → C
```

### Step 4

```
S → A → B → C → E
```

Dead end.

## Backtracking

When a dead end is reached:

Go back to the most recent decision point.

```
S → A → B → C → E
```

Dead end.

![[Pasted image 20260621102919.png|243]]

Backtrack to:

```
S → B
```

Try another choice:

```
S → B → D → G
```

Goal found.

## Backtracking

### Definition

Returning to the most recent node where an unexplored alternative exists.

> [!important]  
> Backtracking is often paired with DFS.
> 
> Without backtracking, DFS can miss valid solutions.

## Characteristics of DFS

### Advantages

- Uses little memory.
- Simple to implement.
- Can find solutions quickly if lucky.

### Disadvantages

- Can waste time exploring long bad paths.
- Not guaranteed to find shortest path.

## Intuition

DFS behaves like a very determined explorer:

> "I'll keep walking this way until I absolutely can't."

# Breadth-First Search (BFS)

## Core Idea

Explore level by level.

Instead of going deep immediately:

- Explore all nodes one step away.
- Then all nodes two steps away.
- Then all nodes three steps away.

## BFS Expansion

### Level 0

```
S
```

### Level 1

```
A - B
```

### Level 2

```
B - D - A - C
```

### Level 3

```
C - G - D - E
```

Goal found.

## Characteristics of BFS

### Advantages

- Guaranteed to find shortest path (if all edges have equal cost).
- Complete.

### Disadvantages

- Requires much more memory.
- Expands many unnecessary nodes.

---

> [!example]  
> If searching a building floor-by-floor:
> 
> - DFS explores one hallway completely.
> - BFS checks every room on the current floor before moving higher.

---

# Comparing DFS and BFS

|Feature|DFS|BFS|
|---|---|---|
|Strategy|Go deep first|Go level by level|
|Memory Use|Low|High|
|Finds Shortest Path|No|Yes (equal costs)|
|Backtracking Needed|Usually|No|
|Can Get Lost|Yes|Less likely|
|Completeness|Yes (with proper backtracking)|Yes|

---

# Queue-Based View of Search
## Depth-First Search (DFS)

> [!important]  
> **Core Idea:** Always explore the most recently generated path first.
> 
> In queue terms, newly generated paths are added to the **front** of the queue (stack-like behavior).

### DFS Algorithm

Start
  │
  ▼
Initialize Queue
[(S)]
  │
  ▼
Take First Path from Queue
  │
  ▼
Goal Reached?
  │
  ├── Yes → Return Solution
  │
  └── No
         │
         ▼
    Extend Path
    Generate Children
         │
         ▼
    Add Children to
    FRONT of Queue
         │
         ▼
       Repeat

---

### Queue Evolution Example

Assume:

```
S → A, B   A → B, D    B → C D → G
```

|Step|Queue Contents|
|---|---|
|Initial|`(S)`|
|Expand S|`(SA) (SB)`|
|Expand SA|`(SAB) (SAD) (SB)`|
|Expand SAB|`(SABC) (SAD) (SB)`|
|Expand SABC|`(SABCE) (SAD) (SB)`|
|Dead End at E|`(SAD) (SB)`|
|Expand SAD|`(SADG) (SB)`|
|Goal Found|`S → A → D → G`|

---

> [!example]  
> Think of DFS like exploring a maze:
> 
> - Keep walking down one corridor.
> - If you hit a dead end, backtrack.
> - Continue from the most recent junction.
> 
> This is why DFS uses a **stack** (LIFO behavior).

---
### Why DFS Goes Deep

```
Queue Front    ↓(SAB) (SAD)  (SB)
```

After expanding `(SAB)`:

```
Queue Front    ↓(SABC)  (SAD)  (SB)
```

The newly generated path `(SABC)` is inserted **before** all older paths.

Therefore DFS immediately continues deeper rather than exploring siblings.

---

> [!summary]  
> **DFS = Expand First Path + Insert New Paths at Front**
> 
> - Uses a Stack (LIFO)
> - Goes deep quickly
> - Requires backtracking
> - May find a poor solution first
> - Uses relatively little memory compared to BFS

## DFS Rule

> Put newly generated paths at the FRONT of the queue.

This creates a stack-like behavior.

---
# General Search Framework

Every search algorithm follows roughly the same process.

```
Initialize queueRepeat:    
	Take path from queue    
	If path reaches goal:       
		 Success    
	Else:        
		Extend path        
	Add new paths to queue
```

The major difference between search algorithms is:

> [!important]  
> The search strategy is determined by **where new paths are inserted into the queue.**

For DFS:

```
Front of queue
```

For BFS:

```
End of queue
```

---

# Why Search Matters in AI

Search is much broader than path-finding.

It applies to:

- Solving puzzles
- Planning actions
- Mathematical reasoning
- Theorem proving
- Game playing
- Decision making
- Language understanding

---

> [!note]  
> Prof. Winston repeatedly emphasizes:
> 
> Search is not about roads and maps.
> 
> Search is a model of how intelligent systems make choices among alternatives.

## Search Optimization

Up to now, **Depth-First Search (DFS)** and **Breadth-First Search (BFS)** differ by only **one line of code**:

> [!important]  
> **DFS:** Add newly generated paths to the **front** of the queue.
> 
> **BFS:** Add newly generated paths to the **back** of the queue.

## Breadth-First Search (BFS)

### Implementation Change

```text
DFS:
Queue = New Paths + Existing Queue

BFS:
Queue = Existing Queue + New Paths
```

### Why BFS Works

Instead of diving deep into one branch, BFS explores **level by level**.

```text
Level 0: S

Level 1:
A   B

Level 2:
B   D   A   C

Level 3:
C   G   D   E
```

The first goal found is usually the **shortest path in terms of number of edges**.

---

> [!note]  
> Winston emphasizes that DFS and BFS use the **same algorithmic framework**.
> 
> The only difference is **where newly generated paths are inserted into the queue**.

---
# Problem: Duplicate Work

Winston points out that BFS is still incredibly stupid.

### Why?

Because it repeatedly extends paths ending at the same node.

Example:

```text
S → A → B

S → B → A
```

Both paths eventually end at **A**.

The algorithm may explore A multiple times even though it already knows what happens after A.

## Extended List Optimization

### New Rule

> [!tip]  
> Never extend a path whose final node has already been extended before.

Instead, maintain a list:

```text
Extended Nodes

[S, A, B, D, ...]
```

When a path ends at a node already in the list:

```text
Path ends at A

Has A been extended before?

YES → Skip it
NO  → Extend it
```

---

### Modified Algorithm

```text
Remove First Path

↓

Check Final Node

↓

Already Extended?
      │
  ┌───┴───┐
  │              │
 Yes           No
  │              │
 Skip      Extend
```

---

> [!important]  
> This optimization dramatically reduces search time because it prevents the algorithm from repeatedly exploring the same region of the graph.

## Search Comparison So Far

|Search Type|Backtracking|Extended List|Informed?|
|---|---|---|---|
|British Museum|❌|❌|❌|
|Depth-First|✅|Optional|❌|
|Breadth-First|❌|Optional|❌|

---

# Hill Climbing Search

DFS and BFS suffer from a major weakness:

> [!warning]  
> They have no idea whether they are moving closer to the goal.

They blindly explore according to queue rules.

## Core Idea

> [!important]  
> Always move toward the node that appears closest to the goal.

Instead of choosing based purely on lexical order:

```text
DFS

A before B

→ choose A
```

Hill Climbing chooses:

```text
Distance(A, Goal) = 7

Distance(B, Goal) = 5

Choose B
```

## Hill Climbing Procedure

```text
Current Node

↓

Generate Children

↓

Estimate Distance to Goal

↓

Choose Closest Child

↓

Repeat
```

## Example

Suppose:

```text
       Goal
         G

      D

A           C

      B

      S
```

Distances to Goal:

```text
A = 7

B = 5
```

Hill Climbing chooses:

```text
S
↓
B
↓
A or C (tie)
↓
D
↓
G
```

---

> [!example]  
> Think of climbing a mountain in thick fog.
> 
> At every step:
> 
> - Look around.
>     
> - Move uphill.
>     
> - Repeat.
>     
> 
> You don't know the entire route.  
> You only know which local move looks best.

## Why Hill Climbing Is Faster

DFS example:

```text
S
↓
A
↓
B
↓
C
↓
Dead End
```

Must backtrack.

Hill Climbing:

```text
S
↓
B
↓
D
↓
G
```

Moves directly toward the goal.

Much less exploration.

## Limitation of Hill Climbing

> [!warning]  
> Being closer to the goal does **not** guarantee you're on the correct path.

You can get trapped in:

- Dead ends
    
- Local maxima
    
- Blind alleys
    

Example:

```text
Goal

   ^
   |
   E   ← appears promising

Dead End
```

The search may choose E because it looks closest, even though no solution exists through E.

## Informed vs Uninformed Search

### Uninformed Search

Search uses **no knowledge** about where the goal is.

- British Museum
    
- DFS
    
- BFS
    

```text
Search blindly
according to rules
```

### Informed Search

Search uses additional information (a heuristic).

- Hill Climbing
    

```text
Distance to Goal

↓

Guide Search
```

---

> [!summary]  
> **Gold Star Idea:** Search becomes dramatically more efficient when you provide information about where the goal might be.
> 
> - DFS → Go deep.
>     
> - BFS → Explore level by level.
>     
> - Extended List → Avoid duplicate work.
>     
> - Hill Climbing → Move toward the goal using a heuristic.
>     
> 
> Hill Climbing is the first **informed search** introduced in the course.