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

# Computing Bayes Rule Efficiently

## Overview

Above, we saw that Bayesian Networks store:

- prior probabilities
- conditional probabilities

However, once we observe evidence, we must compute the **posterior probability**.

For example,

> A patient's test is positive.
>
> What is the probability that the patient actually has cancer?

Mathematically,

$$
P(C|T)
$$

This is where **Bayes' Theorem** is applied.

---

# Revisiting Bayes' Theorem

From [[6 - Bayes' Theorem]],

$$
P(A|B)=\frac{P(B|A)P(A)}{P(B)}
$$

where

- $P(A)$ is the prior probability,
- $P(B|A)$ is the likelihood,
- $P(B)$ is the probability of observing the evidence,
- $P(A|B)$ is the posterior probability.

---

# The Difficult Part

Notice the denominator:

$$
P(B)
$$

This is called the **evidence** (or **marginal likelihood**).

Unfortunately,

> **it is often the hardest quantity to compute.**

The numerator,

$$
P(B|A)P(A)
$$

is usually straightforward because it is simply a multiplication.

The denominator,

$$
P(B),
$$

may require summing over many different possibilities.

For very large Bayesian Networks, this becomes computationally expensive.

---

# A Useful Observation

Suppose we want to compute

$$
P(A|B)
$$

and

$$
P(\neg A|B).
$$

Using Bayes' theorem,

$$
P(A|B)=
\frac{P(B|A)P(A)}
{P(B)}
$$

and

$$
P(\neg A|B)=
\frac{P(B|\neg A)P(\neg A)}
{P(B)}.
$$

Notice something important.

The denominator,

$$
P(B),
$$

is **identical** in both equations.

Only the numerators are different.

This observation allows us to postpone computing the denominator.

---

# Non-Normalized Posterior

Instead of immediately calculating

$$
P(B),
$$

we first compute quantities that are **proportional** to the posterior.

For hypothesis $A$,

$$
P'(A|B)=P(B|A)P(A)
$$

Similarly,

$$
P'(\neg A|B)
=
P(B|\neg A)P(\neg A)
$$

The prime symbol (′) indicates that these are **not yet valid probabilities**.

They are called **unnormalized probabilities** (or **unnormalized posteriors**).

---

# Why Aren't They Probabilities?

Because their sum is usually **not equal to one**.

For example,

Suppose

$$
P'(A|B)=0.18
$$

and

$$
P'(\neg A|B)=0.42.
$$

Their sum is

$$
0.18+0.42=0.60.
$$

Since

$$
0.60\neq1,
$$

these values cannot yet represent a probability distribution.

---

# Normalization

To convert the unnormalized values into valid probabilities,

we divide each by their total.

Suppose

$$
S=P'(A|B)+P'(\neg A|B).
$$

Then

$$
P(A|B)=
\frac{P'(A|B)}{S}
$$

and

$$
P(\neg A|B)=
\frac{P'(\neg A|B)}{S}.
$$

Now,

$$
P(A|B)+P(\neg A|B)=1.
$$

---

# The Normalization Constant

Instead of writing the denominator every time,

AI often introduces a **normalization constant**.

It is usually written as

$$
\eta.
$$

Then,

$$
P(A|B)
=
\eta P(B|A)P(A)
$$

and

$$
P(\neg A|B)
=
\eta P(B|\neg A)P(\neg A).
$$

where

$$
\eta
=
\frac{1}
{P'(A|B)+P'(\neg A|B)}.
$$

In words,

> The normalization constant rescales the unnormalized values so that they sum to one.

---

# Worked Example

Suppose

Prior:

$$
P(A)=0.2
$$

Therefore,

$$
P(\neg A)=0.8.
$$

Evidence likelihoods:

$$
P(B|A)=0.9
$$

$$
P(B|\neg A)=0.3.
$$

---

### Step 1 — Compute unnormalized probabilities

For hypothesis $A$,

$$
P'(A|B)
=
0.9\times0.2
=
0.18
$$

For hypothesis $\neg A$,

$$
P'(\neg A|B)
=
0.3\times0.8
=
0.24
$$

---

### Step 2 — Compute the total

$$
S=0.18+0.24=0.42.
$$

---

### Step 3 — Normalize

$$
P(A|B)
=
\frac{0.18}{0.42}
=
0.4286
$$

and

$$
P(\neg A|B)
=
\frac{0.24}{0.42}
=
0.5714.
$$

Now,

$$
0.4286+0.5714=1.
$$

We now have a valid probability distribution.

---

# Why AI Uses This Method

For a simple network with only two hypotheses, computing

$$
P(B)
$$

directly is manageable.

However, real Bayesian Networks may contain:

- hundreds of variables,
- thousands of possible hidden states.

Computing the denominator directly becomes extremely expensive.

Instead, AI algorithms typically:

1. Compute an unnormalized score for every hypothesis.
2. Add all scores together.
3. Divide each score by the total.

This produces the exact same posterior probabilities while avoiding repeated computation of the denominator.

This idea appears throughout probabilistic AI and is one of the foundations of inference algorithms for Bayesian Networks.

---

# Connection to Bayesian Networks

In Bayesian Networks, each observed piece of evidence contributes another conditional probability.

Rather than recomputing the denominator after every observation, we repeatedly:

- multiply by the appropriate conditional probability,
- keep an unnormalized running score,
- normalize only at the end.

The next lecture applies this exact procedure to the **Two-Test Cancer** example.

---

# Key Takeaways

- The denominator in Bayes' theorem is often the most computationally expensive part.
- The denominator is the same for all competing hypotheses.
- We first compute **unnormalized posterior probabilities** by multiplying the prior and likelihood.
- These values are not probabilities because they do not necessarily sum to one.
- We normalize them by dividing each by their total.
- The normalization constant is commonly written as

$$
\eta.
$$

- This approach is used throughout Bayesian Network inference because it is computationally efficient.

# Two-Test Cancer Example

## Overview

We learned that instead of computing the denominator of Bayes' theorem immediately, we can:

1. Compute **unnormalized posterior probabilities**.
2. Multiply each new piece of evidence into the current values.
3. Normalize only once at the end.

This lecture applies that method to a Bayesian Network with **two independent medical tests**.

---

# Bayesian Network

The network consists of three variables.

```text
          Cancer (C)
          /        \
         ▼          ▼
      Test 1      Test 2
```

- **Cancer (C)** is the hidden (unobservable) variable.
- **Test 1 (T₁)** and **Test 2 (T₂)** are observable.
- Both test results depend on whether cancer is present.

# Given Information

## Prior Probability

The probability that a randomly selected patient has cancer is

$$
P(C)=0.01
$$

Therefore,

$$
P(\neg C)=0.99
$$


## Test Accuracy

For **both tests**, we are given

If the patient has cancer,

$$
P(+|C)=0.9
$$

Therefore,

$$
P(-|C)=0.1
$$

since probabilities must sum to one.

---

If the patient does **not** have cancer,

the probability of a negative test is

$$
P(-|\neg C)=0.8
$$

Therefore,

$$
P(+|\neg C)=0.2
$$

---

# The Question

Suppose

- Test 1 is **positive**
- Test 2 is **positive**

We want to compute

$$
P(C|++)
$$

that is,

> What is the probability that the patient has cancer given that **both tests are positive**?

---

# Step 1 — Start with the Prior

Before seeing any evidence,

| Hypothesis | Probability |
|------------|-------------|
| Cancer | 0.01 |
| No Cancer | 0.99 |

These are our starting values.

---

# Step 2 — Process the First Positive Test

A positive result contributes

For the cancer hypothesis,

$$
P(+|C)=0.9
$$

For the no-cancer hypothesis,

$$
P(+|\neg C)=0.2
$$

Multiply these into the running values.

Cancer:

$$
0.01\times0.9=0.009
$$

No cancer:

$$
0.99\times0.2=0.198
$$

These are still **unnormalized** values.

---

# Step 3 — Process the Second Positive Test

The second positive test contributes exactly the same likelihoods.

Again multiply

Cancer:

$$
0.009\times0.9=0.0081
$$

No cancer:

$$
0.198\times0.2=0.0396
$$

Notice that every new observation simply multiplies into the existing score.

This is why Bayesian updating is computationally efficient.

---

# Running Calculation

| Evidence Processed | Cancer | No Cancer |
|--------------------|---------|------------|
| Prior | 0.01 | 0.99 |
| First Positive | 0.009 | 0.198 |
| Second Positive | 0.0081 | 0.0396 |

These numbers are **not probabilities yet**.

---

# Step 4 — Normalize

Add the two scores.

$$
0.0081+0.0396=0.0477
$$

Now divide each score by the total.

Cancer:

$$
P(C|++)
=
\frac{0.0081}{0.0477}
\approx0.1698
$$

No cancer:

$$
P(\neg C|++)
=
\frac{0.0396}{0.0477}
\approx0.8302
$$

---

# Final Answer

After receiving **two positive test results**,

the probability that the patient actually has cancer is

$$
P(C|++)
\approx0.1698
$$

or approximately

**17%.**

---

# Why Isn't the Probability Higher?

At first glance, two positive tests seem like strong evidence.

However, the disease itself is extremely rare.

Initially,

$$
P(C)=0.01
$$

Only **1%** of the population has cancer.

Even though each test is fairly accurate, false positives still occur.

Since almost everyone is healthy, the healthy population contributes many more false positives than the cancer population contributes true positives.

This illustrates one of the central lessons of Bayesian reasoning:

> **Evidence must always be interpreted together with the prior probability.**

Ignoring the prior often leads to overly confident conclusions.

---

# Efficient Bayesian Updating

Notice how the computation proceeded.

We never calculated

$$
P(++),
$$

the denominator in Bayes' theorem.

Instead we simply

1. started with the prior,
2. multiplied each likelihood,
3. normalized once at the end.

This is exactly the procedure introduced in [[Computing Bayes Rule Efficiently]].

As Bayesian Networks become larger, this approach becomes significantly more efficient than repeatedly applying Bayes' theorem from scratch.

---

# Key Idea

Every new observation contributes another multiplication.

```text
Prior

↓

× Likelihood of Test 1

↓

× Likelihood of Test 2

↓

Normalize

↓

Posterior
```

This repeated multiplication followed by a single normalization is the basic mechanism used for probabilistic inference in Bayesian Networks.

---

# Key Takeaways

- A Bayesian Network allows evidence to be incorporated one observation at a time.
- Each observed variable contributes another likelihood term.
- The prior probability serves as the starting point.
- Every new observation multiplies into the current score.
- The values remain **unnormalized** until all evidence has been processed.
- A single normalization step converts the scores into valid probabilities.
- Even multiple positive tests may not imply a high probability of disease if the disease itself is very rare.

# Mixed Evidence Example

## Overview

In Two-Test Cancer Example, both medical tests returned **positive**.

Now consider a different situation.

Suppose:

- Test 1 is **positive**
- Test 2 is **negative**

We want to compute the probability that the patient has cancer given this mixed evidence.

Mathematically,

$$
P(C|+-)
$$

where

- "+" denotes a positive test result,
- "−" denotes a negative test result.

The important lesson of this lecture is that **the Bayesian updating algorithm does not change**. We simply multiply by different likelihoods depending on the observed evidence.

---

# Bayesian Network

The Bayesian Network remains exactly the same.

```text
          Cancer (C)
          /        \
         ▼          ▼
      Test 1      Test 2
```

Cancer is the hidden variable.

Both test results are observable evidence.


# Given Information

## Prior Probability

The prior probability of cancer is

$$
P(C)=0.01
$$

Therefore,

$$
P(\neg C)=0.99
$$


## Test Accuracy

If the patient has cancer,

Positive result:

$$
P(+|C)=0.9
$$

Negative result:

$$
P(-|C)=0.1
$$

---

If the patient does **not** have cancer,

Negative result:

$$
P(-|\neg C)=0.8
$$

Positive result:

$$
P(+|\neg C)=0.2
$$

---

# Observed Evidence

We observe

- Test 1 = Positive
- Test 2 = Negative

Notice that each observation contributes a different likelihood.

---

# Step 1 — Start with the Prior

Before seeing any evidence,

| Hypothesis | Probability |
|------------|-------------|
| Cancer | 0.01 |
| No Cancer | 0.99 |

---

# Step 2 — Process the Positive Test

For the cancer hypothesis,

multiply by

$$
P(+|C)=0.9
$$

For the no-cancer hypothesis,

multiply by

$$
P(+|\neg C)=0.2
$$

Cancer:

$$
0.01\times0.9=0.009
$$

No cancer:

$$
0.99\times0.2=0.198
$$

---

# Step 3 — Process the Negative Test

The second test is **negative**, so we now use the probabilities associated with a negative result.

For the cancer hypothesis,

multiply by

$$
P(-|C)=0.1
$$

For the no-cancer hypothesis,

multiply by

$$
P(-|\neg C)=0.8
$$

Cancer:

$$
0.009\times0.1=0.0009
$$

No cancer:

$$
0.198\times0.8=0.1584
$$

Again, these are **unnormalized scores**, not probabilities.

---

# Running Calculation

| Evidence Processed | Cancer | No Cancer |
|--------------------|---------|------------|
| Prior | 0.01 | 0.99 |
| Positive Test | 0.009 | 0.198 |
| Negative Test | 0.0009 | 0.1584 |

---

# Step 4 — Normalize

Compute the total.

$$
0.0009+0.1584=0.1593
$$

Now divide each score by the total.

Cancer:

$$
P(C|+-)
=
\frac{0.0009}{0.1593}
\approx0.0056
$$

No cancer:

$$
P(\neg C|+-)
=
\frac{0.1584}{0.1593}
\approx0.9944
$$

The two probabilities sum to approximately one.

---

# Final Answer

After observing

- one positive test,
- one negative test,

the probability that the patient actually has cancer is

$$
P(C|+-)
\approx0.0056
$$

or approximately

**0.56%.**

---

# Comparing the Two Scenarios

| Evidence | Probability of Cancer |
|-----------|----------------------:|
| Positive, Positive | $$0.1698$$ |
| Positive, Negative | $$0.0056$$ |

A single negative test greatly reduces the probability of cancer because:

- cancer is already very rare,
- a negative test is unlikely if cancer is present,
- a negative test is much more likely if the patient is healthy.

---

# The Bayesian Updating Algorithm

Notice that the algorithm never changed.

Regardless of the evidence, we always follow the same four steps.

1. Start with the prior probabilities.
2. Multiply by the likelihood of each observed piece of evidence.
3. Continue multiplying as additional evidence arrives.
4. Normalize once at the end.

Only the likelihood values change depending on what is observed.

---

# Why This Matters

This example demonstrates an important property of Bayesian Networks.

Each new observation is incorporated independently by multiplying its corresponding conditional probability.

As additional evidence becomes available, we simply continue updating the running scores before performing a final normalization.

This repeated process is the foundation of probabilistic inference in Bayesian Networks.

Later in the course, the same idea will be extended to much larger networks containing many hidden variables and many observations.

---

# Key Takeaways

- Bayesian updating works the same regardless of the evidence observed.
- Positive observations use positive likelihoods.
- Negative observations use negative likelihoods.
- Every observation contributes another multiplication.
- Normalization is performed only after all evidence has been incorporated.
- Mixed evidence can dramatically change the posterior probability.
- The prior probability remains an essential part of every Bayesian update.


# Conditional Independence

## Overview

One of the most important ideas in Bayesian Networks is **conditional independence**.

The power of Bayesian Networks does not come from Bayes' Theorem alone. It comes from identifying variables that become independent **once certain information is known**.

Conditional independence allows a large probability distribution to be represented using far fewer probabilities, making inference computationally efficient.

---

# The Cancer Example

Consider the Bayesian Network introduced earlier.

```text
          Cancer (C)
          /        \
         ▼          ▼
      Test 1      Test 2
```

- **Cancer** is the hidden cause.
- **Test 1** and **Test 2** are observable medical tests.

Both tests depend on whether the patient has cancer.

---

# Assumptions

We assume both tests have identical accuracy.

For example,

$$
P(+|C)=0.9
$$

and

$$
P(+|\neg C)=0.2
$$

The lecture makes an additional assumption.

The two tests are **conditionally independent**.

---

# What Does Conditional Independence Mean?

Suppose someone tells you with absolute certainty whether the patient has cancer.

Once you know the value of **Cancer**, learning the outcome of Test 1 provides **no additional information** about Test 2.

Mathematically,

$$
P(T_2 \mid C,T_1)
=
P(T_2 \mid C)
$$

Similarly,

$$
P(T_1 \mid C,T_2)
=
P(T_1 \mid C)
$$

Knowing Cancer completely explains why the tests behave the way they do.

---

# Intuition

Imagine that an all-knowing observer tells you:

> "This patient definitely has cancer."

Now ask yourself:

> Does seeing Test 1 change your expectation for Test 2?

The answer is **No.**

You already know the true cause.

The only remaining uncertainty is the randomness of each individual test.

The tests no longer provide information about one another.

---

# Why Does This Happen?

Look at the graph again.

```text
          Cancer
          /     \
         ▼       ▼
     Test 1   Test 2
```

Cancer independently causes both tests.

Once Cancer is known,

the only influence on each test is Cancer itself.

The information cannot "flow" from Test 1 to Test 2 because both variables already have a known common cause.

The lecture describes this as the cause **cutting off** the relationship between the two tests.

---

# Conditional Independence in General

Suppose we have the following Bayesian Network.

```text
          A
         / \
        ▼   ▼
        B   C
```

The variable

- A causes B
- A causes C

Then,

given A,

B and C become conditionally independent.

Mathematically,

$$
B \perp C \mid A
$$

which means

$$
P(B\mid A,C)
=
P(B\mid A)
$$

or equivalently,

$$
P(C\mid A,B)
=
P(C\mid A)
$$

---

# Why This Matters

Conditional independence is the central idea behind Bayesian Networks.

Instead of describing every possible joint probability,

we only need to describe each variable conditioned on its parents.

This dramatically reduces the number of probabilities that must be stored.

Without conditional independence, Bayesian Networks would lose their computational advantage.

---

# Example

Suppose:

- Cancer is known to be present.
- Test 1 is positive.

Question:

Does observing Test 1 change the probability that Test 2 will be positive?

No.

Because Cancer is already known,

$$
P(T_2=+\mid C,T_1=+)
=
P(T_2=+\mid C)
$$

The first test contributes no new information once the common cause is known.

---

# Important Observation

Conditional independence only holds **after conditioning** on the specified variable.

In this example, the tests become independent only after Cancer is known.

If Cancer is unknown, the tests are generally **not** independent.

This distinction becomes extremely important in Bayesian inference.

---

# Key Takeaways

- Conditional independence means two variables become independent once another variable is known.
- In the cancer example, knowing Cancer makes the two tests independent.
- The common cause blocks information flow between the tests.
- Bayesian Networks rely on conditional independence to represent probability distributions efficiently.
- Conditional independence is the foundation of later concepts such as D-Separation and efficient inference algorithms.


# Conditional Independence vs Independence

## Overview

After introducing **conditional independence**, the lecture addresses an important question:

> Are conditional independence and ordinary (absolute) independence the same thing?

The answer is **No**.

Although the two concepts are related, **neither one implies the other**.

Understanding this distinction is essential for interpreting Bayesian Networks correctly.

---

# Absolute (Ordinary) Independence

Two events are **independent** if knowing one event occurs does not change the probability of the other.

Mathematically,

$$
P(A|B)=P(A)
$$

or equivalently,

$$
P(A\cap B)=P(A)P(B)
$$

This means learning that event \(B\) occurred provides no additional information about event \(A\).

---

# Conditional Independence

Conditional independence means that two variables become independent **only after** another variable is known.

Mathematically,

$$
P(B|A,C)=P(B|A)
$$

or

$$
B \perp C \mid A
$$

The independence exists **only under the condition that \(A\) is known**.

Without conditioning on \(A\), the variables may still influence each other.

---

# Does Conditional Independence Imply Independence?

**No.**

The cancer example demonstrates why.

```text
          Cancer
          /     \
         ▼       ▼
     Test 1   Test 2
```

Suppose the patient has **not** been diagnosed yet.

If Test 1 is positive, our belief that the patient has cancer increases.

Since Cancer also influences Test 2, this makes Test 2 more likely to be positive.

Therefore,

$$
P(T_2=+ \mid T_1=+)
>
P(T_2=+)
$$

The two tests are **not independent**.

They only become independent after Cancer is known.

---

# Computing the Probability of the Second Test

The lecture asks us to compute

$$
P(T_2=+ \mid T_1=+)
$$

This is solved using the **Theorem of Total Probability**.

From the previous note,

$$
P(C \mid T_1=+)\approx0.043
$$

Therefore,

$$
P(\neg C \mid T_1=+)
=
1-0.043
=
0.957
$$

Applying the Total Probability Theorem,

$$
P(T_2=+ \mid T_1=+)
=
P(T_2=+ \mid C,T_1=+)P(C \mid T_1=+)
+
P(T_2=+ \mid \neg C,T_1=+)P(\neg C \mid T_1=+)
$$

---

# Using Conditional Independence

Conditional independence allows us to simplify the equation.

Since

$$
P(T_2|C,T_1)
=
P(T_2|C)
$$

we obtain

$$
P(T_2=+\mid T_1=+)
=
P(T_2=+\mid C)P(C\mid T_1=+)
+
P(T_2=+\mid\neg C)P(\neg C\mid T_1=+)
$$

Substituting the probabilities from the lecture,

$$
=
(0.9)(0.043)
+
(0.2)(0.957)
$$

which gives

$$
P(T_2=+\mid T_1=+)
\approx0.2301
$$

---

# Interpretation

Before performing any tests,

the probability that a test is positive is approximately

$$
0.207
$$

After observing that Test 1 is positive,

the probability that Test 2 will also be positive becomes

$$
0.2301
$$

The probability increases because the first test changes our belief about the hidden cause (Cancer).

---

# Does Independence Imply Conditional Independence?

The lecture also asks the opposite question.

> If two variables are independent, must they also be conditionally independent?

Again,

**No.**

The instructor states that this is false and notes that the reason will become clear later in the course.

The next lecture introduces a different Bayesian Network structure that explains why.

---

# A New Bayesian Network Structure

Until now, we studied a network where **one hidden cause** produced **two observations**.

```text
          Cause
         /     \
        ▼       ▼
 Observation Observation
```

The lecture now introduces the opposite structure.

Two independent causes influence a single outcome.

```text
Sunny ───► Happiness ◄──── Raise
```

where

- Sunny = whether the weather is sunny
- Raise = whether you receive a salary raise
- Happiness = whether you are happy

---

# Prior Probabilities

The lecture assumes

$$
P(Sunny)=0.7
$$

and

$$
P(Raise)=0.01
$$

These two causes are assumed to be independent.

---

# Happiness Probabilities

The conditional probabilities are

| Sunny | Raise | $$P(Happy)$$ |
|--------|-------|--------------|
| Yes | Yes | 1.0 |
| No | Yes | 0.9 |
| Yes | No | 0.7 |
| No | No | 0.1 |

These values define how the two causes jointly influence Happiness.

---

# Independence Before Observing Happiness

The lecture asks

> What is

$$
P(Raise\mid Sunny)?
$$

Because neither variable causes the other,

and Happiness has **not** been observed,

the answer is simply

$$
P(Raise\mid Sunny)
=
P(Raise)
=
0.01
$$

Knowing that the weather is sunny tells us nothing about whether we received a raise.

The two causes remain independent.

---

# Why?

Looking at the network,

```text
Sunny ───► Happiness ◄──── Raise
```

Sunny and Raise only meet at their common effect (Happiness).

Since Happiness has **not** been observed,

there is no mechanism through which information can pass between Sunny and Raise.

Therefore,

they remain independent.

---

# Looking Ahead

The lecture ends by introducing this new network structure.

Later in the course, we will see that **observing Happiness changes everything**.

Once the common effect is observed,

Sunny and Raise are no longer independent.

This phenomenon is known as **Explaining Away**, one of the most important ideas in Bayesian Networks.

---

# Key Takeaways

- Independence and conditional independence are different concepts.
- Conditional independence does **not** imply ordinary independence.
- Ordinary independence does **not** imply conditional independence.
- In the cancer example, the first test changes our belief about Cancer, which changes the probability of the second test.
- A Bayesian Network with two independent causes and one common effect behaves differently from the common-cause structure studied earlier.
- Before observing the common effect, the two causes remain independent.

---

