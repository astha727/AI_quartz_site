
## What Is Big O?

==Big O describes how an algorithm scales as N becomes very large.==

---

## Rule 1: Ignore Constants

```text
O(2N)
```

becomes

```text
O(N)
```

---

### Example

```python
for i in range(n):
    pass

for i in range(n):
    pass
```

Work:

```text
N + N = 2N
```

Big O:

```text
O(N)
```

---

## Rule 2: Ignore Smaller Terms

```text
O(N² + N + 100)
```

becomes:

```text
O(N²)
```

because N² dominates.

---

## Rule 3: Sequential Operations Add

```python
for i in range(n):
    pass

for j in range(n):
    pass
```

Runtime:

```text
O(N + N)
```

↓

```text
O(N)
```

---

## Rule 4: Nested Operations Multiply

```python
for i in range(n):
    for j in range(n):
        pass
```

Runtime:

```text
O(N × N)
```

↓

```text
O(N²)
```

---

## Rule 5: Different Inputs Use Different Variables

```python
for user in users:
    pass

for product in products:
    pass
```

Runtime:

```text
O(U + P)
```

NOT:

```text
O(N)
```

---

## Best Case

Luckiest scenario.

---

## Worst Case

Unluckiest scenario.

---

## Average Case

Expected scenario.

---

> [!Note]  
> Unless stated otherwise, interviewers usually want Worst-Case Complexity.

---

# Complexity Analysis Checklist

When seeing code:

```text
1. What grows?

2. Are there loops?

3. Are loops nested?

4. Is recursion involved?

5. Are extra data structures used?

6. What dominates growth?
```

---
