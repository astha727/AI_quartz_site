# Introduction

In previous search problems, the objective was typically to **find a sequence of actions** that transforms an initial state into a goal state.

Constraint Satisfaction Problems (CSPs) are different.

Instead of finding a path, the objective is simply to find an **assignment of values** to variables such that **all constraints are satisfied simultaneously**.

Many important AI scheduling and planning problems naturally fit this framework.
## Airport Scheduling Motivation

> [!example] Example from the lecture
> 
> Atlanta is home to one of the world's busiest airports.
> 
> - Five runways
>     
> - Approximately **2,500 arrivals and departures per day**
>     
> - Aircraft take off or land approximately **every 30 seconds**
>     
> 
> Scheduling all these flights without conflicts is a classic **Constraint Satisfaction Problem**.

Instead of searching through paths, the scheduler searches for an assignment of:

- runway
    
- time slot
    
- aircraft
    

such that all operational constraints are satisfied.

---

# What is a Constraint Satisfaction Problem?

> [!definition]  
> A **Constraint Satisfaction Problem (CSP)** consists of:
> 
> - Variables
>     
> - Domains
>     
> - Constraints
>     

The objective is to assign every variable a value from its domain while satisfying every constraint.

## Three Components of Every CSP

### 1. Variables

Variables represent the unknown quantities that must be assigned.

Examples:

- Territory colors
    
- Sudoku cells
    
- Classroom assignments
    
- Flight schedules
    
- Factory jobs
    

---

### 2. Domains

The **domain** is the set of allowable values for each variable.

Example:

|Variable|Domain|
|---|---|
|WA|{Red, Green, Blue}|
|NT|{Red, Green, Blue}|
|SA|{Red, Green, Blue}|

---

### 3. Constraints

Constraints specify which assignments are legal.

They eliminate invalid combinations of values.

Example:

```
WA ≠ NT
SA ≠ Q
NSW ≠ V
```

---

# Formal Definition

A CSP can be written as

$$  
CSP=(X,D,C)  
$$

where

- **X** = variables
    
- **D** = domains
    
- **C** = constraints
    

The solution is a complete assignment satisfying every constraint.

---

> [!success] Goal
> 
> Find
> 
> $$  
> assignment(X_i)\in D_i  
> $$
> 
> such that every constraint in
> 
> $$  
> C  
> $$
> 
> is satisfied.

---

# Map Coloring Example

The lecture introduces the classical **Australia Map Coloring Problem**.

The objective is to color every territory using the **minimum number of colors**, while ensuring neighboring regions never share the same color.

## Variables

Each Australian territory is a variable.

```
WA
NT
SA
Q
NSW
V
T
```

## Domains

Each variable may take one of three colors.

```
Red
Green
Blue
```

## Constraints

Neighboring territories cannot have the same color.

For example,

```
WA ≠ NT

WA ≠ SA

NT ≠ SA

NT ≠ Q

SA ≠ Q

SA ≠ NSW

SA ≠ V

Q ≠ NSW

NSW ≠ V
```

---

> [!important]  
> A solution is **not** merely assigning colors.
> 
> A solution is an assignment where **every constraint is simultaneously satisfied**.

# CSP Representation

Instead of drawing the map, AI algorithms work using the variables and constraints.

The Australia problem becomes

```
Variables

WA
NT
SA
Q
NSW
V
T

↓

Domains

{Red, Green, Blue}

↓

Constraints

Adjacent regions must have different colors
```

# Types of Constraints

The lecture introduces several kinds of constraints.

# Unary Constraints

> [!definition]  
> Unary constraints involve only **one variable**.

Example from the lecture:

```
Tasmania cannot be purple.
```

Only Tasmania is involved.

Another example:

```
WA ≠ Red
```

Only WA is restricted.


Unary constraints simply reduce a variable's domain.

Example

Before

```
WA

{Red, Green, Blue}
```

After

```
WA

{Green, Blue}
```

---

# Binary Constraints

> [!definition]  
> Binary constraints relate **two variables**.

Example

```
WA ≠ NT
```

Another

```
SA ≠ NSW
```

These are the most common CSP constraints.

---

# Higher-Order Constraints

Some constraints involve **three or more variables**.

The lecture notes that constraints may involve:

- three variables
    
- four variables
    
- many variables simultaneously
    

Example

```
A+B+C ≤ 20
```

Although the lecture does not expand further, these are called **higher-order constraints**.

---

# Soft Constraints

Unlike hard constraints, soft constraints express **preferences** rather than requirements.

Example from lecture:

> "I prefer to teach on a Tuesday/Thursday schedule."

This is not mandatory.

It is simply preferred.

---

> [!note]  
> Problems involving preferences are called **Constraint Optimization Problems**.

---

# Constraint Optimization Problems

A constraint optimization problem attempts to satisfy constraints while also optimizing preferences.

Instead of asking

> Is this assignment legal?

it asks

> Which legal assignment is best?

The lecture notes that these problems are often solved using **linear programming** techniques.

---

# Constraint Graph

Binary CSPs can be represented using a graph.

## Definition

> [!definition]  
> A Constraint Graph represents:
> 
> - Variables as nodes
>     
> - Binary constraints as edges
>     


Example

```text
WA -------- NT
 \          |
  \         |
   \        |
     SA ---- Q
      |
      |
     NSW
      |
      |
      V

T
```

---

Here

Nodes

```
WA
NT
SA
Q
NSW
V
T
```

represent variables.

Edges indicate binary constraints.

---

> [!important]  
> There is **no edge**
> 
> ⇒
> 
> No binary constraint exists.

---

# Why Constraint Graphs Help

The lecture explains that general CSP algorithms exploit graph structure to speed up search.

Instead of viewing the problem as one enormous search space,

the graph reveals

- independent variables
    
- connected components
    
- heavily constrained variables
    

## Tasmania Example

Tasmania has no neighboring territories.

Therefore,

it is disconnected from the rest of the graph.

```
WA—NT—SA—Q—NSW—V

T
```

Tasmania can be solved completely independently.

---

> [!exam-tip]  
> Independent subgraphs can be solved separately.
> 
> This dramatically reduces search complexity.


# Constraint Hypergraph

Not every CSP consists only of binary constraints.

Some constraints involve many variables simultaneously.

The lecture introduces the **Constraint Hypergraph**.

## Difference

Constraint Graph

```
Edge

connects

2 variables
```

Constraint Hypergraph

```
Hyperedge

connects

many variables
```

---

# Cryptarithmetic Example

The lecture uses

```
  TWO
+ TWO
------
 FOUR
```

Variables

```
T

W

O

F

U

R

X₁

X₂

X₃
```

where

```
X₁

X₂

X₃
```

represent carry variables.

## Global Constraint

Every letter must represent a **different digit**.

```
T ≠ W ≠ O ≠ F ≠ U ≠ R
```

This is a global constraint involving all variables simultaneously.

## Carry Constraints

The lecture introduces equations such as

$$  
O+O=R+10X_1  
$$

where

$$  
X_1\in{0,1}  
$$

Similarly,

$$  
X_1+W+W=U+10X_2  
$$

and

$$  
X_2+T+T=O+10X_3  
$$

Finally,

$$  
F=X_3  
$$

These constraints naturally connect multiple variables simultaneously, motivating the use of a **constraint hypergraph**.

# Real-World CSP Examples

## Sudoku

Variables

```
81 cells
```

Domain

```
1–9
```

Constraints

- Row uniqueness
    
- Column uniqueness
    
- Box uniqueness
    

## Factory Scheduling

Variables

Jobs

Domain

Available machines

Constraints

- No machine overlap
    
- Deadlines
    
- Resource availability
    

## Car Assembly

Variables

Assembly tasks

Constraints

Order dependencies

## Class Scheduling

Variables

Courses

Constraints

- Professor availability
    
- Room availability
    
- Time conflicts
    

## Transportation Scheduling

Variables

Vehicles

Routes

Drivers

Constraints

- Capacity
    
- Time windows
    
- Driver limits
    

## Spreadsheet Problems

Variables

Cells

Constraints

Formula dependencies

## Floor Planning

Variables

Room positions

Constraints

Space limitations

Adjacency requirements


# CSP vs Classical Search

|Classical Search|Constraint Satisfaction|
|---|---|
|Searches for a path|Searches for an assignment|
|Sequence of actions|Variable assignments|
|Goal reached after actions|Goal reached when all constraints hold|
|State = world configuration|State = partial assignment|

# Memory Aid

> [!tip] Remember: **VDC**
> 
> **V** → Variables (what to assign)
> 
> **D** → Domains (possible values)
> 
> **C** → Constraints (rules that assignments must satisfy)

---

# Constraint Graphs, CSP Examples & Backtracking Search

# Constraint Graph

## Motivation

After defining variables, domains, and constraints, we need a way to visualize the structure of a CSP.

Instead of thinking about a long list of constraints, we represent relationships as a graph.

The OMSCS lecture introduces the **constraint graph** as a way to expose the problem structure so that general CSP algorithms can exploit it.


## Constraint Graph Definition

A **constraint graph** represents variables as nodes and constraints as edges.

- Nodes = variables
- Edges (arcs) = constraints between variables

The graph contains **only binary constraints**.

## Australia Example

Variables:

- WA
- NT
- SA
- Q
- NSW
- V
- T

Each node corresponds to one territory.

Edges connect neighboring territories.

For example:

- WA — NT
- WA — SA
- NT — SA
- NT — Q
- SA — Q
- SA — NSW
- SA — V
- NSW — V
- NSW — Q

Tasmania has no neighboring territories.

### Constraint Graph

```text
         NT -------- Q
        / |          |
      WA  |          |
        \ |          |
         SA -------- NSW
          |           |
          |           |
          V           |
                      
          T
```

(The exact drawing is not important—the adjacency relationships are.)


## Why Use Constraint Graphs?

The lecture explains that graph structure allows us to apply general-purpose CSP algorithms more efficiently.

Instead of blindly searching:

- understand dependencies
- separate independent components
- reduce unnecessary computation

## Independent Variables

One important observation from the lecture:

Tasmania has no neighbors.

Therefore:

- its assignment does not affect any other variable
- it can be solved independently

This significantly reduces search effort.

> [!important]
> Independent components of a CSP can be solved separately.


# Types of Constraints

The lecture discusses several kinds of constraints.

## Unary Constraints

Unary constraints involve only **one variable**.

Example:

> Tasmania cannot be purple.

Only Tasmania is involved.

### Characteristics

- restrict one domain
- simplest constraint
- represented directly on one variable

## Binary Constraints

Binary constraints involve **two variables**.

Example:

WA ≠ NT

The colors of WA and NT must differ.

Binary constraints are exactly what appear as edges in a constraint graph.

## Higher-Order Constraints

Some constraints involve three or more variables.

Example mentioned in lecture:

constraints involving three or more variables.

Binary graphs cannot represent these directly.

## Soft Constraints

Unlike hard constraints, soft constraints express preferences.

Lecture example:

> "I prefer to teach on a Tuesday/Thursday schedule."

Violating a soft constraint does **not** invalidate the solution.

Instead:

- some solutions are preferred over others.

### Constraint Optimization Problems

Problems containing preference constraints are called

**Constraint Optimization Problems (COPs).**

The lecture notes that these are related to solving **linear programming** problems.

# Examples of CSPs

## Sudoku

Every cell

- variable

Possible numbers

- domain

Row/column/box rules

- constraints

## Car Assembly

Variables:

manufacturing choices

Constraints:

parts compatibility

production order

availability

## Factory Job Scheduling

Variables:

job times

Constraints:

machine availability

ordering

deadlines

## Class Scheduling

Variables:

course times

Constraints:

- instructor availability
- classroom availability
- student conflicts

## Spreadsheet Problems

Variables:

cell values

Constraints:

formula dependencies

## Transportation Scheduling

Variables:

vehicle assignments

Constraints:

routes

timing

capacity

## Floor Planning

Variables:

object positions

Constraints:

size

adjacency

spacing

> [!note]
> Many practical CSPs use **real-valued variables**, not just discrete values.


# Constraint Hypergraph

The lecture next introduces a more general representation.

## Why Hypergraphs?

Constraint graphs only represent binary constraints.

Many real CSPs contain constraints involving:

- three variables
- four variables
- all variables simultaneously

For these we use a **constraint hypergraph**.

## Hypergraph Definition

A hyperedge may connect **any number of variables**.

Unlike ordinary graph edges:

- 2 variables
- 3 variables
- 5 variables
- all variables

can all participate in one constraint.

---

# Cryptarithmetic Example

The lecture uses the classic puzzle

```
  TWO
+ TWO
------
 FOUR
```

Each letter represents a digit.

## Variables

```
T
W
O
F
U
R
```

Additional carry variables:

```
X1
X2
X3
```

## Domains

Letters:

```
0–9
```

Carry variables:

```
0
1
```


## Global Constraint

The lecture introduces an important global constraint.

> No two letters may represent the same digit.

This involves **all variables simultaneously**.

Therefore it cannot be represented by ordinary binary edges.

## First Column Constraint

The ones column gives

```
O + O = R + 10X1
```

where

```
X1 ∈ {0,1}
```


## Second Column

```
X1 + W + W = U + 10X2
```


## Third Column

```
X2 + T + T = O + 10X3
```


## Fourth Column

```
F = X3
```


Each of these equations becomes a hyperedge connecting multiple variables.


> [!important]
> Hypergraphs allow one constraint to simultaneously connect many variables.

---

# Backtracking Search

The lecture introduces the simplest CSP solving algorithm first.

The instructor jokingly calls it

> "the stupid one first."

The idea is simply systematic search.

---

# State Representation

A state consists of

> values assigned so far.

Initially,

no variables have values.

## Initial State

```
{}
```

Empty assignment.

## Goal Test

Check whether

- every variable has been assigned

and

- all constraints are satisfied.

If yes,

return solution.

---

# General Procedure

The lecture describes the algorithm as follows.

1. Begin with empty assignment.

2. Choose an unassigned variable.

3. Assign one legal value.

4. Continue recursively.

5. If no legal assignment exists

backtrack.

6. Try another value.

7. Continue until

- solution

or

- complete failure.

# Dead Ends

A dead end occurs when

no legal assignment remains.

At this point

the algorithm backs up to the previous assignment.

---

> [!warning]
> Backtracking never continues from an impossible partial assignment.

---

# Australia Example

The lecture demonstrates backtracking step by step.

## Step 1

Choose

```
WA
```

Possible colors

```
Orange
Green
Blue
```

Choose

```
Orange
```


## Step 2

Choose

```
NT
```

Since NT borders WA,

Orange is illegal.

Remaining:

```
Green
Blue
```

Choose

```
Green
```


## Step 3

Choose

```
Queensland
```

Possible:

```
Orange
Blue
```

Choose

```
Blue
```


## Problem

Now attempt to color

```
South Australia
```

South Australia borders

- WA (Orange)
- NT (Green)
- Queensland (Blue)

All three colors are already forbidden.

No color remains.

---

```
SA

Orange ✗
Green ✗
Blue ✗
```

Dead end.

## Backtracking

Return to previous decision.

Undo Queensland.

Choose a different color.

Continue searching.

> [!success]
> Backtracking systematically explores alternative assignments whenever a dead end is reached.

---

# Why Backtracking Works

The algorithm eventually explores every possible assignment.

Therefore,

if a solution exists,

backtracking will eventually find it.

---

# Why It Is Slow

The lecture emphasizes that although backtracking is correct,

it is often very inefficient.

Problems include:

- exploring bad choices deeply
- repeated work
- late detection of failures
- enormous search trees


## Motivation for Later Optimizations

The remainder of the lecture introduces techniques that greatly improve backtracking.

These include:

- Least Constraining Value (LCV)
- Minimum Remaining Values (MRV)
- Degree Heuristic
- Forward Checking
- Constraint Propagation
- Arc Consistency

These optimizations all aim to reduce unnecessary search and detect failures earlier.

# Exam Points

> [!tip] Remember
> **Constraint Graph**
> - Nodes = variables
> - Edges = binary constraints

> [!tip]
> **Unary constraint**
> - One variable

> [!tip]
> **Binary constraint**
> - Two variables

> [!tip]
> **Higher-order constraint**
> - Three or more variables

> [!tip]
> **Hypergraph**
> - Represents multi-variable constraints

> [!tip]
> **Initial CSP state**
> - Empty assignment

> [!tip]
> **Backtracking**
> - Assign
> - Recurse
> - Backtrack on failure

> [!tip]
> **Dead End**
> - No legal values remain

> [!tip]
> Tasmania is independent because it has no neighboring constraints.

---

# Why Improve Backtracking?

Simple backtracking is correct, but it often wastes enormous amounts of work.

The lecture shows that many failures occur **deep in the search tree**, after assigning many variables.

Instead, we would like to:

- make better choices earlier,
- detect failures sooner,
- reduce unnecessary backtracking.

The OMSCS lecture introduces three important heuristics.

---

# Three Major Heuristics

1. Least Constraining Value (LCV)

2. Minimum Remaining Values (MRV)

3. Degree Heuristic

These heuristics do **not** change the solution.

They only change **the order in which search is performed**, often reducing search dramatically.

# Least Constraining Value (LCV)

## Motivation

Suppose there are several legal values for a variable.

Which one should we choose?

Instead of choosing randomly,

choose the value that leaves the greatest flexibility for future assignments.

## Definition

The **Least Constraining Value (LCV)** is the value that eliminates the fewest choices for neighboring unassigned variables.

In other words,

choose the value that constrains the future **least**.

## Australia Example

The lecture begins with

```
WA = Orange
NT = Green
```

Now we need to color Queensland.

Queensland has two legal colors.

```
Orange

Blue
```

Instead of choosing arbitrarily,

the lecture chooses

```
Orange
```

because Queensland is **not adjacent to Western Australia**.

Using Orange again leaves Blue available for future neighboring regions.

---

### Result

Choosing Orange preserves more possibilities later in the search.

Therefore,

Orange is the **Least Constraining Value**.

---

> [!important]
> LCV chooses the value that leaves the largest number of legal choices for the remaining variables.

---

# Why LCV Helps

Suppose two values are available.

One causes many future variables to lose options.

The other causes very few restrictions.

Choosing the second option makes future assignments easier.

This often prevents unnecessary backtracking.


## Intuition

Think of solving a puzzle.

Rather than immediately blocking future moves,

leave yourself as many options as possible.

That is exactly what LCV does.


# Minimum Remaining Values (MRV)

## Motivation

Which variable should be assigned next?

Instead of choosing randomly,

choose the variable with the **fewest legal values remaining**.


## Definition

The **Minimum Remaining Values (MRV)** heuristic selects the variable whose domain is currently the smallest.

It is sometimes called **the most constrained variable heuristic.**


## Australia Example

Suppose we have already assigned

```
WA

NT
```

Several variables remain.

The lecture observes that

```
South Australia
```

has the fewest legal colors remaining.

Therefore,

assign South Australia next.

---

Why?

If South Australia has no legal value, we discover failure immediately.

If we postpone it, we may waste many assignments before discovering the same failure.

> [!important]
> MRV tries to detect dead ends as early as possible.

---

# Why MRV Works

Imagine two variables.

Variable A

```
3 possible values
```

Variable B

```
1 possible value
```

Assigning B first immediately tells us whether the branch can succeed.

Assigning A first may waste many steps before eventually discovering B has no legal assignment.


## Intuition

Always solve the hardest variable first.

# Degree Heuristic

## Motivation

Sometimes several variables tie under MRV.

Which one should we choose?

## Definition

Choose the variable involved in the **largest number of constraints** with unassigned variables.

This is called the **Degree Heuristic.**

## Australia Example

The lecture presents a tie.

Two variables each have only one remaining legal value.

The question is:

Which should we assign?

The lecture compares

```
Queensland

Western Australia
```

Queensland borders:

- Northern Territory
- South Australia
- New South Wales

Western Australia borders:

- Northern Territory
- South Australia

Queensland participates in more constraints.

Therefore,

choose Queensland.

> [!important]
> The Degree Heuristic chooses the variable that constrains the greatest number of other variables.


# Why Degree Helps

Variables connected to many others have greater influence on the remaining search.

Assigning them early reveals conflicts sooner.

This reduces wasted computation.

## Intuition

Solve the variable that affects the largest portion of the remaining problem.

# Combining the Heuristics

The lecture presents these heuristics together.

Typical order:

### Step 1

Choose the variable using

**Minimum Remaining Values (MRV).**

---

### Step 2

If there is a tie,

use the

**Degree Heuristic.**

---

### Step 3

Choose the value using

**Least Constraining Value (LCV).**

This ordering minimizes unnecessary backtracking.


# Example Search Flow

Suppose the search reaches the following state.

Assigned:

```
WA = Orange

NT = Green
```


## Variable Selection

South Australia has the smallest remaining domain.

Choose

```
SA
```

using MRV.


## Tie?

If multiple variables have equally small domains,

choose the one participating in the largest number of constraints.

Use the Degree Heuristic.

## Value Selection

If SA has several legal colors,

select the color that removes the fewest possibilities for neighboring variables.

Use LCV.

# Backtracking Optimization Quiz

The lecture presents a partially colored map.

The question asks:

> Which region should be filled next to minimize future backtracking?

The lecture states that there may be multiple correct answers depending on which heuristic is applied.

## Quiz Solution

The lecture explains two correct approaches.

### Using MRV

Choose the region that has only **two possible colors remaining**.

Among all regions,

this one has the **minimum remaining values**.

---

### Using LCV

For another region,

choose the color

```
Green
```

because neighboring regions can only take

```
Light Blue

Dark Blue
```

Avoiding those colors preserves more options for later assignments.

Therefore,

Green is the **Least Constraining Value**.

---

# Effect on Performance

The lecture compares these heuristics with ordinary backtracking.

For the **N-Queens problem**, adding:

- MRV
- Least Constraining Value

allows solving the

**1000-Queens problem.**

The instructor remarks that this would be impossible to solve manually.

---

> [!success]
> Intelligent variable ordering and value ordering can reduce search by many orders of magnitude without changing the correctness of the algorithm.

# Summary Table

| Heuristic | Chooses | Goal |
|-----------|---------|------|
| **MRV** | Variable with the fewest legal values remaining | Detect failure early |
| **Degree Heuristic** | Variable involved in the largest number of remaining constraints | Expose future conflicts early |
| **LCV** | Value that removes the fewest choices from neighboring variables | Preserve future flexibility |


# Exam Points

> [!tip] MRV
> Choose the variable with the **fewest legal values remaining**.

> [!tip]
> Degree Heuristic
> Break MRV ties by choosing the variable connected to the **most unassigned variables**.

> [!tip]
> Least Constraining Value
> Choose the value that leaves the **maximum flexibility** for future assignments.

> [!tip]
> These heuristics improve **efficiency only**.
>
> They do **not** change the solution.

> [!tip]
> Standard heuristic order:
>
> **MRV → Degree Heuristic (tie-breaker) → LCV**

---
# Why Do We Need More Than Backtracking?

Even after using:

- Minimum Remaining Values (MRV)
- Least Constraining Value (LCV)
- Degree Heuristic

backtracking still explores branches that are already doomed to fail.

The lecture introduces **Forward Checking** and **Constraint Propagation** to detect these failures **before** the search goes deeper.

# Forward Checking

## Motivation

Suppose we assign a value to one variable.

Instead of waiting until later to discover conflicts, we immediately update the remaining variables.

Forward Checking keeps track of the legal values that remain for every unassigned variable.

> [!definition]
> **Forward Checking** removes values from the domains of neighboring unassigned variables whenever a variable receives an assignment.

## Core Idea

Whenever a variable is assigned:

1. Look at every neighboring unassigned variable.
2. Remove any values that violate the new assignment.
3. Continue searching only if every neighbor still has at least one legal value.

> [!important]
> If any unassigned variable loses **all** of its legal values, the current branch can never produce a solution.
>
> Backtrack immediately.

# Forward Checking Algorithm

Whenever a variable is assigned:

```text
Assign variable

↓

Update neighboring domains

↓

Any empty domain?

↓

YES → Backtrack

NO → Continue Search
```

---

# Australia Map Example

Initially, every region can take any of the three colors.

```
WA = {Orange, Green, Blue}
NT = {Orange, Green, Blue}
SA = {Orange, Green, Blue}
Q  = {Orange, Green, Blue}
NSW = {Orange, Green, Blue}
V = {Orange, Green, Blue}
```

## Step 1

Assign

```
WA = Orange
```

Forward Checking removes Orange from every neighboring variable.

Updated domains

```
NT = {Green, Blue}

SA = {Green, Blue}
```

The remaining regions are unchanged.

## Step 2

Assign

```
Queensland = Green
```

Forward Checking now removes Green from Queensland's neighbors.

Updated domains

```
NT = {Blue}

SA = {Blue}

NSW = {Orange, Blue}
```

## Step 3

Assign

```
Victoria = Blue
```

Victoria borders New South Wales.

Remove Blue from NSW.

```
NSW = {Orange}
```


Current domains become

```
NT = {Blue}

SA = ?

NSW = {Orange}

V = Blue
```

At this point,

South Australia has already lost several colors.

Eventually,

```
SA = { }
```

No legal colors remain.

## Result

Forward Checking immediately detects

```
SA = ∅
```

instead of continuing deeper into the search tree.

The search backtracks immediately.

> [!success]
> Forward Checking acts as an **early warning system** by detecting impossible assignments before all variables are assigned.


# Limitation of Forward Checking

The lecture points out an important weakness.

Forward Checking only propagates information from:

> Assigned Variable → Neighboring Unassigned Variables

It does **not** reason about relationships between unassigned variables themselves.

This means some failures are still detected too late.

# Example

After assigning

```
Queensland = Green
```

the lecture observes

```
NT = {Blue}

SA = {Blue}
```

However,

Northern Territory and South Australia are neighbors.

They **cannot both be Blue.**

Forward Checking does not notice this conflict.

It continues searching.

> [!warning]
> Forward Checking only looks one step ahead.
>
> It does not propagate implications through the rest of the network.

---

# Constraint Propagation

To detect these hidden conflicts earlier,

the lecture introduces **Constraint Propagation.**

> [!definition]
> Constraint Propagation repeatedly applies constraints throughout the network until no further domain reductions are possible.

Instead of updating only immediate neighbors,

changes continue propagating through the graph.

## Intuition

One assignment may reduce another variable.

That reduction may reduce another variable.

That reduction may affect yet another variable.

The information "propagates" through the graph.

---

# Arc Consistency

The lecture introduces **Arc Consistency** as a simple form of constraint propagation.

> [!definition]
> A variable is **arc consistent** with respect to another variable if every value in the first variable's domain has at least one compatible value remaining in the second variable's domain.

If every edge in the graph satisfies this condition,

the entire CSP is arc consistent.

---

# Intuition

Suppose

```
A = {Red}

B = {Red}
```

Constraint:

```
A ≠ B
```

There is no possible value in B that satisfies the constraint.

Therefore,

the arc is inconsistent.

---

# Arc Consistency Procedure

The lecture explains the process.

Whenever a domain changes:

1. Examine neighboring variables.
2. Remove incompatible values.
3. If their domains change,
4. Continue propagating the updates.
5. Stop when:
   - no more domains change, or
   - a domain becomes empty.

## Propagation Flow

```text
Assignment

↓

Domain Reduction

↓

Neighbor Updated

↓

Neighbor Domain Reduced

↓

Repeat

↓

No Changes
      OR
Empty Domain
```

---

# Australia Example

The lecture revisits the Australia map.

Suppose

```
Queensland = Green
```

Immediately,

Green is removed from South Australia.

```
SA = {Blue}
```

Constraint propagation now examines South Australia's neighbors.

One neighbor is

```
New South Wales
```

Since South Australia has only Blue available,

New South Wales cannot also be Blue.

Blue is removed.

```
NSW = {Orange}
```

Now New South Wales has changed.

Its neighbors must also be checked.

Victoria is adjacent to New South Wales.

Orange is removed from Victoria.

```
Victoria = {Blue}
```

The propagation continues.

Eventually,

Northern Territory and South Australia both become

```
{Blue}
```

But these two variables are adjacent.

This violates the binary constraint.

Therefore,

the algorithm immediately reports failure.

> [!success]
> Arc Consistency detects the inconsistency **before** the search assigns additional variables.

---

# Why Arc Consistency Is Better

Forward Checking

```
Assigned Variable

↓

Immediate Neighbors
```

Arc Consistency

```
Assigned Variable

↓

Neighbor

↓

Neighbor's Neighbor

↓

Entire Network
```

It reasons much farther through the constraint graph.

---

# Forward Checking vs Arc Consistency

| Forward Checking | Arc Consistency |
|------------------|-----------------|
| Updates only neighbors of assigned variables | Propagates reductions through the entire graph |
| Detects some failures early | Detects many more failures |
| Simpler | More computational work |
| Less pruning | Stronger pruning |

---

# Constraint Propagation Quiz

The lecture presents another partially colored map.

Students are asked to:

- propagate all constraints,
- determine the remaining legal colors for each region,
- decide whether the network is arc consistent.

## Quiz Solution

The lecture notes:

Some regions are isolated islands.

These islands remain unconstrained and therefore retain all three colors.

Another region,

```
K2
```

is restricted to only

```
Green
```

because of its neighboring assignments.

Finally,

the network is declared **arc consistent** because every variable still has at least one legal value.

No domain is empty.

---

# Key Takeaways

> [!summary]
> **Forward Checking**
>
> - Updates neighboring domains.
> - Detects empty domains early.
> - Acts as an early warning system.

---

> [!summary]
> **Constraint Propagation**
>
> - Repeatedly applies constraints.
> - Information spreads through the network.
> - Detects hidden inconsistencies.

---

> [!summary]
> **Arc Consistency**
>
> - Every value must have supporting values in neighboring domains.
> - If every edge satisfies this property, the network is arc consistent.

---

# Exam Points

> [!tip]
> Forward Checking updates only the domains of **neighboring unassigned variables**.

> [!tip]
> If any variable's domain becomes **empty**, immediately backtrack.

> [!tip]
> Constraint Propagation continues updating domains until no further reductions are possible.

> [!tip]
> Arc Consistency is stronger than Forward Checking because it propagates information through the entire constraint graph.

> [!tip]
> Arc Consistency can detect failures that Forward Checking misses.

> [!tip]
> Forward Checking = **one-step look-ahead**.
>
> Arc Consistency = **repeated propagation**.

---

