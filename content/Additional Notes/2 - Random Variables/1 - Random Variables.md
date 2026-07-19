
> **Prerequisites**
>
> - [[3 - Probability]]
> - [[4 - Conditional Porbability]]

## Definition

A **random variable** is a function that maps each outcome in the sample space to a real number.

$$
X:\Omega \rightarrow \mathbb{R}
$$

- Input → outcome from the sample space
- Output → numerical value

A random variable does **not** generate randomness.

It assigns a numerical value to each possible outcome.

## Example: Sum of Two Dice

Sample space:

$$
\Omega=\{(1,1),(1,2),...,(6,6)\}
$$

Define

$$
X=\text{sum of the two dice}
$$

Examples:

| Outcome | X |
|---------|---|
|(2,5)|7|
|(4,6)|10|
|(1,1)|2|
## Probability of a Random Variable

Instead of asking

> Which outcome occurred?

we ask

> What value did the random variable take?

We write

$$
P(X=x)
$$

Example:

For the sum of two dice,

| x | P(X=x) |
|---|---------|
|2|1/36|
|3|2/36|
|4|3/36|
|5|4/36|
|6|5/36|
|7|6/36|
|8|5/36|
|9|4/36|
|10|3/36|
|11|2/36|
|12|1/36|

## Why Random Variables Matter

Random variables convert real-world outcomes into numbers.

This allows us to compute

- probabilities
- averages
- variances
- expectations

and forms the foundation of

- Statistics
- Machine Learning
- Bayesian Networks
- Reinforcement Learning
- Markov Models

---
# Discrete Random Variables

A random variable is **discrete** if it can take

- finitely many values, or
- countably infinite values.

Examples

- Number of heads
- Number of customers
- Number of defective products

## Probability Mass Function (PMF)

The PMF gives

$$
f(x)=P(X=x)
$$

Unlike a pdf, the PMF gives probabilities directly.

### Properties

$$
0\le f(x)\le1
$$

$$
\sum_x f(x)=1
$$

---

### Example

Flip two coins.

Let

$$
X=\text{number of heads}
$$

| x | f(x) |
|---|------|
|0|1/4|
|1|1/2|
|2|1/4|
|otherwise|0|


## Common Discrete Distributions

- Bernoulli
- Binomial
- Geometric
- Poisson

# Continuous Random Variables

A random variable is **continuous** if it can take infinitely many values over an interval.

Example

Height

Weight

Temperature

Time

## Probability Density Function (PDF)

A pdf is

$$
f(x)
$$

Unlike a PMF,

> **A pdf does NOT give probabilities directly.**

Probabilities are areas under the curve.

$$
P(X\in A)=\int_A f(x)\,dx
$$

---

### Properties

$$
f(x)\ge0
$$

$$
\int_{-\infty}^{\infty}f(x)\,dx=1
$$

## Example

Choose a random number between 3 and 7.

$$
f(x)=
\begin{cases}
1/4,&3\le x\le7\\
0,&\text{otherwise}
\end{cases}
$$

Probability that

$$
X\le5
$$

is

$$
\int_3^5\frac14dx=\frac12
$$

## PMF vs PDF

| PMF | PDF |
|------|------|
|Discrete|Continuous|
|Gives probabilities directly|Does not|
|Use summation|Use integration|
|Σf(x)=1|∫f(x)=1|

## Why This Matters in AI

Discrete variables

- Dice
- Categories
- Words
- Classes

Continuous variables

- Images
- Audio
- Sensor values
- Time
- Distances


---
tags:
  - probability
  - ai
---

# Cumulative Distribution Function (CDF)

## Definition

The cumulative distribution function is

$$
F(x)=P(X\le x)
$$

It gives the probability that the random variable is **less than or equal to** a value.

## Discrete Random Variables

$$
F(x)=\sum_{y\le x}f(y)
$$

Simply add all probabilities up to x.

### Example

Flip two coins.

Let

$$
X=\text{number of heads}
$$

PMF

| x | Probability |
|---|-------------|
|0|1/4|
|1|1/2|
|2|1/4|

CDF

| x | F(x) |
|---|------|
|x<0|0|
|0≤x<1|1/4|
|1≤x<2|3/4|
|x≥2|1|


## Continuous Random Variables

For continuous variables,

$$
F(x)=\int_{-\infty}^{x}f(t)\,dt
$$

CDF equals the area under the pdf.

## Properties

$$
0\le F(x)\le1
$$

As

$$
x\rightarrow-\infty
$$

$$
F(x)\rightarrow0
$$

As

$$
x\rightarrow\infty
$$

$$
F(x)\rightarrow1
$$

For continuous variables,

$$
F'(x)=f(x)
$$

The derivative of the CDF is the PDF.

## Why CDFs Matter

CDFs are useful for

- computing probabilities over intervals
- sampling algorithms
- simulation
- statistical inference
- machine learning

Many AI algorithms work with CDFs rather than PDFs directly.