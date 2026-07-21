

Now that we understand the **structure of a Hidden Markov Model (HMM)**—hidden states, observations, transition probabilities, emission probabilities, and the Markov assumptions—the next question is:

> **How do we actually use an HMM?**

Simply defining an HMM does not solve any practical problem. We need efficient algorithms that allow us to perform inference on the model.

The three fundamental computational problems of Hidden Markov Models were formalized by **Lawrence Rabiner (1989)**, and each is solved by a specialized dynamic programming algorithm:

| Problem        | Question                                             | Algorithm                                    |
| -------------- | ---------------------------------------------------- | -------------------------------------------- |
| **Evaluation** | *How likely is an observed sequence?*                | Forward Algorithm                            |
| **Decoding**   | *What is the most likely hidden state sequence?*     | Viterbi Algorithm                            |
| **Learning**   | *How do we estimate the model parameters from data?* | Baum–Welch Algorithm (Forward–Backward / EM) |

These algorithms are the backbone of HMMs and transformed them into practical tools for applications such as **speech recognition, handwriting recognition, natural language processing, bioinformatics, gesture recognition, robotics, and time-series analysis**.

In the following sections, we study each algorithm in detail, beginning with the **Forward Algorithm**, which efficiently computes the probability of an observation sequence under a given HMM.

## Forward Algorithm

> [!info]
> The **Forward Algorithm** is a dynamic programming algorithm used to efficiently compute the probability that a Hidden Markov Model (HMM) generated a given observation sequence.
>
> Instead of enumerating every possible hidden state sequence (which grows exponentially), it recursively combines partial probabilities, reducing the computation to polynomial time.

### Goal

Given:

- Observation sequence:
  $$O=(o_1,o_2,\ldots,o_T)$$

- Hidden Markov Model:
  $$\lambda=(A,B,\pi)$$

Compute:

$$
P(O \mid \lambda)
$$

which is the probability of observing the sequence $O$ under the model.


## Why is it Needed?

A sequence of length $T$ with $N$ hidden states has

$$
N^T
$$

possible hidden-state paths.

Brute-force computation would require summing over all of them:

$$
P(O|\lambda)=\sum_{Q} P(O,Q|\lambda)
$$

where $Q$ is every possible hidden-state sequence.

This quickly becomes computationally impossible.

The **Forward Algorithm** avoids this exponential explosion using **dynamic programming**.

## Forward Variable

The core quantity is the **forward variable**:

$$
\alpha_t(i)
=
P(o_1,o_2,\ldots,o_t,\; q_t=S_i \mid \lambda)
$$

It represents:

> The probability of observing the first $t$ observations **and** ending in state $S_i$ at time $t$.

Each forward probability summarizes all possible paths that could have reached that state.


## Algorithm Steps

### Step 1 — Initialization

For every state $S_i$:

$$
\alpha_1(i)
=
\pi_i\, b_i(o_1)
$$

where

- $\pi_i$ = initial probability of state $S_i$
- $b_i(o_1)$ = probability of observing $o_1$ in state $S_i$

---

### Step 2 — Recursion

For each time step:

$$
\alpha_{t+1}(j)
=
\left(
\sum_{i=1}^{N}
\alpha_t(i)a_{ij}
\right)
b_j(o_{t+1})
$$

Interpretation:

1. Collect probability from every previous state.
2. Transition into state $j$.
3. Emit the next observation.

---

### Step 3 — Termination

The total probability of the observation sequence is

$$
P(O|\lambda)
=
\sum_{i=1}^{N}
\alpha_T(i)
$$

Simply add the probabilities of ending in every possible final state.

## Dynamic Programming Intuition

Instead of remembering every possible path,

```
State A
        \
         \
          → State C
         /
State B
```

the algorithm stores only

- probability of reaching **State A**
- probability of reaching **State B**

When computing **State C**, those probabilities are reused.

No path is recomputed.


## Complexity

Without Forward Algorithm:

$$
O(N^T)
$$

With Forward Algorithm:

$$
O(N^2T)
$$

This reduction is what makes HMMs practical.


## Intuition

Imagine predicting today's weather.

To estimate today's probability, you don't need to remember **every possible weather history**.

Instead, you only need:

- probability of yesterday being Sunny
- probability of yesterday being Rainy

From those, today's probabilities can be computed directly.

The Forward Algorithm follows exactly this principle.


## Key Takeaways

- Computes the likelihood of an observation sequence:
  $$P(O|\lambda)$$
- Uses **dynamic programming**.
- Avoids enumerating all hidden-state paths.
- Runs in **$O(N^2T)$** time instead of **$O(N^T)$**.
- Forms the basis for **HMM inference** and is used in algorithms such as **Baum–Welch (EM)** for HMM training.
---

# Viterbi Algorithm

> [!info]
> The **Viterbi Algorithm** is a dynamic programming algorithm used to determine the **single most likely sequence of hidden states** that produced a given sequence of observations in a Hidden Markov Model (HMM).
>
> While the **Forward Algorithm** answers **"How likely is this observation sequence?"**, the **Viterbi Algorithm** answers **"What hidden state sequence most likely generated these observations?"**


## Goal

Given:

- Observation sequence:

$$
O=(o_1,o_2,\ldots,o_T)
$$

- Hidden Markov Model:

$$
\lambda=(A,B,\pi)
$$

Find the most likely hidden-state sequence:

$$
Q^*=(q_1,q_2,\ldots,q_T)
$$

that maximizes

$$
P(Q|O,\lambda)
$$

or equivalently,

$$
Q^*
=
\arg\max_Q
P(O,Q|\lambda)
$$


## Why is it Needed?

Suppose we observe

```text
Umbrella
Umbrella
Sunglasses
```

Many hidden weather sequences could have produced these observations.

For example:

```
Rainy → Rainy → Sunny
```

or

```
Cloudy → Rainy → Sunny
```

or

```
Rainy → Cloudy → Sunny
```

The Viterbi Algorithm efficiently determines **which hidden-state sequence is the most probable**.

## Brute Force Approach

With

- $N$ hidden states
- sequence length $T$

there are

$$
N^T
$$

possible state sequences.

Evaluating every sequence quickly becomes computationally infeasible.

The Viterbi Algorithm solves this using **dynamic programming**.


## Viterbi Variable

The core quantity is

$$
\delta_t(i)
=
\max_{q_1,\ldots,q_{t-1}}
P(q_1,\ldots,q_{t-1},q_t=S_i,
o_1,\ldots,o_t|\lambda)
$$

It represents:

> The probability of the **most likely path** ending in state $S_i$ after observing the first $t$ observations.

Unlike the Forward Algorithm, which **sums** over all possible paths, Viterbi keeps **only the best path**.


## Algorithm Steps

### Step 1 — Initialization

For every state

$$
S_i
$$

compute

$$
\delta_1(i)
=
\pi_i\,b_i(o_1)
$$

Initialize the backpointer

$$
\psi_1(i)=0
$$

---

### Step 2 — Recursion

For every state

$$
S_j
$$

compute

$$
\delta_t(j)
=
\max_i
\left[
\delta_{t-1}(i)
a_{ij}
\right]
b_j(o_t)
$$

At the same time, record which previous state produced the maximum:

$$
\psi_t(j)
=
\arg\max_i
\left[
\delta_{t-1}(i)
a_{ij}
\right]
$$

The **backpointer** stores the optimal predecessor for each state.

---

### Step 3 — Termination

Find the probability of the best path:

$$
P^*
=
\max_i
\delta_T(i)
$$

Determine the final hidden state:

$$
q_T^*
=
\arg\max_i
\delta_T(i)
$$

---

### Step 4 — Backtracking

Recover the remaining hidden states using the stored backpointers:

$$
q_t^*
=
\psi_{t+1}(q_{t+1}^*)
$$

Repeat until the beginning of the sequence.

## Dynamic Programming Intuition

Instead of exploring every possible path,

```
State A
         \
          \
           → State C
          /
State B
```

the algorithm keeps only

- the **best path to State A**
- the **best path to State B**

When computing **State C**, only those optimal partial paths are considered.

All inferior paths are discarded.

## Forward vs Viterbi

| Forward Algorithm | Viterbi Algorithm |
|-------------------|------------------|
| Computes total probability of observations | Computes the most likely hidden-state sequence |
| Adds probabilities | Takes the maximum probability |
| Sums over all paths | Keeps only the best path |
| Uses $\alpha_t(i)$ | Uses $\delta_t(i)$ |


## Complexity

Without Viterbi:

$$
O(N^T)
$$

With Viterbi:

$$
O(N^2T)
$$

This dramatic reduction makes decoding practical even for long observation sequences.


## Intuition

Imagine navigating through a maze.

At each intersection there may be many possible routes.

Rather than remembering **every route**, you only keep the **best route** leading to each intersection.

By the time you reach the end, you can reconstruct the overall best path simply by following the stored backpointers.

The Viterbi Algorithm applies this same idea to Hidden Markov Models.


## Applications

The Viterbi Algorithm has been widely used in:

- Speech recognition
- Handwriting recognition
- DNA and gene sequence analysis
- Robot localization
- Natural language processing
- Activity recognition
- Time-series analysis


## Key Takeaways

> [!summary]
>
> - The **Viterbi Algorithm** solves the **Decoding Problem** in Hidden Markov Models.
> - It finds the **single most likely hidden-state sequence** that generated an observation sequence.
> - Uses **dynamic programming** to avoid evaluating every possible path.
> - Maintains the **best path** to each state using the Viterbi variable $\delta_t(i)$.
> - Stores **backpointers** to reconstruct the optimal state sequence.
> - Runs in **$O(N^2T)$** time instead of **$O(N^T)$**.
> - Unlike the Forward Algorithm, which computes sequence probability, Viterbi computes the **most probable hidden path**.

Next: [[Inference Algorithms for Hidden Markov Models]]