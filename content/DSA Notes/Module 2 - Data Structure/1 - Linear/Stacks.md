# Stack

> [!info]
> A **Stack** is a linear data structure that follows the **LIFO (Last In First Out)** principle.
>
> The last element inserted is the first element removed.

---

# Why Learn Stacks?

Stacks are one of the most important data structures in DSA.
Many advanced DSA and software engineering concepts are built on stacks because they naturally model situations where the most recent item/action must be processed first.  
  
| Concept                      | Why a Stack is Used                                                                                      |     |
| ---------------------------- | -------------------------------------------------------------------------------------------------------- | --- |
| **Recursion**                | Every recursive function call is pushed onto the call stack and popped when it returns.                  |     |
| **DFS (Depth First Search)** | DFS explores one path as deep as possible before backtracking, which is naturally handled using a stack. |     |
| **Backtracking**             | Previous decisions are stored and reversed in LIFO order when a path fails.                              |     |
| **Expression Evaluation**    | Compilers and calculators use stacks to evaluate infix, postfix, and prefix expressions.                 |     |
| **Browser History**          | Recently visited pages are stored so the latest page can be returned to first when pressing Back.        |     |
| **Undo/Redo Systems**        | Recent actions are pushed onto a stack and undone in reverse order.                                      |     |
| **Function Calls**           | The program keeps track of active function calls using the call stack.                                   |     |
| **Tree Traversals**          | Iterative tree traversals (Preorder, Inorder, Postorder) commonly use stacks.                            |     |
| **Graph Algorithms**         | Many graph algorithms, especially DFS-based ones, rely on stacks to manage exploration order.            |     |


> [!tip]
> If Arrays are the foundation of DSA,
>
> Stacks are the foundation of Recursion and DFS.

---

# Real Life Intuition

## Stack of Books

```text
          ┌─────┐
Top  →│  📘    │
          ├─────┤
          │  📗    │
          ├─────┤
          │  📕    │
          ├─────┤
          │  📙    │
          └─────┘
```

Add a book:

```text
          ┌─────┐
Top  →│   📓   │
          ├─────┤
          │  📘    │
          ├─────┤
          │  📗    │
          ├─────┤
          │  📕    │
          ├─────┤
          │  📙    │
          └─────┘
```

Remove a book:

```text
                   ┌─────┐
Remove →    │ 📓 │
                   └─────┘
```

The most recently added book leaves first.

This is:

```text
LIFO
Last In First Out
```

---

# Stack Philosophy

Stacks intentionally restrict access.

You can only access:

```text
Top Element
```

Not:

```text
Middle Element ❌
Bottom Element ❌
Random Index ❌
```

This restriction gives us:

```text
Push  → O(1)
Pop   → O(1)
Peek  → O(1)
```

---

# Core Operations

In order to make manipulations in a stack, there are certain operations provided to us.

- ***push()*** to insert an element into the stack.
- ***pop()*** to remove an element from the stack.
- ***top()*** Returns the top element of the stack.
- ***isEmpty()*** returns true if stack is empty else false.
- ***size()*** returns the size of the stack.

## Push

Insert element onto stack.

### Before

```text
Top
 ↓

┌─────┐
│   20    │
├─────┤
│   10     │
└─────┘
```

### Push(30)

```text
Top
 ↓

┌─────┐
│   30    │
├─────┤
│   20    │
├─────┤
│   10    │
└─────┘
```

Time Complexity:

```text
O(1)
```

---

## Pop

Remove top element.

### Before

```text
Top
 ↓

┌─────┐
│ 30  │
├─────┤
│ 20  │
├─────┤
│ 10  │
└─────┘
```

### Pop()

```text
Removed → 30
```

Result:

```text
Top
 ↓

┌─────┐
│ 20  │
├─────┤
│ 10  │
└─────┘
```

Time Complexity:

```text
O(1)
```

---

## Peek / Top

View top element without removing it.

```text
Top
 ↓

┌─────┐
│ 30  │
├─────┤
│ 20  │
├─────┤
│ 10  │
└─────┘
```

Result:

```text
30
```

Time Complexity:

```text
O(1)
```

---

## Is Empty

```python
len(stack) == 0
```

Returns:

```text
True / False
```

---

## Size

```python
len(stack)
```

Returns number of elements.

---

# Stack Visualization

Start:

```text
[]
```

Push(10)

```text
┌─────┐
│ 10  │
└─────┘
```

Push(20)

```text
┌─────┐
│ 20  │
├─────┤
│ 10  │
└─────┘
```

Push(30)

```text
┌─────┐
│ 30  │
├─────┤
│ 20  │
├─────┤
│ 10  │
└─────┘
```

Pop()

```text
Removed → 30
```

```text
┌─────┐
│ 20  │
├─────┤
│ 10  │
└─────┘
```

---

# Stack ADT

A stack supports:

| Operation | Description |
|------------|------------|
| push(x) | Insert |
| pop() | Remove top |
| peek() | View top |
| isEmpty() | Check empty |
| size() | Number of elements |

---

# Stack Implementation Using Arrays

## Memory Layout

```text
Index

0    1    2    3
↓    ↓    ↓    ↓

10   20   30   40
                    ↑
                    Top
```

Elements are stored contiguously.

---

## Python Implementation

```python
stack = []

stack.append(10)
stack.append(20)
stack.append(30)

print(stack)
```

Output:

```python
[10, 20, 30]
```

---

## Pop

```python
stack.pop()
```

Output:

```python
30
```

---

## Peek

```python
stack[-1]
```

Output:

```python
20
```

---

# Stack Class Implementation

```python
class Stack:

    def __init__(self):
        self.stack = []

    def push(self, value):
        self.stack.append(value)

    def pop(self):
        if self.is_empty():
            return None
        return self.stack.pop()

    def peek(self):
        if self.is_empty():
            return None
        return self.stack[-1]

    def is_empty(self):
        return len(self.stack) == 0

    def size(self):
        return len(self.stack)
```

---

# Stack Using Linked List

## Why Linked Lists Work Well

Insertion and deletion happen only at:

```text
Top
```

Exactly where linked lists are strongest.

---

## Visualization

```text
Top
 ↓

┌─────┐     ┌─────┐     ┌─────┐
│ 30  │ →   │ 20  │ →   │ 10  │ → null
└─────┘     └─────┘     └─────┘
```

Push(40):

```text
Top
 ↓

┌─────┐
│ 40  │
└──┬──┘
   ↓
┌─────┐
│ 30  │ → 20 → 10
└─────┘
```

Pop():

```text
Remove 40
```

No traversal needed.

---

# Array vs Linked List Stack

| Feature | Array | Linked List |
|----------|--------|-------------|
| Push | O(1) | O(1) |
| Pop | O(1) | O(1) |
| Memory | Less | More |
| Cache Friendly | Yes | No |
| Dynamic Size | Limited | Yes |
| Implementation | Easier | Harder |

---

> [!important]
> Interview Answer:
>
> Arrays are generally preferred because they are:
>
> - Simpler
> - Faster in practice
> - Cache friendly
>
> Linked Lists are preferred when dynamic growth is critical.

---

# Why Push Is O(1)

Push only touches the top.

```text
Before

30
20
10
```

Push 40

```text
40
30
20
10
```

Only one operation.

```text
O(1)
```

---

# Why Pop Is O(1)

Remove only the top element.

```text
40
30
20
```

After pop:

```text
30
20
```

No traversal.

```text
O(1)
```

---

# Why Search Is O(N)

Find:

```text
20
```

Stack:

```text
50
40
30
20
10
```

Need to check:

```text
50 ❌
40 ❌
30 ❌
20 ✅
```

Worst case:

```text
Every element
```

Complexity:

```text
O(N)
```

---

# Call Stack

Every running program uses a stack internally.

Example:

```python
def A():
    B()

def B():
    C()

def C():
    pass
```

Execution:

```text
A()
 ↓
B()
 ↓
C()
```

Call Stack:

```text
Top

┌─────┐
│ C() │
├─────┤
│ B() │
├─────┤
│ A() │
└─────┘
```

As functions finish:

```text
Pop C()
Pop B()
Pop A()
```

---

# Recursion Uses a Stack

```python
def countdown(n):
    if n == 0:
        return

    countdown(n-1)
```

Call:

```python
countdown(3)
```

Stack becomes:

```text
Top

countdown(0)
countdown(1)
countdown(2)
countdown(3)
```

Then:

```text
Pop
Pop
Pop
Pop
```

Every recursive algorithm uses stack memory.

---

# Stack Overflow

Not the website.

The programming error.

```python
def recurse():
    recurse()
```

Execution:

```text
recurse()
recurse()
recurse()
recurse()
...
```

Call stack keeps growing.

Eventually:

```text
Memory Exhausted
```

Result:

```text
StackOverflowError
```

---

# Browser Back Button

Visited:

```text
Google
YouTube
GitHub
LeetCode
```

Stack:

```text
Top

LeetCode
GitHub
YouTube
Google
```

Back button:

```text
Pop LeetCode
```

Back again:

```text
Pop GitHub
```

---

# Undo Feature

Typing:

```text
A
AB
ABC
ABCD
```

Stack:

```text
ABCD
ABC
AB
A
```

Undo:

```text
Pop ABCD
```

Undo again:

```text
Pop ABC
```

---

# Parentheses Matching

Input:

```text
((()))
```

Algorithm:

```text
( → Push
( → Push
( → Push
) → Pop
) → Pop
) → Pop
```

Stack becomes empty.

Valid.

---

# Recognizing Stack Problems

If you see:

### Undo

```text
Ctrl + Z
```

Think:

```text
Stack
```

---

### Browser Back

Think:

```text
Stack
```

---

### Nested Structures

```text
((()))
{{[]}}
```

Think:

```text
Stack
```

---

### Function Calls

Think:

```text
Stack
```

---

### DFS

Think:

```text
Stack
```

---

### Backtracking

Think:

```text
Stack
```

---

# Monotonic Stack

A stack that remains:

```text
Increasing
```

or

```text
Decreasing
```

throughout execution.

Example:

```text
5 4 3 2 1
```

Monotonically decreasing.

Used in:

- Next Greater Element
- Daily Temperatures
- Stock Span
- Largest Rectangle in Histogram

---

> [!tip]
> Interview Shortcut:
>
> If you see:
>
> - Next Greater Element
> - Previous Greater Element
> - Next Smaller Element
> - Previous Smaller Element
>
> Think:
>
> **Monotonic Stack**

---

# Complexity Cheat Sheet

| Operation | Complexity |
|------------|------------|
| Push | O(1) |
| Pop | O(1) |
| Peek | O(1) |
| Search | O(N) |
| Size | O(1) |
| isEmpty | O(1) |

---

# Advantages

✅ Fast insertion

✅ Fast deletion

✅ Excellent for recursion

✅ Perfect for backtracking

✅ Used by compilers

✅ Easy to implement

---

# Disadvantages

❌ No random access

❌ Searching is O(N)

❌ Only top element accessible

---

# Common Interview Problems

## Easy

- Valid Parentheses
- Implement Stack
- Baseball Game
- Backspace String Compare

## Medium

- Min Stack
- Daily Temperatures
- Asteroid Collision
- Evaluate Reverse Polish Notation

## Hard

- Largest Rectangle in Histogram
- Trapping Rain Water
- Basic Calculator

---

# Key Takeaways

1. Stack follows **LIFO**.
2. Push, Pop, Peek are **O(1)**.
3. Stacks can be implemented using Arrays or Linked Lists.
4. Every recursive function uses a Call Stack.
5. Browser History and Undo systems are classic stack applications.
6. Parentheses matching is a fundamental stack problem.
7. Monotonic Stacks are one of the most important interview patterns.
8. DFS and Backtracking rely heavily on stacks.