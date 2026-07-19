> [!quote]
> *"Mathematics is a most exact science and its conclusions are capable of absolute proofs."* — C. P. Steinmetz

# Binomial Theorem

## Why the Binomial Theorem Matters

The **Binomial Theorem** provides a systematic way to expand expressions of the form

$$
(a+b)^n
$$

without performing repeated multiplication.

For small powers, direct multiplication is practical:

$$
(a+b)^2,\qquad (a+b)^3
$$

However, expanding expressions such as

$$
(98)^5,\qquad (101)^6,\qquad (a+b)^{20}
$$

by repeated multiplication quickly becomes tedious.

The Binomial Theorem gives a direct formula for expanding any positive integral power.

> [!info] Connection to AI
> Binomial coefficients appear throughout AI and computer science, including:
>
> - Probability
> - Binomial Distribution
> - Statistics
> - Bayesian Inference
> - Machine Learning
> - Generating Functions
> - Dynamic Programming

---

# Discovering the Pattern

Before introducing the theorem, examine the first few expansions.

$$
(a+b)^0=1
$$

$$
(a+b)^1=a+b
$$

$$
(a+b)^2=a^2+2ab+b^2
$$

$$
(a+b)^3=a^3+3a^2b+3ab^2+b^3
$$

$$
(a+b)^4=a^4+4a^3b+6a^2b^2+4ab^3+b^4
$$

## Observations

> [!important] Number of Terms
>
> The expansion of
>
> $$
> (a+b)^n
> $$
>
> always contains
>
> $$
> n+1
> $$
>
> terms.

---

> [!important] Powers of \(a\)

The exponent of **a** decreases by one in every successive term.

Example:

$$
a^4,\;a^3,\;a^2,\;a,\;1
$$

---

> [!important] Powers of \(b\)

The exponent of **b** increases by one in every successive term.

Example:

$$
1,\;b,\;b^2,\;b^3,\;b^4
$$

---

> [!important] Sum of Exponents

In every term,

$$
\text{Exponent of }a+\text{Exponent of }b=n
$$

Example:

| Term | Sum |
|------|----:|
| $a^4$ | 4 |
| $a^3b$ | 4 |
| $a^2b^2$ | 4 |
| $ab^3$ | 4 |
| $b^4$ | 4 |

---

# Pascal's Triangle

## Definition

Pascal's Triangle is a triangular arrangement of numbers in which every interior number equals the sum of the two numbers directly above it.

![[Pasted image 20260630163152.png|500]]

## Properties

### 1. Diagonal Addition

Each interior number is obtained by adding the two numbers diagonally above it.

---

### 2. Symmetry

Every row is symmetric.

$$
\binom nk=\binom n{n-k}
$$

---

### 3. Sum of a Row

The sum of the entries in row \(n\) is

$$
2^n
$$

Example:

$$
1,\;2,\;4,\;8,\;16,\;32,\dots
$$

---

### 4. Alternating Sum

The alternating sum of every row equals zero.

$$
\binom n0-\binom n1+\binom n2-\cdots+(-1)^n\binom nn=0
$$

---

### 5. Binomial Coefficients

Each entry in Pascal's Triangle is a **combination**:

$$
\binom nk
=
{}^nC_k
$$

---

# From Pascal's Triangle to the Binomial Theorem

Notice the rows of Pascal's Triangle.

| n | Row |
|---|------|
|0|1|
|1|1 1|
|2|1 2 1|
|3|1 3 3 1|
|4|1 4 6 4 1|
|5|1 5 10 10 5 1|

These rows become the coefficients of the corresponding binomial expansions.

For example,

$$
(1+x)^5
=
1+5x+10x^2+10x^3+5x^4+x^5
$$

The coefficients

$$
1,\;5,\;10,\;10,\;5,\;1
$$

come directly from row 5 of Pascal's Triangle.

---

# Binomial Theorem

> [!example] Formula
>
> $$
> (a+b)^n
> =
> \sum_{r=0}^{n}
> {}^nC_r
> a^{\,n-r}
> b^r
> $$

Equivalent expanded form:

$$
(a+b)^n
=
{}^nC_0a^n
+
{}^nC_1a^{n-1}b
+
{}^nC_2a^{n-2}b^2
+\cdots+
{}^nC_nb^n
$$

---

# General Term

The \((r+1)\)-th term of the expansion is

> [!tip] General Term
>
> $$
> T_{r+1}
> =
> {}^nC_r
> a^{\,n-r}
> b^r
> $$

where

- \(r=0,1,\dots,n\)
- coefficient = \({}^nC_r\)
- exponent of \(a\) decreases by one
- exponent of \(b\) increases by one

---

# Important Observations

- Number of terms = **n+1**
- First term

$$
a^n
$$

- Last term

$$
b^n
$$

- Coefficients are obtained from Pascal's Triangle.
- The sum of the exponents in every term is always **n**.

---

# How to Expand a Binomial

> [!note] Strategy
>
> 1. Identify \(a\), \(b\), and \(n\).
> 2. Write the coefficients using \({}^nC_r\).
> 3. Decrease the exponent of \(a\).
> 4. Increase the exponent of \(b\).
> 5. Simplify each term.


# Worked Examples

## Example 1 — Polynomial Expansion

Expand

$$
(x+2)^6
$$

Using the Binomial Theorem,

$$
(x+2)^6
=
{}^6C_0x^6
+
{}^6C_1x^5(2)
+
{}^6C_2x^4(2)^2
+\cdots+
{}^6C_6(2)^6
$$

After simplification,

$$
(x+2)^6
=
x^6
+
12x^5
+
60x^4
+
160x^3
+
240x^2
+
192x
+
64
$$



## Example 2 — Numerical Computation

Compute

$$
98^5
$$

Rewrite

$$
98=100-2
$$

Then

$$
98^5=(100-2)^5
$$

Applying the Binomial Theorem,

$$
\begin{aligned}
98^5
&=
100^5
-5(100)^4(2)
+10(100)^3(2)^2 \\
&\quad
-10(100)^2(2)^3
+5(100)(2)^4
-(2)^5
\end{aligned}
$$

Hence,

$$
98^5=9,\!039,\!207,\!968
$$


# Special Cases

## Expansion of \((x-y)^n\)

Replace

$$
b=-y
$$

Then

$$
(x-y)^n
=
{}^nC_0x^n
-
{}^nC_1x^{n-1}y
+
{}^nC_2x^{n-2}y^2
-\cdots+
(-1)^n{}^nC_ny^n
$$

Notice the alternating signs.


## Expansion of \((1+x)^n\)

Setting

$$
a=1
$$

gives

$$
(1+x)^n
=
{}^nC_0
+
{}^nC_1x
+
{}^nC_2x^2
+\cdots+
{}^nC_nx^n
$$


## Sum of Binomial Coefficients

Substituting

$$
x=1
$$

gives

$$
2^n
=
{}^nC_0
+
{}^nC_1
+\cdots+
{}^nC_n
$$


## Alternating Sum Identity

Using

$$
(1-x)^n
$$

and setting

$$
x=1
$$

gives

$$
0
=
{}^nC_0
-
{}^nC_1
+
{}^nC_2
-\cdots+
(-1)^n{}^nC_n
$$

---

# Summary

> [!insight]
>
> - The Binomial Theorem expands \((a+b)^n\) without repeated multiplication.
> - The coefficients are the binomial coefficients \({}^nC_r\).
> - These coefficients correspond exactly to Pascal's Triangle.
> - The theorem links algebra, combinatorics, probability, and statistics.
> - It serves as the foundation for the Binomial Distribution, Bayesian inference, and many machine learning algorithms.

Source: NCERT Class XI