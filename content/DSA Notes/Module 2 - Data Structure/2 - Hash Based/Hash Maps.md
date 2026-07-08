# Hashing and Universal Hash Functions (Number Theory Application)

> [!abstract]
> Hashing is a technique for storing and retrieving data efficiently using a hash function that maps large key spaces into a smaller table of buckets.
> This section connects hashing with **number theory** and introduces **universal hashing** to reduce collisions.

---

# 1. Motivation for Hashing

Suppose we need to maintain a dynamic set of about **250 IP addresses**.

An IP address:
- 32-bit number
- Usually written as 4 octets (e.g., `128.32.168.80`)
- Total possible values:  
  $2^{32} \approx 4 \times 10^9$

## Naive Approaches (and their problems)

### 1. Direct Address Table

- Array indexed by IP address
- Size required: \(2^{32}\)

> [!danger]
> Extremely wasteful:
> Most entries are empty.

---

### 2. Linked List

- Store only 250 items in a list

> [!danger]
> Lookup time: \(O(250)\), too slow for real-time systems

## Key Question

> Can we achieve both:
- Small memory usage (≈ number of items)
- Fast lookup time

✔ Yes → using **hashing**

---

# 2. Hash Tables

A **hash table** stores data using:

- A hash function \(h(x)\)
- A table of size \(n\)
- Each table entry is a **bucket ([[Linked Lists]])**

## Basic Idea

Each IP address \(x\) is mapped to:

$$
h(x) \in \{0, 1, ..., n-1\}
$$

- Store item in bucket \(h(x)\)
- Collisions handled using linked lists

## Performance Goal

We want:
- Small number of collisions
- Small average bucket size
- Fast lookup: ~O(1) expected time

---

# 3. Problem: Why Hashing is Hard

A simple hash function may fail due to **data distribution bias**.

## Example (Bad Hash Functions)

### Last octet hash:
$$
h(128.32.168.80) = 80
$$

> [!warning]
> If data is not uniformly distributed → collisions explode in certain buckets.

---

### First octet hash

> [!warning]
> If most users are from same region → severe clustering.

## Key Insight

> There is NO single perfect hash function for all inputs.

Because:
- Domain size: \(2^{32}\)
- Table size: ~250

By pigeonhole principle:
$$
\text{Many inputs MUST collide}
$$

---

# 4. Need for Randomization

Instead of one fixed hash function:

> Choose a hash function randomly from a family of functions.

This ensures:
- Even worst-case input behaves well (in expectation)

---

# 5. Number Theory Construction

We now build a **universal family of hash functions**.

---

## Step 1: Choose Prime Table Size

Let:
$$
n = 257
$$

> [!note]
> Prime numbers improve modular arithmetic properties.

## Step 2: Represent IP Address

Each IP address:
$$
x = (x_1, x_2, x_3, x_4)
$$

where each $$(x_i \in \{0, \dots, 255\})$$

We treat values modulo \(n\).

## Step 3: Define Hash Function

Fix coefficients:
$$
a = (a_1, a_2, a_3, a_4)
$$

Define:

$$
h_a(x_1,x_2,x_3,x_4) =
\sum_{i=1}^{4} a_i x_i \mod n
$$

## Key Idea

Each choice of \(a\) defines a different hash function.

Family of hash functions:
$$
H = \{h_a : a \in \{0,...,n-1\}^4\}
$$

---

# 6. Universal Hashing

> [!definition]
> A family of hash functions is **universal** if:
>
> For any $$(x \ne y)$$,
> the probability of collision is:
>
> $$
> P(h(x) = h(y)) = \frac{1}{n}
> $$

## Intuition

- Each pair collides with probability like random assignment
- No adversarial clustering possible (in expectation)

---

# 7. Collision Property (Key Result)

For distinct IPs:
$$
x \neq y
$$

Then:
$$
\Pr[h_a(x) = h_a(y)] = \frac{1}{n}
$$

## Meaning

Each item behaves as if:
- hashed independently
- uniformly distributed into buckets

# 8. Why This Works (Idea of Proof)

Assume:
$$
x \neq y
$$

Then at least one coordinate differs.

Without loss of generality:
$$
x_4 \neq y_4
$$

## Collision Condition

$$
\sum a_i x_i \equiv \sum a_i y_i \pmod n
$$

Rearranged:

$$
\sum_{i=1}^{3} a_i(x_i - y_i)
\equiv a_4 (y_4 - x_4) \pmod n
$$

## Key Number Theory Insight

Since:
- \(n\) is prime
- $$(y_4 - x_4 \neq 0\)$$

Then inverse exists:

$$
(y_4 - x_4)^{-1} \mod n
$$

So exactly **one value of \(a_4\)** satisfies equation.

## Probability

Since \(a_4\) is uniform:

$$
P(\text{collision}) = \frac{1}{n}
$$

---

# 9. Expected Performance

We have:
- \(m = 250\) items
- \(n = 257\) buckets

Expected items per bucket:

$$
\frac{m}{n} = \frac{250}{257} \approx 1
$$

> [!success]
> Expected lookup time is constant: **O(1)**


# 10. Why Universal Hashing Matters

Universal hashing ensures:

- No dependence on input distribution
- Resistant to worst-case clustering
- Predictable performance in expectation

---

# 11. Key Insight

> Instead of designing a perfect hash function,
> we design a **good family of hash functions** and pick one randomly.

---

# 12. Final Generalization

If:
- Table size = \(n\) (prime)
- Data items = k-tuples mod n

Then:

$$
H = \{h_a : a \in \{0,...,n-1\}^k\}
$$

is a **universal family of hash functions**

---

# 13. Exam Summary

> [!tip]
> - Hashing maps large key space → small table
> - Collisions are unavoidable
> - Universal hashing makes collisions random-like
> - Expected lookup time becomes O(1)
> - Number theory ensures collision probability = 1/n