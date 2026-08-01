
## Overview

Up to this point in the course, we have studied several major topics in Artificial Intelligence.

These topics include:

- **Search and Planning**
    
- **Probability**
    
- **Machine Learning**
    

Although all three are fundamental areas of AI, they have been studied **independently**.

For example,

When we studied search algorithms such as **Breadth-First Search**, **Depth-First Search**, **Uniform Cost Search**, and **A***, we assumed the environment was completely predictable.

Later, when we studied probability and Bayes' theorem, we focused on reasoning under uncertainty, but we did **not** discuss how an intelligent agent should actually make decisions in uncertain environments.

In this module, these two worlds finally come together.

We will learn how an agent can:

- reason about uncertainty,
    
- evaluate possible future outcomes,
    
- and still make intelligent decisions.
    

This area of AI is known as **Planning Under Uncertainty**.

---

# Why Do We Need Planning Under Uncertainty?

Imagine you are giving directions to a robot.

You tell the robot:

> Move one step forward.

In the planning algorithms we have studied so far, this command is assumed to work perfectly.

```
Move Forward

↓

Robot moves exactly one square forward.
```

Every action has a **single predictable outcome**.

This assumption makes planning relatively straightforward because the agent always knows what the next state will be after performing an action.

## The Real World Is Not Deterministic

Unfortunately, the real world rarely behaves this way.

Suppose the same robot is navigating through a busy hospital.

It again receives the command:

> Move forward.

Many different things could happen.

- Its wheels may slip on the floor.
    
- A person may suddenly walk in front of it.
    
- Another robot may block the hallway.
    
- The floor may be uneven.
    
- Its sensors may produce noisy measurements.
    

Even though the robot executed exactly the same command, it may not end up where it expected.

```
Command:

Move Forward

Possible Outcomes:

80% → Move forward

10% → Drift left

10% → Drift right
```

The action is no longer perfectly predictable.

Instead, every action has **multiple possible outcomes**, each occurring with some probability.

This uncertainty is present in almost every real-world AI application.

---

# Real-World Examples of Uncertainty

Uncertainty appears in many AI systems.

|AI Application|Source of Uncertainty|
|---|---|
|Self-driving cars|Other drivers, weather, pedestrians|
|Medical diagnosis|Imperfect medical tests|
|Financial trading|Random market behavior|
|Robots|Slipping wheels, noisy sensors|
|Voice assistants|Speech recognition errors|
|Game-playing agents|Opponent behavior|

Notice that uncertainty does **not** mean the agent is making mistakes.

Instead, it means the **environment itself is unpredictable.**

---

# Classical Planning Assumes a Perfect World

All of the planning algorithms studied so far make one important assumption.

> The world behaves exactly as expected.

For example,

Suppose a robot wishes to move north.

Classical planning assumes:

```
Move North

↓

Always move north
```

If the robot executes this action one hundred times,

it will move north one hundred times.

Because every action is predictable, planning algorithms only need to find a sequence of actions that reaches the goal.

Examples include:

- Breadth-First Search
    
- Depth-First Search
    
- Uniform Cost Search
    
- A*
    
- Dynamic Programming on deterministic graphs
    

These algorithms are extremely powerful **when the environment is deterministic.**

However, they begin to fail once uncertainty is introduced.

---

# What Happens When Actions Become Uncertain?

Suppose a robot wants to reach the charging station.

A classical planner might produce the following plan.

```
North

North

East

East

East
```

This plan assumes every action succeeds perfectly.

Now suppose the very first action fails.

Instead of moving north,

the robot accidentally moves west.

```
Expected

□ □ □
□ R □
□ □ □

↓

Move North

↓

□ R □
□ □ □
□ □ □


Actual

↓

Move North

↓

R □ □
□ □ □
□ □ □
```

The entire plan is now incorrect.

The robot is no longer in the location that the planner expected.

The remaining actions may even move it farther away from the goal.

Classical planning provides **no guidance** for what to do next.

---

# The Goal of Planning Under Uncertainty

Instead of asking

> "What sequence of actions reaches the goal?"

we now ask a much more realistic question.

> **"What should the agent do if the world does not behave exactly as expected?"**

The agent must be prepared for **every possible outcome**, not just the most likely one.

This is the central idea behind planning under uncertainty.

Rather than finding a single path,

the agent learns how to behave **in every possible situation** it might encounter.

---

# Planning + Probability

Planning under uncertainty combines two ideas we have already studied separately.

### Planning

Planning answers the question:

> Which action should I take?

---

### Probability

Probability answers the question:

> How likely is each possible outcome?

---

Planning under uncertainty combines both.

The agent must choose actions **while simultaneously reasoning about uncertain outcomes.**

This is one of the biggest ideas in Artificial Intelligence because it allows agents to operate successfully in the real world instead of only in perfectly predictable environments.

---

# Where This Fits Within AI

Earlier in the course, we separated different types of environments.

These categories become important again.

|Environment|Appropriate AI Technique|
|---|---|
|Fully Observable + Deterministic|Classical Planning (A*, BFS, DFS)|
|Fully Observable + Stochastic|**Markov Decision Processes (MDPs)**|
|Partially Observable + Stochastic|**Partially Observable Markov Decision Processes (POMDPs)**|
|Planning + Uncertainty + Learning|**Reinforcement Learning**|

Notice how each new framework adds another layer of complexity.

- Classical planning assumes perfect actions.
    
- MDPs introduce uncertainty.
    
- POMDPs introduce hidden information.
    
- Reinforcement Learning removes the assumption that the agent already knows the environment.
    

---

# Key Idea

> **Classical planning assumes the world is predictable. Planning under uncertainty assumes the world is unpredictable and teaches an agent how to make the best possible decisions despite that uncertainty.**


## Intuition

Think of planning under uncertainty like planning a road trip.

A GPS that assumes there will never be traffic is similar to **classical planning**.

A GPS that considers traffic jams, road closures, accidents, and weather—and continuously adjusts your route—is much closer to **planning under uncertainty**.

Instead of creating **one perfect route**, it continuously reasons about what might happen and chooses the action that is expected to produce the best overall outcome.

---

# Markov Decision Processes (MDPs)

## From Classical Planning to MDPs

Earlier, we saw that classical planning assumes every action always succeeds exactly as expected.

For example,

```
Move North

↓

Always move north
```

However, in real-world environments, actions are uncertain.

```
Move North

↓

80% → Move North

10% → Move West

10% → Move East
```

Because of this uncertainty, simply finding a sequence of actions is no longer sufficient.

We need a mathematical framework that allows an intelligent agent to:

- represent uncertain outcomes,
    
- evaluate future possibilities,
    
- and choose actions that maximize long-term success.
    

This framework is called a **Markov Decision Process (MDP).**

---

# What is a Markov Decision Process?

A **Markov Decision Process (MDP)** is a mathematical model for making decisions in environments where:

- the current situation is fully observable,
    
- actions have uncertain outcomes,
    
- and the agent wants to maximize some notion of long-term reward.
    

An MDP answers the following question:

> **"Given that my actions may not always work as expected, what should I do?"**

Rather than assuming a perfect world, an MDP explicitly models uncertainty.

---

# Why is it called "Markov"?

The word **Markov** comes from the **Markov Property**.

The Markov Property states:

> **The future depends only on the current state, not on the sequence of events that led to that state.**

In other words,

once we know where we are **right now**, our past history becomes irrelevant.

## Example

Imagine a robot standing in a hallway.

```
Start

↓

Room A

↓

Room B

↓

Current Position
```

Another robot arrives at exactly the same current position but followed a completely different path.

```
Garage

↓

Storage

↓

Kitchen

↓

Current Position
```

Although the robots arrived differently,

once both occupy the same state,

their future decisions should be identical.

The planner only cares about:

- the current location,
    
- not how the robot got there.
    

This is the **Markov Property**.

---

# The Four Components of an MDP

Every Markov Decision Process is defined using four fundamental components.

|Component|Purpose|
|---|---|
|States|Describe the possible situations the agent can be in|
|Actions|Choices available to the agent|
|Transition Model|Describes how actions change the state|
|Reward Function|Measures how desirable each state is|

Together, these completely define an MDP.

---

# 1. States

A **state** represents the current situation of the agent.

Examples include:

|Problem|Possible State|
|---|---|
|Robot navigation|Robot's current location|
|Chess|Current board configuration|
|Self-driving car|Position, speed, nearby vehicles|
|Medical diagnosis|Current patient condition|

States are usually denoted by $S$ or $s$. A collection of all possible states is called the **state space**.

## Example State Space

Suppose a robot can occupy only three locations.

```
S₁

S₂

S₃
```

These three locations form the complete state space.

At any moment,

the robot is in exactly one of these states.

---

# 2. Actions

An **action** is something the agent can choose to do.

For a robot navigating a grid,

possible actions might be

- North
    
- South
    
- East
    
- West
    

Actions are commonly represented as

$$  
A  
$$

or

$$  
a  
$$

Unlike states,

actions are chosen by the agent.

---

# 3. Transition Model

The transition model describes what happens **after** an action is taken.

In deterministic planning,

this was very simple.

```
State A

↓

Move East

↓

State B
```

The outcome was guaranteed.

## Transition Model in an MDP

In an MDP,

the outcome is uncertain.

Suppose the robot attempts to move east.

Instead of one guaranteed outcome,

there may be several possible next states.

```
Current State

↓

Move East

↓

80% → State B

10% → State A

10% → State C
```

The transition model stores these probabilities.

---

# Transition Probability

The probability of reaching a new state is written as

$$  
P(s' \mid s,a)  
$$

This notation means:

> **The probability of arriving in state** (s') **after taking action** (a) **while currently in state** (s).

Let's interpret each symbol.

|Symbol|Meaning|
|---|---|
|(s)|Current state|
|(a)|Action taken|
|(s')|Next state after the action|


## Example

Suppose the robot is currently in state

$$  
S_1  
$$

and executes the action

```
Move East
```

There might be

- 80% chance of reaching (S_2)
    
- 20% chance of remaining in (S_1)
    

This would be written as

$$  
P(S_2 \mid S_1,\text{East})=0.8  
$$

and

$$  
P(S_1 \mid S_1,\text{East})=0.2  
$$

These probabilities define the uncertainty of the environment.

---

# Why Is This Different from Bayes' Theorem?

The notation

$$  
P(s' \mid s,a)  
$$

may look similar to conditional probability from Bayes' theorem.

However,

it serves a different purpose.

In Bayes' theorem,

conditional probability answers questions like

> What is the probability of cancer given a positive test?

In an MDP,

the transition probability answers

> After performing an action, what is the probability of ending up in each possible next state?

Instead of reasoning about hidden variables,

we are reasoning about **state transitions**.

---

# 4. Reward Function

Knowing how the world changes is not enough.

The agent also needs to know

> **Which states are desirable?**

This is represented using the **reward function**.

Instead of assigning probabilities,

we assign numerical values indicating how good each state is.

The reward function is usually written as

$$  
R(s)  
$$

meaning

> **The reward received for being in state** (s).

---

## Example

Suppose the robot has three possible states.

```
S₁

Reward = 0

S₂

Reward = 10

S₃

Reward = 100
```

Clearly,

the robot would prefer reaching (S_3).

The reward function tells the planner exactly that.

---

# Rewards Guide Decision Making

The reward function represents the **objective** of the planning problem.

For example,

|State|Reward|
|---|---|
|Empty hallway|0|
|Goal location|+100|
|Dangerous area|-100|

The planner's objective is **not simply to move.**

Its objective is to choose actions that maximize the **total reward** it expects to receive.

This is the central goal of an MDP.

---

# Putting Everything Together

An MDP combines all four components into one mathematical framework.

```
Current State

↓

Choose Action

↓

Transition Model

↓

Possible Next States

↓

Receive Reward

↓

Repeat
```

Unlike classical planning,

the agent does not assume a single predictable outcome.

Instead,

it considers:

- every possible next state,
    
- how likely each one is,
    
- and how rewarding each outcome will be.
    

---

# Summary

A Markov Decision Process is completely defined by four components.

|Component|Question it Answers|
|---|---|
|States|Where am I?|
|Actions|What can I do?|
|Transition Model|Where might I end up after acting?|
|Reward Function|How good is each state?|

Together, these components allow an intelligent agent to plan effectively in uncertain environments.

## Key Idea

> **A classical planner assumes actions always succeed. An MDP assumes every action may have several possible outcomes and chooses actions that maximize the expected long-term reward despite this uncertainty.**

---

# Grid World: The Simplest MDP

## Why Use Grid Worlds?

Real-world planning problems can be extremely complicated.

For example:

- self-driving cars navigate busy roads,
    
- robots move through crowded museums,
    
- drones fly in unpredictable weather.
    

Studying these problems directly would make it difficult to understand the underlying algorithms.

Instead, AI researchers often simplify the environment into a **Grid World**.

A Grid World is essentially a small board made of square cells.

Although simple, it captures all the important ideas behind planning under uncertainty.

> Most introductory reinforcement learning and MDP algorithms are first demonstrated using Grid Worlds before being applied to real robots.

---

# A Simple Grid World

Consider the following environment.

```text
+---------+---------+---------+---------+
|                 |                  |                       +100    |
|                 |                  |                 |     Goal    |
+---------+---------+---------+---------+
|                 |                  |                 |                 |
|      Start   |                  |                 |                 |
+---------+---------+---------+---------+
|                 |                  |                 |      -100    |
|                 |                  |                 |   Danger  |
+---------+---------+---------+---------+
```

The agent begins in the **Start** state.

There are two special states.

- **Goal State** → Reward = +100
    
- **Danger State** → Reward = −100
    

These are called **absorbing states**.

---

# What is an Absorbing State?

An **absorbing state** is a terminal state.

Once the agent reaches it,

the process immediately ends.

There are no further actions.

```text
Start

↓

Move

↓

Goal (+100)

↓

End
```

Likewise,

```text
Start

↓

Move

↓

Danger (-100)

↓

End
```

After reaching either absorbing state,

the game is over.

---

# The Agent's Objective

The goal of the agent is simple.

> Reach the +100 state while avoiding the −100 state.

If the environment were deterministic,

finding the solution would be easy.

Simply compute the shortest path.

For example,

```text
Start

↑

↑

→

→

→

Goal
```

Unfortunately,

the environment is **not deterministic**.

---

# Introducing Uncertainty

Suppose the agent chooses the action

```text
Move North
```

In deterministic planning,

the result is guaranteed.

```text
Current Cell

↓

Move North

↓

North Cell
```

Every single time.

## In an MDP

The same action may produce several different outcomes.

Instead of moving north with certainty,

the movement succeeds only **80%** of the time.

The remaining probability is divided among neighboring cells.

```text
Attempt North

80% → North

10% → West

10% → East
```

Notice something important.

The agent never intended to move west or east.

Those movements happen because the environment is stochastic.

---

# Transition Probabilities

The Grid World used throughout the lecture follows the same transition model for every movement.

When attempting any action,

|Intended Outcome|Probability|
|---|--:|
|Intended direction|80%|
|Left of intended direction|10%|
|Right of intended direction|10%|

This transition model represents imperfect control.

A robot's wheels may slip.

A self-driving car may skid.

A drone may be pushed by wind.

The action requested by the agent is **not always** the action executed by the environment.

---

# Example: Moving North

Suppose the robot is located here.

```text
      N

W   Robot   E

      S
```

The robot chooses

```text
Move North
```

The possible outcomes are

```text
80%

      X

W   Robot   E

      S
```

or

```text
10%

      N

X   Robot   E

      S
```

or

```text
10%

      N

W   Robot   X

      S
```

Even though the robot selected only **one** action,

nature decides which outcome actually occurs.

---

# What Happens at Walls?

Suppose the robot attempts to move into a wall.

```text
##########

Robot

↓

Move North
```

Since there is no valid square above,

the robot cannot move.

Instead,

it **bounces back** into the same cell.

The intended 80% probability is assigned to remaining where it is.

```text
80%

Stay Here
```

The remaining probabilities still apply.

For example,

```text
Stay

80%

Left

10%

Right

10%
```

This prevents impossible movements outside the grid.

---

# Example

Suppose the robot is standing in the upper-left corner.

```text
########

Robot
```

It attempts to move north.

Since north is blocked,

the outcomes become

|Outcome|Probability|
|---|--:|
|Stay in current cell|80%|
|Move left|Impossible (wall)|
|Move right|10%|

If both north and left are walls,

their probabilities combine,

meaning the robot may remain in place with even higher probability.

This explains why corner cells often have a large probability of staying put.

---

# Why Does This Matter?

Imagine planning a route like this.

```text
North

North

East

East

East
```

This sequence assumes every movement succeeds perfectly.

But what if the very first action fails?

Instead of

```text
Start

↓

North
```

the robot accidentally moves sideways.

```text
Start

↓

West
```

Now the original plan is no longer valid.

Every remaining action was designed assuming the robot occupied a different position.

The planner has no instructions for recovering.

---

# Classical Planning Breaks Down

Traditional planning computes

```text
Action 1

↓

Action 2

↓

Action 3

↓

Goal
```

This works only if every action succeeds exactly as predicted.

Under uncertainty,

the robot might end up somewhere unexpected after any action.

The planner therefore loses track of what to do next.

---

# The Need for Something Better

Instead of planning a **single sequence of actions**,

we need something much more flexible.

We need instructions that answer the question

> **"If I end up here, what should I do?"**

for **every possible state**.

Rather than planning one path,

we want a complete decision strategy.

This strategy is called a **policy**, which becomes the central idea of MDPs.

---

# Summary

The Grid World demonstrates why uncertainty fundamentally changes planning.

Unlike deterministic environments,

each action may have several possible outcomes.

|Deterministic Planning|MDP Planning|
|---|---|
|One action → one outcome|One action → many possible outcomes|
|Fixed action sequence|Adaptive decision strategy|
|Predictable environment|Stochastic environment|

Because the robot can end up in unexpected states,

planning must consider **every possible future state**, not just the intended one.

## Key Insight

> **In a stochastic environment, planning is no longer about finding one perfect path. It is about deciding the best action for every possible situation the agent might encounter.**

---

# Why Conventional Planning Fails Under Uncertainty

## Review

Until now, all of the planning algorithms we've studied assumed that:

- every action succeeds exactly as expected,
    
- the environment behaves predictably,
    
- executing the same action twice always produces the same result.
    

Examples include:

- Depth-First Search (DFS)
    
- Breadth-First Search (BFS)
    
- Uniform Cost Search (UCS)
    
- A*
    
- Dynamic Programming
    

These algorithms work extremely well in **deterministic environments**.

## What Changes in an MDP?

In a Markov Decision Process, **actions are stochastic**.

That means:

> Choosing an action does **not** guarantee a single outcome.

Instead,

each action produces **a probability distribution over possible next states**.

For example,

suppose the robot is currently at state **C1**.

It chooses

```
Go North
```

Instead of always arriving at B1,

the robot might end up in several different locations.

```
          80%

C1 ─────────────► B1

          10%

C1 ─────────────► C1

          10%

C1 ─────────────► C2
```

The robot chooses the action,

but **Nature chooses the outcome.**

This single difference completely changes how planning works.

---

# Conventional Planning Builds a Search Tree

Previously,

a search tree looked like this.

```
Start

 │

 ▼

Action

 │

 ▼

One next state
```

Every action produced **exactly one child node**.

Example:

```
      C1

     / | | \

    N S E W

```

Each branch represented one action.

## In an MDP, Every Action Splits Into Multiple Outcomes

Now every action has several possible results.

Instead of

```
Action

↓

One state
```

we now have

```
Action

      ↓

Nature chooses

 ┌────┼────┐

▼        ▼         ▼

State State State
```

For example,

choosing North from C1 becomes

```
             Choose North

                  │

        ┌─────────┼─────────┐

         ▼                ▼                    ▼

        B1               C1                  C2

        80%           10%                10%
```

The robot cannot decide which branch happens.

Only the probabilities are known.

---

# The Branching Factor Explodes

In deterministic planning,

suppose every state has

```
4 actions
```

The branching factor is

```
b = 4
```

Every level of the search tree grows by a factor of four.

## Under Uncertainty

Now each action has multiple possible outcomes.

Suppose

- North has 3 possible outcomes
    
- South has 3 possible outcomes
    
- East has 3 possible outcomes
    
- West has 3 possible outcomes
    

Instead of

```
4 children
```

we now have

```
4 actions

×

3 possible outcomes

=

12 branches
```

The search tree becomes

```
                  C1

          N        S        E        W

         / | \    / | \    / | \    / | \

         •  •  •  •  •  •  •  •  •  •  •  •
```

Instead of expanding

```
4
```

nodes,

we may now need to consider

```
12
```

possible futures.

---

# Problem 1 — The Search Tree Grows Too Fast

The first problem is therefore:

> Every action creates **multiple possible future states**, causing the search tree to grow much faster.

The search complexity becomes enormous.

Even a few planning steps ahead can produce thousands or millions of possible futures.

---

# Problem 2 — The Tree Can Become Infinite

The second problem is even more serious.

Because actions are stochastic,

the robot may never reach the goal immediately.

Instead,

it may accidentally return to previous states.

For example,

```
C1

↓

C2

↓

C3

↓

C2

↓

C1

↓

C2

↓

...
```

The robot can keep looping forever.

Unlike deterministic planning,

there is **no guarantee** that every sequence eventually reaches the goal.

---

## Why This Is a Problem

Conventional planning searches until it finds a goal.

But if loops are possible,

the search tree may never end.

```
Goal?

↓

No

↓

Keep searching...

↓

Still no goal...

↓

More loops...

↓

Tree keeps growing forever
```

The planner may spend enormous effort exploring repeated possibilities.

---

# Problem 3 — The Same State Appears Repeatedly

Consider this example.

```
        Start

       /     \

      A       B

       \     /

        ▼   ▼

         C
```

There are two different ways to reach state **C**.

In a deterministic planner,

this already happens occasionally.

---

## Under Stochastic Actions

It happens constantly.

The same state may be reached through dozens or hundreds of different action sequences.

For example,

```
Start

 │

 ▼

C1

 │

 ▼

C2

 │

 ▼

C1

 │

 ▼

C2

 │

 ▼

C1
```

Notice that

```
C1
```

appears repeatedly.

However,

the planner treats each occurrence as a completely different node in the search tree.

This wastes a tremendous amount of computation.

---

# Why This Is Wasteful

Suppose we already know

> "The best action from C1 is Go North."

If we encounter C1 again,

there is no reason to recompute the best action.

The answer should still be

```
Go North
```

Conventional search does **not** remember this.

It keeps solving the same state repeatedly.

---

# Summary of the Three Problems

|Problem|Why It Happens|
|---|---|
|**1. Huge branching factor**|Every action has multiple possible outcomes instead of one.|
|**2. Infinite search depth**|Randomness can cause the agent to loop forever before reaching a goal.|
|**3. Repeated states**|The same state can be reached through many different action sequences, causing redundant computation.|

---

# Why Policies Solve These Problems

Instead of searching for

> **one sequence of actions**

MDPs search for

> **the best action for every possible state.**

This collection of state-to-action mappings is called a **policy**.

Rather than asking:

> "What should I do next?"

the planner asks:

> "If I ever find myself in this state, what is the best action to take?"

This is a much more robust strategy because it prepares the agent for **every possible situation**, including unexpected outcomes caused by randomness.

## Key Takeaways

- Stochastic actions make planning fundamentally different from deterministic search.
    
- Every action can lead to multiple possible future states.
    
- Conventional search trees become inefficient because they:
    
    - grow too quickly,
        
    - may become infinitely deep,
        
    - repeatedly solve the same states.
        
- MDPs overcome these problems by computing a **policy** instead of a single action sequence.
    
- A policy tells the agent **what to do in every state**, allowing it to recover from unexpected outcomes and continue toward its goal.
---
# Rewards, Costs, and the Objective of an MDP

## Why the Previous Policy Feels Strange

In the previous section, we assumed:

- Reaching the **+100** absorbing state gives a reward of **+100**.
- Reaching the **−100** absorbing state gives a reward of **−100**.
- **Every other move is free** (reward = 0).

Because moving had **no cost**, the optimal policy sometimes behaved in surprising ways.

For example, instead of moving directly toward the goal, the agent might intentionally take a longer route or even keep trying to move into a wall if doing so slightly reduced the chance of accidentally entering the **−100** state.

Although this policy is mathematically optimal, it does **not** resemble intelligent real-world behavior.

## Why Does This Happen?

The reason is simple:

> **Time has no value.**

If moving is free, then taking:

- 5 steps,
- 50 steps,
- or even 500 steps

costs exactly the same.

The only thing that matters is eventually reaching the **+100** state.

The agent therefore has no incentive to reach the goal quickly.

---

# Real Life Is Different

Almost every real planning problem has some cost associated with actions.

Examples include:

| Problem | Cost |
|----------|------|
| Robot navigation | Battery consumption |
| Self-driving car | Fuel or energy |
| Delivery drone | Flight time |
| Video game AI | Turns spent |
| Medical treatment planning | Time, money, risk |

Every extra action consumes some limited resource.

Therefore, intelligent agents should prefer plans that are:

- **safe**, and
- **efficient**.

---

# Introducing Step Costs

Instead of rewarding only the terminal states, we now assign a reward (or cost) to **every state**.

For example:

| State | Reward |
|--------|--------|
| Goal | +100 |
| Bad terminal state | −100 |
| Every ordinary state | −3 |

The value **−3** means:

> Every time the agent enters a normal state, it loses 3 reward points.

This is called the **step cost** (also known as the **living cost**).

---

# Why Step Costs Matter

Suppose two different paths both reach the goal.

### Path A

```
Goal reached in 4 steps

Reward

100 − (4 × 3)

= 88
```

### Path B

```
Goal reached in 10 steps

Reward

100 − (10 × 3)

= 70
```

Although both paths eventually reach the goal, **Path A** receives a higher total reward because it wastes fewer steps.

Thus, step costs naturally encourage shorter and more efficient plans.

---

# The Objective of an MDP

The agent is no longer trying to maximize only the final reward.

Instead, it wants to maximize **the total reward collected over its entire lifetime**.

Conceptually,

```
Total Reward

=

R₀ + R₁ + R₂ + R₃ + ...
```

where

- **R₀** is the reward received immediately,
- **R₁** is the reward after one step,
- **R₂** after two steps,
- and so on.

---

# Why Do We Use an Expectation?

The environment is **stochastic**.

Even if the agent chooses exactly the same action,

the environment may produce different outcomes.

For example:

```
Move North

80% → North

10% → Left

10% → Right
```

Since future states are uncertain, the total reward is also uncertain.

Therefore, we maximize the **expected** total reward.

Conceptually,

```
Expected Total Reward

=

Average reward over all possible future outcomes
```

---

# Mathematical Objective

The lecture defines the objective as

\[
E\left[\sum_{t=0}^{\infty} R_t\right]
\]

where

- \(R_t\) is the reward received at time \(t\),
- \(E[\cdot]\) denotes the expected value.

This simply means:

> Choose actions that maximize the average total reward over every possible future that could occur.

---

# Discounting Future Rewards

Many MDPs introduce another important idea:

the **discount factor**.

Instead of valuing rewards equally regardless of when they occur,

future rewards become slightly less valuable.

The objective becomes

$$
E\left[\sum_{t=0}^{\infty}\gamma^tR_t\right]
$$

where

$$
0 < \gamma < 1
$$

and **γ (gamma)** is called the **discount factor**.

---

# Why Discount Future Rewards?

Imagine someone offers you:

- ₹100 today
- ₹100 one year from now

Most people prefer receiving the money today.

Future rewards are usually worth slightly less because of:

- uncertainty,
- inflation,
- opportunity cost,
- delayed usefulness.

Discounting models this intuition mathematically.

---

# Example

Suppose

```
γ = 0.9
```

Then the value of a reward decreases over time.

| Time | Effective Reward |
|------|-----------------:|
| Today | 100 |
| After 1 step | 90 |
| After 2 steps | 81 |
| After 3 steps | 72.9 |

The farther into the future a reward occurs, the less valuable it becomes.

---

# Step Cost vs Discount Factor

Interestingly, **step costs** and **discount factors** encourage similar behavior.

## Step Cost

```
Lose reward every time you move.
```

Longer paths accumulate larger penalties.

## Discount Factor

```
Future rewards become smaller.
```

The longer it takes to reach a reward, the less valuable that reward becomes.

Many practical MDPs use **both** mechanisms together.

---

# Why Introduce γ?

Besides modeling realistic preferences, the discount factor has an important mathematical advantage.

Because

$$
0 < \gamma < 1
$$

the infinite reward sum always remains **finite**.

This guarantees that algorithms such as **Value Iteration** eventually converge to a stable solution.

Without discounting, the total reward could become infinite in some problems.

---

# Intuition

Think of the objective as answering the question:

> **"If I start in this state and continue following my policy, how much total reward should I expect to earn over time?"**

The answer depends on:

- immediate rewards,
- future rewards,
- uncertainty in the environment,
- and how much we value the future.

This idea leads directly to the **Value Function**, which is the central concept in the next section.

---

# Key Takeaways

- In the previous MDP examples, moving had **no cost**, which sometimes produced unintuitive policies.
- Step costs assign a small penalty to every move, encouraging shorter paths.
- An MDP seeks to maximize the **expected cumulative reward**, not just the final reward.
- Because outcomes are uncertain, the objective uses an **expected value**.
- A **discount factor (γ)** makes future rewards less valuable than immediate rewards.
- Discounting also guarantees that Value Iteration converges to a finite solution.
- The next concept—the **Value Function**—uses this objective to evaluate how good each state is.
---
# The Value Function

## From Rewards to Values

In the previous section, we defined the objective of an MDP:

> **Maximize the expected cumulative future reward.**

The next question is:

> **How do we know whether one state is "better" than another?**

Simply looking at the immediate reward is not enough.

For example, consider two states.

```
State A
```

```
Immediate Reward = -3
```

```
State B
```

```
Immediate Reward = -3
```

Both states have exactly the same immediate reward.

However:

- one state may be only **one step away from +100**, while
- the other may be close to **−100**.

Clearly these two states should not be considered equally good.

This motivates the idea of assigning every state a **value**.

---

# What is a Value?

A **value** tells us

> **How good it is to start from a particular state if we continue following a given policy.**

Notice that this is **not** the reward of the current state.

Instead, it includes:

- the immediate reward,
- the future rewards,
- all future uncertainty,
- and the actions chosen by the policy.

---

# Definition of the Value Function

For every state \(s\), the value function is written as

$$
V^\pi(s)
$$

which is read as

> **"The value of state \(s\) under policy \(\pi\)."**

The lecture defines it as

$$
V^\pi(s)
=
E\left[
\sum_{t=0}^{\infty}
\gamma^tR_t
\;\middle|\;
S_0=s
\right]
$$

Although this expression looks intimidating, it has a very intuitive meaning.

It simply says:

> Start in state **s**, follow policy **π**, and compute the **expected total discounted reward** you will receive.

---

# Breaking Down the Equation

Let's examine each part.

$$S_0 = s$$

This means

> The agent starts in state **s**.

---

$$R_t$$

This is

> the reward received at time **t**.

---

$$gamma^t$$

This discounts future rewards.

Rewards received later contribute less than immediate rewards.

---

$$E[\cdot]$$

Because the environment is stochastic,

many different futures are possible.

Therefore we compute the **expected value**, or average over all possible futures.

---

# A Simple Interpretation

Suppose we have this grid world.

```
S ----> ----> +100
|
|
v

-100
```

Imagine starting in the left-most state.

Sometimes you may

```
Go directly to +100.
```

Sometimes

```
Slip sideways.

Take extra steps.

Eventually reach +100.
```

Sometimes

```
Accidentally fall into −100.
```

Each possible future produces a different total reward.

The value function computes

> **the average reward across all these possible futures.**

---

# Value Depends on the Policy

An important idea is that

> **The value of a state is not fixed.**

It depends entirely on **what policy you follow afterward.**

For example,

suppose from the same state we have two different policies.

### Policy A

```
Always move toward the goal.
```

Expected reward might be

```
85
```

---

### Policy B

```
Wander randomly.
```

Expected reward might be

```
25
```

Same state.

Different behavior.

Different value.

Therefore we always write

$$
V^\pi(s)
$$

instead of simply

$$
V(s)
$$

because the value depends on the chosen policy.

---

# Example from the Grid World

Recall the grid world.

```
+100
```

is the good terminal state.

```
−100
```

is the bad terminal state.

Every normal square has

```
Reward = -3
```

Suppose our policy is

```
Always move toward +100.
```

Then

- states near the goal should have **high values**,
- states far away should have **lower values**,
- states near the −100 region should have **even lower values**.

The value function captures all of this automatically.

---

# Value is an Expectation

Notice something important.

The value is **not** one particular reward.

It is an **average** over many possible executions.

For example,

starting from one state,

one execution might produce

```
100
```

Another execution might produce

```
82
```

Another might produce

```
−25
```

The value function averages all of these according to their probabilities.

---

# Why is the Value Function Useful?

Suppose we know the value of **every state**.

Then decision making becomes much easier.

Imagine each state has a number written inside it.

```
70     85     97     100

55     72     89

40     60     74
```

If the agent always moves toward neighboring states with larger values,

it naturally moves toward better long-term outcomes.

The value function therefore transforms planning into a simple problem:

> **Move toward states with higher values.**

---

# Computing the Value Function

Unfortunately,

we do **not** know the values beforehand.

Instead,

we must calculate them.

The algorithm used in this lecture is called

> **Value Iteration.**

Instead of computing the correct values immediately,

Value Iteration gradually improves its estimates.

Initially,

we know almost nothing.

For example,

```
0     0     0     100

0     0     0

0     0    -100
```

After several updates,

the values slowly spread through the grid.

Eventually,

they converge to the true optimal values.

This iterative improvement is the central idea behind **Value Iteration**.

---

# Sebastian Thrun's Intuition

Sebastian describes the value function as a kind of **potential field**.

Imagine pouring water (or milk) into the goal state.

```
Goal

↓

↓

↓

Water spreads through the environment.
```

Eventually,

every location receives some amount of "potential."

An agent simply follows the direction where this potential increases,

naturally reaching the goal.

This physical intuition helps explain why Value Iteration works so well.

---

# Key Takeaways

- A **reward** measures the immediate payoff of entering a state.
- A **value** measures the **expected total future reward** starting from that state.
- The value depends on the **policy** being followed.
- Values include:
  - immediate rewards,
  - future rewards,
  - uncertainty,
  - and discounting.
- States closer to desirable outcomes usually receive higher values.
- We do not know the values initially.
- **Value Iteration** is the algorithm used to compute them.
---
# Value Iteration: Intuition and the Bellman Backup

## Why Do We Need Value Iteration?

In the previous section, we defined the **value function**.

The value of a state tells us:

> **How good is it to start in this state and continue acting optimally?**

However, there is one major problem.

> **We do not know these values.**

The entire purpose of **Value Iteration** is to compute them.

Instead of trying to solve the whole problem at once, Value Iteration gradually improves its estimate of every state's value until the estimates stop changing.

---

# Sebastian Thrun's Intuition

Sebastian Thrun explains Value Iteration using a beautiful physical analogy.

Imagine that the goal state contains a bucket of milk.

```
        +100
         🥛
```

Now imagine pouring the milk onto the grid.

Instead of staying in one square,

the milk slowly spreads outward.

```
Iteration 1

          +100

Iteration 2

      80     100

Iteration 3

   60   80   100

Iteration 4

40   60   80   100
```

Eventually,

every reachable square receives some amount of "milk."

The amount in each square represents **how valuable that state is**.

---

# Another Way to Think About It

Instead of milk,

imagine the goal creates a **gravitational field**.

```
Goal

↓↓↓↓↓↓↓↓

Every nearby state is pulled toward it.
```

States closer to the goal feel a stronger pull.

States farther away feel a weaker pull.

The value function is essentially this "pull."

An agent simply climbs uphill toward larger values.

---

# Why Values Spread Backwards

Notice something interesting.

The goal already knows its value.

```
Goal

Value = +100
```

The square beside the goal can estimate its value because it knows it can reach +100.

Then the square behind that can estimate its value.

Then the next one.

Information always flows

```
Goal

↓

Neighbor

↓

Neighbor

↓

Neighbor
```

rather than

```
Start

↓

Goal
```

This is why Value Iteration is sometimes described as

> **Propagating values backward from the goal.**

---

# The Recursive Idea

Suppose we are standing here.

```
Current State

      S
```

We want to know

```
Value(S)
```

Instead of solving the entire future,

we ask a much simpler question.

> **Where could I be after taking one action?**

Suppose taking one action could move us to

```
S₁

S₂

S₃
```

If we already know the values of those states,

then estimating the value of the current state becomes much easier.

This idea is called **dynamic programming**.

Rather than solving one huge problem,

we solve many small problems that build upon one another.

---

# The Bellman Principle

Richard Bellman made one key observation.

> **The value of a state depends on the values of its successor states.**

Instead of thinking about an entire journey,

we only need to think about

- one action,
- one transition,
- and then trust the value of the next state.

This recursive relationship is the foundation of Value Iteration.

---

# The Bellman Backup Equation

The update performed during Value Iteration is called the **Bellman Backup**.

The update rule is

$$
V(s)
=
R(s)
+
\gamma
\max_a
\sum_{s'}
P(s'|s,a)V(s')
$$

This equation looks complicated,

but every part has a simple interpretation.

---

# Breaking the Equation Into Pieces

## Step 1 — Immediate Reward

$$
R(s)
$$

Every state has an immediate reward (or cost).

Example:

```
Normal square

Reward = -3
```

Goal state

```
Reward = +100
```

Bad terminal state

```
Reward = -100
```


## Step 2 — Future Value

After taking an action,

we arrive in another state.

Those future states already have value estimates.

Their values help determine the value of the current state.

## Step 3 — Transition Probabilities

The environment is stochastic.

Taking one action may lead to several different outcomes.

For example,

```
Move East

80% → Right

10% → Up

10% → Down
```

Therefore,

we cannot simply use one successor.

We must compute the **expected value**

by averaging over all possible successors.

This is represented by
$$
\sum_{s'}
P(s'|s,a)V(s')
$$

## Step 4 — Discount Factor

Future rewards are multiplied by

$$
\gamma
$$

If

```
γ = 1
```

future rewards are worth exactly as much as immediate rewards.

If

```
γ = 0.9
```

future rewards are slightly less valuable.

## Step 5 — Choose the Best Action

The agent controls its own action.

Therefore,

it chooses whichever action produces the largest expected value.

This is why the equation contains

$$
\max_a
$$

Nature determines **which successor state occurs**,

but the agent determines **which action to take**.

This distinction is one of the most important ideas in MDPs.

---

# Agent vs Nature

There are two different decisions happening.

## The Agent Chooses

```
North

South

East

West
```

The agent selects one action.

## Nature Chooses

Once the action is selected,

the environment decides what actually happens.

Example:

```
Command:

Go East
```

Actual result

```
80% → East

10% → North

10% → South
```

Therefore,

the Bellman equation contains

- **max** over actions (agent's choice),
- **expectation** over successor states (nature's randomness).

---

# One Backup Operation

Suppose our current value table is

```
0     0     100

0     0       0

0     0    -100
```

We now update one state.

For example,

the square beside the goal.

Since it can almost reach +100,

its new estimate becomes much larger.

```
0    77    100

0     0      0

0     0   -100
```

That single update is called a **backup**.

---

# Repeating the Process

Now another state can use the newly updated value.

```
Iteration 1

0   77   100

Iteration 2

58  77   100

Iteration 3

58  77   100

40  58   77
```

Each update spreads information farther away from the goal.

Eventually,

the values stop changing.

When this happens,

Value Iteration has **converged**.

---

# Bellman Equation at Convergence

Initially,

the Bellman equation is only an update rule.

The left side and right side are not equal.

```
Old Value

↓

Updated Value
```

After enough iterations,

the values stop changing.

At this point,

the Bellman update becomes an equality.

This is called the **Bellman Equation**.

It represents the optimal relationship between every state and its successors.

---

# Why Value Iteration Works

Each update improves our estimate.

Better estimates produce even better estimates for neighboring states.

Eventually,

the entire grid becomes consistent.

The final values represent

> **the maximum expected future reward obtainable from every state.**

---

# Key Takeaways

- Value Iteration computes the value of every state.
- Values spread backward from the goal through the state space.
- Each update is called a **Bellman Backup**.
- A state's value depends on:
  - its immediate reward,
  - the values of successor states,
  - transition probabilities,
  - the discount factor.
- The agent chooses the **best action** (max).
- Nature chooses the **actual outcome** (expectation).
- Repeating backups eventually converges to the optimal value function.
---
# Value Iteration Examples (Deterministic vs Stochastic)

After introducing the Bellman Backup equation, Sebastian Thrun demonstrates how it is actually used by working through several examples.

These examples are extremely important because they show **how the Bellman equation is applied numerically**.

---

# Example 1: Deterministic Grid World

To make the calculations easier, Thrun first removes uncertainty.

Instead of actions succeeding **80% of the time**, he assumes they always succeed.

This means

- there is **no randomness**
- every action leads to exactly one next state

For this example, he also assumes:

- **Discount factor:** $\gamma = 1$
- **Cost of each move:** $-3$
- Terminal rewards:
  - Goal = $+100$
  - Bad terminal = $-100$

The initial value table is

```
0      0      +100

0      0        0

0      0      -100
```

Only the terminal states have known values.

Everything else starts at zero.

---

# Quiz 1 — What is the Value of A3?

Consider the square immediately to the left of the goal.

```
A3  →  Goal(+100)
```

Since movement is deterministic,

going East guarantees reaching the goal.

The Bellman update becomes

$$
V(A3)=100-3=97
$$

---

## Why Subtract 3?

Remember,

moving itself has a cost.

Although reaching the goal gives +100,

we must pay the movement cost first.

```
Reward from goal

100

↓

Movement cost

−3

↓

Value

97
```

---

# Result

After one backup,

```
97     100
```

The value of A3 becomes

```
97
```

---

# Quiz 2 — What is the Value of B3?

Now update the square directly below A3.

```
97

↑

B3
```

Again,

movement is deterministic.

The best action is

```
Go North
```

which reaches the state worth 97.

Therefore,

$$
V(B3)=97-3=94
$$

---

# Result

```
97   100

94
```

---

# Quiz 3 — Value After Convergence

Now suppose Value Iteration continues until convergence.

What is the value of C1?

```
Start

↓

Goal
```

Every movement costs

```
−3
```

Therefore,

every extra step simply subtracts another 3.

The shortest path from C1 requires

```
5 steps
```

Hence

$$
100-(5\times3)=85
$$

---

# Final Value Function (Deterministic)

The values form a beautiful gradient.

```
97   100

94    97

91    94

88    91

85    88
```

Every step away from the goal decreases the value by exactly 3.

---

# Important Observation

Because the environment is deterministic,

Value Iteration essentially computes

> **Shortest distance to the goal × movement cost**

The value function behaves almost like a distance map.

---

# Why This Case Is Simple

Every action has only one outcome.

```
Go East

↓

Always reach East
```

There is

- no uncertainty
- no probabilities
- no expected values

This is much simpler than a true MDP.

---

# Example 2: Stochastic Grid World

Now Thrun restores uncertainty.

Actions behave as before.

```
Command East

80% → East

10% → Up

10% → Down
```

Everything else stays the same.

- $\gamma = 1$
- movement cost = $-3$

The initial value table is

```
0      0      100

0      0        0

0      0     -100
```

---

# Quiz 1 — Value of A3

Again,

consider the square beside the goal.

If we command

```
East
```

then

```
80%

→ Goal (+100)

10%

→ Stay

10%

→ Move Down
```

The two non-goal states still have value 0.

Therefore,

Expected future value is

$$
0.8(100)+0.1(0)+0.1(0)=80
$$

Subtract the movement cost.

$$
80-3=77
$$

---

# Result

Instead of

```
97
```

we now obtain

```
77
```

---

# Why Is It Smaller?

In the deterministic world,

reaching the goal was guaranteed.

Now,

there is only an

```
80%

chance
```

of reaching it immediately.

Uncertainty lowers the expected reward.

---

# Quiz 2 — Value of B3

Now consider the state below A3.

This example is much more interesting because **two actions compete**.

---

## Option 1 — Go North

Possible outcomes:

```
80%

Reach A3 (77)

10%

Fall into -100

10%

Stay in place (0)
```

Expected value

$$
0.8(77)+0.1(-100)+0.1(0)
$$

$$
=61.6-10
$$

$$
=51.6
$$

Subtract movement cost

$$
51.6-3=48.6
$$


## Option 2 — Go West

Possible outcomes

```
10%

Reach A3 (77)

80%

Stay

10%

Move elsewhere
```

Expected value

$$
0.1(77)=7.7
$$

Subtract movement cost

$$
7.7-3=4.7
$$

---

# Which Action Should We Choose?

Compare both values.

```
North

48.6

West

4.7
```

Clearly,

$$
48.6>4.7
$$

Therefore,

the Bellman backup chooses

```
North
```

---

# Why Doesn't It Avoid the -100 Yet?

This is an important observation.

At this stage,

almost every state still has value

```
0
```

The algorithm has only begun propagating information.

The positive value

```
77
```

already exists,

making North appear attractive.

The safer western route has not yet accumulated value.

As Value Iteration continues,

those values gradually spread,

and eventually the policy may change.

---

# Key Insight

Early iterations

```
Only nearby states know about the goal.
```

Later iterations

```
The entire grid understands where the safest path lies.
```

This gradual improvement is exactly why Value Iteration is called an **iterative** algorithm.

---

# Comparison: Deterministic vs Stochastic

| Deterministic | Stochastic |
|--------------|------------|
| Actions always succeed | Actions may fail |
| One successor state | Multiple possible successors |
| Simple subtraction | Expected value calculation |
| Value ≈ shortest path | Value balances reward and risk |
| No probabilities | Transition probabilities required |

---

# Key Takeaways

- Deterministic Value Iteration behaves like shortest-path planning.
- Stochastic Value Iteration must compute **expected future rewards**.
- Uncertainty lowers the value of risky states.
- Every Bellman backup compares all actions and chooses the one with the highest expected value.
- Early iterations are only rough estimates.
- As backups continue, values spread through the grid until convergence.

---
# From Value Functions to Policies

So far, we have learned how to compute the **value** of every state.

However, an intelligent agent ultimately needs to answer a different question:

> **"What action should I take?"**

Knowing that a state has a value of 82 or 94 is useful, but a robot cannot execute a value.

It must execute an **action**.

The beautiful idea behind MDPs is that **the optimal action is already hidden inside the Bellman equation.**

---

# Recall the Bellman Backup

The Bellman update computes

$$
V(s)
=
R(s)
+
\gamma
\max_a
\sum_{s'}
P(s'|s,a)V(s')
$$

Notice that the equation contains two different operations.

1. Nature computes the expected outcome

$$
\sum_{s'}
P(s'|s,a)V(s')
$$

2. The agent chooses the action

$$
\max_a
$$

These represent two different decision makers.

---

# Two Decision Makers

## Nature

Nature controls uncertainty.

The agent cannot decide which successor state actually occurs.

Instead,

Nature samples according to the transition probabilities.

For example,

```
Move East

↓

80% East

10% North

10% South
```

The agent has no control over these probabilities.

They are properties of the environment.

---

## The Agent

The agent controls only one thing:

**Which action to attempt.**

It may choose

- North
- South
- East
- West

For each possible action,

the Bellman equation computes the expected future reward.

The agent then selects the action with the highest expected value.

---

# The Bellman Equation Already Chooses the Best Action

Notice the

$$
\max_a
$$

inside the Bellman equation.

This means

> While computing the value of a state, we are already determining which action is best.

The value function and the optimal policy are therefore tightly connected.

---

# Extracting the Policy

Suppose Value Iteration has converged.

Every state now has an optimal value.

For example,

```
93    97   100

89    94

85    90
```

The agent now asks:

> "Which neighboring state has the highest expected value?"

The answer determines which action should be taken.

---

# Policy Equation

Mathematically,

the optimal policy is

$$
\pi(s)
=
\arg\max_a
\sum_{s'}
P(s'|s,a)V(s')
$$

Notice this looks almost identical to the Bellman equation.

The only difference is:

- Bellman computes **values**
- Policy extraction computes **actions**

---

# Understanding Argmax

Many students confuse

$$
\max
$$

and

$$
\arg\max
$$

They are different.

## Max

Returns the largest value.

Example

```
Actions

North → 48.6

South → 12

West → 4.7

East → 35
```

The maximum value is

$$
48.6
$$

---

## Argmax

Returns **which action produced that value.**

In the same example,

```
North → 48.6

South → 12

West → 4.7

East → 35
```

the result is

```
North
```

The Bellman equation uses

$$
\max
$$

to compute the value,

while the policy uses

$$
\arg\max
$$

to recover the best action.

---

# Building the Policy

Imagine standing in one square.

```
Current State
```

Look at every possible action.

For each action,

compute its expected future reward.

Example

| Action | Expected Value |
|---------|---------------:|
| North | 48.6 |
| East | 35 |
| South | 12 |
| West | 4.7 |

The optimal policy simply stores

```
North
```

for this state.

Now repeat this for **every state**.

The result is a complete policy.

---

# Policy as a Map of Actions

Instead of storing numbers,

the policy stores arrows.

Example

```
→   →   Goal

↑   ↑

↑   ←
```

Each arrow answers

> "If I am in this state, which action should I execute?"

Unlike a fixed path,

this policy works from **every possible state**.

Even if randomness causes the agent to drift away from the intended path,

the policy immediately tells it what to do next.

---

# Why Policies Are Better Than Plans

Recall why ordinary planning failed.

A fixed action sequence assumes everything goes exactly as expected.

Example

```
North

North

East

East
```

But suppose the first move fails.

```
Expected

↓

A2

Actual

↓

B1
```

The original plan is now incorrect.

A policy avoids this problem.

No matter where the agent ends up,

there is already an action assigned to that state.

This makes policies much more robust in stochastic environments.

---

# Important Insight

A **value function** answers

> "How good is this state?"

A **policy** answers

> "What should I do in this state?"

Value Iteration computes the value function first.

The policy is then extracted simply by choosing the action with the highest expected future value.

---

# Key Takeaways

- Value Iteration computes **how valuable every state is**.
- The Bellman equation already compares every possible action.
- The optimal policy is obtained using **argmax** over those action values.
- Nature determines which successor state actually occurs.
- The agent determines which action to attempt.
- Policies are far more robust than fixed action sequences because they specify an action for **every possible state**.

# From Value Function to Policy

At this point, we know how to compute the **value of every state** using Value Iteration.

However, the agent still does not know **what action to take**.

A value function only tells us:

> "How good is it to be in this state?"

To actually act, the agent must convert these values into a **policy**.

---

# Recall

A **value function** answers

> "If I start in this state and behave optimally, how much future reward should I expect?"

A **policy** answers

> "Given that I am in this state right now, what action should I take?"

Value functions evaluate states.

Policies choose actions.

---

# Extracting a Policy

Suppose the value function has already converged.

Now imagine standing in some state.

You look at every possible action:

- North
- South
- East
- West

For each action, you compute

- where you might end up,
- the probability of each outcome,
- and the value of those successor states.

The best action is simply the one that gives the **largest expected value**.

---

# Policy Equation

Mathematically,

the optimal policy is

$$
\pi(s)
=
\arg\max_a
\sum_{s'}
P(s'|s,a)V(s')
$$

where

- $$\pi(s)$$ = action chosen in state $$s$$
- $$\arg\max$$ = choose the action that gives the highest value
- $$P(s'|s,a)$$ = transition probability
- $$V(s')$$ = value of the successor state

---

# Difference Between max and argmax

This is an important distinction.

## max

Returns the **largest value**.

Example

```
North → 48.6

West → 4.7
```

The maximum is

```
48.6
```

---

## argmax

Returns **which action produced the maximum**.

Using the same example

```
North → 48.6

West → 4.7
```

The answer is

```
North
```

Notice

```
max

↓

48.6

argmax

↓

North
```

One returns a number.

The other returns an action.

---

# Bellman Backup Already Finds the Best Action

When performing Value Iteration,

we already maximize over all possible actions.

Therefore,

once Value Iteration converges,

the optimal action is already hidden inside the Bellman equation.

Extracting the policy simply means asking

> Which action produced the maximum value?

---

# Relationship Between Value Function and Policy

```
Environment

↓

Value Iteration

↓

Optimal Value Function

↓

Choose Best Action (argmax)

↓

Optimal Policy
```

This is why Value Iteration solves **both** problems:

- computing state values
- finding the optimal policy

---

# Key Idea

A value function tells us

> "How valuable is this state?"

A policy tells us

> "What should I do here?"

The policy is obtained by choosing the action that leads to the successor states with the highest expected value.

# How Costs Change the Optimal Policy

One of the most interesting ideas in MDPs is that changing the **reward (or cost) function** changes the agent's behaviour.

The environment stays exactly the same.

The transition probabilities stay exactly the same.

Only the rewards change.

Yet the optimal policy becomes completely different.

---

# Case 1 — Movement Cost = -3

This is the example used throughout the lecture.

Every move costs

$$
-3
$$

Goal reward

$$
+100
$$

Bad terminal

$$
-100
$$

---

## Resulting Behaviour

The agent wants to

- reach the goal quickly,
- but also avoid the dangerous state.

Sometimes it accepts a small amount of risk because taking a long detour would accumulate too many movement costs.

This creates a balance between

- **speed**, and
- **safety**.

---

# Case 2 — Movement Cost = 0

Now suppose moving has **no cost**.

Every step is free.

The only rewards are

- +100 at the goal
- -100 at the bad terminal

---

## What Happens?

Since moving costs nothing,

there is **no penalty for taking a longer route**.

The agent becomes extremely patient.

Instead of risking the -100 terminal,

it willingly takes a long detour if that makes the path safer.

---

## Value Function

Eventually every non-terminal state reaches

$$
100
$$

Why?

Because the agent can always keep trying until it eventually reaches the positive terminal.

Since moving is free,

there is no disadvantage to taking many extra steps.

---

## Policy Changes

Some actions that previously moved directly toward the goal are replaced by safer actions.

For example,

near the dangerous terminal,

the policy deliberately moves **away from the goal** first,

avoiding any chance of accidentally entering the -100 state.

---

# Case 3 — Movement Cost = -200

Now consider the opposite extreme.

Every move costs

$$
-200
$$

This is **twice as bad** as falling into the negative terminal.

---

## What Happens?

Now every additional step is extremely expensive.

The agent no longer cares very much about reaching the +100 goal.

Instead,

its priority becomes

> **End the episode as quickly as possible.**

---

## Surprisingly...

Sometimes the optimal policy intentionally moves toward the

$$
-100
$$

terminal.

At first this seems irrational.

Why would an agent deliberately choose a negative reward?

---

## Explanation

Suppose the two choices are

### Option 1

Walk five more steps.

Cost

$$
5\times(-200)
=
-1000
$$

then receive

$$
+100
$$

Total

$$
-900
$$

---

### Option 2

Immediately enter

$$
-100
$$

Total

$$
-100
$$

Clearly

$$
-100>-900
$$

The second option is actually better.

---

# Lesson

The agent is **not trying to reach the goal.**

It is trying to **maximize total expected reward.**

Sometimes that means

- reaching the goal,
- taking a detour,
- or even intentionally failing.

Everything depends on the reward function.

---

# The Reward Function Defines Behaviour

Changing only the rewards can produce completely different strategies.

| Reward Structure | Behaviour |
|------------------|-----------|
| Small movement cost | Balance speed and safety |
| Zero movement cost | Always choose the safest route |
| Huge movement cost | End the episode immediately |

---

# Key Insight

The reward function determines

- what the agent considers "good,"
- what it considers "bad,"
- and therefore how it behaves.

The planning algorithm never changes.

Only the rewards change.

---
# Markov Decision Processes — Lecture Summary

This lecture introduced **planning under uncertainty** using **Markov Decision Processes (MDPs).**

Unlike classical planning,

MDPs assume that actions are **stochastic**.

Even if the agent chooses an action,

the environment may produce different outcomes.

---

# Components of an MDP

An MDP is defined by four main components.

## 1. States

The possible situations the agent can be in.

Example

```
Robot location

Grid cell

Game position
```

---

## 2. Actions

The choices available in each state.

Example

```
North

South

East

West
```

---

## 3. Transition Model

Specifies how actions change the state.

Instead of being deterministic,

the outcome is represented by

$$
P(s'|s,a)
$$

which gives the probability of reaching state $$s'$$ after taking action $$a$$ in state $$s$$.

---

## 4. Reward Function

Every state (or state-action pair) receives a reward.

Examples

```
Goal

+100

Danger

-100

Movement

-3
```

The reward function defines what the agent should optimize.

---

# Objective of an MDP

The goal is to find a policy that maximizes the expected discounted sum of future rewards.

$$
\max_\pi
E\left[
\sum_{t=0}^{\infty}
\gamma^tR_t
\right]
$$

where

- $$R_t$$ = reward at time $$t$$
- $$\gamma$$ = discount factor
- $$E[\cdot]$$ = expectation over stochastic outcomes

---

# Value Iteration

The central algorithm introduced in this lecture is **Value Iteration**.

It repeatedly updates the value of every state using the Bellman Backup equation until the values stop changing.

After convergence,

the resulting value function is called the **optimal value function**.

---

# Bellman Backup

The Bellman equation computes the value of a state by considering

- every possible action,
- every possible successor state,
- the probability of each outcome,
- and the immediate reward.

It forms the foundation of dynamic programming methods for MDPs.

---

# Policy Extraction

Once the optimal value function is known,

the optimal policy is obtained by selecting the action with the highest expected successor value.

In other words,

```
Value Function

↓

Choose Highest Expected Value

↓

Optimal Policy
```

---

# Classical Planning vs MDPs

| Classical Planning | MDP |
|-------------------|-----|
| Deterministic actions | Stochastic actions |
| Produces one action sequence | Produces a policy |
| Assumes plan always succeeds | Handles unexpected outcomes |
| No probabilities | Uses transition probabilities |

---

# Why Policies Are Better Than Plans

A fixed plan only works if everything goes exactly as expected.

An MDP policy tells the agent what to do **from every possible state**.

If the environment behaves unexpectedly,

the agent simply consults the policy for its current state and continues.

This makes policies much more robust in uncertain environments.

---

# Real-World Applications

MDPs are widely used in Artificial Intelligence.

Examples include

- robot navigation,
- autonomous vehicles,
- medical treatment planning,
- resource allocation,
- dialogue systems,
- inventory management,
- reinforcement learning.

Any problem involving **sequential decision-making under uncertainty** can often be modeled as an MDP.

---

# Key Takeaways

- MDPs combine planning with probability.
- Actions have probabilistic outcomes.
- The objective is to maximize expected discounted future reward.
- Value Iteration computes the optimal value function.
- The Bellman Backup equation is the core update rule.
- The optimal policy is extracted from the optimal value function.
- Reward functions determine the behaviour of the agent.
- Policies are more powerful than fixed action sequences because they specify what to do in **every possible state**.

# Partial Observability and POMDPs

---

# From Fully Observable to Partially Observable Planning

So far in the course, we have assumed that the agent always knows exactly what state it is in.

This assumption allowed us to model problems as **Markov Decision Processes (MDPs)**.

However, many real-world problems are **not fully observable**.

The agent may know:

- where it is,
- what actions it can perform,

but it may **not know everything about the environment**.

Examples include:

- A robot whose sensors are noisy.
- A self-driving car whose cameras are temporarily blocked.
- A doctor who cannot directly observe a patient's disease.
- A robot exploring an unknown building.

In all of these situations, the agent must make decisions despite **missing information**.

---

# Why MDPs Are Not Enough

Recall what an MDP assumes.

An MDP assumes that the current state is completely known.

```
Current State

↓

Choose Action

↓

Environment changes

↓

Observe new state
```

Since the state is always known,

there is **never any reason to gather information**.

The agent already knows everything it needs to know.

This is a major limitation.

---

# The Need for Information Gathering

Suppose you are searching for your car keys.

You have two possible actions:

- Search the living room.
- Go directly to work.

Clearly,

the first action does **not immediately move you toward your goal**.

Instead,

it gathers information.

Only after finding the keys do you know what to do next.

This kind of reasoning cannot be represented naturally using an MDP.

---

# Partially Observable Markov Decision Processes (POMDPs)

To model uncertainty about the current world,

AI uses **Partially Observable Markov Decision Processes (POMDPs).**

A POMDP extends an MDP by allowing the agent to have **incomplete knowledge** about the environment.

Instead of knowing exactly which state it is in,

the agent maintains a **belief** about possible states.

---

# MDP vs POMDP

| MDP | POMDP |
|------|--------|
| State is fully known | State is uncertain |
| No need to gather information | Information gathering is valuable |
| Plans directly in physical states | Plans over beliefs about states |
| Agent always knows where it is | Agent reasons about what it might know |

The key difference is **knowledge**.

---

# Exploration vs Exploitation

One of the biggest advantages of POMDPs is that they naturally solve the **exploration vs exploitation** problem.

## Exploitation

Exploitation means:

> Use the information you already have to maximize reward.

Example:

A delivery robot already knows the fastest route.

It simply follows it.

---

## Exploration

Exploration means:

> Spend time gathering information that will improve future decisions.

Example:

A robot first explores a building before deciding which corridor is safest.

---

## Why This Is Impossible in an MDP

In an MDP,

the current state is already known.

Therefore,

there is no uncertainty to reduce.

Every action is judged only by the reward it directly produces.

Information-gathering actions have no special value.

---

# A Simple Maze Example

To explain why POMDPs are necessary,

Sebastian Thrun introduces a very small maze.

```
             Exit
            (+100 ?)

               |

Start ------- Junction

               |

            Sign

               |

             Exit
            (-100 ?)
```

The agent starts on the left.

There are two exits.

One exit gives

```
+100
```

The other gives

```
−100
```

However,

the agent **does not know which exit is which.**

---

# What Information Is Hidden?

Notice something interesting.

The agent **does know its physical location**.

It always knows where it is standing.

What it does **not** know is:

> Which exit contains the positive reward.

Instead,

there is a sign located below the junction.

The sign reveals the correct exit.

For example,

```
LEFT
```

means

```
Left exit = +100
Right exit = −100
```

while

```
RIGHT
```

means the opposite.

---

# Why Conventional Planning Fails

Suppose the robot ignores the sign.

It might simply choose an exit immediately.

```
Start

↓

Junction

↓

Guess Left
```

Half the time,

this guess is correct.

Half the time,

it leads directly to

```
−100
```

Clearly,

guessing is not optimal.

---

# The Optimal Strategy

The optimal strategy is surprisingly different.

```
Start

↓

Go South

↓

Read the sign

↓

Return

↓

Take the correct exit
```

Notice something very important.

The first movement

```
Go South
```

does **not move the robot toward the goal**.

Instead,

it gathers information.

Only after reading the sign can the robot confidently choose the correct exit.

---

# Information Has Value

This example illustrates one of the most important ideas in AI.

Sometimes,

an action is valuable **not because it immediately earns reward**,

but because it **reduces uncertainty**.

The trip to the sign is worthwhile because it prevents making an expensive mistake later.

---

# Why Averaging Two MDP Solutions Doesn't Work

One might think of solving the problem twice.

Scenario 1:

```
Left = +100
```

Scenario 2:

```
Right = +100
```

Then average the two policies.

Unfortunately,

this completely fails.

Why?

Because averaging tells the robot:

```
Sometimes go left

Sometimes go right
```

It never discovers that the correct first action is actually

```
Go read the sign.
```

The need to gather information disappears entirely.

This shows that **planning separately in each possible world is not enough.**

We must plan while considering **uncertainty itself**.

---

# Belief States

Instead of planning over physical states,

POMDPs plan over **belief states**.

A belief state represents

> what the agent currently believes about the world.

Initially,

the robot believes:

```
50%

Left is good

50%

Right is good
```

This uncertainty itself becomes the state.

---

# Updating Beliefs

Once the robot reaches the sign,

its belief changes.

Suppose the sign says

```
LEFT
```

Then the belief immediately becomes

```
100%

Left = +100
```

The uncertainty disappears.

Reading the sign therefore changes the **belief state**, even though the physical maze has not changed.

---

# Belief Space

Instead of planning through physical locations,

the robot now plans through **belief space**.

A simplified picture looks like this.

```
Unknown

↓

Read Sign

↓

Left is Good

or

Right is Good
```

Notice that

reading the sign causes a transition between **beliefs**, not merely locations.

---

# Value Iteration Works Again

Here is the elegant insight.

Once we represent uncertainty as belief states,

we can use the **same Value Iteration algorithm** we learned for MDPs.

Instead of propagating values through physical locations,

we propagate values through **belief space**.

The algorithm is mathematically almost identical.

Only the states have changed.

---

# Intuition: Value Flows Through Beliefs

Imagine pouring water into the goal state.

Just as before,

value spreads backward through the graph.

Eventually,

the value reaches the initial uncertain belief.

Because reading the sign eventually leads to certainty,

the value flowing backward makes the action

```
Go South
```

appear optimal.

The algorithm naturally discovers that gathering information is worthwhile.

---

# Key Insight

POMDPs transform

```
Unknown World
```

into

```
Known Belief
```

and then solve the planning problem in that new space.

Instead of asking

> "Where am I?"

the agent asks

> "What do I currently know?"

This is a much richer representation of decision making.

---

# Conclusion: Planning Under Uncertainty

This lecture completes the transition from classical planning to probabilistic planning.

We began with deterministic planning algorithms like A*.

Then we introduced uncertainty using **Markov Decision Processes (MDPs)**.

Finally,

we extended those ideas to **Partially Observable Markov Decision Processes (POMDPs)**, where the agent must reason not only about actions and rewards, but also about **information**.

---

# What We Learned

## Markov Decision Processes (MDPs)

An MDP models environments where:

- the current state is fully observable,
- actions have stochastic outcomes,
- the objective is to maximize long-term expected reward.

An MDP is defined by:

- States
- Actions
- Transition probabilities

$$
P(s' \mid s, a)
$$

- Reward function

$$
R(s)
$$

- Discount factor

$$
\gamma
$$

---

## Objective of an MDP

The goal is to maximize the expected cumulative discounted reward.

$$
\mathbb{E}\left[\sum_{t=0}^{\infty}\gamma^tR_t\right]
$$

Rather than maximizing immediate reward,

the agent optimizes **all future rewards**.

---

## Value Iteration

The central algorithm for solving an MDP is **Value Iteration**.

It repeatedly applies the Bellman Backup equation

$$
V(s)
=
R(s)
+
\gamma
\max_a
\sum_{s'}
P(s'|s,a)
V(s')
$$

until the values converge.

---

## Policy Extraction

Once the optimal value function is known,

the optimal policy is obtained by selecting the action that maximizes the Bellman expression.

$$
\pi^*(s)
=
\arg\max_a
\sum_{s'}
P(s'|s,a)
V(s')
$$

Thus,

Value Iteration first computes **how valuable each state is**, and then derives **what action should be taken**.

---

# Why Policies Are Better Than Plans

A deterministic planner produces

```
One fixed sequence of actions.
```

An MDP produces

```
A complete policy.
```

A policy specifies what to do **from every possible state**, including states reached unexpectedly because of randomness.

This makes MDPs much more robust in uncertain environments.

---

# Why POMDPs Are Even More Powerful

MDPs assume:

```
The world is known.
```

POMDPs assume:

```
The world is only partially known.
```

Instead of planning over physical states,

the agent plans over

```
Belief States
```

which encode everything the agent currently knows about the world.

This allows actions whose purpose is to **gather information**, not just achieve goals.

---

# The Big Picture

Throughout the AI course,

planning gradually became more realistic.

```
Deterministic Planning

↓

Stochastic Planning (MDPs)

↓

Partially Observable Planning (POMDPs)

↓

Reinforcement Learning
```

Each stage adds another layer of realism:

- deterministic actions,
- uncertain actions,
- uncertain observations,
- finally learning from experience.

---

# Real-World Applications

Planning under uncertainty is used in many AI systems.

Examples include:

- Autonomous robots navigating crowded environments.
- Self-driving cars dealing with uncertain sensor readings.
- Warehouse robots avoiding obstacles.
- Medical decision support systems.
- Financial decision making.
- Space exploration robots.
- Search-and-rescue robots.
- Dialogue systems that reason about uncertain user intentions.

In nearly all real-world environments,

actions are uncertain,

observations are incomplete,

and intelligent agents must continuously balance **reward, risk, and information**.

---

# Final Takeaway

The central lesson of this lecture is:

> Intelligent planning is not simply about finding the shortest path.

Instead,

an intelligent agent must reason about:

- uncertainty,
- future consequences,
- probabilities,
- long-term rewards,
- and sometimes even the value of obtaining **more information** before acting.

This idea forms the foundation for modern robotics, autonomous systems, reinforcement learning, and sequential decision making under uncertainty.