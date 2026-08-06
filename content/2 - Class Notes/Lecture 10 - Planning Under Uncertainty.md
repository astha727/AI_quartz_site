
## Overview

Up to this point in the course, we have studied three major areas of Artificial Intelligence independently:

- **Search & Planning** — finding sequences of actions to achieve a goal.
- **Probability** — reasoning under uncertainty.
- **Machine Learning** — learning patterns from data.

Each of these solved a different problem.

- Search assumed the environment was **deterministic**.
- Probability modeled **uncertainty**, but did not explain how an agent should act.
- Machine Learning focused on learning from experience.

Planning Under Uncertainty combines the first two.

Instead of asking:

> *"How do I reach the goal?"*

we now ask:

> *"How should I act when the outcome of my actions is uncertain?"*

The mathematical framework used to answer this question is the **Markov Decision Process (MDP)**.

---

# Why Classical Planning Breaks Down

All classical planning algorithms studied so far assume that every action has a **single predictable outcome**.

```
Move Forward

↓

Robot moves forward
```

Because every action is deterministic, planning reduces to finding a sequence of actions from the start state to the goal.

Examples include:

- Breadth-First Search
- Depth-First Search
- Uniform Cost Search
- A*
- Dynamic Programming

These algorithms work extremely well **only when the environment behaves exactly as expected.**

## Real-World Actions Are Uncertain

Real environments are rarely deterministic.

A robot instructed to move forward may instead

- slip,
- collide with an obstacle,
- encounter sensor noise,
- or be blocked by another agent.

Instead of one outcome, an action produces several possible outcomes.

```
Move Forward

↓

80% → Forward

10% → Left

10% → Right
```

The same action no longer guarantees the same result.

Instead, each possible outcome has an associated probability.

This type of environment is called **stochastic**.

## Why This Matters

Suppose a planner generates the path

```
North

North

East

East
```

If the very first action fails,

the robot is no longer where the planner expected.

The remainder of the plan may now be completely invalid.

Classical planning offers no mechanism for adapting to unexpected outcomes.

Instead of planning for **one future**, we must reason about **many possible futures simultaneously**.

# Planning Under Uncertainty

Planning under uncertainty extends classical planning by combining

- **Planning** — deciding which action to take
- **Probability** — reasoning about uncertain outcomes

Rather than searching for a single perfect path, the agent chooses actions that perform well **on average across all possible outcomes.**

## Real-World Examples

| Application | Source of Uncertainty |
|-------------|-----------------------|
| Self-driving cars | Traffic, pedestrians, weather |
| Robots | Wheel slip, noisy sensors |
| Medical diagnosis | Imperfect tests |
| Financial trading | Market fluctuations |
| Voice assistants | Speech recognition errors |

Notice that uncertainty comes from the **environment**, not necessarily from the agent.

---

# Where This Fits in AI

| Environment | Appropriate Framework |
|-------------|----------------------|
| Fully observable + deterministic | Classical Planning |
| Fully observable + stochastic | **Markov Decision Processes (MDPs)** |
| Partially observable + stochastic | **POMDPs** |
| Unknown environment | **Reinforcement Learning** |

Each framework relaxes another assumption about the world.

> [!important]
> **Key Idea**
>
> Classical planning assumes actions always succeed.
>
> Planning under uncertainty assumes actions have probabilistic outcomes and seeks the action that produces the best long-term expected result.


# Markov Decision Processes (MDPs)

## Motivation

Once actions become uncertain, planning is no longer about finding a fixed sequence of moves.

Instead, the agent must evaluate

- every possible action,
- every possible outcome,
- and the long-term consequences of each.

This motivates the **Markov Decision Process (MDP)**.

## Definition

A **Markov Decision Process (MDP)** is a mathematical framework for sequential decision making in environments that are

- fully observable,
- stochastic,
- and reward-driven.

The objective is to choose actions that maximize **expected cumulative reward**.

---

# The Markov Property

The defining assumption of an MDP is the **Markov Property**.

> The future depends only on the current state—not on the sequence of states that came before it.

Once the current state is known,

the history becomes irrelevant for predicting future behavior.

```
Path A

Start

↓

Room 1

↓

Room 2

↓

Current State


Path B

Garage

↓

Kitchen

↓

Current State
```

Although the two paths are different,

both agents make exactly the same decision because they occupy the same current state.

---

# Components of an MDP

Every MDP consists of four fundamental components.

| Component | Purpose |
|------------|----------|
| States | Describe the current situation |
| Actions | Choices available to the agent |
| Transition Model | Probabilities of future states |
| Reward Function | Describes how desirable outcomes are |

Together these completely specify the decision problem.

---

# States

A **state** represents everything the agent needs to know about the current situation.

Examples include

| Problem | State |
|----------|-------|
| Robot navigation | Robot location |
| Chess | Board configuration |
| Self-driving car | Position, speed, nearby vehicles |
| Medical diagnosis | Patient condition |

The collection of all possible states is called the **state space**.

---

# Actions

Actions are the decisions available to the agent.

For a navigation robot

- North
- South
- East
- West

Unlike states, actions are chosen by the agent.

---

# Transition Model

The transition model describes how actions change the state.

Unlike deterministic planning,

each action now has multiple possible outcomes.

```
Current State

↓

Move East

↓

80% → S₂

10% → S₁

10% → S₃
```

The transition probabilities are written as

$$
P(s' \mid s,a)
$$

which means

> Probability of reaching state $s'$ after taking action $a$ in state $s$.

Unlike Bayes' Rule,

this conditional probability models **state transitions**, not inference about hidden variables.

---

# Reward Function

The reward function assigns a numerical value to states.

$$
R(s)
$$

represents the immediate reward obtained from state $s$.

Example

| State | Reward |
|--------|---------|
| Empty hallway | 0 |
| Goal | +100 |
| Dangerous area | -100 |

The objective of an MDP is **not** simply to reach the goal,

but to maximize the **total expected reward over time.**

---

# The MDP Cycle

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

The agent continually

- observes the current state,
- selects an action,
- experiences an uncertain transition,
- receives a reward,
- and repeats the process.

---

# Summary

| Component | Question Answered |
|------------|-------------------|
| States | Where am I? |
| Actions | What can I do? |
| Transition Model | Where might I end up? |
| Reward Function | How desirable is that outcome? |

Together these components allow an intelligent agent to make optimal decisions despite uncertainty.

> [!summary]
> **Takeaway**
>
> Classical planning searches for the best sequence of actions assuming perfect execution.
>
> MDPs generalize this idea by planning over probabilistic outcomes and optimizing **expected long-term reward** instead of a single deterministic path.


# Grid World: The Simplest MDP

## Why Study Grid Worlds?

Real-world planning problems—such as autonomous driving, robotics, or drone navigation—are often too complex to analyze directly.

Instead, AI researchers introduce a much simpler environment called a **Grid World**.

A Grid World is a two-dimensional grid in which an agent moves between square cells.

Although simple, it captures the essential ingredients of a Markov Decision Process:

- states,
- actions,
- stochastic transitions,
- rewards,
- and decision making under uncertainty.

> [!note]
> Most introductory MDP and Reinforcement Learning algorithms are first developed on Grid Worlds before being applied to real-world problems.

---

# A Simple Grid World

```text
+---------+---------+---------+---------+
|                 |                  |                 |   +100    |
|                 |                  |                 |   Goal    |
+---------+---------+---------+---------+
|                 |                  |                 |              |
|    Start    |                  |                 |               |
+---------+---------+---------+---------+
|                 |                  |                 |   -100     |
|                 |                  |                 |  Danger |
+---------+---------+---------+---------+
```

The agent starts in the **Start** state. Two cells have special rewards:

| State | Reward |
|--------|-------:|
| Goal | +100 |
| Danger | -100 |

These are **terminal (absorbing) states**.

---

# Absorbing States

An **absorbing state** is a state that ends the decision process.

Once the agent enters one of these states,

- it receives the corresponding reward,
- no further actions are taken,
- and the episode terminates.

```text
Start

↓

Goal (+100)

↓

End
```

Likewise,

```text
Start

↓

Danger (-100)

↓

End
```

---

# Actions in a Grid World

At every non-terminal state, the agent can choose one of four actions:

- North
- South
- East
- West

Unlike classical planning, selecting an action **does not guarantee** the intended movement.

The environment determines the actual outcome according to the transition model.

---

# Stochastic Actions

Suppose the agent chooses

```
Move North
```

Instead of always moving north,

the action succeeds with probability **0.8**.

The remaining probability is distributed between the neighboring directions.

| Outcome | Probability |
|----------|-----------:|
| Intended direction | 0.8 |
| Left of intended direction | 0.1 |
| Right of intended direction | 0.1 |

For example,

```text
Attempt North

80% → North

10% → West

10% → East
```

The agent selects the action,

but the environment determines which transition actually occurs.

This uncertainty is captured by the transition probabilities

$$
P(s' \mid s,a).
$$

---

# Example

Suppose the robot is in the center cell.

```text
      N

W   Robot   E

      S
```

After selecting **Move North**, three outcomes are possible.

```
80% → North

10% → West

10% → East
```

Although the robot intended only one movement,

all three transitions must be considered during planning.

---

# Walls and Invalid Movements

If the intended movement would leave the grid,

the agent remains in its current state.

For example,

```text
########

Robot

↓

Move North
```

Since there is no valid cell above,

the 80% probability corresponds to **staying in place**.

If multiple directions are blocked,

their probabilities accumulate.

For example, in a corner,

| Outcome | Probability |
|----------|-----------:|
| Stay in current state | 0.9 |
| Move to the only valid neighboring cell | 0.1 |

This guarantees that transition probabilities always sum to one.

---

# Why Grid Worlds Matter

Unlike deterministic search, a Grid World requires the agent to reason about **all possible future states**.

Choosing an action means evaluating

- where the agent is likely to end up,
- the reward associated with those outcomes,
- and how those outcomes affect future decisions.

Planning therefore becomes a problem of **optimizing expected long-term reward**, rather than simply finding the shortest path.

---

# Looking Ahead: Policies

Because actions have uncertain outcomes,

a fixed sequence of moves is no longer sufficient.

Instead, the agent requires a rule that specifies

> **Which action should be taken in every possible state?**

Such a decision rule is called a **policy**, and it becomes the central object studied in Markov Decision Processes.

---

# Summary

Grid Worlds provide a simple environment for studying decision making under uncertainty.

Key characteristics include:

- discrete states arranged in a grid,
- probabilistic state transitions,
- terminal (absorbing) states,
- rewards associated with outcomes,
- and stochastic actions.

> [!summary]
> **Key Insight**
>
> In an MDP, selecting an action does **not** determine the next state—it determines a **probability distribution over possible next states**. The agent must therefore plan using expected future outcomes rather than a single deterministic path.

# Why Classical Search Does Not Work for MDPs

The search algorithms studied earlier in the course—such as **DFS**, **BFS**, **Uniform Cost Search**, **A***, and **Dynamic Programming on deterministic graphs**—all assume a **deterministic transition model**.

That assumption has an important consequence:

> **Each action produces exactly one successor state.**

As a result, planning reduces to searching for a sequence of actions from the start state to the goal.

An MDP violates this assumption.

Instead of producing a single successor, every action produces a **probability distribution over successor states**.

This seemingly small change fundamentally alters the planning problem.

---

# From Search Trees to Chance Nodes

In classical search,

each action generates exactly one child node.

```text
State

 │

Action

 ▼

Next State
```

The search tree branches only because the **agent has multiple actions**.

For example,

```text
          C1

      /   |   |   \

     N    S   E    W
```

Each branch represents one possible action.

---

## In an MDP

Choosing an action does **not** determine the next state.

Instead, the environment randomly selects one of several possible outcomes according to the transition probabilities.

```text
             Choose North

                  │

              Chance

        ┌─────────┼─────────┐

        ▼         ▼         ▼

       B1        C1        C2

      0.8       0.1       0.1
```

Notice the distinction:

- **The agent chooses an action.**
- **The environment determines the resulting state.**

Planning must therefore consider **all possible outcomes**, not only the intended one.

---

# Consequence 1: Larger Search Trees

Suppose every state offers four actions.

In deterministic search,

```
Branching factor = 4
```

If each action can lead to three possible successor states,

the planner must reason about

```
4 actions

×

3 possible outcomes

=

12 possible transitions
```

The search tree grows much more rapidly because every decision is followed by several stochastic outcomes.

This phenomenon is often called the **explosion of the search tree**.

---

# Consequence 2: Cycles Become Common

Stochastic transitions also make repeated states unavoidable.

For example,

```text
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

...
```

Even when the agent follows the same policy,

random outcomes may continually return it to previously visited states.

Unlike deterministic search, there is no guarantee that the goal will be reached after a fixed number of actions.

Planning algorithms must therefore reason about **ongoing decision processes**, not finite paths.

---

# Consequence 3: Paths Become Less Important Than States

In classical search,

the objective is to find the **best path** to the goal.

In an MDP,

many different paths may repeatedly arrive at the same state.

```text
        Start

        /     \

        A       B

        \     /

        ▼   ▼

          C
```

Once the agent reaches state **C**, its previous history is irrelevant because of the **Markov Property**.

Only the current state matters when selecting the next action.

Consequently,

planning shifts from evaluating **paths** to evaluating **states**.

This observation is fundamental and motivates the algorithms studied later, such as **Value Iteration** and **Policy Iteration**, which compute the value of each state rather than searching through every possible path.

---

# Why Classical Search Is No Longer Sufficient

The combination of

- stochastic transitions,
- repeated states,
- and potentially infinite interaction with the environment

makes conventional search algorithms inefficient or even inapplicable.

Instead of asking

> "Which path reaches the goal?"

an MDP asks

> "What is the best action to take from each state, considering all possible future outcomes?"

This requires a different solution framework based on **state values**, **expected rewards**, and **policies** rather than deterministic search trees.

---

# Summary

Classical search and MDP planning differ in several fundamental ways.

| Classical Search | MDP Planning |
|------------------|--------------|
| One action produces one successor | One action produces multiple possible successors |
| Search for the best path | Compute the best decision for every state |
| Finite search tree | Stochastic process with repeated states |
| Goal is a sequence of actions | Goal is an optimal policy |

> [!summary]
> **Key Insight**
>
> Classical planning searches for the **best path**.  
> MDPs instead compute the **best action for every state**, since the actual path followed depends on stochastic outcomes that cannot be predicted in advance.

# Policies: From Plans to Decision Rules

## Why Search Is No Longer Enough

In deterministic planning, the output of a search algorithm is a **plan**—a fixed sequence of actions that leads from the start state to the goal.

For example,

```text
North

North

East

East
```

This works because every action is assumed to produce exactly one predictable outcome.

If the agent follows the plan correctly, it will always arrive at the expected state.

In a **Markov Decision Process (MDP)**, however, this assumption no longer holds.

Actions are **stochastic**, meaning the same action can lead to multiple possible outcomes.

A robot that intends to move north may instead drift east or west due to wheel slippage, sensor noise, or environmental factors.

As a result, the agent may quickly find itself in a state that was **never part of the original plan**.

A fixed action sequence is therefore no longer sufficient.

---

# From Plans to Policies

Instead of computing a single sequence of actions, an MDP computes a **policy**.

A policy answers a different question.

Instead of asking

> *"What sequence of actions reaches the goal?"*

it asks

> *"For every possible state I might encounter, what is the best action to take?"*

A policy can therefore be viewed as a **decision rule** that tells the agent how to behave regardless of how it arrived at its current state.

---

# Definition of a Policy

A **policy** is a mapping from states to actions.

It is commonly written as

$$
\pi : S \rightarrow A
$$

where

- $S$ is the set of all possible states,
- $A$ is the set of available actions.

For every state $s$,

$$
\pi(s)
$$

returns the action that the agent should perform when it is in that state.

Unlike a plan, a policy is **not tied to one particular path** through the environment.

It provides instructions for **every state** that the agent may encounter.

> [!info]
> A **plan** answers *"What actions should I perform?"*  
> A **policy** answers *"What action should I perform from this state?"*

---

# A Policy is a Contingency Plan

One way to think about a policy is as a **contingency plan**.

Rather than assuming everything will go according to plan, the agent prepares for every possible situation in advance.

Imagine a robot attempting to move north.

```text
Attempt North

80% → Move North

10% → Drift West

10% → Drift East
```

If the robot unexpectedly drifts west, it does **not** stop and compute a new plan from scratch.

Instead, it simply asks:

> **"I am now in this state. According to my policy, what should I do next?"**

The policy immediately provides the appropriate action.

This ability to recover from unexpected outcomes is one of the major advantages of MDPs over classical planning.

---

# Visualizing a Policy

Instead of storing a path, we can imagine writing an arrow inside every state of the environment.

```text
→   →   →   G

↑   ↑   →   ↑

↑   ↑   ↑   X
```

Each arrow indicates the action recommended by the policy.

For example,

- **→** means "Move East"
- **↑** means "Move North"

The agent simply looks at the current state and follows the corresponding arrow.

Even if randomness causes it to enter an unexpected state, another arrow is already waiting there to guide its next decision.

---

# Plans vs Policies

The difference between the two approaches is fundamental.

| Classical Planning | Markov Decision Processes |
|--------------------|---------------------------|
| Produces a **plan** | Produces a **policy** |
| Sequence of actions | State → Action mapping |
| Assumes actions succeed | Assumes actions are uncertain |
| Fails when the agent leaves the planned path | Naturally handles unexpected outcomes |

A policy is therefore much more robust because it specifies the best action **for every possible state**, not just those on one intended path.

---

# Why Policies Solve the Problems of Search

Earlier, we identified three major challenges that arise when planning under uncertainty:

1. Large branching factors
2. Potentially infinite search trees
3. Repeated visits to the same states

A policy addresses these issues by changing **what** we compute.

Instead of repeatedly searching through every possible future, the agent computes the best action for each state **once**.

If the same state is encountered again—even through a completely different sequence of actions—the agent simply reuses the previously computed decision.

This avoids redundant computation and allows the agent to react immediately when the environment behaves unexpectedly.

---

# Example

Suppose the robot reaches state **C1**.

The policy might specify:

```text
C1

↓

Move North
```

Later, because of random transitions, the robot returns to **C1**.

Rather than searching again, it simply applies the same decision:

```text
C1

↓

Move North
```

The policy is reused every time the state is encountered.

This is one of the key reasons MDP algorithms scale far better than repeatedly replanning after every unexpected event.

> [!summary]
> A **plan** is a fixed sequence of actions designed for deterministic environments.
>
> A **policy** is a mapping from states to actions that tells the agent how to behave in **every possible state**.
>
> Because actions in an MDP are stochastic, the agent cannot rely on a single path. Instead, it follows a policy that allows it to recover from unexpected outcomes and continue making optimal decisions throughout its interaction with the environment.


---

# Rewards and the Objective of an MDP

## Why Do We Need Rewards?

So far, we have answered **how** an agent should make decisions under uncertainty:

- the environment is modeled as an **MDP**,
- the agent follows a **policy** instead of a fixed plan.

However, one important question remains:

> **How does the agent decide whether one policy is better than another?**

To answer this, we need a way to measure how desirable different outcomes are.

This is the role of the **reward function**.

Rather than simply reaching a goal, the agent seeks to maximize the **total reward** it expects to receive over time.

---

# The Reward Function

A **reward** is a numerical signal that tells the agent how desirable a particular outcome is.

It is commonly written as

$$
R(s)
$$

meaning

> **the reward received when entering state** $s$.

Positive rewards encourage desirable behavior, while negative rewards discourage undesirable behavior.

For example,

| State | Reward |
|--------|--------:|
| Goal | +100 |
| Dangerous terminal state | −100 |
| Ordinary state | 0 |

In this simple setting,

- reaching the goal is highly desirable,
- entering the dangerous state is strongly penalized,
- all other states are neutral.

---

> [!note]
> **Reward** and **cost** are simply opposite conventions.
>
> - Positive rewards encourage behavior.
> - Negative rewards (costs) discourage behavior.
>
> A step cost of **−3** is simply a reward of **−3** received after every move.

---

# When Zero-Cost Movement Becomes a Problem

Suppose that every ordinary move has a reward of **0**.

The agent receives

- **+100** for reaching the goal,
- **−100** for entering the dangerous state,
- **0** everywhere else.

Under this reward structure, moving has **no cost**. As a result, the agent has no incentive to reach the goal quickly.

Whether it takes

- 5 steps,
- 50 steps,
- or even 500 steps,

the total reward remains exactly the same as long as it eventually reaches the goal.

This can produce policies that appear unintuitive.

For example, the agent may intentionally take a longer but safer route, or even remain near a wall if that slightly reduces the probability of accidentally entering the dangerous state.

Mathematically, this behavior is perfectly rational.

In practice, however, it is unrealistic because actions almost always consume some resource.

---

# Why Real Agents Care About Time

In real-world applications, every action has an associated cost.

| Application | Resource Being Consumed |
|--------------|-------------------------|
| Mobile robot | Battery power |
| Self-driving car | Fuel or energy |
| Delivery drone | Flight time |
| Video game agent | Turns |
| Manufacturing robot | Time and wear |

Each additional action consumes time, energy, money, or other limited resources.

An intelligent agent should therefore prefer solutions that are not only **successful**, but also **efficient**.

---

# Introducing Step Costs

To encourage efficient behavior, we assign a small negative reward to every ordinary state.

For example,

| State | Reward |
|--------|--------:|
| Goal | +100 |
| Dangerous state | −100 |
| Every normal state | −3 |

The reward **−3** is called the **step cost** (or **living cost**).

It means that every additional action slightly reduces the total reward.

The longer the agent spends reaching the goal, the more reward it loses.

---

# Example

Suppose two policies both eventually reach the goal.

### Policy A

```
Goal reached in 4 steps
```

Total reward

$$
100 - (4 \times 3) = 88
$$

---

### Policy B

```
Goal reached in 10 steps
```

Total reward

$$
100 - (10 \times 3) = 70
$$

Although both policies reach the same goal,

Policy A is preferred because it reaches the goal more efficiently.

Step costs naturally encourage shorter and more purposeful behavior without explicitly telling the agent to minimize path length.

---

# The Objective of an MDP

Because rewards are received repeatedly throughout the agent's interaction with the environment, the objective is no longer to maximize a **single reward**.

Instead, the agent seeks to maximize the **total reward accumulated over time**.

Conceptually,

$$
R_0 + R_1 + R_2 + R_3 + \cdots
$$

where

- $R_0$ is the immediate reward,
- $R_1$ is the reward after one action,
- $R_2$ after two actions,
- and so on.

The quality of a policy is therefore measured by the total reward it is expected to accumulate, not simply by whether it eventually reaches the goal.

---

# Why We Use an Expected Value

Unlike deterministic planning,

the future is uncertain.

The same action may produce different outcomes each time it is executed.

For example,

```text
Move North

80% → North

10% → West

10% → East
```

Since future states are random, the total reward is also random.

Instead of maximizing one particular outcome, the agent maximizes the **expected cumulative reward**— the probability-weighted average over all possible future trajectories.

---

# Mathematical Objective

The objective of an MDP is written as

$$
E\left[
\sum_{t=0}^{\infty}
R_t
\right]
$$

where

- $R_t$ is the reward received at time $t$,
- $E[\cdot]$ denotes the expected value.

This expression simply means

> **Choose actions that maximize the average total reward across all possible futures.**

---

# Discounting Future Rewards

In many planning problems, future rewards are considered less valuable than immediate rewards. This is modeled using a **discount factor**,

denoted by

$$
0 < \gamma < 1.
$$

The objective becomes

$$
E\left[
\sum_{t=0}^{\infty}
\gamma^tR_t
\right].
$$

Each future reward is multiplied by

$$
\gamma^t,
$$

making rewards received later contribute less to the total value.

---

# Why Do We Discount?

Discounting captures an important intuition:

> **Immediate rewards are generally more valuable than delayed rewards.**

There are several reasons for this.

- The future is uncertain.
- Delayed rewards may never be received.
- Resources available today can often be used immediately.
- Many real-world tasks naturally prioritize quicker success.

The discount factor therefore models an agent that prefers achieving its objectives sooner rather than later.

---

# Interpreting γ

The discount factor also determines **how far ahead** the agent plans.

| Discount Factor | Agent Behavior |
|-----------------|----------------|
| γ close to 0 | Focuses almost entirely on immediate rewards |
| γ close to 1 | Places significant importance on long-term rewards |

For this reason,

γ is often interpreted as controlling the agent's **planning horizon**.

A larger γ produces a more far-sighted agent,

while a smaller γ makes the agent increasingly short-sighted.

---

# Discounting vs Step Costs

Although both mechanisms encourage efficient behavior, they do so in different ways.

### Step Cost

Every action incurs a small penalty.

Longer paths accumulate larger costs.

---

### Discounting

Rewards received far in the future become less valuable.

Longer paths delay rewards, reducing their contribution to the objective.

---

Many practical MDPs combine both mechanisms.

Step costs discourage unnecessary actions,

while discounting naturally favors earlier rewards.

---

# Why Discounting Is Also Important Mathematically

Discounting is not only a modeling choice.

It also provides an important mathematical guarantee.

Because

$$
0 < \gamma < 1,
$$

the infinite reward sequence

$$
R_0 + \gamma R_1 + \gamma^2R_2 + \cdots
$$

always converges to a finite value.

This property allows algorithms such as **Value Iteration** and **Policy Iteration** to converge to stable solutions.

Without discounting, infinite reward sums may fail to converge in continuing tasks.

---

# Summary

Rewards define **what the agent wants**.

The objective of an MDP is not simply to reach the goal, but to maximize the **expected cumulative reward** collected over time.

Step costs encourage efficient behavior by penalizing unnecessary actions, while discounting encourages the agent to value immediate rewards more highly than distant ones.

Together, these ideas define the optimization objective that every MDP algorithm attempts to solve.

> [!summary]
> An MDP chooses actions that maximize the **expected discounted cumulative reward**.
>
> - **Rewards** define desirable outcomes.
> - **Step costs** encourage efficiency.
> - **Expected value** accounts for stochastic transitions.
> - **Discounting** balances immediate and future rewards while ensuring mathematical convergence.

---

# The Value Function

## From Immediate Rewards to Long-Term Decisions

In the previous section, we defined the objective of an MDP:

> **Choose actions that maximize the expected cumulative reward.**

This immediately raises an important question.

> **How can an agent tell whether one state is better than another?**

At first, it might seem sufficient to compare the **immediate reward** of each state.

However, this is often misleading.

Consider the following two states.

```text
State A

Immediate Reward = -3
```

```text
State B

Immediate Reward = -3
```

Although both states have the same immediate reward:

- State A may be only one step away from the goal.
- State B may be close to a dangerous terminal state.

Clearly, these states should not be considered equally desirable.

An intelligent agent therefore needs to look **beyond the immediate reward** and consider what is likely to happen in the future.

This motivates the idea of the **Value Function**.

---

## What Does "Value" Mean?

A **reward** answers the question:

> *"What do I receive right now?"*

A **value** answers a different question:

> *"If I start here and continue making decisions according to my policy, how much total reward should I expect to collect in the future?"*

Unlike rewards, values incorporate:

- immediate rewards,
- future rewards,
- uncertainty in the environment,
- and the decisions made by the policy.

In other words,

> **A state's value measures the quality of the future, not just the present.**

---

## Reward vs Value

Although the terms are related, they describe different ideas.

| Reward | Value |
|---------|-------|
| Immediate payoff for entering a state | Expected long-term return from that state |
| Local information | Global information |
| Known immediately | Depends on future decisions and uncertainty |

For example, every ordinary square in a Grid World may have a reward of **−3**, yet their values can differ dramatically depending on their location.

A state close to the goal is usually much more valuable than one near a dangerous terminal state.

---

## The Value Function

The value of a state is written as

$$
V^\pi(s)
$$

which is read as

> **"The value of state $s$ while following policy $\pi$."**

The formal definition is

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

Although this expression appears complicated, it is simply a compact mathematical description of the idea introduced above.

It asks:

> **If the agent starts in state $s$ and follows policy $\pi$, what is the expected total discounted reward it will receive?**

---

## Understanding the Equation

Each part of the equation represents one aspect of planning under uncertainty.

| Notation | Meaning |
|-----------|---------|
| $$S_0=s$$ | The agent starts in state $s$. |
| $$R_t$$ | Reward received at time $t$. |
| $$\gamma^t$$ | Discounts rewards that occur further in the future. |
| $$E[\cdot]$$ | Averages over all possible future outcomes. |

Together, these capture the two key challenges of planning:

- the future is uncertain,
- and rewards accumulate over time.

---

## Why Do We Use an Expected Value?

Because actions are stochastic, the future is not fixed.

Suppose the agent chooses to move north.

```text
Move North

80% → Move North

10% → Drift Left

10% → Drift Right
```

Each possible outcome leads to a different future sequence of rewards.

The value function therefore computes the **average long-term return** across all possible futures, weighted by their probabilities.

This is why the expectation operator $$E[\cdot]$$ appears in the definition.

---

## A Simple Example

Imagine the following Grid World.

```text
S ───► ───► Goal (+100)
│
│
▼
Danger (−100)
```

Suppose the agent starts at **S**.

Different executions of the same policy may produce different outcomes.

```text
Run 1

S → Goal

Return = 91
```

```text
Run 2

S → Slip → Extra Step → Goal

Return = 85
```

```text
Run 3

S → Slip → Danger

Return = -100
```

The value of **S** is **not** any one of these returns.

Instead, it is the **expected average** over all possible executions.

---

## Value Depends on the Policy

An important property of the value function is that it is **policy-dependent**.

The same state may have different values under different decision strategies.

For example,

### Policy A

```text
Always move toward the goal.
```

Expected return:

```text
85
```

### Policy B

```text
Move randomly.
```

Expected return:

```text
23
```

The starting state is identical.

Only the behavior changes.

Consequently,

$$
V^\pi(s)
$$

always includes the policy symbol $$\pi$$, reminding us that **the quality of a state depends on the decisions that follow it.**

---

## Interpreting Values in a Grid World

Suppose every ordinary square has a reward of **−3**.

The goal provides **+100**, while the dangerous terminal state gives **−100**.

After computing the value function, the states might look conceptually like this.

```text
72    84    94   100

60    70    81

42    51   -100
```

Notice that neighboring states no longer have identical values.

Their values reflect:

- their distance from the goal,
- the risk of entering dangerous regions,
- accumulated step costs,
- and uncertainty in future actions.

The value function summarizes all of this information into a **single number** for each state.

---

## Why Is the Value Function Useful?

Once every state has a value, planning becomes much simpler.

Instead of searching for an entire path from scratch, the agent repeatedly asks:

> **"Which neighboring state has the highest value?"**

By moving toward states with larger values, the agent naturally follows actions that maximize long-term expected reward.

The value function therefore transforms planning into a local decision problem guided by long-term outcomes rather than immediate rewards.

---

## Computing the Value Function

The values are not known in advance.

Instead, they are estimated iteratively.

Initially, every state may be assigned a rough guess.

```text
0    0    0   100

0    0    0

0    0  -100
```

An algorithm called **Value Iteration** repeatedly updates these estimates using the **Bellman Equation**.

With each iteration, information propagates outward from the terminal states until every state's value converges to its optimal estimate.

The next section introduces this algorithm in detail.

## Key Takeaways

- A **reward** measures the immediate payoff of entering a state.
- A **value** measures the expected long-term return from that state.
- Values incorporate immediate rewards, future rewards, uncertainty, and discounting.
- The value of a state depends on the **policy** being followed.
- States with identical immediate rewards can have very different values.
- Once state values are known, choosing actions becomes straightforward.
- **Value Iteration** is the algorithm used to compute these values.
---

# Value Iteration: Intuition and the Bellman Backup

## Why Do We Need Value Iteration?

In the previous section, we introduced the **value function**, which measures the expected long-term return of starting in a particular state.

The challenge, however, is that these values are **not known in advance**.

> **How can an agent determine the value of every state in the environment?**

This is precisely the purpose of **Value Iteration**.

Rather than solving the entire planning problem at once, Value Iteration starts with rough estimates and repeatedly improves them.

With each iteration, the estimates become more accurate until they eventually converge to the optimal values.

---

# Sebastian Thrun's Intuition

Sebastian Thrun explains Value Iteration using a simple analogy.

Imagine that the goal state contains a bucket of milk.

```text
          Goal
         (+100)

           🥛
```

When the milk is poured, it gradually spreads through the grid.

```text
Iteration 1

            100
```

```text
Iteration 2

       80    100
```

```text
Iteration 3

   60    80    100
```

```text
Iteration 4

40    60    80    100
```

Eventually, every reachable state receives some amount of "milk."

The amount that reaches each square represents **how valuable that state is**.

States that are easier, safer, and quicker to reach from the goal naturally receive larger values than states that are farther away or more risky.

---

# Why Do Values Spread Backward?

Notice that the goal is the **only state whose value is immediately known**.

```text
Goal

Value = +100
```

The neighboring states can estimate their values because they can reach the goal.

Once those estimates improve, states further away can improve their own estimates.

Information therefore propagates **backward** through the state space.

```text
Goal

↓

Neighbors

↓

Neighbors

↓

Remaining States
```

Instead of searching forward from the start, Value Iteration repeatedly propagates information outward from states whose values are already known.

---

# A Recursive View of Planning

Suppose we want to compute the value of the current state.

```text
Current State

      S
```

Rather than considering every possible future path, we ask a much simpler question.

> **If I take one action, where might I end up next?**

Suppose one action could lead to

```text
S₁

S₂

S₃
```

If we already have good estimates for the values of these successor states, then estimating the value of the current state becomes much easier.

This recursive idea is the essence of **Dynamic Programming**.

Large planning problems are solved by repeatedly combining solutions to many smaller subproblems.

---

# The Bellman Principle of Optimality

Richard Bellman's key insight was remarkably simple.

> **The value of a state depends on the value of the states that can be reached from it.**

Instead of reasoning about an entire future trajectory, we only need to consider:

1. the immediate reward,
2. one action,
3. the possible successor states,
4. and the values already assigned to those successor states.

This recursive relationship is known as the **Bellman Principle of Optimality**, and it forms the foundation of Value Iteration.

---

# The Bellman Backup Equation

The update performed during Value Iteration is called the **Bellman Backup**.

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

Although the equation appears intimidating, each component has a straightforward interpretation.

Rather than memorizing it, it is more useful to understand how each part contributes to updating the value of a state.

---

# Understanding the Bellman Backup

The update can be read from left to right.

## 1. Receive the Immediate Reward

The agent first receives the reward associated with its current state.

$$
R(s)
$$

For example,

| State | Reward |
|--------|--------|
| Ordinary state | −3 |
| Goal state | +100 |
| Dangerous terminal state | −100 |

This is the reward obtained **immediately**, before considering the future.

---

## 2. Consider Every Possible Outcome

After choosing an action, the environment determines the next state.

Because actions are stochastic, several outcomes may be possible.

For example,

```text
Move East

80% → East

10% → North

10% → South
```

Each successor state already has a value estimate.

Rather than selecting one outcome, we compute their **expected value** using the transition probabilities.

$$
\sum_{s'}
P(s'|s,a)V(s')
$$

This term represents the **average value of the future** after taking a particular action.

---

## 3. Discount Future Rewards

Future rewards are multiplied by the discount factor

$$
\gamma
$$

If

$$
\gamma = 1
$$

future rewards are valued exactly the same as immediate rewards.

If

$$
\gamma = 0.9
$$

rewards received further into the future contribute slightly less.

Discounting encourages earlier rewards and guarantees convergence of Value Iteration.

## 4. Choose the Best Action

The environment controls **which successor state occurs**, but the agent controls **which action to take**.

Therefore, the agent evaluates every possible action and selects the one with the largest expected value.

This is represented by

$$
\max_a
$$

Nature introduces uncertainty through the transition probabilities.

The agent responds by choosing the action that maximizes its expected long-term return.

---

# Reading the Bellman Equation in Plain English

The Bellman Backup can be summarized as

> **The value of a state equals its immediate reward plus the discounted expected value of the best action available from that state.**

Every iteration applies this update to every state in the Grid World.

As the values improve, better estimates propagate throughout the environment until the values eventually stop changing.

At that point, the Value Function has converged to the optimal solution.

## Key Takeaways

- Value Iteration computes the value of every state through repeated updates.
- Information propagates backward from states whose values are already known.
- The Bellman Principle states that a state's value depends on the values of its successor states.
- The Bellman Backup combines:
  - the immediate reward,
  - expected future value,
  - transition probabilities,
  - discounting,
  - and optimal action selection.
- Repeated Bellman updates eventually converge to the optimal Value Function.

---

# Value Iteration

## Why Do We Need Value Iteration?

In the previous section, we introduced the **value function**, which measures how desirable it is to start in a particular state and continue following the optimal policy.

The challenge is that these values are **unknown**. Before an agent can decide which action is best, it must first estimate how valuable every state is.

The purpose of **Value Iteration** is to compute these values.

Rather than solving the entire planning problem in one step, Value Iteration begins with rough estimates and repeatedly improves them. Each iteration refines the value of every state by using information from neighboring states until the values stabilize.

> [!important] Core Idea
> Value Iteration does **not** search for paths. Instead, it computes the long-term value of every state in the environment.

---

# Intuition: Values Spread Through the State Space

One of the most intuitive explanations of Value Iteration comes from Sebastian Thrun.

Imagine the goal state contains a source of water (or milk). As time passes, the liquid spreads outward through the grid.

```text
Iteration 0

          Goal (+100)


Iteration 1

       97      Goal


Iteration 2

    94      97      Goal


Iteration 3

 91     94      97      Goal
```

Initially, only the goal has a known value.

During each iteration, neighboring states "learn" how valuable they are because they can reach states whose values are already known.

Eventually, every reachable state receives an appropriate value.

---

## A Different Perspective: A Potential Field

Another way to visualize the value function is as a **potential field**.

Imagine the goal generates an invisible force that attracts the agent.

```text
          Goal

        ↓↓↓↓↓↓↓

     Higher Value

        ↓↓↓↓↓↓↓

     Lower Value
```

States closer to the goal experience a stronger "pull," while distant states experience a weaker one.

Instead of explicitly searching for a path, an agent can simply move toward neighboring states with higher values.

This is why a value function naturally induces a good policy.

---

# Why Information Flows Backward

An important observation is that the goal already knows its own value.

$$
V(\text{Goal}) = 100
$$

A neighboring state can estimate its own value because it knows it can eventually reach the goal.

Once that value is updated, its neighbors can do the same.

Information therefore propagates outward from the terminal states.

```text
Goal

↓

Nearby States

↓

Farther States

↓

Entire State Space
```

This explains why Value Iteration is often described as **backward propagation of value**.

Unlike classical search, which starts from the initial state and explores forward, Value Iteration repeatedly improves value estimates throughout the entire state space.

---

# Dynamic Programming Intuition

Suppose we want to know the value of the current state.

```text
Current State

      S
```

At first glance, this seems difficult because there are countless possible future trajectories.

Instead of reasoning about every future step, Dynamic Programming breaks the problem into much smaller pieces.

The key question becomes:

> **"If I take one action, where might I end up next?"**

Suppose one action could lead to three possible successor states.

```text
          S

       /  |  \

     S₁  S₂  S₃
```

If we already have estimates for

- $$V(S_1)$$
- $$V(S_2)$$
- $$V(S_3)$$

then estimating the value of the current state becomes much easier.

Rather than solving the entire future repeatedly, we reuse previously computed information.

> [!tip]
> This reuse of smaller solutions is the essence of **Dynamic Programming**.

---

# The Bellman Principle of Optimality

The idea above was formalized by **Richard Bellman**.

His key insight is remarkably simple:

> [!important]
> **The value of the current state depends on the values of its successor states.**

Instead of planning an entire future from scratch, an optimal agent only needs to consider:

1. the immediate reward,
2. the possible next states,
3. how valuable those states already are.

Because every state can be defined in terms of the states that follow it, the entire planning problem becomes recursive.

This recursive relationship is known as the **Bellman Principle of Optimality**.

---

# The Bellman Backup

The Bellman Principle leads directly to the update rule used by Value Iteration.

This update is called the **Bellman Backup**.

$$
V(s)
=
R(s)
+
\gamma
\max_a
\sum_{s'}
P(s' \mid s,a)V(s')
$$

Although the equation appears intimidating, it is simply a recipe for updating one state's value.

Every iteration applies this update to every state until the values converge.

---

# Understanding the Bellman Backup

Instead of memorizing the equation, it helps to interpret it from left to right.

---

## Step 1 — Immediate Reward

Every state contributes an immediate reward (or cost).

$$
R(s)
$$

Examples:

| State | Reward |
|-------|--------:|
| Ordinary state | -3 |
| Goal | +100 |
| Bad terminal | -100 |

This is the reward received **before** considering any future consequences.

---

## Step 2 — Consider Every Action

From the current state, the agent can choose among several actions.

For example,

```text
North

South

East

West
```

Each action leads to different future possibilities.

The Bellman Backup evaluates **every available action**, not just one.

---

## Step 3 — Predict Possible Outcomes

Because the environment is stochastic, a chosen action may lead to several different successor states.

For example,

```text
Attempt East

80% → East

10% → North

10% → South
```

Instead of assuming one outcome, the Bellman Backup computes the **expected value** across all possible successor states.

This is represented by

$$
\sum_{s'}
P(s' \mid s,a)V(s')
$$

Each successor contributes according to both:

- its probability of occurring,
- and its current value estimate.

---

## Step 4 — Discount Future Rewards

Future rewards are multiplied by the discount factor

$$
\gamma
$$

The discount factor controls how much importance is given to rewards that occur later.

- $$\gamma = 1$$ means future rewards are valued equally with immediate rewards.
- Smaller values of $$\gamma$$ make distant rewards less important.

Discounting also guarantees that the infinite reward sum remains finite, allowing Value Iteration to converge.

---

## Step 5 — Choose the Best Action

After evaluating every action, the agent selects the one with the highest expected return.

This is represented by

$$
\max_a
$$

Notice that the Bellman Backup does **not** average over actions.

The agent is assumed to act optimally, so it always chooses the action with the greatest expected value.

---

# Putting the Bellman Backup Together

The Bellman Backup can be read almost like a sentence:

> **The value of the current state equals its immediate reward plus the discounted expected value of the best action available.**

Thinking about the equation in this way is much more useful than trying to memorize the formula.

---

# Agent vs Nature

One of the most important ideas in MDPs is that **two different entities make decisions**.

These decisions should never be confused.

## The Agent Chooses the Action

The agent decides **what to attempt**.

```text
North

South

East

West
```

This is an intentional decision made by the policy.

---

## Nature Determines the Outcome

After an action is chosen, the environment determines what actually happens.

For example,

```text
Attempt East

80% → East

10% → North

10% → South
```

The agent has **no control** over which successor state occurs.

It only knows the probabilities.

---

## Why Both Appear in the Bellman Backup

This distinction explains the two mathematical operations inside the Bellman equation.

The agent chooses the best action:

$$
\max_a
$$

Nature determines the outcome through transition probabilities:

$$
\sum_{s'}
P(s' \mid s,a)V(s')
$$

> [!important]
> The **agent optimizes** over actions, while **nature averages** over uncertain outcomes.

---

# One Bellman Backup

Initially, most state values are unknown.

For example,

```text
0      0      100

0      0       0

0      0     -100
```

Suppose we update the state immediately beside the goal.

Because it has a high probability of reaching the goal, its value increases substantially.

```text
0      77      100

0       0        0

0       0     -100
```

Updating the value of a single state using the Bellman equation is called a **Bellman Backup**.

---

# Repeating the Process

After one backup, neighboring states can take advantage of the newly improved estimate.

```text
Iteration 1

0      77     100


Iteration 2

58     77     100


Iteration 3

40     58      77

58     77     100
```

Each iteration propagates information farther across the grid.

States become increasingly accurate because they rely on better estimates from their neighbors.

---

# Convergence

Eventually, repeating Bellman Backups no longer changes the value estimates.

```text
Old Value

↓

Bellman Backup

↓

Same Value
```

When successive iterations produce negligible changes, the algorithm is said to have **converged**.

At convergence,

$$
V(s)
=
R(s)
+
\gamma
\max_a
\sum_{s'}
P(s' \mid s,a)V(s')
$$

is no longer just an update rule—it becomes the **Bellman Optimality Equation**, meaning every state's value is perfectly consistent with the values of its successors.

---

# Why Value Iteration Works

Each Bellman Backup uses the best information currently available.

As value estimates improve, neighboring estimates improve as well.

Because information continually propagates through the state space, repeated updates eventually produce the optimal value function.

The final values answer a single question:

> **"If I start from this state and always act optimally, what is the maximum expected discounted reward I can obtain?"**

---

# Key Takeaways

> [!summary]
> - Value Iteration computes the value of **every state**, not a single path.
> - Values propagate backward from terminal states through repeated Bellman Backups.
> - The Bellman Principle expresses a state's value recursively in terms of its successors.
> - The Bellman Backup combines:
>   - immediate reward,
>   - transition probabilities,
>   - successor state values,
>   - discounting,
>   - and optimal action selection.
> - The **agent chooses actions** (max), while **nature determines outcomes** (expectation).
> - Repeated Bellman Backups eventually converge to the optimal value function.


# Worked Example: Value Iteration

The Bellman Backup equation defines **how** values should be updated.

The best way to understand it, however, is to work through concrete examples.

In this section, we apply Value Iteration to two versions of the same Grid World:

1. **Deterministic Grid World** — every action succeeds.
2. **Stochastic Grid World** — actions have uncertain outcomes.

By comparing these two cases, we can see how uncertainty changes both the value function and the resulting policy.

---

# Example 1 — Deterministic Grid World

To isolate the mechanics of Value Iteration, we first assume a **deterministic environment**.

Every action succeeds exactly as intended.

```text
Move East

↓

Always move East
```

There are:

- no transition probabilities,
- no accidental slips,
- no uncertainty.

The Bellman Backup therefore becomes much simpler because every action leads to exactly one successor state.

---

## Environment

For this example, assume:

| Parameter | Value |
|-----------|-------|
| Discount factor | $$\gamma = 1$$ |
| Step cost | $$-3$$ |
| Goal reward | $$+100$$ |
| Bad terminal reward | $$-100$$ |

The initial value function is

```text
0      0      +100

0      0        0

0      0      -100
```

Only the terminal states have known values.

All other states begin with an initial estimate of zero.

---

# Example 1 — Updating State A3

Consider the state immediately to the left of the goal.

```text
A3  →  Goal (+100)
```

Since movement is deterministic, moving East always reaches the goal.

The Bellman Backup becomes

$$
V(A3)
=
100-3
=
97
$$

The value consists of:

- the future reward of reaching the goal,
- minus the cost of taking one step.

After one update,

```text
97     100
```

The value of A3 becomes **97**.

---

# Example 2 — Updating State B3

Now consider the state below A3.

```text
97

↑

B3
```

The optimal action is again obvious.

Moving North reaches the state whose value is already known.

Applying the Bellman Backup,

$$
V(B3)
=
97-3
=
94
$$

After this update,

```text
97     100

94
```

Notice how information has propagated one step farther from the goal.

---

# Continuing the Iterations

Each iteration repeats exactly the same process.

Every state updates its value using the latest estimates of its neighbors.

After enough iterations, the values converge.

The final value function becomes

```text
97     100

94      97

91      94

88      91

85      88
```

---

# Interpreting the Result

Notice the regular pattern.

Each step away from the goal decreases the value by exactly three.

This happens because

- every move costs $$3$$,
- every action succeeds,
- and the shortest path is always optimal.

In this deterministic setting, the value function behaves almost like a **distance map**.

States closer to the goal naturally receive higher values because fewer movement costs remain.

> [!note]
> In deterministic environments, Value Iteration often resembles shortest-path planning, with state values decreasing steadily as distance from the goal increases.

---

# Example 2 — Stochastic Grid World

Now we restore uncertainty.

The environment once again behaves like the original MDP.

Attempting an action no longer guarantees its intended outcome.

```text
Attempt East

80% → East

10% → North

10% → South
```

Everything else remains unchanged.

| Parameter | Value |
|-----------|-------|
| Discount factor | $$\gamma=1$$ |
| Step cost | $$-3$$ |
| Goal reward | $$+100$$ |
| Bad terminal reward | $$-100$$ |

The initial value function is again

```text
0      0      +100

0      0        0

0      0      -100
```

---

# Example 3 — Updating State A3

Consider the state beside the goal.

```text
A3  →  Goal
```

Suppose the agent attempts to move East.

Possible outcomes are

```text
80% → Goal (+100)

10% → Stay

10% → Move Down
```

Since the remaining neighboring states still have value zero,

the expected future value is

$$
0.8(100)
+
0.1(0)
+
0.1(0)
=
80
$$

Subtracting the movement cost,

$$
80-3
=
77
$$

Therefore,

```text
77      100
```

The value is **77**, considerably lower than the deterministic value of **97**.

---

# Why Did the Value Decrease?

Nothing about the reward changed.

Only the certainty changed.

Although the goal still provides a reward of +100,

the agent now reaches it only **80% of the time**.

The remaining probability corresponds to less favorable outcomes.

Uncertainty therefore lowers the state's expected value.

This illustrates one of the central ideas of MDPs:

> [!important]
> State values measure **expected future reward**, not guaranteed reward.

---

# Example 4 — Updating State B3

Now consider the state below A3.

Unlike the deterministic example, multiple actions must now be evaluated.

The Bellman Backup compares the expected return of every available action before choosing the best one.

---

## Action 1 — Move North

Possible outcomes are

```text
80% → A3 (77)

10% → -100

10% → Stay (0)
```

Expected future value

$$
0.8(77)
+
0.1(-100)
+
0.1(0)
=
51.6
$$

Including the movement cost,

$$
51.6-3
=
48.6
$$

---

## Action 2 — Move West

Possible outcomes are

```text
10% → A3 (77)

80% → Stay

10% → Other state
```

Expected future value

$$
0.1(77)
=
7.7
$$

After subtracting the movement cost,

$$
7.7-3
=
4.7
$$

---

# Choosing the Better Action

The Bellman Backup compares both expected returns.

| Action | Expected Value |
|---------|---------------:|
| North | 48.6 |
| West | 4.7 |

Since

$$
48.6>4.7
$$

the update selects

```text
North
```

This demonstrates an important point.

The Bellman Backup always evaluates **all available actions** before selecting the one with the highest expected return.

---

# Why the Early Policy May Look Strange

At this stage of Value Iteration, many surrounding states still have value zero.

Only states close to the goal contain useful information.

As additional Bellman Backups are performed, these values continue to propagate through the environment.

Consequently,

- early policies may appear shortsighted,
- while later iterations produce increasingly sensible behavior.

Only after convergence does the value function correctly represent the long-term consequences of every decision.

---

# Deterministic vs Stochastic Value Iteration

Although the same Bellman Backup algorithm is used in both environments, the interpretation is very different.

| Deterministic | Stochastic |
|--------------|------------|
| One successor state | Multiple possible successors |
| Guaranteed outcome | Expected outcome |
| No transition probabilities | Transition probabilities required |
| Values depend mainly on path length | Values balance reward, risk, and uncertainty |

The deterministic case resembles shortest-path planning.

The stochastic case requires reasoning about **both probability and long-term reward**, making it a true planning-under-uncertainty problem.

---

# What These Examples Teach Us

The numerical calculations reveal several important ideas.

> [!summary]
> - Bellman Backups are local computations performed one state at a time.
> - Repeated backups gradually propagate information through the state space.
> - In deterministic environments, values primarily reflect distance from the goal.
> - In stochastic environments, values represent **expected** long-term reward.
> - Uncertainty reduces the value of risky states because favorable outcomes are no longer guaranteed.
> - The Bellman Backup always evaluates every action before selecting the one with the highest expected return.

---

# From Value Functions to Policies

## Why Values Alone Are Not Enough

After Value Iteration converges, every state has an associated value.

For example,

```text
93      97      100

89      94

85      90
```

These numbers tell us **how desirable** each state is.

However, knowing that a state has value **94** does not tell the agent what it should actually do.

A robot cannot execute a value—it must execute an **action**.

Ultimately, an intelligent agent needs to answer a different question:

> [!question]
> **"Given my current state, which action should I take?"**

This is where the concept of a **policy** becomes essential.

---

# What Is a Policy?

A **policy** specifies the action the agent should take in every possible state.

Formally, a policy is a mapping

$$
\pi : S \rightarrow A
$$

which means

> For every state $$s$$, the policy assigns one action $$a$$.

Unlike a fixed sequence of moves, a policy provides a complete decision strategy for the entire environment.

Instead of storing values, a policy stores **decisions**.

```text
State A  →  Move East

State B  →  Move North

State C  →  Move West
```

---

# How Do We Obtain the Policy?

The remarkable feature of Value Iteration is that the policy is **not computed separately**.

It is already hidden inside the Bellman Backup.

Recall the Bellman equation

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

Notice the optimization step

$$
\max_a
$$

While computing the value of a state, the algorithm has already evaluated every possible action.

Once Value Iteration finishes, we simply recover **which action produced the maximum expected value**.

This process is called **policy extraction**.

---

# Policy Extraction

The optimal policy is defined by

$$
\pi^*(s)
=
\arg\max_a
\sum_{s'}
P(s'|s,a)V^*(s')
$$

Although this equation closely resembles the Bellman equation, it answers a different question.

The Bellman equation computes

> **"How valuable is this state?"**

The policy equation asks

> **"Which action leads to the highest expected value?"**

Notice that the immediate reward and discount factor no longer appear explicitly.

Those quantities have already been incorporated into the optimal value function $$V^*(s)$$.

---

# Max vs Argmax

Students often confuse these two operations.

Understanding the distinction is crucial.

## Max

The **maximum** operator returns the largest numerical value.

Suppose the expected returns for four actions are

| Action | Expected Value |
|--------|---------------:|
| North | 48.6 |
| East | 35 |
| South | 12 |
| West | 4.7 |

Then

$$
\max = 48.6
$$

The result is a **number**.

---

## Argmax

The **argmax** operator returns the action that produced the maximum value.

Using the same example,

| Action | Expected Value |
|--------|---------------:|
| North | 48.6 |
| East | 35 |
| South | 12 |
| West | 4.7 |

we obtain

$$
\arg\max = \text{North}
$$

The result is **an action**, not a value.

> [!important]
> - $$\max$$ answers **"How good is the best option?"**
> - $$\arg\max$$ answers **"Which option is the best?"**

---

# Building the Policy

Policy extraction is performed independently for every state.

Suppose we are evaluating one particular state.

The expected returns of the available actions are

| Action | Expected Return |
|--------|----------------:|
| North | 48.6 |
| East | 35 |
| South | 12 |
| West | 4.7 |

The policy simply stores

```text
North
```

for this state.

The same procedure is repeated throughout the entire state space.

Eventually, every state has one recommended action.

---

# Visualizing a Policy

Unlike a value function, which stores numbers,

```text
85     90     94

82     87     91
```

a policy stores directions.

```text
→     →     Goal

↑     ↑

↑     ←
```

Each arrow answers a single question:

> **"If the agent finds itself here, what action should it attempt?"**

This makes policies easy to visualize, especially in Grid World problems.

---

# Why Policies Are More Robust Than Plans

Earlier, we saw why classical planning struggles in stochastic environments.

A deterministic planner produces a fixed sequence of actions.

```text
North

North

East

East
```

This sequence assumes every action succeeds exactly as expected.

If the first movement fails,

```text
Expected Position

↓

A2
```

but the agent actually reaches

```text
B1
```

the remaining plan may no longer be appropriate.

The planner has no instructions for recovering.

---

## Policies Handle Unexpected Outcomes

A policy does not depend on following one predefined path.

Instead, every reachable state already has an associated action.

For example,

```text
A1 → East

A2 → North

B1 → East

B2 → North
```

If the environment causes the agent to drift into an unexpected state, it simply consults the policy for that state and continues.

There is no need to recompute an entirely new plan.

> [!note]
> A policy acts like a navigation guide that always knows the best next move, regardless of where the agent currently is.

---

# Value Functions and Policies Work Together

The value function and policy represent two different aspects of decision making.

The **value function** evaluates states.

The **policy** selects actions.

These two concepts complement one another.

| Value Function | Policy |
|---------------|--------|
| Measures how good a state is | Specifies which action to take |
| Numerical estimate | Decision rule |
| Used during Value Iteration | Extracted after Value Iteration converges |

The value function provides the information needed to construct the policy.

The policy is the component the agent actually executes.

---

# The Complete Value Iteration Pipeline

Putting everything together, the entire planning process looks like this.

```text
Define the MDP

↓

Initialize State Values

↓

Repeated Bellman Backups

↓

Optimal Value Function

↓

Policy Extraction (argmax)

↓

Optimal Policy

↓

Agent Executes Actions
```

Notice that Value Iteration itself never directly computes actions.

It computes **state values first**.

The policy naturally follows from those values.

---

# Why This Matters

Policies solve the central challenge of planning under uncertainty.

Instead of producing one fragile action sequence, they provide a decision for every possible situation the agent might encounter.

This makes them much more suitable for real-world environments, where unexpected events occur frequently.

Whether the agent slips, encounters an obstacle, or is pushed into another state, it can immediately recover by following the policy associated with its current state.

---

# Key Takeaways

> [!summary]
> - A value function tells us **how desirable** each state is.
> - A policy tells us **which action** to take in each state.
> - Policy extraction uses
>
> $$
> \arg\max
> $$
>
> to select the action with the highest expected return.
> - $$\max$$ returns a value, whereas $$\arg\max$$ returns the action that achieves that value.
> - Policies are derived **after** Value Iteration has converged.
> - Unlike fixed action sequences, policies provide a complete decision strategy that is robust to uncertainty and unexpected outcomes.


# Designing Agent Behaviour Through Rewards

## The Reward Function Shapes Behaviour

One of the most powerful ideas in MDPs is that **the planning algorithm does not determine the agent's behaviour—the reward function does.**

The Bellman Backup, Value Iteration, and Policy Extraction remain exactly the same.

What changes is **what the agent considers desirable.**

Changing the rewards changes the optimization objective, which naturally changes the optimal policy.

> [!important]
> **Same environment + same transition model + different rewards = different optimal behaviour**

This is one reason MDPs are so flexible: the same planning algorithm can solve very different problems simply by redefining the reward function.

---

# Case 1 — Moderate Step Cost

Suppose every ordinary move has a cost of

$$
-3
$$

while the terminal rewards remain

- Goal: $$+100$$
- Bad terminal: $$-100$$

This is the Grid World used throughout most of the lecture.

---

## Behaviour

Every extra step slightly reduces the total reward.

Consequently, the agent tries to:

- reach the goal reasonably quickly,
- avoid unnecessary wandering,
- but still avoid obviously dangerous regions.

The resulting policy reflects a **trade-off** between two competing objectives:

- minimizing travel cost,
- minimizing risk.

Neither objective dominates completely.

> [!note]
> Moderate step costs often produce realistic behaviour because they balance **efficiency** and **safety**.

---

# Case 2 — No Step Cost

Now suppose moving has **zero cost**.

Normal states receive

$$
0
$$

instead of

$$
-3.
$$

The terminal rewards remain unchanged.

---

## Behaviour Changes

Without any penalty for movement,

time no longer matters.

The agent has no reason to prefer a shorter path over a longer one.

Instead, it focuses entirely on maximizing the probability of eventually reaching the positive terminal.

This often produces surprisingly cautious behaviour.

Near dangerous regions, the optimal policy may deliberately move **away** from the goal before approaching it from a safer direction.

Although this requires more steps, those extra steps are now free.

---

## Why Do Many State Values Become Large?

If movement is free and the goal is always eventually reachable,

the expected long-term reward for many states approaches the goal reward.

Intuitively,

the agent can simply keep trying until it succeeds.

Since repeated attempts carry no penalty,

there is little disadvantage to taking extremely conservative routes.

> [!tip]
> Removing the step cost encourages the agent to optimize **success probability** rather than **speed**.

---

# Case 3 — Extremely Large Step Cost

Now consider the opposite extreme.

Suppose every move costs

$$
-200.
$$

This penalty is larger than the negative terminal reward itself.

---

## A Counterintuitive Policy

At first glance,

one might expect the agent to work even harder to reach the goal.

Instead, the opposite happens.

The cost of continuing becomes so severe that **ending the episode quickly** becomes more valuable than pursuing the positive reward.

This illustrates an important principle:

> [!warning]
> An optimal policy does **not** necessarily try to reach the goal. It tries to maximize **expected cumulative reward**.

If continuing incurs extremely large penalties, terminating early—even in a bad state—may produce a higher total return.

---

## Example

Suppose the agent has two options.

### Continue toward the goal

Five additional steps cost

$$
5\times(-200)
=
-1000
$$

followed by the goal reward

$$
+100.
$$

Total return

$$
-900.
$$

---

### Enter the negative terminal immediately

Reward

$$
-100.
$$

Since

$$
-100>-900,
$$

terminating immediately is actually the better decision.

The behaviour appears irrational only if we forget the optimization objective.

The agent is **not maximizing goal achievement**.

It is maximizing **expected return**.

---

# Reward Engineering

These examples illustrate a broader idea that appears throughout AI and Reinforcement Learning.

Small changes to the reward function can produce dramatically different behaviours.

This process is often called **reward engineering** or **reward design**.

The planner itself remains unchanged.

Instead, designers specify what outcomes should be encouraged or discouraged through rewards.

Examples include:

| Desired Behaviour | Reward Design |
|-------------------|---------------|
| Fast navigation | Larger step costs |
| Safe navigation | Strong penalties for dangerous states |
| Energy-efficient robot | Penalty for expensive actions |
| Risk-taking behaviour | Smaller penalties for failure |

Designing an effective reward function is often one of the hardest parts of solving real-world decision problems.

---

# Comparing the Three Reward Structures

| Step Cost | Behaviour |
|-----------|-----------|
| Moderate negative cost | Balance efficiency and safety |
| Zero cost | Prioritize safety; long detours become acceptable |
| Very large negative cost | End the episode quickly to avoid accumulating penalties |

Although the environment never changes, the agent's behaviour changes dramatically because its notion of **optimality** has changed.

---

# Key Insight

> [!summary]
> The reward function defines **what the agent is trying to achieve**, while the planning algorithm determines **how to achieve it optimally**.

---

# Lecture Summary

This lecture introduced **Markov Decision Processes (MDPs)** as a framework for planning under uncertainty.

Unlike classical search algorithms, MDPs explicitly model environments where actions may have multiple possible outcomes.

Rather than producing a single fixed plan, an MDP computes a policy that specifies the best action for every state.

---

# Core Components of an MDP

An MDP is defined by four interacting components.

| Component | Role |
|-----------|------|
| **States** | Describe the agent's current situation |
| **Actions** | Choices available to the agent |
| **Transition Model** | Specifies the probability of moving between states |
| **Reward Function** | Defines the objective the agent should optimize |

Together, these components fully describe the decision-making problem.

---

# The Planning Objective

The agent seeks a policy that maximizes expected discounted return

$$
\max_\pi
E\left[
\sum_{t=0}^{\infty}
\gamma^tR_t
\right].
$$

This objective combines four important ideas:

- immediate rewards,
- future rewards,
- uncertainty,
- and discounting.

---

# Value Iteration

Value Iteration solves this optimization problem using dynamic programming.

Instead of reasoning about complete action sequences, it repeatedly updates the value of every state using the Bellman Backup.

Each iteration improves the estimates until they converge to the optimal value function.

A useful way to think about this process is that information gradually propagates outward from important states, allowing every location in the environment to estimate its long-term desirability.

---

# From Values to Decisions

Once optimal state values are known,

determining the best action becomes straightforward.

For every state, the agent simply chooses the action whose expected successor value is highest.

Thus,

```text
Optimal Value Function

↓

Policy Extraction

↓

Optimal Policy
```

The policy is therefore a direct consequence of the value function.

---

# Why MDPs Extend Classical Planning

Classical search algorithms assume that actions always succeed.

MDPs remove this assumption by incorporating probabilities directly into the planning process.

| Classical Planning | Markov Decision Process |
|-------------------|-------------------------|
| Deterministic actions | Stochastic actions |
| Single action sequence | Policy for every state |
| No uncertainty | Explicit probabilistic transitions |
| Fixed execution | Adaptive decision making |

This makes MDPs far better suited to real-world environments where uncertainty is unavoidable.

---

# Where MDPs Are Used

Many sequential decision-making problems can naturally be modeled as MDPs.

Examples include:

- robot navigation,
- autonomous vehicles,
- medical treatment planning,
- inventory management,
- financial decision making,
- recommendation systems,
- dialogue systems.

MDPs also provide the mathematical foundation for **Reinforcement Learning**, where the transition model or reward function is no longer known in advance and must be learned through interaction.

---

# Big Picture

> [!summary]
> Markov Decision Processes extend classical planning by combining **planning**, **probability**, and **optimization** into a single framework.
>
> - The **transition model** captures uncertainty.
> - The **reward function** specifies the objective.
> - **Value Iteration** estimates long-term utility.
> - **Policy extraction** converts those values into actions.
>
> Together, these ideas allow intelligent agents to make rational decisions even when the outcome of every action is uncertain.

# Partial Observability and POMDPs

## When MDPs Are No Longer Enough

Throughout this lecture, we assumed that the agent always knows **exactly which state it is in**.

This assumption is known as **full observability**, and it is one of the defining assumptions of a Markov Decision Process (MDP).

However, many real-world environments violate this assumption.

Examples include:

- A robot navigating with noisy sensors.
- A self-driving car whose cameras are temporarily blocked.
- A doctor diagnosing a patient using imperfect test results.
- A search-and-rescue robot exploring an unfamiliar building.

In these situations, the agent must make decisions **without knowing the true state of the world**.

---

# Full Observability vs Partial Observability

The difference between MDPs and POMDPs is **not uncertainty in actions**.

Both models already allow actions to have probabilistic outcomes.

The difference lies in **uncertainty about the current state**.

| MDP | POMDP |
|------|--------|
| Agent knows the current state exactly | Agent is uncertain about the current state |
| Plans in state space | Plans in belief space |
| No need to gather information | Information gathering becomes valuable |

> [!important]
> **MDPs model uncertainty about what will happen next.**
>
> **POMDPs additionally model uncertainty about where the agent currently is (or what the world currently looks like).**

---

# Why Information Can Have Value

In an MDP,

the current state is already known.

Therefore, there is never any reason to perform an action whose sole purpose is to gain information.

Every action is evaluated only by the rewards it eventually produces.

In many real-world problems, however, information itself has value.

Consider searching for your car keys.

Before driving to work, you may first search the house.

Searching does not directly achieve the goal of arriving at work.

Instead, it reduces uncertainty and allows better decisions afterward.

This kind of reasoning cannot be represented naturally using an ordinary MDP.

---

# The Maze Example

Sebastian Thrun illustrates this idea using a simple maze.

```text
              Exit
            (+100 or -100)

                 |

Start -------- Junction

                 |

               Sign

                 |

              Exit
            (-100 or +100)
```

The robot knows its physical location throughout the task.

What it **does not know** is which exit contains the positive reward.

The sign reveals this hidden information.

---

# The Optimal Behaviour

A purely reward-seeking agent might immediately choose an exit.

Unfortunately, without reading the sign, it is essentially guessing.

A better strategy is

```text
Start

↓

Read the sign

↓

Return to the junction

↓

Choose the correct exit
```

Notice that the first action does **not** move the robot closer to the reward.

Instead, it increases the robot's knowledge about the environment.

This demonstrates one of the defining ideas of POMDPs:

> Sometimes an action is valuable because it improves future decisions rather than producing an immediate reward.

---

# Belief States

Since the true state is unknown, the agent cannot plan directly in physical state space.

Instead, it maintains a **belief state**.

A belief state is a probability distribution over all possible world states.

Initially, the robot might believe

```text
50%  Left exit is good

50%  Right exit is good
```

After reading the sign,

the belief changes to

```text
100%  Left exit is good
```

or

```text
100%  Right exit is good
```

The environment itself has not changed.

Only the agent's **knowledge** has changed.

---

# Planning in Belief Space

A POMDP transforms an uncertain planning problem into planning over belief states.

Instead of asking

> "Which physical state am I in?"

the agent asks

> "Given everything I have observed so far, what do I currently believe about the world?"

Each action now affects two things:

- the physical world,
- the agent's knowledge.

This makes planning considerably richer than in an MDP.

---

# Relationship to Value Iteration

One elegant aspect of POMDPs is that many of the same dynamic programming ideas still apply.

Instead of computing values for physical states,

algorithms compute values for **belief states**.

Conceptually,

```text
MDP

Physical States

↓

Value Function

↓

Optimal Policy
```

becomes

```text
POMDP

Belief States

↓

Value Function over Beliefs

↓

Optimal Policy
```

The underlying idea remains the same:

choose actions that maximize expected long-term return.

The difference is that uncertainty about the world is now explicitly represented inside the state itself.

---

# The Progression of Planning Methods

This lecture illustrates how planning becomes progressively more realistic.

| Framework | Main Assumption | Main Challenge |
|-----------|-----------------|----------------|
| Classical Planning | Actions are deterministic | Find a sequence of actions |
| MDP | Actions are stochastic | Optimize decisions under uncertainty |
| POMDP | State is partially observable | Act while simultaneously gathering information |
| Reinforcement Learning | Model is unknown | Learn the optimal behaviour through interaction |

Each framework extends the previous one by relaxing another simplifying assumption.

---

# Why POMDPs Matter

Many real-world AI systems must reason under **both action uncertainty and incomplete information**.

Examples include:

- Autonomous robots with noisy sensors.
- Self-driving vehicles operating in poor visibility.
- Medical diagnosis under uncertain test results.
- Human-robot interaction.
- Dialogue systems reasoning about user intent.
- Search-and-rescue missions in unknown environments.

In these problems, acting optimally requires balancing three competing objectives:

- maximizing reward,
- minimizing risk,
- reducing uncertainty.

# Big Picture

> [!summary]
> Classical planning assumes **certainty**.
>
> MDPs introduce **uncertain actions**.
>
> POMDPs additionally introduce **uncertain knowledge**.
>
> This progression moves AI closer to how intelligent agents must operate in the real world, where both actions and observations are imperfect.

---

# Final Takeaway

Planning under uncertainty is not simply about finding a path to a goal.

An intelligent agent must decide

- **what action to perform,**
- **how future outcomes might unfold,**
- **how uncertain its current knowledge is,**
- and **whether gathering more information is worth the cost.**

This progression—from deterministic planning, to MDPs, to POMDPs—provides the conceptual foundation for modern robotics, autonomous systems, and reinforcement learning.