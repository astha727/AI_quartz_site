
> [!Note]
> A **Queue** is one of the most fundamental linear data structures in Computer Science.
>
> While a **Stack** follows **LIFO (Last In First Out)**, a **Queue** follows:
>
> ```text
> FIFO
> ```
>
> ```text
> First In First Out
> ```
>
> The first element inserted into the queue is the first element removed.
>
> Queues are heavily used in:
>
> - BFS (Breadth First Search)
> - Operating Systems
> - CPU Scheduling
> - Print Queues
> - Task Scheduling
> - Networking
> - Message Queues
> - Producer-Consumer Systems
> - Simulation Systems

---

# What is a Queue?

A **Queue** is a linear data structure that follows:

```text
FIFO
```

or

```text
First In First Out
```

The first element added to the queue is the first element removed.

---

# Why Was The Queue Invented?

Suppose tasks arrive continuously:

```text
Task A
Task B
Task C
Task D
```

If Task A arrived first, it should usually be processed first.

A queue ensures fairness:

```text
Arrival Order
      =
Processing Order
```

This makes queues ideal whenever things must be handled in the same order they arrive.

---

# Real Life Example: Waiting Line

Imagine people standing in a line at a coffee shop.

```text
Front

👩 👨 👩 👨 👩

            Rear
```

The first person to enter the line gets served first.

New people always join at the back.

```text
Front

👩 👨 👩 👨 👩 👨

                Rear
```

The next person served is always at the front.

This is exactly how a queue works.

---

# Queue Visualization with Books

Imagine a librarian receiving books to process.

New books always arrive at the back.

```text
Front                                   Rear
 ↓                                       ↓

📘  📗  📙
```

---

## Enqueue (Add Book)

A new book arrives:

```text
Front                                        Rear
 ↓                                            ↓

📘  📗  📙  📕
```

The new book joins the end of the line.

---

## Dequeue (Process Book)

Before:

```text
Front
 ↓

📘  📗  📙  📕
```

Process the first book:

```text
📘
```

After:

```text
Front
 ↓

📗  📙  📕
```

Notice:

```text
First Arrived
      ↓
First Processed
```

---

# Queue Philosophy

Unlike arrays, queues intentionally restrict access.

You can:

```text
✅ Insert at Rear
✅ Remove from Front
```

You cannot:

```text
❌ Insert in Middle
❌ Remove from Middle
❌ Access Random Elements Efficiently
```

This restriction guarantees:

```text
Fair Processing Order
```

where the earliest element is always processed first.

---

# Queue Terminology

## Front

The first element in the queue.

```text
Front
 ↓

[10][20][30][40]
```

The next element to be removed.

Also called:

```text
Head
```

---

## Rear

The last element in the queue.

```text
Front

[10][20][30][40]
                    ↑
                    Rear
```

The newest element added.

Also called:

```text
Tail
```

---

## Enqueue

Insert an element at the rear.

```text
Before

Front
 ↓

[10][20][30]

Enqueue(40)

Front
 ↓

[10][20][30][40]
                    ↑
                    Rear
```

---

## Dequeue

Remove an element from the front.

```text
Before

Front
 ↓

[10][20][30][40]

Dequeue()

Front
 ↓

[20][30][40]
```

Removed:

```text
10
```

---

## Peek / Front

View the front element without removing it.

```text
Front
 ↓

[10][20][30]

Peek() = 10
```

---

## Is Empty

Checks if queue contains any elements.

```python
len(queue) == 0
```

---

## Size

Returns number of elements.

```python
len(queue)
```

---

## Capacity

Maximum number of elements the queue can hold.

```text
Capacity = 10
Current Size = 7
```

---

# Queue Visualization

Start:

```text
[]
```

Enqueue 10

```text
[10]
```

Enqueue 20

```text
[10][20]
```

Enqueue 30

```text
[10][20][30]
```

Dequeue

```text
[20][30]
```

Dequeue

```text
[30]
```

Enqueue 50

```text
[30][50]
```

Notice:

```text
First Inserted
       ↓
First Removed
```

---

# Why Queues Matter

Many advanced algorithms rely on queues because they naturally process items in arrival order.

| Concept | Why Queue is Used |
|----------|------------------|
| BFS (Breadth First Search) | Nodes are explored level-by-level in FIFO order |
| CPU Scheduling | Processes wait their turn for CPU time |
| Printer Scheduling | Documents are printed in arrival order |
| Networking | Packets wait in queues before processing |
| Task Scheduling | Jobs are processed in arrival order |
| Message Brokers | Messages are consumed in FIFO order |
| Simulation Systems | Events are processed chronologically |
| Streaming Systems | Incoming data is buffered using queues |

---

# Stack vs Queue

## Stack

```text
Top
 ↓

📕
📙
📗
📘
```

Remove:

```text
📕
```

Rule:

```text
LIFO
```

```text
Last In First Out
```

---

## Queue

```text
Front                 Rear

📘  📗  📙  📕
```

Remove:

```text
📘
```

Rule:

```text
FIFO
```

```text
First In First Out
```

---

# Queue Operations

| Operation | Description | Time |
|------------|------------|---------|
| Enqueue | Insert at rear | O(1) |
| Dequeue | Remove from front | O(1) |
| Peek | View front | O(1) |
| isEmpty | Check empty | O(1) |
| Size | Count elements | O(1) |

---

# Queue Using Python List

A simple implementation:

```python
queue = []

queue.append(10)
queue.append(20)
queue.append(30)

print(queue)
```

Output:

```text
[10, 20, 30]
```

---

## Dequeue

```python
queue.pop(0)
```

Output:

```text
10
```

---

## Problem with Python Lists

Before:

```text
[10][20][30][40]
```

Remove:

```text
10
```

After:

```text
[20][30][40]
```

Everything shifts left.

```text
20 ← shift
30 ← shift
40 ← shift
```

Complexity:

```text
O(N)
```

This is inefficient for large queues.

---

# Why deque is Preferred in Python

Python provides an optimized queue structure.

```python
from collections import deque

queue = deque()
```

---

## Enqueue

```python
queue.append(10)
queue.append(20)
queue.append(30)
```

---

## Dequeue

```python
queue.popleft()
```

Output:

```text
10
```

Complexity:

```text
O(1)
```

No shifting required.

---

# Implementing Queue Class

```python
from collections import deque

class Queue:

    def __init__(self):
        self.queue = deque()

    def enqueue(self, value):
        self.queue.append(value)

    def dequeue(self):
        if not self.is_empty():
            return self.queue.popleft()

    def peek(self):
        if not self.is_empty():
            return self.queue[0]

    def is_empty(self):
        return len(self.queue) == 0

    def size(self):
        return len(self.queue)
```

---

# Array vs Linked List Queue

## Array Queue

```text
Front                     Rear
 ↓                           ↓

[10][20][30][40][50]
```

### Advantages

✅ Less memory

✅ Cache friendly

✅ Easy implementation

### Disadvantages

❌ Dequeue may require shifting

❌ Fixed size in low-level languages

❌ Resizing can be expensive

---

## Linked List Queue

```text
Front
 ↓

[10] → [20] → [30] → [40]
                           ↑
                         Rear
```

### Advantages

✅ Dynamic size

✅ No shifting

✅ O(1) enqueue

✅ O(1) dequeue

### Disadvantages

❌ Extra pointer memory

❌ More code

❌ Poor cache locality

---

# Queue Memory Visualization

## Array Queue

```text
Address

1000 → A
1001 → B
1002 → C
1003 → D
```

Stored contiguously in memory.

Advantages:

```text
Fast Access
Cache Friendly
```

---

## Linked List Queue

```text
Front

[A] → [B] → [C] → [D]
                       ↑
                     Rear
```

Nodes can be anywhere in memory.

Advantages:

```text
Dynamic Growth
No Shifting
```

---

# Front and Rear Pointers

Every queue maintains two important positions:

```text
Front
```

and

```text
Rear
```

Example:

```text
Front                     Rear
 ↓                           ↓

[10][20][30][40][50]
```

---

## Front

Next element to leave.

```text
10
```

---

## Rear

Most recently inserted.

```text
50
```

---

# Why Enqueue is O(1)

Before:

```text
Front

[10][20][30]
            ↑
          Rear
```

Add:

```text
40
```

After:

```text
Front

[10][20][30][40]
                ↑
              Rear
```

Only one insertion.

```text
O(1)
```

---

# Why Dequeue is O(1)

Before:

```text
Front
 ↓

[10][20][30]
```

Remove:

```text
10
```

After:

```text
Front
 ↓

[20][30]
```

Only one removal.

```text
O(1)
```

(using linked lists or deque)

---

# Why Searching is O(N)

Suppose:

```text
Front

📘 📗 📙 📕 📔
```

Find:

```text
📕
```

Need to inspect:

```text
📘 ❌
📗 ❌
📙 ❌
📕 ✅
```

Worst case:

```text
Check every element
```

Complexity:

```text
O(N)
```

---

# Queue Overflow

Occurs when:

```text
Queue is Full
```

and another insertion is attempted.

Example:

```text
Capacity = 5

[A][B][C][D][E]
```

Attempt:

```text
Enqueue(F)
```

Result:

```text
Overflow
```

---

# Queue Underflow

Occurs when:

```text
Queue is Empty
```

and deletion is attempted.

Example:

```text
[]
```

Attempt:

```text
Dequeue()
```

Result:

```text
Underflow
```

---

# Types of Queues

## 1. Simple Queue

Standard FIFO queue.

```text
Front → [1][2][3][4] ← Rear
```

Insertion:

```text
Rear
```

Deletion:

```text
Front
```

---

## 2. Circular Queue

### Problem

```text
[A][B][C][D]
```

Dequeue twice:

```text
[ ][ ][C][D]
```

Space exists at the front but cannot be reused efficiently.

### Solution

```text
Circular Queue
```

Rear wraps around.

```text
[A][B][C][D]
 ↑         ↓
 └─────────┘
```

Purpose:

```text
Efficient Memory Utilization
```

---

## 3. Double Ended Queue (Deque)

Insertion and deletion allowed at both ends.

```text
Front ⇄ [10][20][30] ⇄ Rear
```

Operations:

```python
append()
appendleft()

pop()
popleft()
```

---

## 4. Priority Queue

Elements leave according to priority.

Not arrival order.

Example:

```text
Emergency Patient (Priority 1)
Regular Patient   (Priority 3)
```

Processed:

```text
Emergency Patient First
```

even if they arrived later.

---

# Queue Applications

## Printer Queue

```text
Doc1
Doc2
Doc3
```

Printed in order received.

---

## Customer Service Line

```text
Customer A
Customer B
Customer C
```

Served in arrival order.

---

## CPU Scheduling

```text
Process1
Process2
Process3
```

Processes wait for CPU time.

---

## Network Packets

```text
Packet A
Packet B
Packet C
```

Packets wait to be processed.

---

## Message Queues

```text
Producer
    ↓
Queue
    ↓
Consumer
```

Common in distributed systems.

---

# BFS and Queues

One of the most important queue applications.

Consider:

```text
        A
      /   \
     B     C
    / \   / \
   D  E  F  G
```

BFS Order:

```text
A
B C
D E F G
```

Queue evolution:

```text
[A]

[B,C]

[C,D,E]

[D,E,F,G]
```

Why?

Because nodes are processed in FIFO order.

---

> [!ai]
>
> Interview Shortcut:
>
> If you hear:
>
> ```text
> Level Order Traversal
> Breadth First Search
> Shortest Path in Unweighted Graph
> Multi-Source BFS
> ```
>
> Think:
>
> ```text
> Queue
> ```

---

# Recognizing Queue Problems

When you see:

### Level-by-Level Processing

```text
Tree Levels
Graph Layers
```

Think:

```text
Queue
```

---

### First Come First Serve

```text
Customers
Tasks
Tickets
Requests
```

Think:

```text
Queue
```

---

### Processing Items in Arrival Order

Think:

```text
Queue
```

---

### Shortest Path in Unweighted Graph

Think:

```text
BFS
↓
Queue
```

---

# Queue Complexity Analysis

| Operation | Complexity |
|------------|------------|
| Enqueue | O(1) |
| Dequeue | O(1) |
| Peek | O(1) |
| Search | O(N) |
| Size | O(1) |
| isEmpty | O(1) |

---

# Common Interview Problems

## Easy

- Implement Queue
- Implement Stack Using Queues
- Number of Recent Calls
- Moving Average from Data Stream

---

## Medium

- Design Circular Queue
- Rotting Oranges
- Open the Lock
- Binary Tree Level Order Traversal

---

## Advanced

- Multi-Source BFS
- Topological Sort
- Sliding Window Maximum
- Shortest Path Problems

---

# Advantages

✅ Maintains processing order

✅ Fair scheduling

✅ O(1) insertion

✅ O(1) deletion

✅ Essential for BFS

✅ Widely used in real-world systems

---

# Disadvantages

❌ No random access

❌ Searching is O(N)

❌ Access restricted to front and rear

---

# Queue Cheat Sheet

| Operation | Complexity |
|------------|------------|
| Enqueue | O(1) |
| Dequeue | O(1) |
| Peek | O(1) |
| Search | O(N) |
| Size | O(1) |
| isEmpty | O(1) |

---

# Interview Takeaways

> [!ai]
>
> If you remember only five things:
>
> 1. Queue follows ==FIFO==
> 2. Enqueue happens at Rear
> 3. Dequeue happens at Front
> 4. BFS is built on Queues
> 5. In Python, use `collections.deque`

---

# Queue Pattern Recognition

| Problem Clue | Think |
|-------------|--------|
| Level Order Traversal | Queue |
| BFS | Queue |
| First Come First Serve | Queue |
| Task Scheduling | Queue |
| Printer Queue | Queue |
| Customer Line | Queue |
| Network Packets | Queue |
| Unweighted Shortest Path | Queue |

---

# Key Takeaways

1. Queue follows ==FIFO (First In First Out)==.
2. Insertions happen at the rear.
3. Deletions happen at the front.
4. Enqueue and Dequeue are O(1).
5. Python's `deque` is preferred over lists.
6. BFS is built on queues.
7. Circular Queues efficiently reuse memory.
8. Deques allow insertion/removal from both ends.
9. Priority Queues remove based on priority rather than arrival order.
10. Mastering queues is essential before learning Trees and Graphs.

---

# Connections

```text
Arrays
   ↓
Linked Lists
   ↓
Stacks
   ↓
Queues
   ↓
Deques
   ↓
Priority Queues
   ↓
Hash Tables
   ↓
Trees
   ↓
Graphs
```

> [!ai]
>
> Before moving forward, solve:
>
> 1. Implement Queue Using Array
> 2. Implement Queue Using Linked List
> 3. Number of Recent Calls
> 4. Binary Tree Level Order Traversal
> 5. Rotting Oranges
>
> These problems build most of the queue intuition needed for BFS, Trees, and Graphs.