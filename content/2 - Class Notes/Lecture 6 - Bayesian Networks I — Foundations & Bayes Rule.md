# Introduction to Bayesian Networks

## Overview

Bayesian Networks (or **Bayes Nets**) are one of the most important probabilistic models in Artificial Intelligence.

Instead of representing one enormous probability table for every variable, a Bayes Network represents:

- uncertain variables,
- how they influence one another,
- and how probabilities can be computed efficiently.

The power of Bayes Networks lies in combining **probability theory** with a **graphical structure**, allowing complex uncertain systems to be represented compactly.

> Sebastian Thrun describes Bayes Networks as one of the greatest accomplishments in AI because they combine uncertainty with efficient graphical representations instead of treating probabilities as a large "mumble jumble."

---

# Prerequisites

Before studying Bayes Networks, review:

- [[3 - Probability]]
- [[4 - Conditional Porbability]]
- [[6 - Bayes' Theorem]]

Also, for additional background refer:
- [[MIT 6.034 Lecture 21 - Probabilistic Reasoning]]

Bayesian Networks repeatedly use conditional probability and Bayes' theorem to reason about uncertain events.

---

# The Simplest Bayesian Network

Consider the following situation.

A patient may or may not have cancer.

Unfortunately, **cancer cannot be directly observed**.

Instead, we perform a medical test.

```
Cancer ─────► Test Result
```

The network contains two variables.

- **Cancer (C)** — hidden (unobservable)
- **Test Result (T)** — observable

The arrow points from **Cancer** to **Test Result** because:

> Whether someone has cancer influences the outcome of the medical test.

The direction of the arrow represents a **causal relationship**, not merely a correlation.

---

# Hidden vs Observable Variables

In many AI problems, the quantity we truly care about cannot be observed directly.

Instead, we observe evidence produced by that hidden variable.

| Variable    | Observable? |
| ----------- | ----------- |
| Cancer      | ❌ No        |
| Test Result | ✅ Yes       |

This idea appears repeatedly in AI.

Examples include:

| Hidden Variable | Observable Evidence |
|-----------------|--------------------|
| Disease | Medical test |
| Weather | Wet grass |
| Spam email | Words inside the email |
| Robot position | Sensor readings |

---

# What Information Defines This Network?

The graph itself is **not enough**.

We must also know the probabilities.

For this simple network we require two types of probabilities.

## 1. Prior Probability

The probability that cancer exists before seeing any evidence.

$$
P(C)
$$

This is called the **prior probability**.

Because there are only two possibilities,

- Cancer
- No Cancer

we automatically know

$$
P(\neg C)=1-P(C)
$$

where $\neg C$ means "not cancer."

## 2. Conditional Probability

Next we need the probability of different test results given the patient's condition.

Specifically,

$$
P(T|C)
$$

and

$$
P(T|\neg C)
$$

These tell us:

- how likely the test is positive if cancer exists,
- how likely the test is positive if cancer does not exist.

Since probabilities sum to one,

$$
P(\neg T|C)=1-P(T|C)
$$

and

$$
P(\neg T|\neg C)=1-P(T|\neg C)
$$

---

# Diagnostic Reasoning

The probabilities above describe **causal reasoning**.

Cause

↓

Effect

```
Cancer
   │
   ▼
Test Result
```

This is straightforward because we know

$$
P(T|C)
$$

However, doctors usually want the reverse question.

> The test is positive.
>
> What is the probability the patient actually has cancer?

Mathematically,

$$
P(C|T)
$$

This is called **diagnostic reasoning**.

Instead of predicting the test result from the disease,

we infer the disease from the observed evidence.

This is exactly the problem solved by [[Bayes' Theorem]].

---

# Bayes Network Representation

A Bayesian Network consists of two components.

## 1. Graph Structure

Shows which variables influence other variables.

Example:

```
Cancer ─────► Test Result
```


## 2. Probability Tables

Each node stores probabilities.

For this network we need

- Prior probability

$$
P(C)
$$

- Conditional probabilities

$$
P(T|C)
$$

and

$$
P(T|\neg C)
$$

Together, these completely define the probability distribution represented by the network.

---

# How Many Parameters Are Needed?

A natural question is:

> How many numerical probabilities must we specify?

At first it may seem like we need many probabilities.

However, only **three independent parameters** are required.

### Parameter 1

The prior probability

$$
P(C)
$$

Since

$$
P(\neg C)=1-P(C)
$$

we do **not** need to specify the complement separately.

---

### Parameter 2

The conditional probability

$$
P(T|C)
$$

From this we automatically obtain

$$
P(\neg T|C)=1-P(T|C)
$$

---

### Parameter 3

The conditional probability

$$
P(T|\neg C)
$$

Again,

$$
P(\neg T|\neg C)=1-P(T|\neg C)
$$

Therefore, the entire Bayesian Network is completely specified using only **three independent numerical parameters**.

---

# Why This Is Efficient

Without exploiting relationships between variables, we would need to specify every possible joint probability.

Bayesian Networks avoid this by storing only:

- prior probabilities, and
- conditional probabilities.

As networks become larger, this reduction becomes enormous and is one of the main reasons Bayesian Networks are so powerful in AI.

---

# Key Takeaways

- A Bayesian Network represents uncertain variables using a directed graph.
- Arrows indicate causal influence.
- Some variables are hidden, while others are directly observed.
- Each node stores either a prior probability or conditional probabilities.
- Diagnostic reasoning asks for the probability of a hidden cause given observed evidence.
- [[6 - Bayes' Theorem]] allows us to perform this reverse reasoning.
- Even a simple two-node Bayesian Network can be represented using only **three independent parameters**.

Next: [[Lecture 6 - Bayesian Networks II - Bayesian Inference In Simple Networks]]
