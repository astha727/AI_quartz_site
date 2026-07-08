
## The Goal of This Chapter

Before learning [[Arrays]], [[Linked Lists]], [[Trees]], or [[Dynamic Programming]], we need to answer one question:

> How do we know whether one solution is better than another?

Imagine two programmers solve the same problem.

```text
Programmer A:
Correct Solution

Programmer B:
Correct Solution
```

Both are correct.

But:

```text
Programmer A → 1 second
Programmer B → 3 hours
```

Suddenly the difference matters.

---

> [!Note]  
> In technical interviews, correctness gets you into the conversation.
> 
> Efficiency often determines whether you pass.

---

## The Kingdom of Algorithms

Imagine you are the royal engineer of a kingdom.

Every day the king gives you problems.

```text
👑 Find a missing treasure.

👑 Search a giant library.

👑 Organize 10 million records.

👑 Plan routes across the kingdom.
```

Every solution must answer three questions.

```text
1. Is it correct?

2. How long does it take?

3. How much memory does it use?
```

These correspond to:

```text
Correctness
Time Complexity
Space Complexity
```

---

# Time Complexity

## What Is Time Complexity?

==Time Complexity measures how the amount of work grows as the input size grows.==

Input size is usually represented by:

```text
N
```

Examples:

```text
Array Size
Number of Users
Number of Cards
Number of Tree Nodes
Length of a String
```

We are NOT measuring actual seconds.

We are measuring:

```text
Growth Rate
```

---

# O(1) — The Magical Bookshelf

## Story

You own a magical library.

Every book has a numbered shelf.

```text
[1] [2] [3] [4] [5] [6]
```

Someone asks:

```text
Bring me Book #5
```

You immediately grab it.

```text
[1] [2] [3] [4] [5] [6]
                 ↑
```

No searching.

No scanning.

No extra work.

---

### What If We Add More Books?

```text
100 Books
```

or

```text
1,000,000 Books
```

You still go directly to:

```text
Shelf #5
```

The amount of work never changes.

```text
Complexity = O(1)
```

---

### Real Examples

- Array indexing
    
- Accessing first element
    
- Hash table lookup (average case)
    

---

### Memory Hook

```text
Magic Shelf = O(1)
```

---

# O(N) — The Lost Card

## Story

You lost:

```text
♥7
```

inside a shuffled deck.

```text
♣4 ♦Q ♠9 ♥2 ♣A ♥7
```

You search.

```text
♣4 ❌

♦Q ❌

♠9 ❌

♥2 ❌

♣A ❌

♥7 ✅
```

---

### Why O(N)?

More cards means more searching.

```text
10 cards → ~10 checks

100 cards → ~100 checks

1000 cards → ~1000 checks
```

The work grows linearly.

```text
Complexity = O(N)
```

---

### Real Examples

- Linear Search
    
- Traversing an Array
    
- Traversing a Linked List
    

---

### Memory Hook

```text
One-by-One Searching
```

---

# O(log N) — The Detective

## Story

You need to find a name in a phone book.

Would you start on page 1?

No.

You open the middle.

```text
A -------- M -------- Z
```

Need:

```text
Sharma
```

Sharma comes after M.

Throw away half.

```text
N -------- Z
```

Repeat.

---

### What Happens?

```text
1,000,000 names

↓

500,000

↓

250,000

↓

125,000

↓

...
```

Every step removes half.

---

### Complexity

```text
O(log N)
```

---

### Real Examples

- [[Binary Search]]
    
- Balanced Trees
    
- Divide and Conquer Algorithms
    

---

### Memory Hook

```text
Cut It In Half
```

---

# O(N²) — The School Dance

Imagine:

```text
100 Boys

100 Girls
```

Every boy introduces himself to every girl.

```text
Boy 1 → Girl 1
Boy 1 → Girl 2
...
Boy 1 → Girl 100

Boy 2 → Girl 1
...
```

---

### Visualization

```text
N × N
```

```text
100 × 100 = 10,000 interactions
```

---

### Complexity

```text
O(N²)
```

---

### Programming Pattern

```python
for i in range(n):
    for j in range(n):
        pass
```

---

### Memory Hook

```text
Everyone Meets Everyone
```

---

# O(N³) — The Tournament

Now add:

```text
Players
Referees
Stadiums
```

Every player must be checked against every referee in every stadium.

```text
N × N × N
```

---

### Complexity

```text
O(N³)
```

---

# O(N log N) — The Postal Service

Imagine sorting packages.

For every package:

```text
Find Correct Shelf
```

using:

```text
Binary Search
```

Work done:

```text
N × log(N)
```

---

### Real Examples

- [[Merge Sort]]
    
- [[Heap Sort]]
    
- [[Quick Sort]] (Average)
    

---

### Memory Hook

```text
Many Items
+
Fast Searching
```

---

# O(2ᴺ) — The Coin Explosion

One coin:

```text
H
T
```

Two possibilities.

Add another.

```text
HH
HT
TH
TT
```

Four possibilities.

Add another.

```text
8 possibilities
```

Add another.

```text
16 possibilities
```

Every new coin doubles reality.

---

### Complexity

```text
O(2ᴺ)
```

---

### Real Examples

- Brute Force Backtracking
    
- Recursive Fibonacci
    

---

# O(N!) — Wedding Planner Nightmare

Five guests.

```text
Alice
Bob
Charlie
David
Emma
```

Arrange everyone.

```text
5 × 4 × 3 × 2 × 1
```

```text
120 arrangements
```

Add one guest.

```text
720 arrangements
```

Explosion.

---

### Complexity

```text
O(N!)
```

---

### Real Examples

- Permutations
    
- Traveling Salesman (Brute Force)
    

---

# Space Complexity

## The Backpack Analogy

Imagine your algorithm is an explorer.

Every extra data structure goes into a backpack.

---

### O(1) Space

Carry:

```text
Sword
Map
Compass
```

No matter how long the journey.

Space stays constant.

---

### O(N) Space

Collect every treasure.

```text
💎
💎💎
💎💎💎
```

Backpack grows.

---

### O(N²) Space

Store an entire grid.

```text
⬜⬜⬜
⬜⬜⬜
⬜⬜⬜
```

Memory grows much faster.

---

# The Time-Space Tradeoff

Sometimes we use more memory to save time.

Example:

Instead of recalculating answers:

```text
Compute Again
Compute Again
Compute Again
```

Store them.

```text
📓 Cache
```

Now retrieval is instant.

---

> [!ai]  
> Hash Maps, Memoization, Dynamic Programming, and Caching all rely on trading memory for speed.

---

