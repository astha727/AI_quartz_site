
> [!quote]
> *"Probability tells us how likely something is. Conditional probability tells us how that likelihood changes when new information becomes available."*

## Prerequisites

Before studying this topic, review:

- [[3 - Probability]]
- [[1 - Combination and Permutation]]
- [[2 - Binomial Theorem]]

---

# Why Conditional Probability?

In many real-world situations, we gain **additional information** before making a decision.

This new information changes the probability of an event.

For example:

> What is the probability of drawing an Ace?

is different from

> What is the probability of drawing an Ace **given that the card is a Spade?**

The second question restricts the possible outcomes.

This idea is called **Conditional Probability**.

## Motivation

Suppose an AI system is diagnosing diseases.

Initially,

$$
P(\text{Flu})
$$

may be low.

After learning that the patient has

- fever
- sore throat

the probability changes to

$$
P(\text{Flu} \mid \text{Fever})
$$

The diagnosis becomes more accurate because of new evidence.

Conditional probability is therefore the foundation of probabilistic reasoning.

---

# Intuition

Imagine tossing three fair coins.

The sample space is

$$
S=
\{
HHH,
HHT,
HTH,
THH,
HTT,
THT,
TTH,
TTT
\}
$$

Let

- **E** = At least two heads
- **F** = First toss is Tail

Originally,

$$
P(E)=\frac48=\frac12
$$

Now suppose someone tells us

> The first toss was Tail.

The sample space immediately becomes

$$
F=
\{
THH,
THT,
TTH,
TTT
\}
$$

Instead of considering 8 possibilities, we now consider only 4.

Among these,

only

$$
THH
$$

belongs to event **E**.

Therefore,

$$
P(E|F)=\frac14
$$


> [!important]
> Conditional probability **reduces the sample space**.

Instead of looking at every possible outcome, we only consider outcomes where the given condition is true.

---

# Definition

If

- \(E\) and \(F\) are events
- $P(F)\neq0$

then

$$
P(E|F)
=
\frac{P(E\cap F)}
{P(F)}
$$

where

- \(P(E|F)\) = Probability of **E given F**
- $P(E\cap F)$ = Probability that both events occur.
- \(P(F)\) = Probability that the condition occurs

## Counting Form

When all outcomes are equally likely,

$$
P(E|F)
=
\frac{n(E\cap F)}
{n(F)}
$$

where

- $n(E\cap F)$ = favourable outcomes
- $n(F)$ = possible outcomes after conditioning

---

# Visual Interpretation

Originally

```text
Entire Sample Space

+-----------------------------+
|                                                     |
|        F                                           |
|     +-----------+                        |
|     |                      |                        |
|     |       E ∩ F       |                        |
|     |                      |                         |
|     +-----------+                          |
|                                                       |
+-----------------------------+
```

After learning that **F occurred**, everything outside **F** is ignored.

```text
New Sample Space = F

+------------------+
|                                  |
|             E ∩ F             |
|                                  |
+------------------+
```

Conditional probability asks

> Inside **F**, what fraction also belongs to **E**?


# Properties

## 1. Entire Sample Space

$$
P(S|F)=1
$$


## 2. Given Event

$$
P(F|F)=1
$$


## 3. Complement Rule

$$
P(E^c|F)
=
1-P(E|F)
$$


## 4. Addition Rule

$$
P((A\cup B)|F)
=
P(A|F)
+
P(B|F)
-
P((A\cap B)|F)
$$

If A and B are mutually exclusive,

$$
P((A\cup B)|F)
=
P(A|F)
+
P(B|F)
$$


# Worked Examples

## Example 1

Given

$$
P(A)=\frac7{13}
$$

$$
P(B)=\frac9{13}
$$

$$
P(A\cap B)=\frac4{13}
$$

Find

$$
P(A|B)
$$

### Solution

$$
P(A|B)
=
\frac{P(A\cap B)}
{P(B)}
$$

$$
=
\frac{4/13}{9/13}
=
\frac49
$$


## Example 2

A family has two children.

Find the probability that **both are boys**, given that **at least one is a boy**.

Sample Space

$$
\{
BB,
BG,
GB,
GG
\}
$$

Given

$$
\{
BB,
BG,
GB
\}
$$

Only one favourable outcome remains.

Therefore,

$$
P
=
\frac13
$$


## Example 3

Ten cards numbered

$$
1-10
$$

Given that the chosen card is greater than 3,

find the probability that it is even.

Reduced sample space

$$
\{
4,5,6,7,8,9,10
\}
$$

Even numbers

$$
\{
4,6,8,10
\}
$$

Therefore,

$$
P=\frac47
$$

---

# Common Mistakes

> [!warning]

**Mistake 1**

Using the original sample space after information has been given.

Always reduce the sample space first.

---

**Mistake 2**

Using

$$
\frac{P(E)}
{P(F)}
$$

instead of

$$
\frac{P(E\cap F)}
{P(F)}
$$

---

**Mistake 3**

Forgetting that

$$
P(F)\neq0
$$

must hold.

---

# Relationship to Other Probability Topics

Conditional probability leads directly to

```text
Conditional Probability
        │
        ▼
Multiplication Rule
        │
        ▼
Total Probability
        │
        ▼
Bayes' Theorem
        │
        ▼
Bayesian Networks
        │
        ▼
Probabilistic AI
```

---

# Connection to AI

Conditional probability is one of the most important ideas in Artificial Intelligence.

It appears in

- Bayesian Networks
- Naive Bayes Classifiers
- Hidden Markov Models
- Medical Diagnosis
- Robotics
- Speech Recognition
- Natural Language Processing
- Reinforcement Learning
- Probabilistic Graphical Models

Almost every probabilistic AI algorithm begins with

$$
P(E|F)
=
\frac{P(E\cap F)}
{P(F)}
$$

> [!summary]
>- Conditional probability updates probability after new information is known.
>- The sample space becomes smaller.
>- Formula
>$$
>P(E|F)
>=
>\frac{P(E\cap F)}
>{P(F)}
>$$
>- Foundation for Bayes' Theorem.
>- Essential for modern AI and Machine Learning.

