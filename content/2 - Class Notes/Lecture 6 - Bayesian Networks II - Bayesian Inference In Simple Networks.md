Previous: [[Lecture 6 - Bayesian Networks I — Foundations & Bayes Rule]]
Next: [[Lecture 6 - Bayesian Networks III — Conditional Independence]]
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
- The normalization constant is commonly written as $\eta.$
- This approach is used throughout Bayesian Network inference because it is computationally efficient.


# Two-Test Cancer Example

## Overview

We learned that instead of computing the denominator of Bayes' theorem immediately, we can:

1. Compute **unnormalized posterior probabilities**.
2. Multiply each new piece of evidence into the current values.
3. Normalize only once at the end.

This lecture applies that method to a Bayesian Network with **two independent medical tests**.

---
<iframe
  src="/assets/bayes-calculator.html"
  width="100%"
  height="650"
  style="border:none;">
</iframe>
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

Next: [[Lecture 6 - Bayesian Networks III — Conditional Independence]]
