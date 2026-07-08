
(![](https://www.youtube.com/watch?v=STjW3eH0Cik&list=PLUl4u3cNGP63gFHB6xb-kVBiQHYe_4hSi&index=6))
## Lecture Goal

The lecture explores how computers play games such as chess and why game playing became one of the earliest successful areas of AI research.

A central theme is:

> Computers do not necessarily play games the same way humans do.

The lecture uses chess as the primary example and explains how techniques such as minimax, alpha-beta pruning, and progressive deepening enabled programs like Deep Blue to defeat world champions.

---

# Historical Context

## Hubert Dreyfus and Chess

In the 1960s, philosopher Hubert Dreyfus argued that:

> "Computers can't play chess."

His argument was not entirely wrong.

The deeper point was:

> Computers could not play chess the way humans play chess.

Years later, chess programs became extremely strong, but largely through search and evaluation rather than human-like reasoning.

---

## John McCarthy's Prediction

John McCarthy predicted that computers would eventually defeat world champions.

However:

- Early researchers expected computers to win using human-like reasoning.
    
- Actual success came through large-scale search and evaluation.
    

This culminated in:

```text
1997
↓
Deep Blue defeats Garry Kasparov
```

After that, chess became a solved benchmark for AI research.

---

# How Might A Computer Play Chess?

The lecture presents several possibilities.

## Human-Like Strategic Reasoning

A hypothetical system might reason about:

- Pawn structure
    
- King safety
    
- Castling opportunities
    
- Long-term strategy
    

Humans often think this way.

The challenge:

> Nobody really knew how to build such a system directly.

This is why early AI pursued search-based methods instead.

---

# Game Trees

A game can be represented as a tree.

The root is the current position.

Each branch corresponds to a legal move.

Each level alternates between:

```text
MAX
MIN
MAX
MIN
...
```

The leaves contain utility values.

---

# Core Idea of Minimax

Minimax assumes:

```text
MAX plays perfectly
MIN plays perfectly
```

Each player assumes the opponent is rational and attempting to maximize their own outcome.

---

## Value Propagation

Minimax works by propagating values upward.

Example:

```text
      MAX
     /   \
    8     7
```

MAX chooses:

```text
max(8,7)=8
```

---

Example:

```text
      MIN
     /   \
    8     3
```

MIN chooses:

```text
min(8,3)=3
```

---

This process repeats until the root receives a value.

The root value represents:

> The outcome that will occur if both players play optimally.

---

## Important Insight

The selected value is often neither:

```text
largest leaf
```

nor

```text
smallest leaf
```

Instead it is:

> The value produced by rational adversarial interaction.

---
![[Pasted image 20260616193431.png|277]]
---

# Why Minimax Is Recursive

The lecture emphasizes an important intuition.

To evaluate a move:

```text
My move
↓
Opponent response
↓
My response
↓
Opponent response
↓
...
```

The same question is repeatedly asked:

> What is the best achievable outcome from this position?

Because the problem repeats at every level, recursion is natural.

---

# Alpha-Beta Pruning

## Key Insight

Many branches can never affect the final answer.

If we already know:

```text
MAX can achieve 2
```

and another branch can never exceed:

```text
1
```

then:

```text
That branch is irrelevant.
```

It is as though it does not exist.

---

## Example

Suppose:

```text
MAX already knows:
Score ≥ 2
```

Another subtree guarantees:

```text
Score ≤ 1
```

MAX would never choose that subtree.

Therefore:

```text
Stop searching.
```

The remaining nodes can be pruned.

---

## The Dead Horse Principle

One of the lecture's memorable phrases:

> Don't keep beating a dead horse.

Meaning:

If a branch cannot affect the answer:

- Don't generate moves.
    
- Don't evaluate positions.
    
- Don't waste computation.
    

Alpha-beta pruning is essentially an implementation of this principle.

---

![[Pasted image 20260616193559.png]]

---

# Alpha-Beta Is NOT A Different Algorithm

One of the most important points from the lecture:

Students often ask:

> Is alpha-beta an alternative to minimax?

Answer:

```text
No.
```

Alpha-beta:

```text
Minimax
+
Speed improvement
```

It always returns:

```text
exactly the same answer
```

as minimax.

It simply examines fewer nodes.

---

# Why Alpha-Beta Matters

Without pruning:

```text
O(b^d)
```

With ideal alpha-beta:

```text
O(b^(d/2))
```

Meaning:

If ordinary minimax reaches:

```text
7 levels
```

then alpha-beta may reach:

```text
14 levels
```

with similar effort.

---

## Practical Interpretation

The lecture describes this as:

> The difference between a jerk and a world champion.

A small reduction in the exponent produces enormous gains.

---

# Progressive Deepening

The lecture introduces another critical idea:

> Always have a move ready.

Instead of searching directly to depth d:

Search:

```text
depth 1
depth 2
depth 3
...
depth d
```

This guarantees that the program always has a usable answer if time expires.

---

## Anytime Algorithms

Progressive deepening is an example of:

> Anytime algorithms

An anytime algorithm can return:

```text
some answer now
```

and

```text
better answers later
```

if additional computation time becomes available.

---

## Additional Benefit

Progressive deepening improves alpha-beta pruning.

Earlier searches help determine:

```text
which moves appear strongest
```

Those moves can then be searched first.

Better ordering:

```text
↓
More pruning
↓
Deeper search
```

---

# Deep Blue

The lecture argues that Deep Blue was not fundamentally different from minimax systems.

Deep Blue was essentially:

```text
Minimax
+
Alpha-Beta
+
Progressive Deepening
+
Massive Parallel Computing
+
Opening Books
+
Endgame Databases
+
Selective Deep Search
```

---

## Deep Blue's Speed

Around 1997:

```text
≈ 200 million
position evaluations per second
```

while searching:

```text
14–16 ply
```

deep.

---

# Most Important Takeaway

The biggest insight from the MIT lecture is:

```text
Minimax = Value propagation

Alpha-Beta = Proof that some branches cannot matter

Progressive Deepening = Always have an answer available
```
