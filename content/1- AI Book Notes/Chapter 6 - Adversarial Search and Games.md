Refer: [[Lecture 3 - Game Playing]], [[MIT 6.034 Lecture 6 - Game Playing, Minimax, Alpha-Beta, and Deep Blue]]

> [!historical-context]
> Game playing has served as one of the primary testbeds for AI research.
> Major milestones:
> - 1952: A. S. Douglas creates a Tic-Tac-Toe program
> - 1950s: Arthur Samuel develops a self-learning Checkers program.
> - 1997: Deep Blue defeats Garry Kasparov.
> - 2016: AlphaGo defeats Lee Sedol.
> - 2017: AlphaGo Zero learns entirely through self-play.
> - 2017: AlphaZero achieves superhuman performance in Chess, Go, and Shogi.
> - 2019: OpenAI Five defeats professional Dota 2 teams.
>-- 2019: AlphaStar reaches Grandmaster level in StarCraft II.

## Why Games Are Important in AI

Games provide:

- Clearly defined states.
- Well-defined actions.
- Measurable outcomes.
- Repeatable experiments.

Because of these properties, games serve as controlled environments for developing and testing AI algorithms.

Many advances in AI were first demonstrated in games before being applied to real-world domains.
## Adversarial Search and Games

**In which we explore environments where other agents are plotting against us.**

This chapter covers **competitive environments**, in which two or more agents have conflicting goals, giving rise to **adversarial search problems**.

Rather than deal with the chaos of real-world skirmishes, we concentrate on games such as:

- Chess
    
- Go
    
- Poker
    

For AI researchers, the simplified nature of these games is advantageous because:

- The **state** of the game is easy to represent.
    
- Agents are usually restricted to a small number of actions.
    
- The effects of actions are defined by precise rules.
    

Physical games such as:

- Croquet
    
- Ice hockey
    

have:

- More complicated descriptions
    
- Larger ranges of possible actions
    
- Less precise rules governing legality of actions
    

With the exception of **robot soccer**, these physical games have attracted relatively little interest within the AI community.

---

# 6.1 Game Theory

There are at least **three stances** we can take toward multi-agent environments.

## 1. Economy View

When there are very large numbers of agents, we may consider them in aggregate as an **economy**.

This allows us to predict outcomes such as:

> Increasing demand causes prices to rise.

without predicting the behavior of any individual agent.

## 2. Adversaries as Part of the Environment

We may treat adversarial agents as simply another part of the environment, making the environment **nondeterministic**.

However, this misses an important distinction:

- Rain may or may not fall.
    
- Adversaries actively attempt to defeat us.
    

The adversary possesses intentions that ordinary environmental uncertainty does not.

## 3. Explicit Modeling of Adversaries

The third stance is to explicitly model adversarial agents using **adversarial game-tree search**.

This chapter focuses on this approach.

Key topics include:

- **Minimax Search**
    
- **Pruning**
    
- **Heuristic Evaluation Functions**
    
- **Monte Carlo Simulation**
    
- Games with **Chance**
    
- Games with **Imperfect Information**
    

---

### Minimax Search

We begin with a restricted class of games and define:

- The optimal move
    
- An algorithm for finding it
    

This algorithm is **Minimax Search**, a generalization of **AND–OR Search**.

---

### Pruning

Pruning improves efficiency by ignoring portions of the search tree that cannot affect the optimal decision.

---

### Cutoff Search

For nontrivial games there is usually insufficient time to find the true optimal move.

Search is therefore cut off at some depth.

At cutoff states we estimate who is winning using either:

#### Heuristic Evaluation Functions

Estimate the quality of a state from its features.

#### Monte Carlo Simulation

Average outcomes of many fast simulations from the current state to the end of the game.

---

### Later Sections

- **Section 6.5:** Games involving chance (dice, shuffled cards)
    
- **Section 6.6:** Games of imperfect information (poker, bridge)
    

---

# 6.1.1 Two-Player Zero-Sum Games

The games most commonly studied in AI are:

- **Deterministic**
    
- **Two-player**
    
- **Turn-taking**
    
- **Perfect information**
    
- **Zero-sum**
    

Examples:

- Chess
    
- Go
    

## Perfect Information

**Perfect information** is synonymous with **fully observable**.

All players can observe the complete game state.

## Zero-Sum Games

A game is **zero-sum** when:

> What is good for one player is equally bad for the other.

There is no "win-win" outcome.

## Terminology

### Move

Often used as a synonym for **action**.

### Position

Often used as a synonym for **state**.

## MAX and MIN

The two players are named:

- **MAX**
    
- **MIN**
    

MAX moves first.

Players alternate turns until the game ends.

## Formal Definition of a Game

### S₀: **Initial State**

Specifies how the game is set up at the start.

---
### TO-MOVE(s)

Returns the player whose turn it is in state **s**.

---
### ACTIONS(s)

Returns the legal moves available in state **s**.

---
### RESULT(s, a)

**Transition Model**

Defines the state produced by applying action **a** in state **s**.

---
### IS-TERMINAL(s)

**Terminal Test**

Returns:

- True if the game is over
    
- False otherwise
    

States where the game has ended are called **terminal states**.

---
### UTILITY(s, p)

**Utility Function**  
(also called **objective function** or **payoff function**)

Defines the final numeric value to player **p** when the game ends in terminal state **s**.

Examples:

#### Chess

- Win = 1
    
- Draw = 1/2
    
- Loss = 0
    

#### Backgammon

Payoffs range from:

- 0 to 192
    

## State Space Graph

The:

- Initial state
    
- ACTIONS function
    
- RESULT function
    

define the **state space graph**.

Properties:

- Vertices = states
    
- Edges = moves
    
- A state may be reachable by multiple paths
    

## Search Tree

A **search tree** can be superimposed on the state space graph to determine what move to make.

## Game Tree

A **complete game tree** is a search tree that follows every sequence of moves all the way to terminal states.

The game tree may be infinite if:

- The state space is unbounded
    
- Rules permit infinitely repeating positions
    

## Tic-Tac-Toe Example

In Tic-Tac-Toe:

- MAX places X
    
- MIN places O
    

Players alternate until:

- One player obtains three in a row
    
- All squares are filled
    

Leaf node values represent utility from MAX's perspective.

High values:

- Good for MAX
    
- Bad for MIN
    
---
### Visual Example: Partial Tic-Tac-Toe Game Tree

The diagram below shows a partial game tree for Tic-Tac-Toe.

- The root node is the initial empty board.
- MAX (X) moves first.
- MIN (O) responds.
- Each level of the tree corresponds to one ply.
- The tree expands until terminal states are reached.
- Terminal states are assigned utility values.

This illustrates the structure that Minimax will later search.

![[Pasted image 20260616180236.png|546]]

---
### Size of the Game Tree

#### Tic-Tac-Toe

- Fewer than 9! = 362,880 terminal nodes
    
- Only 5,478 distinct states
    

#### Chess

- More than 10⁴⁰ nodes
    

The game tree is therefore primarily a theoretical construct.

---

# 6.2 Optimal Decisions in Games

MAX seeks a sequence of actions leading to victory.

MIN actively opposes this goal.

Therefore MAX requires a:

> **Conditional Plan**

also called a:

> **Contingent Strategy**

which specifies a response to every possible move by MIN.

---

## Connection to AND–OR Search

For games with binary outcomes (win/loss), AND–OR Search can generate the required conditional plan.

A **winning strategy** in a game is identical to:

> A solution in a nondeterministic planning problem.

In both cases:

> Success must be guaranteed regardless of what the other side does.

---

## Minimax Search

When games have multiple outcome values rather than simple win/loss outcomes, a more general algorithm is needed:

**Minimax Search**

---

## Ply

In some games the word "move" may refer to actions by both players.

To avoid ambiguity, we use:

> **Ply**

meaning:

> One move by one player.

Each ply corresponds to moving one level deeper in the game tree.

---

## Minimax Value

The **Minimax Value** of a state:

**MINIMAX(s)**

is the utility of being in that state assuming:

- MAX plays optimally
    
- MIN plays optimally
    

from that point until the end of the game.

---

### Terminal States

For terminal states:

MINIMAX(s) = UTILITY(s, MAX)

---

### MAX Nodes

When it is MAX's turn:

MAX chooses the successor with the highest minimax value.

---

### MIN Nodes

When it is MIN's turn:

MIN chooses the successor with the lowest minimax value.

---

## Minimax Decision

The **Minimax Decision** is the move leading to the successor state with the highest minimax value.

---

## Suboptimal Opponents

Minimax assumes MIN also plays optimally.

If MIN is weaker:

- MAX will do at least as well as predicted by minimax.
    
- MAX may do better.
    

However, minimax is not always the best practical strategy against a weak opponent.

Example:

- Safe move guarantees a draw.
    
- Risky move gives:
    
    - 90% chance of victory
        
    - 10% chance of defeat
        

Against a weak opponent, the risky move may be preferable.

---

# 6.2.1 The Minimax Search Algorithm

Once MINIMAX(s) can be computed, it can be turned into a search algorithm.

Procedure:

1. Try every legal action.
    
2. Compute the minimax value of the resulting state.
    
3. Choose the action with the highest value.
    

---

## Characteristics

### Recursive

The algorithm recursively explores the game tree.

### Leaf Evaluation

Terminal nodes are assigned utility values.

### Backup Process

Values are propagated upward through the tree as recursion unwinds.

---
### Example: Backing Up Minimax Values

Consider the following game tree:

                A (MAX)
               /       \
           B (MIN)    C (MIN)
           /   \       /   \
       D(MAX) E(MAX) F(MAX) G(MAX)
        / \     / \    / \    / \
      -1  4   2   6  -3 -5  0   7

Step 1: Evaluate terminal states.

Step 2: Compute MAX nodes.

D = max(-1, 4) = 4
E = max(2, 6) = 6
F = max(-3, -5) = -3
G = max(0, 7) = 7

Step 3: Compute MIN nodes.

B = min(4, 6) = 4
C = min(-3, 7) = -3

Step 4: Compute root MAX node.

A = max(4, -3) = 4

Result:
The minimax value of the root is 4.
MAX chooses the action leading to node B.

---
## Complexity

Let:

- b = branching factor
    
- m = maximum depth
    

### Time Complexity

**O(bᵐ)**

### Space Complexity

If all actions generated simultaneously:

**O(bm)**

If actions generated one at a time:

**O(m)**

---

## Limitation

The exponential growth makes minimax impractical for complex games.

### Chess Example

- Branching factor ≈ 35
    
- Average depth ≈ 80 ply
    

Search size:

35⁸⁰ ≈ 10¹²³ states

which is computationally infeasible.

---

## Practical Intuition for Minimax

### Mental Model

Minimax assumes:

- MAX tries to maximize utility.
- MIN tries to minimize MAX's utility.
- Both players play optimally.

The algorithm:

1. Generate possible moves.
2. Generate opponent responses.
3. Continue until terminal states.
4. Assign utilities to terminal states.
5. Propagate values upward:
   - MAX chooses highest value.
   - MIN chooses lowest value.
6. Select root action with highest backed-up value.

---

### Why Recursion Works

A move cannot be evaluated without considering:

My move
→ Opponent response
→ My response
→ Opponent response
→ ...

Therefore the same decision problem repeats at every level of the game tree, making minimax naturally recursive.

---

### Practical Limitations

1. Exponential search growth:
   - Time complexity: O(b^m)

2. Assumes a perfect opponent:
   - May be overly conservative against weaker players.

3. Requires perfect information:
   - Standard minimax does not work well for hidden-information games such as poker.

These limitations motivate:
- Alpha-Beta Pruning
- Evaluation Functions
- Monte Carlo Tree Search
- Reinforcement Learning

---

# 6.2.2 Optimal Decisions in Multiplayer Games

For multiplayer games, a single value is insufficient.

Each state receives a:

> **Utility Vector**

Example:

For players A, B, and C:

<vA, vB, vC>

---

## Terminal States

The utility vector specifies the payoff to every player.

---

## Backed-Up Values

At each nonterminal node:

The player whose turn it is selects the successor maximizing their own component of the utility vector.

The backed-up value becomes the utility vector of that successor.

---

## Alliances

Multiplayer games often involve:

> **Alliances**

Formal or informal.

These may emerge naturally from selfish optimization.

Example:

- A and B are weak.
    
- C is strong.
    

Both A and B may attack C because:

> Preventing C from winning benefits each of them.

---

## Alliance Instability

As C weakens:

- The alliance becomes less valuable.
    
- One ally may betray the other.
    

---

## Cooperation in Non-Zero-Sum Games

Even two-player games can involve cooperation.

Example:

A terminal state yields:

<1000, 1000>

If 1000 is the maximum payoff for both players:

- Both players will cooperate to reach it.
    

---

# 6.2.3 Alpha–Beta Pruning

The number of states grows exponentially with depth.

While the exponent cannot be eliminated, it can often be reduced dramatically.

This is accomplished through:

> **Alpha–Beta Pruning**

---

## Core Idea

Large portions of the game tree may have no influence on the final minimax decision.

Such portions can be safely ignored.

---

## Alpha (α)

Represents:

> The best (highest) value found so far for MAX.

Think:

**α = "at least"**

---

## Beta (β)

Represents:

> The best (lowest) value found so far for MIN.

Think:

**β = "at most"**

---

## Pruning Rule

Search can terminate exploration of a subtree whenever:

- MAX already has a better alternative than the current branch.
    
- MIN already has a better alternative than the current branch.
    

At that point the subtree cannot affect the final decision.

---

## Historical Example: Deep Blue

IBM's Deep Blue defeated Garry Kasparov in 1997.

Key techniques:

- Minimax Search
- Alpha-Beta Pruning
- Evaluation Functions
- Specialized Hardware

Deep Blue evaluated approximately 200 million positions per second.

---
# 6.2.4 Move Ordering

The effectiveness of alpha–beta pruning depends heavily on:

> **Move Ordering**

---

## Best Case

If the best moves are explored first:

Alpha–beta examines only:

O(b^(m/2))

instead of:

O(b^m)

---

### Effective Branching Factor

For chess:

- Original branching factor ≈ 35
    
- Effective branching factor ≈ √35 ≈ 6
    

---

## Random Ordering

Expected complexity:

O(b^(3m/4))

---

## Practical Ordering Heuristics

Common chess ordering:

1. Captures
    
2. Threats
    
3. Forward moves
    
4. Backward moves
    

---

## Iterative Deepening

Procedure:

1. Search 1 ply deep.
    
2. Record move rankings.
    
3. Search deeper using previous rankings.
    

Benefits:

- Better move ordering
    
- Often outweighs additional search cost
    

---

## Killer Move Heuristic

Moves that have frequently proven best are called:

> **Killer Moves**

Trying them first is known as:

> **The Killer Move Heuristic**

---

## Transpositions

Different move sequences can lead to the same position.

These are called:

> **Transpositions**

---

## Transposition Tables

A **Transposition Table** stores previously computed values.

Benefits:

- Avoid repeated searches
    
- Significantly increase effective search depth
    

In chess, transposition tables can approximately double the reachable depth within the same amount of computation.

---

## Shannon's Classification

### Type A Strategy

- Search all moves to a fixed depth.
    
- Use heuristic evaluation at cutoff.
    

Characteristics:

- Wide search
    
- Shallow search
    

---

### Type B Strategy

- Ignore poor-looking moves.
    
- Follow promising lines deeply.
    

Characteristics:

- Narrow search
    
- Deep search
    

---

Historically:

- Chess programs tended to be **Type A**
    
- Go programs tended to be **Type B**
    

because Go has a much larger branching factor.

More recently, Type B approaches have achieved world-champion-level performance in many games.

## Heuristic Alpha-Beta Tree Search (AIMA)

Up to this point, Minimax and Alpha-Beta pruning assume that the search can continue all the way to terminal states. In simple games this is possible, but in complex games such as chess the complete game tree is far too large.

A practical game-playing agent therefore cannot search until the game ends. Instead, it must stop searching at some depth and estimate the quality of the position.

This leads to **heuristic game tree search**.

---

> [!important] Core Idea  
> Instead of searching until the game ends:
> 
> - Stop at a chosen depth.
>     
> - Estimate the value of the position.
>     
> - Use that estimate as if it were the true utility.
>     

---

# From Utility to Evaluation

In standard Minimax:

```text
Terminal State
        ↓
UTILITY(state)
```

In heuristic search:

```text
Cutoff State
        ↓
EVAL(state)
```

The algorithm pretends the cutoff node is a terminal state.

---

# H-MINIMAX

The textbook defines a heuristic version of minimax:

```text
H-MINIMAX(s,d)
```

where:

- `s` = current state
    
- `d` = current depth
    

---

## Definition

If the cutoff condition is reached:

```text
H-MINIMAX(s,d)
=
EVAL(s)
```

Otherwise:

```text
MAX node
=
maximum child value
```

```text
MIN node
=
minimum child value
```

Exactly like ordinary minimax.

The only difference is that the search may stop before reaching the end of the game.

---

# Cutoff Test

A cutoff test decides when search should stop.

Instead of:

```text
IS-TERMINAL(state)
```

we use:

```text
IS-CUTOFF(state, depth)
```

---

## Typical Cutoff Rule

Search until:

```text
Depth = d
```

For example:

```text
Depth 6
Depth 8
Depth 10
```

Then evaluate.

---

## Why Use a Cutoff?

Because complete search is impossible.

For chess:

```text
Branching Factor ≈ 35
Game Length ≈ 80 ply
```

Total possibilities:

```text
35^80
```

which is astronomically large.

---

# Evaluation Functions

An evaluation function estimates how good a position is.

---

## Definition

```text
EVAL(state)
→ estimated utility
```

It approximates:

```text
UTILITY(state)
```

without having to reach the end of the game.

---

> [!note]  
> Evaluation functions in games play the same role as heuristic functions in search algorithms.
> 
> Search heuristics estimate distance to goal.
> 
> Evaluation functions estimate quality of position.

---

# Requirements of a Good Evaluation Function

A useful evaluation function should satisfy two properties.

### 1. Fast

The entire purpose of using evaluation functions is to save time.

If evaluation itself takes too long:

```text
No advantage gained.
```

---

### 2. Correlated with Winning

Higher scores should correspond to better chances of winning.

Even if the values are not perfectly accurate:

```text
Better position
→ Higher evaluation
```

---

# Expected Utility Interpretation

Although games like chess are deterministic, the program is uncertain because it cannot search forever.

Therefore:

```text
Evaluation
≈ Expected utility
```

The evaluation represents the likelihood of future success given limited search depth.

---

# Features

Most evaluation functions do not evaluate the board directly.

Instead they examine features.

A feature is some measurable property of the state.

---

## Examples of Chess Features

```text
Number of pawns
Number of bishops
Number of rooks
King safety
Pawn structure
Mobility
Board control
```

Each feature contributes to the final score.

---

# Expected Value Example

Suppose a category of positions historically produces:

```text
82% wins
16% draws
2% losses
```

Utilities:

```text
Win  = 1
Draw = 0.5
Loss = 0
```

Expected value:

```text
0.82(1)
+
0.16(0.5)
+
0.02(0)

=
0.90
```

Thus:

```text
EVAL = 0.90
```

---

# Material Value

Traditional chess evaluation often starts with material count.

Approximate values:

|Piece|Value|
|---|---|
|Pawn|1|
|Knight|3|
|Bishop|3|
|Rook|5|
|Queen|9|

These values were developed through centuries of chess experience.

---

# Weighted Linear Evaluation Functions

Most classical evaluation functions use weighted sums.

Formula:

```text
EVAL(s)
=
w1f1(s)
+
w2f2(s)
+
...
+
wnfn(s)
```

where:

```text
fi = feature
wi = weight
```

---

## Example

```text
Material Advantage
+
King Safety
+
Mobility
+
Pawn Structure
```

Each term receives a weight.

---

> [!important]  
> The evaluation score does not need to equal the true probability of winning.
> 
> It only needs to preserve ordering:
> 
> ```text
> Better position
> →
> Higher evaluation
> ```

---

# Limitation of Linear Functions

Weighted sums assume:

```text
Features are independent.
```

This is often false.

Example:

```text
Two bishops together
```

may be stronger than:

```text
2 × Single Bishop Value
```

This is called a nonlinear interaction.

---

# Nonlinear Evaluation

Modern game-playing systems often use nonlinear combinations of features.

Examples:

- Piece combinations
    
- Positional interactions
    
- Endgame-specific values
    

A bishop may become more valuable in the endgame than in the opening.

---

# Learning Evaluation Functions

Features and weights do not need to be handcrafted.

Machine learning can estimate them automatically.

---

> [!note]  
> The textbook notes that machine learning rediscovered values close to those used by human chess players for centuries.
> 
> Example:
> 
> ```text
> Bishop ≈ 3 Pawns
> ```

---

# Modifying Alpha-Beta Search

To use heuristic search, replace:

```text
IS-TERMINAL
```

with:

```text
IS-CUTOFF
```

When cutoff occurs:

```text
Return EVAL(state)
```

instead of utility.

Everything else remains the same.

---

# Iterative Deepening

Rather than choosing a single depth:

```text
Depth 8
```

search repeatedly:

```text
Depth 1
Depth 2
Depth 3
...
Depth 8
```

until time expires.

---

## Benefits

If time runs out:

```text
Still have a valid move.
```

Additionally:

```text
Earlier searches
→ Better move ordering
→ Better Alpha-Beta pruning
```

---

# Quiescence Search

A major problem appears when evaluation occurs in unstable positions.

---

## Example

Imagine:

```text
Black ahead materially
```

but White can capture Black's queen next move.

A shallow evaluation might incorrectly conclude:

```text
Black winning
```

when White is actually winning.

---

# Quiescent Positions

A position is quiescent if:

```text
No major tactical explosion imminent.
```

Examples:

- No immediate captures
    
- No immediate threats
    
- No forced tactical sequence
    

---

# Non-Quiescent Positions

Examples:

```text
Queen hanging
Immediate capture available
Forced tactical attack
```

These positions should not be evaluated immediately.

---

## Solution

Continue searching beyond the normal depth limit.

Only stop when a stable position is reached.

---

> [!important]  
> Quiescence Search:
> 
> ```text
> Search deeper only in unstable positions.
> ```

---

# Horizon Effect

One of the most famous problems in game tree search.

## Definition

A critical event exists beyond the search depth.

The algorithm cannot see it.

## Example

A bishop is doomed to be captured.

The program discovers a series of delaying moves.

The capture happens:

```text
Move 9
```

but search only reaches:

```text
Move 8
```

The algorithm incorrectly believes the bishop survives.

> [!warning]  
> Horizon Effect
> 
> The AI pushes bad news beyond the search horizon and mistakenly believes it has solved the problem.

# Singular Extensions

A technique for reducing horizon effects.

---

## Idea

If one move is obviously much stronger than all others:

```text
Continue searching deeper.
```

even if cutoff depth has been reached.

---

## Example

Suppose a rook has a forced sequence:

```text
h2 → h1
h1 → a1
a1 × bishop
```

The algorithm may extend the search specifically along this line.

---

> [!note]  
> Singular extensions selectively deepen the search along clearly superior moves.

---

# Forward Pruning

Alpha-Beta pruning is safe.

Forward pruning is not.

---

## Difference

### Alpha-Beta

Prunes moves that cannot affect the answer.

```text
Always correct.
```

---

### Forward Pruning

Prunes moves that appear poor.

```text
May be wrong.
```

---

# Shannon's Type A vs Type B

Claude Shannon proposed two approaches.

---

## Type A Strategy

Search:

```text
Many moves
Shallow depth
```

Uses evaluation functions.

---

## Type B Strategy

Search:

```text
Few promising moves
Greater depth
```

Ignores many possibilities.

---

> [!important]  
> Forward pruning is a Type B strategy.

---

# Beam Search

A simple forward-pruning method.

Instead of exploring all moves:

```text
Explore only top N moves.
```

according to evaluation.

---

## Problem

The true best move might be discarded.

No guarantee of correctness.

---

# PROBCUT

Probabilistic Cut.

Developed by:

```text
Michael Buro (1995)
```

---

## Idea

Alpha-Beta prunes when a node is certainly outside bounds.

PROBCUT prunes when a node is probably outside bounds.

---

### Process

1. Perform shallow search.
    
2. Estimate deeper value statistically.
    
3. Decide whether deeper search is worthwhile.
    

---

> [!note]  
> PROBCUT trades certainty for speed.

---

# Late Move Reduction (LMR)

Assumption:

```text
Move ordering is good.
```

Therefore:

```text
Later moves
=
less promising
```

---

## Strategy

Search late moves at reduced depth.

If a move later appears strong:

```text
Re-search at full depth.
```

---

# Practical Search Strength

Approximate chess performance:

|Technique|Approximate Search Depth|
|---|---|
|Minimax|~5 ply|
|Alpha-Beta + Transposition Table|~14 ply|
|Top Engines (Stockfish)|30+ ply|

---

# Search vs Lookup

Not every position requires search.

Sometimes lookup is better.

---

# Opening Books

For early moves:

```text
Use databases
```

instead of searching.

The computer follows known strong opening lines.

---

# Endgame Tables

Near the end of the game:

```text
Use lookup tables
```

containing perfect play.

---

## Endgame Tablebases

A table stores:

```text
Position
→ Best Move
```

for every possible state.

---

# Retrograde Search

Endgame tables are built backward.

---

## Process

Start with:

```text
Known wins
Known losses
```

Then repeatedly determine:

```text
Which positions lead to them?
```

This is called:

```text
Retrograde Minimax Search
```

---

> [!summary] Key Takeaways
> 
> - Heuristic search replaces UTILITY with EVAL.
>     
> - Cutoff tests stop search before terminal states.
>     
> - Evaluation functions estimate position strength.
>     
> - Weighted linear functions combine multiple features.
>     
> - Quiescence search prevents evaluating unstable positions.
>     
> - Horizon effect occurs when important events lie beyond search depth.
>     
> - Singular extensions help reduce horizon effects.
>     
> - Forward pruning sacrifices guaranteed correctness for speed.
>     
> - PROBCUT and Late Move Reduction are advanced forward-pruning techniques.
>     
> - Opening books and endgame tablebases replace search with lookup when possible.
>     
> - Retrograde search builds perfect endgame solutions by working backward from known outcomes.

# 6.5 Stochastic Games

## Overview

So far, adversarial search assumed deterministic games where every move leads to a known outcome. Many real-world games contain randomness, such as dice rolls or card shuffling. These are called **stochastic games**.

In stochastic games, players must reason not only about their opponent's choices but also about uncertain events generated by chance.

A classic example is backgammon, where dice rolls determine which moves are available.

---

## Chance Nodes

Standard game trees contain only MAX and MIN nodes.

Stochastic games introduce a third type:

**Chance Nodes**

These represent random events such as:

- Dice rolls
    
- Card draws
    
- Random game mechanics
    

Each outgoing branch corresponds to a possible random outcome and is labeled with its probability.

Example:

- Rolling two dice creates multiple possible outcomes.
    
- Each outcome leads to different legal moves for the players.
    

Thus the search tree becomes:

```
MAX
 ↓
Chance
 ↓
MIN
 ↓
Chance
 ↓
MAX
```

instead of simply alternating MAX and MIN.

---

## Expected Value

Because future outcomes depend partly on chance, positions no longer have fixed minimax values.

Instead, we calculate their:

**Expected Value**

Expected value is the weighted average of all possible outcomes.

General formula:

```
Expected Value =
Σ Probability(outcome) × Value(outcome)
```

A move is preferred if it leads to the highest expected utility.

---

## Expectiminimax

Minimax is extended to stochastic games through:

**Expectiminimax**

The algorithm behaves as follows:

### Terminal Nodes

Return:

```
UTILITY(state)
```

### MAX Nodes

Choose:

```
maximum child value
```

### MIN Nodes

Choose:

```
minimum child value
```

### Chance Nodes

Choose:

```
weighted average of child values
```

using outcome probabilities.

---

## Expectiminimax Summary

|Node Type|Operation|
|---|---|
|MAX|Maximum|
|MIN|Minimum|
|Chance|Expected Value|
|Terminal|Utility|

Thus expectiminimax combines:

- Adversarial reasoning
    
- Probabilistic reasoning
    

into a single framework.

---

## Evaluation Functions in Stochastic Games

Evaluation functions become more delicate when chance nodes are present.

In deterministic games, only ordering matters:

```
Position A > Position B
```

is sufficient.

In stochastic games this is no longer enough.

Because expected values are averaged, evaluation scores must correspond to:

- probability of winning
    
- expected utility
    

through a positive linear relationship.

Otherwise changing the scale of evaluations can completely alter move selection.

The numerical values themselves therefore carry meaning, not merely their ranking.

---

## Complexity of Expectiminimax

For deterministic minimax:

```
O(b^m)
```

where:

- b = branching factor
    
- m = depth
    

For stochastic games:

```
O(b^m n^m)
```

where:

- n = number of possible chance outcomes
    

This additional factor can make search extremely expensive.

Backgammon illustrates the problem:

- ~21 distinct dice outcomes
    
- branching factor often around 20
    
- occasionally much higher
    

As a result, only shallow lookahead is usually practical.

---

## Alpha–Beta Ideas for Chance Nodes

Traditional alpha–beta pruning relies on bounds.

At first glance, chance nodes appear impossible to prune because expected value requires considering every outcome.

However, if utility values have known limits:

```
Utility ∈ [Min, Max]
```

then upper and lower bounds can be placed on partially evaluated chance nodes.

This allows some pruning.

The technique is less powerful than ordinary alpha–beta but can still reduce computation.

---

## Sampling Chance Outcomes

When chance branching becomes very large, evaluating every outcome may be infeasible.

Two alternatives are:

### Forward Pruning

Evaluate only a subset of chance branches.

### Monte Carlo Methods

Sample random outcomes during simulations rather than enumerating them all.

These approaches trade exactness for efficiency.

---

# 6.6 Partially Observable Games

## Overview

Many real-world situations involve incomplete information.

Players cannot fully observe the game state and must make decisions under uncertainty.

Examples:

- Poker
    
- Bridge
    
- Battleship
    
- Stratego
    
- StarCraft
    
- Military operations
    

These games differ fundamentally from fully observable games like chess.

---

## Kriegspiel

A famous example is:

**Kriegspiel**

In Kriegspiel:

- Players see only their own pieces.
    
- Opponent pieces are invisible.
    
- A referee enforces legality and announces limited information.
    

Players must reason about hidden positions rather than directly observed states.

---

## Belief States

The key concept becomes:

**Belief State**

A belief state is:

> The set of all game states that could be true given everything observed so far.

Instead of searching one board position, the player searches over many possible positions simultaneously.

As the game progresses:

- observations eliminate impossible states
    
- belief states shrink
    
- uncertainty decreases
    

This is identical to state-estimation ideas from partially observable search.

---

## Strategies in Partially Observable Games

In fully observable games:

```
Strategy = response to opponent moves
```

In partially observable games:

```
Strategy = response to possible percept sequences
```

The player must plan for every possible observation they may receive.

---

## Guaranteed Checkmate

A:

**Guaranteed Checkmate**

works for:

- every possible true board state
    
- every opponent response
    

within the current belief state.

This is analogous to AND–OR search solutions where success must be guaranteed regardless of uncertainty.

---

## Probabilistic Checkmate

Partially observable games introduce a new concept:

**Probabilistic Checkmate**

The strategy wins with probability approaching 1 but not necessarily with certainty.

Randomization becomes part of optimal play.

A player may repeatedly create situations where the opponent must guess correctly, eventually making a mistake.

---

## Accidental Checkmate

Sometimes a strategy succeeds only in some states of the belief state.

If the hidden position happens to be favorable:

```
checkmate occurs
```

even though the player could not know it would happen.

This is called an:

**Accidental Checkmate**

Most human checkmates in hidden-information games fall into this category.

---

## Importance of Randomization

In partially observable games, predictable play leaks information.

Therefore optimal play often includes deliberate randomness.

Benefits include:

- preventing opponents from inferring hidden information
    
- reducing predictability
    
- enabling bluffing
    
- maintaining uncertainty
    

This is a major difference from deterministic perfect-information games.

---

# Card Games

## Hidden Information + Chance

Card games combine:

1. Partial observability
    
2. Stochastic events
    

Examples:

- Bridge
    
- Poker
    
- Hearts
    
- Whist
    

The hidden information comes from card dealing.

---

## Averaging Over Clairvoyance

A tempting approach is:

1. Assume a particular card deal.
    
2. Solve the game perfectly.
    
3. Repeat for all deals.
    
4. Average the results.
    

This is called:

**Averaging Over Clairvoyance**

because it assumes future states become fully known.

---

## Why Averaging Over Clairvoyance Fails

The method ignores the value of information.

It assumes future uncertainty disappears automatically.

Consequently it:

- does not seek information
    
- does not conceal information
    
- does not bluff
    
- does not communicate information to partners
    

These are precisely the behaviors that matter in card games.

---

## Dealing with Huge Numbers of Deals

Bridge contains over:

```
10 million
```

possible unseen card distributions.

Two common techniques are used:

### Abstraction

Treat strategically similar hands as equivalent.

Example:

```
AAA72 ≈ AAA64
```

because both represent:

```
three aces + low cards
```

---

### Sampling

Randomly sample only a subset of deals.

Typical sample sizes:

```
100–1000 deals
```

This provides a good approximation while keeping computation manageable.

---

## Poker AI

Modern poker systems have achieved superhuman performance.

Notable examples include:

- Libratus
    
- ALPHAZERO
    
- ALPHASTAR
    

Key techniques include:

- abstraction
    
- equilibrium strategies
    
- opponent modeling
    
- large-scale computation
    

These systems demonstrated that hidden-information games can be mastered by AI.

---

# 6.7 Limitations of Game Search Algorithms

## Limitation 1: Evaluation Function Errors

Alpha–beta search depends heavily on evaluation functions.

A small error in evaluation can cause:

- wrong move ordering
    
- incorrect minimax values
    
- poor decisions
    

Since minimax often bases decisions on a small difference between scores, even modest evaluation noise can reverse the preferred move.

---

## Limitation 2: Wasted Computation

Search algorithms evaluate move values.

Sometimes this is unnecessary.

Examples:

- only one legal move exists
    
- several moves are obviously equivalent
    

Computing exact values wastes time.

What matters is whether additional search can actually improve the decision.

---

## Utility of Node Expansion

A more rational approach is to ask:

> Is expanding this node worth the computational cost?

Search should continue only if expected improvement exceeds computation cost.

This idea leads directly to:

**Metareasoning**

---

## Metareasoning

**Metareasoning = reasoning about reasoning**

The algorithm decides:

- what computations to perform
    
- where to spend time
    
- when to stop searching
    

The goal is to maximize decision quality, not search depth.

Monte Carlo methods partially address this by allocating more effort to promising regions of the tree.

---

## Limitation 3: Move-Level Reasoning

Alpha–beta and MCTS reason mainly about individual moves.

Humans often reason differently.

Instead of thinking:

```
move → move → move
```

they think:

```
trap queen
control center
launch attack
defend king
```

These higher-level concepts correspond to planning and abstraction, which are covered later in AI planning.

---

## Limitation 4: Dependence on Human Expertise

Traditional game-playing systems relied heavily on:

- handcrafted evaluation functions
    
- opening books
    
- pruning heuristics
    
- domain knowledge
    

This required significant human engineering.

---

## Shift Toward Learning

Modern systems increasingly learn through self-play.

Examples include:

- ALPHAZERO
    
- ALPHASTAR
    

Rather than encoding expert knowledge manually, these systems learn:

- evaluation functions
    
- policies
    
- strategies
    

from experience.

---

# Exam / Interview Quick Summary

### Deterministic Games

```
Minimax
Alpha–Beta
Evaluation Functions
Move Ordering
```

### Stochastic Games

```
Chance Nodes
Expected Value
Expectiminimax
```

### Partially Observable Games

```
Belief States
Kriegspiel
Guaranteed Checkmate
Probabilistic Checkmate
Bluffing
```

### Modern Search

```
Monte Carlo Tree Search
UCT/UCB1
Self-play Learning
```

### Key Limitation Themes

```
Evaluation Errors
Search Cost
Uncertainty
Hidden Information
Need for Learning
Metareasoning
```

---

## Connection to CS6601 Game Playing

For your game-playing assignments, the concepts that matter most are:

1. **Minimax**
    
2. **Alpha–Beta Pruning**
    
3. **Move Ordering**
    
4. **Evaluation Functions**
    
5. **Cutoff Search**
    
6. **Game Tree Complexity**
    
7. **Monte Carlo Tree Search (high level)**
    
8. **Metareasoning (why we can't search everything)**
    

The stochastic and partially observable sections are usually not directly implemented in Isolation-style assignments, but they explain how adversarial search extends to dice games, poker, and real-world decision making.

## Modern Challenges

Games such as:

- Poker
- StarCraft II
- Dota 2

introduce:

- Partial observability
- Multi-agent coordination
- Real-time decision making
- Massive action spaces

Systems such as AlphaStar and OpenAI Five extended game-playing AI beyond classical board games.