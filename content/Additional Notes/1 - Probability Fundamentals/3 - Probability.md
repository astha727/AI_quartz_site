# Probability — Events

> [!quote]  
> _"Where a mathematical reasoning can be had, it is as great a folly to make use of any other, as to grope for a thing in the dark, when you have a candle in your hand."_  
> — **John Arbuthnot**


# Why Events Matter

Probability is built on three fundamental ideas:

1. **Random Experiment**
    
2. **Sample Space**
    
3. **Event**
    

Once these are understood, everything else in probability - conditional probability, Bayes' theorem, Bayesian networks, and machine learning builds upon them.

# Event

## Definition

An **event** is **any subset of the sample space**.

If the sample space is

$$  
S  
$$

then an event is simply

$$  
E \subseteq S  
$$

In other words,

> An event is a collection of outcomes that satisfy a particular condition.


## Example

### Experiment

Toss two coins.

Sample space:

$$  
S={HH,HT,TH,TT}  
$$

Suppose we are interested in

> Exactly one head.

Then

$$  
E={HT,TH}  
$$

Since

$$  
E\subseteq S  
$$

it is a valid event.

---

# Occurrence of an Event

An event occurs if the observed outcome belongs to that event.

If

$$  
\omega\in E  
$$

then

> Event **E has occurred.**

Otherwise,

$$  
\omega\notin E  
$$

and the event has **not** occurred.

## Example

Roll a die.

Event:

> Number less than 4

$$  
E={1,2,3}  
$$

If the die shows

- 1 
    
- 2 
    
- 3 
    

the event occurs.

If the die shows

- 4
    
- 5
    
- 6
    

the event does not occur.

# Types of Events

## 1. Impossible Event

An event that can never happen.

It contains **no outcomes**.

$$  
E=\varnothing  
$$

### Example

Rolling a 7 on a standard die.

$$  
E=\varnothing  
$$


## 2. Sure (Certain) Event

An event that always happens.

It contains every possible outcome.

$$  
E=S  
$$

### Example

Rolling an odd or even number on a die.

$$  
E={1,2,3,4,5,6}=S  
$$



## 3. Simple (Elementary) Event

Contains **exactly one outcome**.

Example:

Two coin tosses

$$  
S={HH,HT,TH,TT}  
$$

Simple events are

$$  
{HH},{HT},{TH},{TT}  
$$


## 4. Compound Event

Contains **more than one outcome**.

Example

Exactly one head:

$$  
{HT,TH}  
$$

At least one head:

$$  
{HH,HT,TH}  
$$


# Algebra of Events

Probability follows the same algebra as sets.


## Complement

Everything **not** in the event.

Notation

$$  
A'  
$$

or

$$  
A^c  
$$

Formula

$$  
A'=S-A  
$$

### Example

Die

Event:

Prime number

$$  
A={2,3,5}  
$$

Complement

$$  
A'={1,4,6}  
$$


## Union (A or B)

Occurs if **either event happens**.

Notation

$$  
A\cup B  
$$

### Example

Roll a die.

Prime number

$$  
A={2,3,5}  
$$

Odd number

$$  
B={1,3,5}  
$$

Then

$$  
A\cup B={1,2,3,5}  
$$

## Intersection (A and B)

Occurs only when **both events happen simultaneously**.

Notation

$$  
A\cap B  
$$

Example

$$  
A={2,3,5}  
$$

$$  
B={1,3,5}  
$$

Then

$$  
A\cap B={3,5}  
$$


## Difference (A but not B)

Notation

$$  
A-B  
$$

or

$$  
A\cap B'  
$$

Example

$$  
A={2,3,5}  
$$

$$  
B={1,3,5}  
$$

Then

$$  
A-B={2}  
$$

---

# Mutually Exclusive Events

Two events are **mutually exclusive** if they **cannot occur together**.

Mathematically,

$$  
A\cap B=\varnothing  
$$


## Example

Roll a die.

Odd

$$  
A={1,3,5}  
$$

Even

$$  
B={2,4,6}  
$$

Since

$$  
A\cap B=\varnothing  
$$

they are mutually exclusive.


## Counterexample

Odd numbers

$$  
A={1,3,5}  
$$

Numbers less than 4

$$  
B={1,2,3}  
$$

Now

$$  
A\cap B={1,3}  
$$

They are **not** mutually exclusive.

---

# Exhaustive Events

Events are **exhaustive** if together they cover every possible outcome.

Mathematically,

$$  
E_1\cup E_2\cup\cdots\cup E_n=S  
$$

At least one of the events must occur.


## Example

Roll a die.

Let

$$  
A={1,2,3}  
$$

$$  
B={4}  
$$

$$  
C={5,6}  
$$

Then

$$  
A\cup B\cup C=S  
$$

Hence,

- A, B and C are exhaustive.
    

---

# Mutually Exclusive and Exhaustive

A collection of events is both if

1. They never overlap.
    

$$  
E_i\cap E_j=\varnothing  
$$

2. Together they cover the entire sample space.
    

$$  
E_1\cup E_2\cup\cdots\cup E_n=S  
$$

These partitions of the sample space are fundamental in probability and later appear in Bayes' theorem.

---

# Quick Summary

| Concept            | Meaning                | Mathematical Form     |
| ------------------ | ---------------------- | --------------------- |
| Event              | Subset of sample space | $E\subseteq S$        |
| Impossible Event   | Never occurs           | $varnothing$          |
| Sure Event         | Always occurs          | (S)                   |
| Simple Event       | One outcome            |                       |
| Compound Event     | Multiple outcomes      |                       |
| Complement         | Not A                  | (A'= S-A)             |
| Union              | A or B                 | $A\cup B$             |
| Intersection       | A and B                | $A\cap B$             |
| Difference         | A but not B            | (A-B)                 |
| Mutually Exclusive | Cannot occur together  | $A\cap B=\varnothing$ |
| Exhaustive         | Cover every outcome    | $\bigcup E_i=S$       |

# Connection to AI

These ideas become the language of uncertainty in AI.

They are used in:

- Probability theory
    
- Conditional probability
    
- Bayes' theorem
    
- Bayesian networks
    
- Hidden Markov Models
    
- Probabilistic graphical models
    
- Machine learning
    
- Reinforcement learning
    
- Robotics
    
- Medical diagnosis systems
    

Almost every probabilistic AI algorithm starts by defining **events** over a sample space.


