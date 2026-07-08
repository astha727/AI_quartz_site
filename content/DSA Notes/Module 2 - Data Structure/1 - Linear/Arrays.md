## Chapter Overview

Arrays are the **most fundamental data structure in computer science**.

Many advanced data structures and algorithms are built on top of arrays:

- [[Binary Search]]
    
- [[Sliding Window]]
    
- [[Two Pointers]]
    
- [[Prefix Sum]]
    
- [[Hash Maps]]
    
- [[Stacks]]
    
- [[Queues]]
    
- [[Heaps]]
    
- [[Dynamic Programming]]
    

> [!Note]  
> If DSA were a city, Arrays would be the roads that connect everything else.

---

# What Is An Array?

An **array** is a collection of values stored together.

```text
myFruits

┌────────┬────────┬────────┐
│    banana │    apple     │   orange   │
└────────┴────────┴────────┘
     0                  1                    2
    Indexes
```

Each value has a unique position called an **index**.

Arrays use **zero-based indexing**:

```text
Index:   0   1   2
Value:   A   B   C
```

---

## Real-Life Analogy: Apartment Building

Imagine a hallway of apartments.

```text
Door Number

┌────┬────┬────┬────┐
│  101  │   102 │  103 │  104 │
└────┴────┴────┴────┘
```

If someone asks:

> "Who lives in Apartment 103?"

You go directly to that apartment.

No searching required.

This is why arrays provide:

```text
O(1) Access Time
```

---

# Creating Arrays

### Python

```python
myFruits = ["banana", "apple", "orange"]
```

### Visual Representation

```text
myFruits

┌────────┬────────┬────────┐
│ banana    │     apple    │   orange   │
└────────┴────────┴────────┘
     0                   1                 2
```

---

# Why Arrays Exist

Without arrays:

```python
fruit1 = "banana"
fruit2 = "apple"
fruit3 = "orange"
fruit4 = "kiwi"
fruit5 = "mango"
```

Imagine storing 10,000 fruits.

Arrays solve this problem:

```python
fruits = [...]
```

One variable.

Many values.

---

# How Arrays Are Stored In Memory

This is the most important concept to understand.

Arrays are stored **contiguously in memory**.

```text
Memory

   1000      1004     1008       1012

┌─────┬─────┬─────┬─────┐
│    10    │   20    │    30  │    40   │
└─────┴─────┴─────┴─────┘
```

Notice:

- No gaps
    
- Stored side-by-side
    
- Easy to calculate addresses
    

Because of this:

```text
Address = Base + (Index × Size)
```

The computer can instantly find any element.

---

> [!Note]  
> Contiguous memory is the secret behind the O(1) access time of arrays.

---

# Core Array Operations

|Operation|Description|
|---|---|
|Access|Read a value|
|Update|Change a value|
|Insert|Add a value|
|Delete|Remove a value|
|Traverse|Visit all values|
|Search|Find a value|
|Length|Count values|

---

# Accessing Elements

```python
fruits[1]
```

Visual:

```text
┌────────┬────────┬────────┐
│ banana     │    apple    │    orange │
└────────┴────────┴────────┘
     0                     1                    2
                           ↑
```

Result:

```python
apple
```

### Complexity

```text
Time  : O(1)
Space : O(1)
```

---

# Updating Elements

```python
fruits[1] = "kiwi"
```

Before:

```text
banana apple orange
```

After:

```text
banana kiwi orange
```

### Complexity

```text
Time : O(1)
```

Because we already know the location.

---

# Traversing An Array

To see every element:

```python
for fruit in fruits:
    print(fruit)
```

Visual:

```text
banana → apple → orange
```

### Complexity

```text
O(N)
```

Because every element must be visited.

---

# Searching

## Scenario 1: Unsorted Array

```text
Mango
Apple
Orange
Kiwi
Banana
```

Searching for:

```text
Banana
```

Must check:

```text
Mango ❌
Apple ❌
Orange ❌
Kiwi ❌
Banana ✅
```

### Complexity

```text
O(N)
```

---

## Card Deck Analogy

Imagine a shuffled deck.

```text
♠4 ♥7 ♣K ♦2 ♠A ♥3
```

Searching for:

```text
♠A
```

You may need to check every card.

This is:

```text
Linear Search → O(N)
```

---

## Scenario 2: Sorted Array

```text
1 2 3 4 5 6 7 8 9
```

Search for:

```text
7
```

Check middle:

```text
1 2 3 4 5 6 7 8 9
        ↑
```

Discard half.

```text
6 7 8 9
```

Check middle again.

Found.

This is:

```text
Binary Search → O(log N)
```

---

# Insertion

## Inserting At The End

```python
fruits.append("kiwi")
```

```text
banana apple orange kiwi
```

Average complexity:

```text
O(1)
```

---

## Inserting In The Middle

Insert:

```text
kiwi
```

At index:

```text
1
```

Before:

```text
banana apple orange
```

After:

```text
banana kiwi apple orange
```

What happened?

```text
apple  → shifted right
orange → shifted right
```

### Complexity

```text
O(N)
```

---

## Train Analogy

Imagine train compartments.

```text
[A][B][C][D]
```

Insert:

```text
[X]
```

Between B and C.

```text
[A][B][X][C][D]
```

Every compartment must move.

This is why insertion can become:

```text
O(N)
```

---

# Deletion

Delete:

```text
apple
```

Before:

```text
banana apple orange kiwi
```

After:

```text
banana orange kiwi
```

Everything shifts left.

```text
orange → move left
kiwi   → move left
```

### Complexity

```text
O(N)
```

---

# Time Complexity Summary

|Operation|Complexity|
|---|---|
|Access|O(1)|
|Update|O(1)|
|Traverse|O(N)|
|Search (Linear)|O(N)|
|Search (Binary)|O(log N)|
|Insert End|O(1)*|
|Insert Middle|O(N)|
|Delete|O(N)|

> [!Note]  
> Interviewers love asking:
> 
> "Why are insertion and deletion expensive in arrays?"
> 
> Answer:
> 
> Because elements must be shifted.

---

# Advantages of Arrays

## 1. Fast Random Access

```text
O(1)
```

Access any element instantly.

---

## 2. Cache Friendly

Because memory is contiguous:

```text
[A][B][C][D][E]
```

Modern CPUs can load nearby values efficiently.

Arrays are one of the fastest structures in practice.

---

## 3. Easy To Sort

Arrays work beautifully with:

- [[Merge Sort]]
    
- [[Quick Sort]]
    
- [[Heap Sort]]
    
- [[Counting Sort]]
    

---

## 4. Foundation of Many Structures

Built using arrays:

- [[Stacks]]
    
- [[Queues]]
    
- [[Heaps]]
    
- [[Hash Maps]]
    
- [[Dynamic Programming]]
    

---

# Limitations of Arrays

## Fixed Size (Traditional Arrays)

```text
Size = 5
```

```text
[A][B][C][D][E]
```

Want another element?

```text
❌ No space available
```

Need a new array.

---

## Expensive Insertions

```text
O(N)
```

because shifting is required.

---

## Expensive Deletions

```text
O(N)
```

because shifting is required.

---

## Poor For Frequent Modifications

Arrays work best when:

```text
Reads >> Writes
```

Lots of reading.

Few insertions/deletions.

---

# Dynamic Arrays

Modern languages solve the fixed-size problem.

Examples:

|Language|Dynamic Array|
|---|---|
|Python|List|
|Java|ArrayList|
|C++|Vector|
|JavaScript|Array|

These automatically resize when needed.

---

# Multi-Dimensional Arrays

## 1D Array

```text
[10][20][30][40]
```

One index.

```python
arr[2]
```

---

## 2D Array

```text
         Col
        0    1    2

Row 0       A   B   C
Row 1        D   E   F
Row 2       G   H   I
```

Access:

```python
matrix[1][2]
```

Result:

```text
F
```

---

## Real-Life Example

Student Grades

```text
          Math   Science   English

Student1    90            85            88
Student2    70           92             81
Student3    95           89             94
```

A 2D array naturally represents rows and columns.

---

# Common Interview Patterns Using Arrays

These patterns solve hundreds of interview questions.

- [[Two Pointers]]
    
- [[Sliding Window]]
    
- [[Prefix Sum]]
    
- [[Fast and Slow Pointer]]
    
- [[Binary Search]]
    
- [[Greedy Arrays]]
    
- [[Dynamic Programming]]
    

---

# Interview Takeaways

> [!Note]  
> Remember these five facts:
> 
> 1. Array access is O(1).
>     
> 2. Arrays are stored contiguously in memory.
>     
> 3. Insertion and deletion may require shifting.
>     
> 4. Traversal is O(N).
>     
> 5. Arrays are the foundation of most DSA interview problems.
>     

---

# Quick Revision Sheet

```text
Access      → O(1)
Update      → O(1)
Traverse    → O(N)
Search      → O(N)
BinarySearch→ O(log N)
Insert      → O(N)
Delete      → O(N)
```

### Remember

```text
Arrays are optimized for:
✓ Fast Access

Arrays are NOT optimized for:
✗ Frequent Insertions
✗ Frequent Deletions
```
