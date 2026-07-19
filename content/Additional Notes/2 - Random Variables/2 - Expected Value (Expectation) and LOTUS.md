## Why this matters

Expected value is one of the most important concepts in probability.

It appears throughout machine learning, statistics, Bayesian inference, reinforcement learning, decision theory, and optimization.

Whenever someone asks:

> "On average, what should we expect?"

they are asking for the **expected value**.

---

# Intuition

Suppose you roll a fair die.

Possible outcomes are

$$
1,2,3,4,5,6
$$

Each occurs with probability

$$
\frac16
$$

If you roll the die thousands of times, the average result will approach

$$
3.5
$$

Notice that you can never actually roll **3.5**.

Expected value is **not necessarily a possible outcome**.

Instead, it is the **long-run average**.

---

# Definition

The expected value (or expectation) of a random variable is the weighted average of all possible outcomes.

Each value is weighted by its probability.

---

# Expected Value of a Discrete Random Variable

If

$$
X
$$

is discrete with probability mass function

$$
P(X=x),
$$

then

$$
E[X]
=
\sum_x xP(X=x)
$$

where the sum is over every possible value of the random variable.

---

# Example 1 — Fair Die

Suppose

$$
X=\text{result of one die roll}
$$

Then

$$
P(X=x)=\frac16
$$

for

$$
x=1,\ldots,6.
$$

Therefore

$$
E[X]
=
1\left(\frac16\right)
+
2\left(\frac16\right)
+\cdots+
6\left(\frac16\right)
$$

Factor out

$$
\frac16
$$

$$
=
\frac16(1+2+3+4+5+6)
$$

Since

$$
1+2+3+4+5+6=21,
$$

we obtain

$$
E[X]
=
\frac{21}{6}
=
3.5
$$

---

# Example 2 — Bernoulli Random Variable

Suppose

$$
X=
\begin{cases}
1,&\text{with probability }p\\
0,&\text{with probability }1-p
\end{cases}
$$

Then

$$
E[X]
=
1(p)+0(1-p)
=
p
$$

This is why the expected value of a Bernoulli random variable equals its success probability.

---

# Expected Value of a Continuous Random Variable

For continuous random variables, probabilities come from a probability density function (pdf).

Instead of summing, we integrate.

If

$$
X
$$

has density

$$
f(x),
$$

then

$$
E[X]
=
\int_{-\infty}^{\infty} xf(x)\,dx
$$

---

# Example — Uniform Distribution

Suppose

$$
X\sim\text{Uniform}(a,b)
$$

Its density is

$$
f(x)=
\begin{cases}
\frac1{b-a},&a\le x\le b\\
0,&\text{otherwise}
\end{cases}
$$

Then

$$
E[X]
=
\int_a^b
x\cdot\frac1{b-a}\,dx
$$

Evaluating the integral gives

$$
E[X]
=
\frac{a+b}{2}
$$

The expected value is simply the midpoint of the interval.

---

# Why Expected Value Matters

Expected value appears everywhere.

Examples include

- Average reward in Reinforcement Learning
- Average classification error
- Bayesian decision making
- Machine learning loss functions
- Simulation outputs
- Queueing systems
- Economics

Many optimization algorithms try to minimize or maximize an expected value.

---

# Law of the Unconscious Statistician (LOTUS)

## Motivation

Suppose you already know

$$
E[X]
$$

but now you need

$$
E[X^2]
$$

or

$$
E[\ln(X)]
$$

or

$$
E[\sin(X)].
$$

Do you have to find the probability distribution of

$$
g(X)
$$

first?

Fortunately,

**No.**

LOTUS provides a shortcut.

---

# LOTUS for Discrete Random Variables

If

$$
Y=g(X),
$$

then

$$
E[g(X)]
=
\sum_x g(x)P(X=x)
$$

Instead of finding the distribution of

$$
g(X),
$$

we simply evaluate

$$
g(x)
$$

at each possible value and weight by the probabilities.

---

# LOTUS Example (Discrete)

Suppose

| x | Probability |
|----|------------|
|2|0.3|
|3|0.6|
|4|0.1|

Suppose

$$
g(X)=X^3.
$$

Then

$$
E[X^3]
=
2^3(0.3)
+
3^3(0.6)
+
4^3(0.1)
$$

Compute each term:

$$
=
8(0.3)
+
27(0.6)
+
64(0.1)
$$

$$
=
2.4+16.2+6.4
=
25
$$

Notice that we never computed the distribution of

$$
X^3.
$$

LOTUS lets us skip that step.

---

# LOTUS for Continuous Random Variables

If

$$
X
$$

has density

$$
f(x),
$$

then

$$
E[g(X)]
=
\int_{-\infty}^{\infty}
g(x)f(x)\,dx
$$

Again, there is no need to derive the distribution of

$$
g(X).
$$

---

# Why LOTUS is Important

Many machine learning algorithms compute expectations of transformed random variables.

Examples include

- Variance

$$
E[X^2]
$$

- Mean squared error

$$
E[(X-\mu)^2]
$$

- Expected utility

$$
E[U(X)]
$$

- Bayesian inference

- Reinforcement learning

LOTUS makes all of these calculations straightforward.

---

# Key Takeaways

- Expected value is the long-run average outcome.
- Discrete random variables use summation.
- Continuous random variables use integration.
- Expected value is not necessarily an achievable value.
- LOTUS computes the expectation of any function of a random variable directly.
- LOTUS avoids finding the distribution of the transformed variable.

---

# Connections

- [[1 - Random Variables]]
- [[6 - Bayes' Theorem]]
- [[Gaussian Distribution]]
- [[Maximum Likelihood Estimation]]
- [[Expectation-Maximization (EM)]]
- [[Monte Carlo Methods]]


# Sources

1. NCERT Mathematics Class 12, Chapter 13 (Random Variables introduction)
2. Matt Schlenker, *Simulation* (Sections 2.7.1–2.7.7)
3. Sheldon Ross, *A First Course in Probability*, Chapters 4–5
4. Dimitri P. Bertsekas & John Tsitsiklis, *Introduction to Probability*