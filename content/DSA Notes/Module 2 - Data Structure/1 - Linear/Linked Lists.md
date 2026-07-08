
## Why Do We Need Linked Lists?

Imagine an array:

```text
[10] [20] [30] [40] [50]
```

Suppose we want to insert `25` between `20` and `30`.

```text
Before

[10] [20] [30] [40] [50]

After

[10] [20] [25] [30] [40] [50]
```

To make space, all elements after `20` must shift one position.

```text
30 → move
40 → move
50 → move
```

For large arrays, this becomes expensive.

---

Linked Lists solve this problem differently.

Instead of storing values next to each other, each value stores a reference to the next value.

![[Pasted image 20260603180533.png|540]]
```text
10 → 20 → 30 → 40 → 50 → NULL
```

To insert `25`:

```text
10 → 20 → 25 → 30 → 40 → 50 → NULL
```

Only a few pointers change.

No shifting required.

---

> [!Note]  
> Arrays optimize for **fast access**.
> 
> Linked Lists optimize for **fast insertion and deletion**.

---

# Building Intuition

## The Treasure Hunt Analogy

Imagine five treasure chests scattered across an island.

```text
Chest A
Chest B
Chest C
Chest D
Chest E
```

They are NOT next to each other.

Instead, each chest contains:

1. Treasure
    
2. Directions to the next chest
    

```text
[A | → B]

[B | → C]

[C | → D]

[D | → E]

[E | → NULL]
```

To reach Chest D:

```text
A → B → C → D
```

You cannot jump directly.

You must follow the chain.

That is exactly how a Linked List works.

---

# Formal Definition

==A Linked List is a linear data structure where each node contains data and a reference (pointer) to the next node.==

A node contains:

```text
┌─────────┬─────────┐
│      Data      │      Next      │
└─────────┴─────────┘
```

Example:

```text
┌─────┬─────┐
│    10   │      •──┼────┐
└─────┴─────┘         │
                   ▼

┌─────┬─────┐
│   20    │     •──┼────┐
└─────┴─────┘        │
                   ▼

┌─────┬─────┐
│    30   │  NULL│
└─────┴─────┘
```

---

# Important Terminology

## Head

The first node.

```text
Head
 ↓
10 → 20 → 30 → NULL
```

---

## Tail

The last node.

```text
10 → 20 → 30
                ↑
                Tail
```

---

## Node

Each individual element.

```text
[10 | next]
```

is one node.

---

## Pointer / Reference

Stores where the next node lives in memory.

```text
10 → 20
```

The arrow represents the pointer.

---

# How Linked Lists Are Stored in Memory

## Arrays

Arrays are stored contiguously.

```text
Memory

100
101
102
103
104

[10][20][30][40][50]
```

Everything is together.

This allows:

```python
arr[3]
```

to work instantly.

---

## Linked Lists

Nodes can be anywhere.

```text
Memory

100  → Node(10)
742  → Node(20)
201  → Node(30)
980  → Node(40)
555  → Node(50)
```

They are connected using pointers.

```text
10 → 20 → 30 → 40 → 50
```

not by physical location.

---

> [!Note]  
> This is why Linked Lists do NOT support random access.

---

# Why Arrays Are Fast

Suppose:

```python
arr[4]
```

The computer calculates:

```text
Base Address + (Index × Size)
```

and jumps directly.

```text
O(1)
```

---

# Why Linked Lists Are Slow

Suppose we want:

```text
Node #5
```

We must walk through:

```text
Head
 ↓

1 → 2 → 3 → 4 → 5
```

One step at a time.

```text
O(N)
```

---

# Creating a Node in Python

```python
class Node:

    def __init__(self, data):
        self.data = data
        self.next = None
```

Visual:

```text
┌─────┬──────┐
│Data │ Next │
└─────┴──────┘
```

---

# Creating a Linked List

```python
node1 = Node(10)
node2 = Node(20)
node3 = Node(30)

node1.next = node2
node2.next = node3
```

Visualization:

```text
10 → 20 → 30 → NULL
```

---

# Traversal

## What Is Traversal?

Visiting every node.

```text
10 → 20 → 30 → 40 → NULL
```

Traversal means:

```text
Visit 10
Visit 20
Visit 30
Visit 40
```

---

## Code

```python
current = head

while current:
    print(current.data)
    current = current.next
```

---

## Visualization

```text
Head

10 → 20 → 30 → 40

↑
current

      ↑
   current

            ↑
         current
```

---

## Complexity

```text
Time  : O(N)

Space : O(1)
```

---

# Searching

Find:

```text
30
```

```text
10 → 20 → 30 → 40
```

Check:

```text
10 ❌
20 ❌
30 ✅
```

---

## Complexity

```text
O(N)
```

---

# Insertion

One of the biggest strengths of Linked Lists.

---

## Insert at Beginning

Before:

```text
10 → 20 → 30
```

Insert:

```text
5
```

After:

```text
5 → 10 → 20 → 30
```

---

### Steps

```python
new_node.next = head
head = new_node
```

---

### Complexity

```text
O(1)
```

---

## Insert at End

Before:

```text
10 → 20 → 30
```

After:

```text
10 → 20 → 30 → 40
```

Need to find tail first.

---

### Complexity

```text
O(N)
```

---

## Insert in Middle

Before:

```text
10 → 20 → 30
```

Insert:

```text
25
```

After:

```text
10 → 20 → 25 → 30
```

---

### Pointer Changes

```text
20 → 30
```

becomes

```text
20 → 25 → 30
```

---

### Complexity

```text
O(N)
```

(searching for location)

---

# Deletion

---

## Delete Head

Before:

```text
10 → 20 → 30
```

After:

```text
20 → 30
```

Simply move head.

```python
head = head.next
```

---

### Complexity

```text
O(1)
```

---

## Delete Middle Node

Before:

```text
10 → 20 → 30 → 40
```

Delete:

```text
30
```

After:

```text
10 → 20 → 40
```

---

### Pointer Update

```text
20 → 30 → 40
```

becomes

```text
20 ─────→ 40
```

---

### Complexity

```text
O(N)
```

Need to find node first.

---

# Types of Linked Lists

---

## 1. Singly Linked List

Each node points only forward.

```text
10 → 20 → 30 → NULL
```

Most interview questions use this.

---

## 2. Doubly Linked List

Each node points both directions.

![[Pasted image 20260603180340.png|462]]
```text
NULL ← 10 ⇄ 20 ⇄ 30 → NULL
```

Node structure:

```text
┌─────┬──────┬──────┐
│Prev   │   Data   │  Next   │
└─────┴──────┴──────┘
```

---

### Advantages

Can move:

```text
Forward
Backward
```

---

### Disadvantages

More memory.

---

## 3. Circular Linked List

A **circular linked list** is like a singly or doubly linked list with the first node, the "head", and the last node, the "tail", connected.

In singly or doubly linked lists, we can find the start and end of a list by just checking if the links are null. But for circular linked lists, more complex code is needed to explicitly check for start and end nodes in certain applications.

Circular linked lists are good for lists you need to cycle through continuously.

![[Pasted image 20260603180851.png|348]]

```text
10 → 20 → 30
↑          ↓
└──────────┘
```

Useful for:

- Round-robin scheduling
    
- Music playlists
    
- Multiplayer game turns
    

---

# Arrays vs Linked Lists

|Operation|Array|Linked List|
|---|---|---|
|Access Index|O(1)|O(N)|
|Search|O(N)|O(N)|
|Insert Beginning|O(N)|O(1)|
|Delete Beginning|O(N)|O(1)|
|Insert End|O(1)*|O(N)|
|Delete End|O(1)*|O(N)|
|Memory Usage|Low|Higher|

* Amortized for dynamic arrays.

---

# Linked List Interview Patterns

These appear constantly in LeetCode.

---

## Fast & Slow Pointer

```text
🐢 Slow

🐇 Fast
```

Applications:

- Find middle node
    
- Detect cycle
    
- Happy Number
    
- Linked List Cycle
    

---

## Reversal

```text
1 → 2 → 3 → 4
```

becomes

```text
4 → 3 → 2 → 1
```

One of the most important Linked List questions.

---

## Dummy Node

Create a fake starting node.

```text
Dummy → Head
```

Makes insertion/deletion easier.

---

## Merge Lists

```text
1 → 3 → 5

2 → 4 → 6
```

Merge into:

```text
1 → 2 → 3 → 4 → 5 → 6
```

---

# Complexity Cheat Sheet

|Operation|Complexity|
|---|---|
|Access by Position|O(N)|
|Search|O(N)|
|Traverse|O(N)|
|Insert at Head|O(1)|
|Delete Head|O(1)|
|Insert at Tail|O(N)|
|Delete Tail|O(N)|
|Insert After Known Node|O(1)|
|Delete After Known Node|O(1)|

---

> [!Note]  
> For interviews, remember this rule:
> 
> **Arrays = Fast Access, Slow Modification**
> 
> **Linked Lists = Slow Access, Fast Modification**
> 
> Most Linked List problems revolve around manipulating pointers correctly rather than performing calculations.

---

# Key Takeaways

1. Linked Lists store data using nodes.
    
2. Each node contains data and a pointer.
    
3. Nodes are not stored contiguously in memory.
    
4. Random access is impossible.
    
5. Traversal is O(N).
    
6. Insert/Delete at the head is O(1).
    
7. Linked Lists trade access speed for modification speed.
    
8. Fast & Slow Pointer is the most important Linked List interview pattern.
    
9. Reversing a Linked List is the "Two Sum" equivalent of Linked Lists.
    
10. Master Singly Linked Lists before Doubly and Circular Lists.
    