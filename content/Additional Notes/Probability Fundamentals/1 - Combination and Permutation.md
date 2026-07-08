# Fundamental Principle of Counting

> [!note]
> The **Fundamental Principle of Counting** (also called the **Multiplication Principle**) is the foundation of permutations, combinations, probability, search complexity, and many AI algorithms.

## Why It Matters for AI

Many AI algorithms explore a **search space**.

The size of that search space depends on how many possible choices exist at each step.

Instead of listing every possibility, we count them mathematically.

Examples:

- Search trees
- State spaces
- [[Branching Factor]]
- Password cracking
- Game trees [[Chapter 6 - Adversarial Search and Games]]
- Constraint Satisfaction Problems (CSPs) [[Chapter 4 - Search in Complex Environments]]
- Machine Learning hypothesis spaces

## Motivation

Imagine a suitcase lock with four wheels.

Each wheel contains digits:

```
0 1 2 3 4 5 6 7 8 9
```

Suppose:

- The first digit is known to be **7**
- The remaining three digits are unknown
- Digits cannot repeat

Instead of listing every possibility manually, we use counting principles to determine how many combinations must be checked.

# Fundamental Principle of Counting

> [!definition]
> If one event can occur in **m** ways, and after that a second event can occur in **n** ways, then the total number of possible outcomes is
>
> $$
> m \times n
> $$


## General Form

If events occur one after another:

- First event → $m$ choices
- Second event → $n$ choices
- Third event → $p$ choices

Then

$$
\boxed{m \times n \times p}
$$

possible outcomes exist.


> [!important]
> The principle applies whenever choices are made **in sequence**.


# Why Multiplication?

Each choice of the first event creates an entirely new set of possibilities for the second event.

For every first choice,

all second choices are possible.

Hence,

the possibilities multiply rather than add.

```
Choice A
├── Option 1
├── Option 2
└── Option 3

Choice B
├── Option 1
├── Option 2
└── Option 3
```

Total outcomes

$$
2 \times 3 = 6
$$

---

# Example 1 — Pants and Shirts

Suppose Mohan owns

- 3 pants
- 2 shirts

How many outfits can he wear?


## Step 1

Choose a pant.

Choices:

$$
3
$$


## Step 2

For each pant,

choose one shirt.

Choices:

$$
2
$$


## Total

$$
3 \times 2 = 6
$$

possible outfits.


### Visualization

```
Pant 1
    Shirt 1
    Shirt 2

Pant 2
    Shirt 1
    Shirt 2

Pant 3
    Shirt 1
    Shirt 2
```

---

# Example 2 — School Bag, Tiffin, Water Bottle

Choices:

- 2 school bags
- 3 tiffin boxes
- 2 water bottles


## Step-by-step

Choose a bag

$$
2
$$

Choose a tiffin

$$
3
$$

Choose a bottle

$$
2
$$

---

Total

$$
2 \times 3 \times 2 = 12
$$

possible combinations.


> [!tip]
> Every new independent choice multiplies the total number of possibilities.

# 6.3 Permutations

> [!quote]  
> **Definition**
> 
> A **permutation** is an arrangement of objects in a **definite order**, where the **order matters**.


## Why Permutations?

In many counting problems, the goal is **not merely to choose objects**, but to determine **how many different ordered arrangements** are possible.

For example, consider the letters of the word **ROSE**.

Different arrangements include:

- ROSE
    
- REOS
    
- SORE
    
- ORES
    

Although the same letters are used each time, every arrangement is considered different because the **order of the letters changes**.

This idea is called a **permutation**.


## Example: Word "NUMBER"

Find the number of 3-letter words that can be formed from the letters of **NUMBER**, assuming repetition is **not allowed**.

Available letters:

```
N U M B E R
```

There are **6 distinct letters**.

Using the multiplication principle:

- First position → 6 choices
    
- Second position → 5 choices
    
- Third position → 4 choices
    

Therefore,

$$  
6\times5\times4=120  
$$

Thus,

> **Number of 3-letter arrangements = 120**


## When Repetition is Allowed

If letters may repeat,

each position can be filled by **any of the six letters**.

Therefore,

- First position → 6 choices
    
- Second position → 6 choices
    
- Third position → 6 choices
    

Hence,

$$  
6^3=216  
$$


> [!summary]
> 
> The key difference is:
> 
> - **Without repetition:** available choices decrease after every selection.
>     
> - **With repetition:** every position always has the same number of choices.
>     

---

# 6.3.1 Permutations of Distinct Objects

Suppose there are

- **n distinct objects**
    
- we arrange **r of them**
    
- no object can repeat.
    

Imagine filling **r empty positions** one by one.

```
_  _  _  ...  _
```

### Filling the positions

The first position can be filled in

$$  
n  
$$

ways.

After one object has been used,

the second position has

$$  
n-1  
$$

choices.

Similarly,

- third position → $(n-2)$ choices
    
- fourth position → $(n-3)$ choices
    

Continuing this process,

the last position has

$$  
n-r+1  
$$

choices.

Applying the multiplication principle,

$$  
n(n-1)(n-2)\cdots(n-r+1)  
$$


> [!theorem]  
> **Permutation Formula**
> 
> The number of permutations of **n distinct objects taken r at a time** is
> 
> $$  
> {}^{n}P_r = 
> 
> n(n-1)(n-2)\cdots(n-r+1)  
> $$


## Interpretation

The formula counts the number of **ordered selections**.

Changing the order produces a different permutation.

For example,

```
ABC
```

and

```
BAC
```

are two different permutations.

---

# 6.3.2 Factorial Notation

Writing long products repeatedly becomes inconvenient.

To simplify notation, factorial is introduced.

> [!definition]  
> For any natural number
> 
> $$  
> n  
> $$
> 
> factorial is defined as
> 
> $$  
> n!=1\times2\times3\times\cdots\times n  
> $$


## Examples

$$  
1!=1  
$$

$$  
2!=2  
$$

$$  
3!=6  
$$

$$  
4!=24  
$$

$$  
5!=120  
$$


## Recursive Form

Factorials satisfy

$$  
n!=n(n-1)!  
$$

which can be expanded repeatedly:

$$  
n!=n(n-1)(n-2)!  
$$

or

$$  
n!=n(n-1)(n-2)(n-3)!  
$$

---

> [!important]  
> By definition,
> 
> $$  
> 0!=1  
> $$


## Examples

### Example 1

Evaluate

$$  
5!  
$$

Solution

$$  
5!=120  
$$


---

### Example 2

Evaluate

$$  
\frac{n!}{r!(n-r)!}  
$$

for

$$  
n=5,\quad r=2  
$$

Substituting,

$$

\frac{5!}{2!3!}

10  
$$

---

### Example 3

If

$$  
\frac1{8!}+\frac1{9!}

\frac{x}{10!},  
$$

find

$$  
x.  
$$

Using

$$  
9!=9\times8!  
$$

and

$$  
10!=10\times9\times8!,  
$$

simplification gives

$$  
x=100.  
$$

---

> [!tip]  
> Whenever factorials appear in fractions,
> 
> **expand only as much as necessary.**
> 
> Most terms cancel immediately.