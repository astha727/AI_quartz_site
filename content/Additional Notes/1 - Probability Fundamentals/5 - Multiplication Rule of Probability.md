

> [!insight]
> The probability that **multiple events occur together** can be computed by multiplying probabilities, provided we account for information gained from previous events.


## Why We Need It

Often we want the probability that **two or more events occur simultaneously**.

Examples:

- Drawing two black cards
- Getting two kings consecutively
- Rain **and** traffic
- Patient has Disease A **and** Test B is positive

The multiplication theorem provides a systematic way to calculate these probabilities.

---

# Multiplication Rule

For two events \(A\) and \(B\),

$$
P(A\cap B)
=
P(A)\times P(B|A)
$$

Equivalently,

$$
P(A\cap B)
=
P(B)\times P(A|B)
$$

where

- \(P(A)\) = probability that A occurs first
- \(P(B|A)\) = probability that B occurs after A has occurred


## Interpretation

Think of the events occurring in sequence.

Step 1:

Probability that the first event occurs.

↓

Step 2:

Given that the first event has already happened,

find the probability of the second.

Multiply them together.

---

# Why Does This Work?

From conditional probability,

$$
P(B|A)
=
\frac{P(A\cap B)}{P(A)}
$$

Rearranging,

$$
P(A\cap B)
=
P(A)P(B|A)
$$

This is called the **Multiplication Rule of Probability**.

---

# Multiplication Rule for Three Events

For three events,

$$
P(A\cap B\cap C)
=
P(A)
P(B|A)
P(C|A\cap B)
$$

Likewise,

$$
P(A_1\cap A_2\cap\cdots\cap A_n)
=
P(A_1)
P(A_2|A_1)
\cdots
P(A_n|A_1\cap\cdots\cap A_{n-1})
$$

# Example 1 (NCERT)

## Two Black Balls

An urn contains

- 10 black balls
- 5 white balls

Two balls are drawn **without replacement**.

Find the probability that both are black.

### Step 1

Probability first ball is black

$$
P(B_1)=\frac{10}{15}
$$

### Step 2

After one black ball is removed,

9 black remain out of 14 balls.

$$
P(B_2|B_1)=\frac{9}{14}
$$

### Step 3

Multiply

$$
P(B_1\cap B_2)
=
\frac{10}{15}
\times
\frac{9}{14}
=
\frac37
$$

---

# Example 2 (Cards)

Three cards are drawn without replacement.

Find the probability of

- King
- King
- Ace

### Step 1

$$
P(K)=\frac4{52}
$$

### Step 2

$$
P(K|K)=\frac3{51}
$$

### Step 3

$$
P(A|KK)=\frac4{50}
$$

Therefore,

$$
P(KKA)
=
\frac4{52}
\times
\frac3{51}
\times
\frac4{50}
=
\frac2{5525}
$$


# With Replacement vs Without Replacement

## With Replacement

Each draw is independent.

Example:

Drawing a card, replacing it, then drawing again.

$$
P(A\cap B)=P(A)P(B)
$$


## Without Replacement

The first draw changes the sample space.

The second probability becomes conditional.

$$
P(A\cap B)
=
P(A)P(B|A)
$$

---

# When to Use the Multiplication Rule

Use it whenever the question asks for

- both
- and
- together
- consecutively
- simultaneously
- without replacement

These phrases usually indicate

$$
P(A\cap B)
$$

---

# Key Takeaways

- "AND" usually means **intersection**.
- Use conditional probability whenever earlier events affect later ones.
- Independent events simplify the multiplication rule.