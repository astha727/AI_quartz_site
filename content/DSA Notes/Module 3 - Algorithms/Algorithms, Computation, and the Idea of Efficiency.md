

> [!abstract]
> This section introduces the fundamental idea of algorithms through historical context (books, numbers, Fibonacci) and shows why **efficient algorithms** are central to modern computing.

---

# 1. Why Algorithms Matter

Computers and networks now power:

- Education
- Commerce
- Entertainment
- Research
- Healthcare
- Manufacturing
- Communication
- Warfare

Two major drivers of this revolution:

> [!important]
> 1. Hardware advances (microelectronics, chips)
> 2. Efficient algorithms (this book’s focus)

# 2. Books and Algorithms: A Historical Perspective

## The Gutenberg Revolution (1448)

Johann Gutenberg introduced **movable type printing**, enabling:

- Mass production of books
- Spread of literacy
- End of knowledge monopoly
- Scientific and industrial revolution

## But another revolution was just as important

> [!quote]
> Many historians argue that the real transformation came from algorithms, not printing.

# 3. Numbers Before Algorithms

## Roman Numerals Problem

Example:

- MCDXLVIII + DCCCXII

Issues:
- Hard to compute
- No positional structure
- No efficient arithmetic rules

Even multiplication becomes impractical.

## The Decimal Revolution

Origin: India (~600 AD)

Key idea:
- Positional number system
- 10 symbols (0–9)

Benefits:
- Compact representation
- Efficient arithmetic procedures
- Scalable computation

---

# 4. Al-Khwarizmi and the Birth of Algorithms

> [!info]
> Muhammad ibn Musa al-Khwarizmi (Baghdad, 9th century)

He formalized procedures for:
- Addition
- Multiplication
- Division
- Square roots
- π approximations

These step-by-step procedures were:

> [!definition]
> **Algorithms = precise, mechanical, finite procedures for computation**

The term “algorithm” comes from his name.

# 5. Fibonacci and the Spread of Computation

## Leonardo of Pisa (Fibonacci)

- Promoted decimal system in Europe
- Helped spread positional arithmetic
# 6. The Fibonacci Sequence

Defined as:

$$
F_n =
\begin{cases}
F_{n-1} + F_{n-2} & n > 1 \\
1 & n = 1 \\
0 & n = 0
\end{cases}
$$

Sequence:

```
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...
```

## Growth Rate

- Grows exponentially
- Approximation:

$$
F_n \approx 2^{0.694n}
$$

Example:
- F30 > 1 million
- F100 is 21 digits

---

# 7. The Computational Problem

We want:

> [!question]
> How do we compute \(F_n\) efficiently?

---

# 8. Algorithm 1: Naive Recursion (fib1)

```text
function fib1(n)
    if n = 0: return 0
    if n = 1: return 1
    return fib1(n−1) + fib1(n−2)
```

## Correctness

- Direct implementation of definition
- Always correct

## Running Time Analysis

Let T(n) = time for fib1(n)

$$
T(n) = T(n-1) + T(n-2) + 3
$$

This mirrors Fibonacci growth:

$$
T(n) \geq F_n
$$

---

> [!failure]
> fib1 runs in **exponential time**

## Why it is slow

- Recomputes same values repeatedly
- Massive recursion tree overlap

## Real-world impact

Computing F200:
- Requires ≥ \(2^{138}\) operations
- Even fastest supercomputers would take absurd time

# 9. Moore’s Law Insight (Why exponential is still bad)

Even if computers get:

- 1.6× faster per year

fib1 only improves linearly in n:

> One extra Fibonacci number per year


> [!warning]
> Exponential growth outpaces hardware improvements


# 10. Algorithm 2: Dynamic Programming (fib2)

Key idea:

> Store intermediate results instead of recomputing them

## Algorithm

```text
function fib2(n)
    if n = 0: return 0
    create array f[0..n]
    f[0] = 0, f[1] = 1

    for i = 2 to n:
        f[i] = f[i−1] + f[i−2]

    return f[n]
```

## Why it works

- Each value computed once
- Builds solution bottom-up

## Running Time

- Loop runs n times
- Each step = constant work

$$
T(n) = O(n)
$$

> [!success]
> Exponential → Polynomial improvement

# 11. Key Insight: Algorithmic Revolution

> [!summary]
> Choosing the right algorithm changes feasibility completely.

Example:
- fib1: impossible for large n
- fib2: practical even for very large n

---

# 12. More Honest Cost Model (Important Correction)

Earlier assumption:
- “Each operation is O(1)” ❌ (not always true)

## Problem: Large Numbers

Fibonacci numbers grow in bit-length:

$$
\text{bit length of } F_n \approx O(n)
$$

So arithmetic is not constant-time.

---

## Correct Cost Model

### Addition cost:

$$
O(n)
$$

## Revised complexity

### fib1:
- ~Fₙ additions
- Each addition costs O(n)

$$
T(n) \approx nF_n
$$

Still exponential

---

### fib2:
- n additions
- each costs O(n)

$$
T(n) = O(n^2)
$$

---

> [!important]
> Even after correction:
> - fib1 = exponential
> - fib2 = polynomial

---

# 13. Big Picture Insight

> [!quote]
> The right algorithm matters more than faster hardware.

---

# 14. Core Takeaways

### Historical insight:
- Decimal system → computational revolution
- Algorithms → foundation of modern computing

---

### Algorithmic insight:
- Naive recursion → exponential explosion
- Dynamic programming → polynomial efficiency

---

Refer: [[Module 1A - Time and Space Complexity - Building Intuition]]
### Final idea:

> [!tip]
> Efficiency is not about doing more work faster — it is about **avoiding unnecessary work entirely**