
Refer: [[Chapter 6 - Adversarial Search and Games]], [[MIT 6.034 Lecture 6 - Game Playing, Minimax, Alpha-Beta, and Deep Blue]]
# 1. Game Theory Foundations

> [!info] Definition  
> "Game theory is the study of mathematical models of conflict and cooperation between intelligent rational decision-makers."
> 
> — Roger B. Myerson

Game-playing AI is fundamentally an application of **Game Theory**.

Game theory studies situations where:

- Multiple intelligent agents make decisions
    
- Outcomes depend on actions of others
    
- Agents behave rationally
    
- Agents seek to maximize their own utility
    

Examples:

- Chess
    
- Checkers
    
- Go
    
- Isolation
    
- Poker
    
- Auctions
    
- Economic negotiations

## Rational Agent Assumption

Most game-playing algorithms assume:

```text
Players are rational
Players act optimally
Players maximize utility
```

This assumption is what allows Minimax to work.

---

# 2. Why Search Changes in Games

In traditional search problems:

```text
Environment is fixed
Actions are deterministic
Nobody is actively working against you
```

In games:

```text
Opponent actively works against you
Future states depend on opponent decisions
Search becomes adversarial
```

## Two-Player Framework

We model players as:

```text
MAX
MIN
```

MAX tries to:

```text
maximize score
```

MIN tries to:

```text
minimize score
```

---

# 3. Game Trees

A Game Tree represents possible future states.

```text
Current State
     ↓
Possible Moves
     ↓
Future States
     ↓
More Moves
     ↓
Terminal States
```

## Tree Terminology

### Root Node

Current game state.

### Internal Node

Intermediate game state.

### Leaf Node

End of search.

Can represent:

```text
Win
Loss
Draw
```

or

```text
Heuristic Evaluation
```

## Example

```text
          MAX
        /  |  \
       A   B   C
```

Each branch corresponds to a legal move.

---

# 4. Minimax Algorithm

> [!important]  
> Assume the opponent always makes the best possible move for themselves.

## Applicable To

Minimax works for:

```text
Two-player
Zero-sum
Perfect-information
Adversarial games
```

Examples:

- Chess
    
- Checkers
    
- Isolation
    
- Tic-Tac-Toe
    

## Zero-Sum Games

A gain for one player is a loss for the other.

```text
My gain = Opponent loss
```

Example utility values:

```text
Win  = +1
Draw =  0
Loss = -1
```


## MAX Nodes

MAX chooses:

```text
maximum(child values)
```

Example:

```text
MAX

3 7 2
```

Result:

```text
7
```


## MIN Nodes

MIN chooses:

```text
minimum(child values)
```

Example:

```text
MIN

3 7 2
```

Result:

```text
2
```

## Example Minimax Tree

```text
            MAX
           /   \
         MIN   MIN
        / \    / \
       3  5   2  9
```

### Step 1

Left MIN:

```text
min(3,5)=3
```

Right MIN:

```text
min(2,9)=2
```

Tree becomes:

```text
        MAX
       /   \
      3     2
```

### Step 2

MAX chooses:

```text
max(3,2)=3
```

Final answer:

```text
3
```

## Minimax Procedure

1. Generate game tree
    
2. Evaluate leaf nodes
    
3. Propagate values upward
    
4. Choose best root action
    

## Why Minimax Works

MAX assumes:

```text
Opponent is perfect.
```

Therefore:

```text
Choose move with best worst-case outcome.
```

---

# 5. Minimax Complexity

Let:

```text
b = branching factor
d = depth
```

Then:

```text
Time Complexity = O(b^d)
```

## Example

Chess:

```text
b ≈ 35
```

Searching:

```text
depth = 8
```

requires:

```text
35^8
≈ 2.25 trillion nodes
```

Clearly impossible.

---

# 6. Cutoff Search

Instead of searching entire game:

```text
Search fixed depth
```

Example:

```text
Depth = 4
```

Then stop.

---

# 7. Evaluation Functions

> [!important]  
> Used when search cannot reach terminal states.

Evaluation Function:

```text
State → Score
```

---

## Score Interpretation

```text
Positive → Good for MAX

Negative → Good for MIN

0 → Neutral
```

## Common Features

### Material Advantage

Example:

```text
Queen = 9
Rook  = 5
Bishop= 3
Knight= 3
Pawn  = 1
```

---

### Positional Strength

Examples:

```text
Center control
King safety
Territory
```

---

### Mobility

Number of legal moves available.

More mobility generally means:

```text
More future opportunities
```

---

## Isolation Evaluation Functions

Used heavily in CS6601.

### Simple Version

```text
# Legal Moves Available
```

---

### Better Version

```text
My Moves - Opponent Moves
```

---

# 8. Horizon Effect

> [!warning]  
> One of the most important search problems.

## Definition

The algorithm cannot see beyond its search depth.

```text
Important event
↓
Exists beyond cutoff
↓
Algorithm misses it
```

## Example

```text
Depth = 4
```

But a major piece is lost at:

```text
Move 5
```

Algorithm never sees it.

## Consequences

AI may:

- Delay inevitable loss
    
- Miss winning opportunities
    
- Make short-sighted moves
    

---

# 9. Quiescence Search

> [!info]  
> Solution to the Horizon Effect.

## Main Idea

Do not stop search in unstable positions.

Instead:

```text
Continue searching
until position becomes stable.
```

## Quiet Position

Examples:

- No captures available
    
- No checks
    
- No immediate threats

## Noisy Position

Examples:

- Capture available
    
- Checkmate threat
    
- Forced tactical sequence

## Procedure

At cutoff depth:

```text
Position Quiet?
```

If YES:

```text
Evaluate
```

If NO:

```text
Search deeper
```

Only tactical moves are explored.

## Typical Tactical Moves

- Captures
    
- Checks
    
- Immediate threats
    
- Forced responses
    

---

# 10. Iterative Deepening

Instead of:

```text
Search depth 8
```

Do:

```text
Depth 1
Depth 2
Depth 3
...
Depth 8
```

## Benefits

### Better Move Ordering

Earlier searches identify promising moves.

### Anytime Algorithm

If time expires:

```text
Still have a legal move
```

### Used In Practice

Most strong game engines combine:

```text
Iterative Deepening
+
Alpha-Beta
```

---

# 11. Alpha-Beta Pruning

> [!important]  
> Alpha-Beta returns EXACTLY the same answer as Minimax.

Only faster.

## Motivation

Many branches can never affect the final decision.

```text
Don't evaluate them.
```

## Alpha (α)

Best value MAX can guarantee.

Initialization:

```text
α = -∞
```

## Beta (β)

Best value MIN can guarantee.

Initialization:

```text
β = +∞
```

## Rules

### At MAX Node

```text
α = max(α,current)
```

Prune when:

```text
α ≥ β
```

---

### At MIN Node

```text
β = min(β,current)
```

Prune when:

```text
β ≤ α
```

## Example

```text
MAX
├── 8
└── MIN
     ├── 4
     ├── ?
```

MAX already has:

```text
α = 8
```

MIN finds:

```text
β = 4
```

Since:

```text
8 ≥ 4
```

Remaining branches are pruned.

## Complexity

Without pruning:

```text
O(b^d)
```

Best case:

```text
O(b^(d/2))
```

## Move Ordering

> [!tip]  
> Alpha-Beta becomes dramatically more effective if good moves are searched first.

---

# 12. Stochastic Games

Until now:

```text
Moves are deterministic
```

Now introduce randomness.

Examples:

- Dice rolls
    
- Card draws
    
- Slippery movement
    
- Isolation with move errors
    

## Chance Nodes

New node type:

```text
MAX
MIN
CHANCE
```

## Chance Node Formula

Expected Value:

```text
EV = Σ P(outcome) × Value(outcome)
```

## Example

```text
Chance

80% → 10
20% → 0
```

Expected Value:

```text
0.8(10)+0.2(0)
=
8
```

---

# 13. Expectimax

> [!important]  
> Expectimax = Minimax + Probability

## Node Types

### MAX

```text
max(children)
```

### MIN (if opponent exists)

```text
min(children)
```

### CHANCE

```text
Σ(p × value)
```

## Example

```text
MAX
├── A = 4
└── B

B
├─80%→10
└─20%→0
```

Expected Value:

```text
0.8(10)+0.2(0)=8
```

MAX chooses:

```text
max(4,8)=8
```

---

# 14. Isolation Example (Probabilistic)

Suppose movement succeeds:

```text
90%
```

Overshoots:

```text
10%
```

---

Expected Value:

```text
0.9 × State1
+
0.1 × State2
```

---

Example:

```text
90% → value 1
10% → value 2
```

Expected Value:

```text
0.9(1)+0.1(2)
=
1.1
```

---

# 15. Why Minimax Fails Here

Minimax assumes:

```text
Opponent chooses outcome
```

But randomness does not choose outcomes.

Randomness follows:

```text
Probabilities
```

Therefore:

```text
Use Expectimax
```

---

# 16. Expectimax Pruning

> [!warning]  
> This is the hardest topic in the lecture.

## Why Alpha-Beta Works

Because:

```text
MIN can only decrease values
MAX can only increase values
```

Bounds are obvious.

## Why Chance Nodes Break This

Example:

```text
0.5 × ?
+
0.5 × ?
```

You cannot know final value until both sides are known.

## Important Rule

> Expectimax cannot generally be pruned like Minimax.

## When Can We Prune?

Only if we know bounds.

Example:

```text
Evaluation values
between 0 and 10
```

Then we can compute:

```text
Maximum possible remaining value
```

## Lecture Example

Current best branch:

```text
6.5
```

Another subtree:

First branch:

```text
0
```

Probability:

```text
0.5
```

Contribution:

```text
0
```

Remaining branch maximum:

```text
0.5 × 10 = 5
```

Maximum achievable value:

```text
5
```

Since:

```text
5 < 6.5
```

Entire subtree can be pruned.

## Key Insight

> [!important]  
> Expectimax pruning requires known upper and lower bounds on evaluation values.

Without bounds:

```text
Pruning is unsafe.
```

## Better Ordering

Evaluate first:

1. Highest probability branches
    
2. Highest expected value branches
    

This increases pruning opportunities.

---

# 17. Relationship Between Concepts

```text
Game Theory
      ↓
Game Trees
      ↓
Minimax
      ↓
Alpha-Beta
      ↓
Evaluation Functions
      ↓
Cutoff Search
      ↓
Horizon Effect
      ↓
Quiescence Search
      ↓
Iterative Deepening
      ↓
Stochastic Games
      ↓
Expectimax
      ↓
Probabilistic Pruning
```

---

# Exam Cheat Sheet

|Concept|One-Line Definition|
|---|---|
|Game Tree|Tree of possible future states|
|MAX Node|Choose largest value|
|MIN Node|Choose smallest value|
|Minimax|Assume opponent is optimal|
|Alpha (α)|Best value MAX can guarantee|
|Beta (β)|Best value MIN can guarantee|
|Alpha-Beta|Prune branches that cannot matter|
|Evaluation Function|Estimate state quality|
|Horizon Effect|Important event beyond search depth|
|Quiescence Search|Extend search in unstable positions|
|Iterative Deepening|Search depth 1,2,3,... progressively|
|Chance Node|Probabilistic outcome node|
|Expected Value|Σ(probability × value)|
|Expectimax|Minimax with randomness|
|Expectimax Pruning|Possible only with known bounds|

---

> [!summary] Memory Shortcut
> 
> **Minimax = Worst-case opponent**
> 
> **Alpha-Beta = Ignore branches that cannot matter**
> 
> **Evaluation Function = Estimate board strength**
> 
> **Horizon Effect = Can't see far enough**
> 
> **Quiescence Search = Keep searching noisy positions**
> 
> **Expectimax = Average-case randomness**
> 
> **Probabilistic Pruning = Only works when value bounds are known**

Next: [[Lecture 4 - Constraint Satisfaction]]