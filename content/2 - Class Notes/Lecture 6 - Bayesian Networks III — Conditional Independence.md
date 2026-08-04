Previous: [[Lecture 6 - Bayesian Networks II - Bayesian Inference In Simple Networks]]
Next: [[Lecture 6 – Bayesian Networks VI - Exact Inference]]
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

The lecture states that this is false and notes that the reason will become clear later in the course.

The next lecture introduces a different Bayesian Network structure that explains why.


Next: [[Lecture 6 - Bayesian Networks IV — Bayesian Network Structures]]

