
> [!insight] 
> Bayes' Theorem tells us how to **reverse conditional probabilities**.
>
> Instead of asking
>
> > "What is the probability of observing evidence if a hypothesis is true?"
>
> it answers
>
> > "Given the evidence, how likely is the hypothesis?"

---

# Motivation

Suppose a medical test is positive.

We naturally ask

> **What is the probability that the patient actually has the disease?**

However,

the test accuracy usually tells us something different:

> Probability of a positive test **given** the disease.

That is

$$
P(\text{Positive}|\text{Disease})
$$

But what we actually want is

$$
P(\text{Disease}|\text{Positive})
$$

Bayes' theorem allows us to reverse these probabilities.

---

# Partition of a Sample Space

Bayes' theorem assumes that the possible causes form a **partition** of the sample space.

A collection of events

$$
E_1,E_2,\ldots,E_n
$$

forms a partition if

### 1. They are mutually exclusive

$$
E_i\cap E_j=\varnothing
\qquad (i\neq j)
$$

---

### 2. They are exhaustive

$$
E_1\cup E_2\cup\cdots\cup E_n=S
$$

---

### 3. Each has positive probability

$$
P(E_i)>0
$$


## Intuition

Exactly **one** of these events must be true.

Examples

- Which machine produced a product?
- Which disease caused the symptoms?
- Which email class generated this message?
- Which digit was written?

---

# Total Probability Theorem

Before Bayes' theorem comes the **Theorem of Total Probability**.

Suppose

$$
E_1,E_2,\ldots,E_n
$$

form a partition.

Then

$$
P(A)
=
\sum_{i=1}^{n}
P(E_i)P(A|E_i)
$$


## Interpretation

Overall probability

=

Probability through Cause 1

+

Probability through Cause 2

+

...

---

Think of every possible path that can produce event A.

```
Cause 1 → A

Cause 2 → A

Cause 3 → A

...

Add all paths together.
```

---

# Why It Matters

Many real-world events can occur through multiple causes.

Examples

Disease

↓

Positive Test

or

Factory A

↓

Defective Bolt

or

Weather

↓

Late Arrival

The Total Probability Theorem computes the overall probability by adding contributions from every possible cause.

---

# Bayes' Theorem

Using

- Conditional Probability
- Multiplication Rule
- Total Probability

we obtain

$$
P(E_i|A)
=
\frac{
P(E_i)P(A|E_i)
}{
\sum_{j=1}^{n}
P(E_j)P(A|E_j)
}
$$

---

# Understanding the Formula

Numerator

$$
P(E_i)P(A|E_i)
$$

=

Probability that

- hypothesis was true

AND

- evidence occurred.

---

Denominator

$$
P(A)
$$

=

Overall probability of observing the evidence.

It acts as a normalization factor.

---

# Standard AI Form

In Machine Learning,

Bayes' theorem is usually written as

$$
P(H|E)
=
\frac{
P(H)P(E|H)
}{
P(E)
}
$$

where

- \(H\) = Hypothesis
- \(E\) = Evidence

---

# Terminology

| Name | Meaning |
|-------|---------|
| Prior | \(P(H)\) |
| Likelihood | \(P(E|H)\) |
| Evidence | \(P(E)\) |
| Posterior | \(P(H|E)\) |


## Prior

Initial belief before seeing evidence.

Example

Probability a patient has a disease.

## Likelihood

Probability of observing the evidence assuming the hypothesis is true.

## Posterior

Updated belief after observing evidence.

This is the quantity Bayes' theorem computes.

---

# Bayesian Updating

Bayes' theorem can be summarized as

$$
\boxed{
\text{Posterior}
=
\frac{
\text{Prior}
\times
\text{Likelihood}
}{
\text{Evidence}
}
}
$$

This process is called **Bayesian Updating**.

New evidence changes our belief.

---

# Example 1 (Bags)

Bag I

- 3 Red
- 4 Black

Bag II

- 5 Red
- 6 Black

A red ball is drawn.

Find

$$
P(\text{Bag II}|\text{Red})
$$

Using Bayes' theorem,

$$
P(\text{Bag II}|\text{Red})
=
\frac{
\frac12\times\frac5{11}
}{
\frac12\times\frac37+
\frac12\times\frac5{11}
}
=
\frac{35}{68}
$$

---

# Example 2 (Medical Testing)

Disease prevalence

$$
0.1\%
$$

Test sensitivity

$$
90\%
$$

False positive rate

$$
1\%
$$

Bayes' theorem gives

$$
P(\text{Disease}|\text{Positive})
\approx0.083
$$

Although the test is accurate,

most positive tests are false positives because the disease is very rare.

This illustrates the importance of considering the **prior probability**.

---

# Example 3 (Factory)

Three machines manufacture bolts.

A defective bolt is selected.

Bayes' theorem determines the probability that the bolt came from each machine.

This is a classic **reverse inference** problem.

---

# Why Bayes' Theorem Matters

Bayes' theorem is the mathematical foundation of reasoning under uncertainty.

Instead of treating probabilities as fixed,

it allows beliefs to be updated whenever new evidence becomes available.

---

# AI Connection

Bayes' theorem appears throughout Artificial Intelligence.

Applications include

- Naive Bayes Classifier
- Bayesian Networks
- Hidden Markov Models
- Robot Localization
- Medical Diagnosis
- Spam Filtering
- Speech Recognition
- Probabilistic Robotics
- Reinforcement Learning
- Generative AI

---

# Key Takeaways

- Bayes' theorem reverses conditional probabilities.
- The Total Probability Theorem computes the denominator.
- Posterior = Prior × Likelihood ÷ Evidence.
- Every Bayesian model ultimately performs belief updating using this theorem.

Source: NCERT Grade XII