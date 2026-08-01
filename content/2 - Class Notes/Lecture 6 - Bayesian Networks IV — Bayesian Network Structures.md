Previous:  [[Lecture 6 - Bayesian Networks III — Conditional Independence]]
Next: [[Lecture 6 – Bayesian Networks V -  Probabilistic Inference]]
# A New Bayesian Network Structure

Until now, we studied a network where **one hidden cause** produced **two observations**.


```text
          Cause
         /     \
        ▼       ▼
 Observation Observation
```

The lecture now introduces the opposite structure.

Two independent causes influence a single outcome.

```text
Sunny ───► Happiness ◄──── Raise
```

where

- Sunny = whether the weather is sunny
- Raise = whether you receive a salary raise
- Happiness = whether you are happy

---

# Prior Probabilities

The lecture assumes

$$
P(Sunny)=0.7
$$

and

$$
P(Raise)=0.01
$$

These two causes are assumed to be independent.

---

# Happiness Probabilities

The conditional probabilities are

| Sunny | Raise | $$P(Happy)$$ |
|--------|-------|--------------|
| Yes | Yes | 1.0 |
| No | Yes | 0.9 |
| Yes | No | 0.7 |
| No | No | 0.1 |

These values define how the two causes jointly influence Happiness.

---

# Independence Before Observing Happiness

The lecture asks

> What is

$$
P(Raise\mid Sunny)?
$$

Because neither variable causes the other,

and Happiness has **not** been observed,

the answer is simply

$$
P(Raise\mid Sunny)
=
P(Raise)
=
0.01
$$

Knowing that the weather is sunny tells us nothing about whether we received a raise.

The two causes remain independent.

---

# Why?

Looking at the network,

```text
Sunny ───► Happiness ◄──── Raise
```

Sunny and Raise only meet at their common effect (Happiness).

Since Happiness has **not** been observed,

there is no mechanism through which information can pass between Sunny and Raise.

Therefore,

they remain independent.

---

# Looking Ahead

The lecture ends by introducing this new network structure.

Later in the course, we will see that **observing Happiness changes everything**.

Once the common effect is observed,

Sunny and Raise are no longer independent.

This phenomenon is known as **Explaining Away**, one of the most important ideas in Bayesian Networks.

---

# Key Takeaways

- Independence and conditional independence are different concepts.
- Conditional independence does **not** imply ordinary independence.
- Ordinary independence does **not** imply conditional independence.
- In the cancer example, the first test changes our belief about Cancer, which changes the probability of the second test.
- A Bayesian Network with two independent causes and one common effect behaves differently from the common-cause structure studied earlier.
- Before observing the common effect, the two causes remain independent.

---
# Explaining Away

> [!info] Prerequisites
> - [[6 - Bayes' Theorem]]
> - [[Lecture 6 - Bayesian Networks I — Foundations & Bayes Rule]]

---

# The Idea

One of the most important reasoning patterns in Bayes Networks is called **Explaining Away**.

It occurs when:

- two independent causes
- produce the same effect.

Once the effect is observed, learning one cause makes the other cause **less likely**.

## The Bayes Network

```

Sunny ─────▶
\
▶ Happy
/
Raise ─────▶

```

- Sunny (S)
- Raise (R)
- Happy (H)

Sunny and Raise are initially independent.

Both influence Happiness.

## Intuition

Suppose someone notices that Sebastian is very happy.

They wonder:

> "Why is he happy?"

Two explanations exist:

- it is sunny
- he received a raise

Initially both are possible.

Now suppose they look outside.

It is sunny.

The happiness is already explained.

Therefore,

receiving a raise becomes **less necessary** to explain the observation.

This is called

> **Explaining Away**

One explanation reduces belief in the other explanation.

---

# Given Probabilities

The lecture defines

$$
P(S)=0.7
$$

$$
P(R)=0.01
$$

Conditional happiness probabilities

|Sunny|Raise|P(Happy)|
|------|------|---------|
|Yes|Yes|1.0|
|No|Yes|0.9|
|Yes|No|0.7|
|No|No|0.1|

---

# Question 1

Compute

$$
P(R|H,S)
$$

Probability of receiving a raise given

- Sebastian is happy
- it is sunny

---

# Step 1

Apply Bayes Rule

$$
P(R|H,S)=
\frac{P(H|R,S)P(R|S)}
{P(H|S)}
$$

---

# Step 2

Use Independence

Sunny and Raise are independent.

Therefore

$$
P(R|S)=P(R)
$$

So

$$
P(R)=0.01
$$

---

# Step 3

Expand the Denominator

Using the Law of Total Probability,

$$
P(H|S)
=
P(H|R,S)P(R)
+
P(H|\neg R,S)P(\neg R)
$$

---

# Step 4

Insert Numbers

From the table,

$$
P(H|R,S)=1
$$

$$
P(H|\neg R,S)=0.7
$$

Also,

$$
P(R)=0.01
$$

$$
P(\neg R)=0.99
$$

Therefore,

$$
P(H|S)
=
1(0.01)
+
0.7(0.99)
$$

$$
=
0.703
$$

---

# Final Result

$$
P(R|H,S)
=
\frac{1\times0.01}
{0.703}
\approx0.0142
$$

Only about

**1.4%**

---

# Why?

Because

the sunshine already explains why Sebastian is happy.

There is little need to believe a raise also occurred.

This is the essence of **explaining away**.

---

# Question 2

Now suppose

we only know

Sebastian is happy.

We do **not** know the weather.

Compute

$$
P(R|H)
$$

---

# Step 1

Apply Bayes Rule

$$
P(R|H)
=
\frac{P(H|R)P(R)}
{P(H)}
$$

Now we must compute

- $$P(H|R)$$
- $$P(H)$$

using the Law of Total Probability.

---

# Computing $$P(H)$$

Consider all four possibilities.

$$
P(H)
=
P(H|S,R)P(S,R)
+
P(H|\neg S,R)P(\neg S,R)
+
P(H|S,\neg R)P(S,\neg R)
+
P(H|\neg S,\neg R)P(\neg S,\neg R)
$$

Plugging in the lecture values gives

$$
P(H)=0.5245
$$

---

# Computing $$P(H|R)$$

Again use total probability.

$$
P(H|R)
=
P(H|S,R)P(S)
+
P(H|\neg S,R)P(\neg S)
$$

Insert numbers

$$
=
1(0.7)+0.9(0.3)
$$

$$
=
0.97
$$

---

# Final Result

$$
P(R|H)
=
\frac{0.97\times0.01}
{0.5245}
\approx0.0185
$$

---

# Compare the Results

Knowing only happiness:

$$
P(R|H)=0.0185
$$

Knowing happiness **and** sunshine:

$$
P(R|H,S)=0.0142
$$

Notice

$$
0.0142
<
0.0185
$$

Knowing it is sunny makes the raise **less likely**.

---

# Question 3

Now suppose

Sebastian is happy

and

it is **not** sunny.

Compute

$$
P(R|H,\neg S)
$$

The lecture gives

$$
P(R|H,\neg S)
=
0.0833
$$

---

# Interpretation

Now the weather cannot explain happiness.

Therefore,

receiving a raise becomes much more likely.

Compare

|Evidence|Probability of Raise|
|---------|-------------------|
|Nothing|0.01|
|Happy|0.0185|
|Happy + Sunny|0.0142|
|Happy + Not Sunny|0.0833|

Notice how observing sunshine decreases the probability of a raise,

while observing bad weather greatly increases it.

---

# Conditional Dependence

Initially

Sunny and Raise are independent.

$$
S\perp R
$$

However,

after observing Happiness,

they become dependent.

$$
S\not\perp R\mid H
$$

Knowing one cause changes our belief about the other.

This phenomenon is called

> **Explaining Away**

and is one of the defining reasoning patterns in Bayes Networks.

---

# Key Takeaways

- Multiple independent causes can produce the same effect.
- Observing the effect couples the causes.
- Learning one cause reduces belief in the others.
- Explaining Away creates conditional dependence from independent variables.

# General Bayes Networks

# From Small Networks to Large Networks

So far, we have seen Bayes Networks with only a few variables.

Examples include:

- Cancer → Test
- Cancer → Test 1, Test 2
- Sunny + Raise → Happiness

Real-world AI systems contain many variables.

Instead of writing one enormous joint probability table, Bayes Networks exploit **conditional independence** to represent the same distribution much more compactly.

---

# General Structure

A Bayes Network is a graph where:

- each node represents a random variable
- directed edges represent direct probabilistic influence
- every node stores only the probability conditioned on its parents

Example:

```

A      B
\    /
▼  ▼
C
/ \
▼   ▼
D   E

```

---

# What Probabilities Are Stored?

Variables with **no parents** store only their prior probabilities.

Therefore,

$$
P(A)
$$

$$
P(B)
$$

Node C has two parents.

Therefore it stores

$$
P(C|A,B)
$$

Node D has one parent.

Therefore it stores

$$
P(D|C)
$$

Node E also stores

$$
P(E|C)
$$

Notice that every node only depends on its immediate parents.

---

# Joint Probability

A remarkable property of Bayes Networks is that the complete joint distribution factors into small local probabilities.

For the network above,

$$
P(A,B,C,D,E)
=
P(A)
P(B)
P(C|A,B)
P(D|C)
P(E|C)
$$

Instead of storing one enormous table,

we simply multiply together the local probability tables.

---

# Why Is This Useful?

Without a Bayes Network,

the joint probability table must contain every possible combination of variables.

For

5 binary variables,

there are

$$
2^5=32
$$

possible assignments.

Since probabilities must sum to one,

we need

$$
2^5-1=31
$$

independent probability values.

---

# Using a Bayes Network

Instead,

we only store probabilities for each node.

For the example network:

### Node A

No parents.

Needs

$$
1
$$

parameter.

---

### Node B

No parents.

Needs

$$
1
$$

parameter.

---

### Node C

Parents:

- A
- B

Two binary parents create

$$
2^2=4
$$

parent combinations.

Therefore

C requires

$$
4
$$

parameters.

---

### Node D

One parent.

Needs

$$
2^1=2
$$

parameters.

---

### Node E

One parent.

Needs

$$
2^1=2
$$

parameters.

---

# Total Parameters

Therefore

$$
1+1+4+2+2=10
$$

parameters.

Compare this with

31

parameters for the full joint distribution.

The Bayes Network stores exactly the same probability distribution much more efficiently.

---

# General Rule

For a **binary** variable with K parents, the Conditional Probability Table (CPT) requires $2^K$ parameters.

Examples

|Number of Parents|Parameters Needed|
|-----------------|-----------------|
|0|1|
|1|2|
|2|4|
|3|8|
|4|16|

This is one of the most important counting rules for Bayes Networks.

---

# Lecture Example 1

Network:

```

A      B
\    /
▼  ▼
C
/ \
▼   ▼
D   E

```

Count the parameters.

|Node|Parents|Parameters|
|----|-------|----------|
|A|0|1|
|B|0|1|
|C|2|4|
|D|1|2|
|E|1|2|

Total:

$$
1+1+4+2+2=10
$$

---

# Lecture Quiz

Consider

```

A   B   C
\ | /
▼
D
/|\
▼▼▼
E F G

C ─► G

```

Count the parameters.

## Step 1

A

No parents

$$
1
$$


## Step 2

B

No parents

$$
1
$$


## Step 3

C

No parents

$$
1
$$


## Step 4

D

Three parents.

Therefore

$$
2^3=8
$$

parameters.


## Step 5

E

One parent. 2




## Step 6

F

One parent. 2


## Step 7

G

Two parents.

$$
2^2=4
$$

---

# Total

$$
1+1+1+8+2+2+4=19
$$

which matches the lecture solution.

---

# Car Diagnosis Example

The lecture discusses a car diagnosis network containing

16 binary variables.

Without a Bayes Network,

the complete joint distribution would require

$$
2^{16}-1
=
65,\!535
$$

probabilities.

Using the Bayes Network, only 47 probability values are required.

This enormous reduction is the main practical advantage of Bayes Networks.

---

# Why Bayes Networks Scale

As the number of variables increases,

the complete joint distribution grows exponentially.

Bayes Networks avoid this explosion because they only model **local dependencies**.

Instead of every variable depending on every other variable,

each variable depends only on its parents.

Conditional independence removes unnecessary probability entries.

---

# Key Takeaways

- A Bayes Network represents a full joint distribution.
- Each node stores probabilities conditioned only on its parents.
- The joint probability is the product of the local conditional probabilities.
- A binary node with **K** parents requires $2^K$ probability values.
- Bayes Networks drastically reduce storage requirements compared to full joint probability tables.
- This compact representation is the primary reason Bayes Networks are widely used in Artificial Intelligence.

# D-Separation I

# What is D-Separation?

After learning that Bayes Networks encode conditional independence, we now need a systematic way to determine **which variables are independent**.

This concept is called **D-Separation** (Directional Separation).

D-Separation allows us to answer questions such as:

- Are two variables independent?
- Does observing another variable make them independent?
- Does observing another variable make them dependent?

Instead of computing probabilities, we inspect the graph structure.

---

# Example 1

Consider the following network.

```

A → B → C

↓

D

```

The lecture asks several conditional independence questions.

## Question 1

Is

$$
C \perp A
$$

?

### Answer

**No.**

Reason:

There is an active path

$$
A \rightarrow B \rightarrow C
$$

Information can flow from A to C.

Therefore,

A and C are **not independent**.

## Question 2

Is

$$
C \perp A \mid B
$$

?

### Answer

**Yes.**

Once B is known,

A provides no additional information about C.

Knowing B completely blocks the influence from A.

The path

$$
A \rightarrow B \rightarrow C
$$

is blocked.


## Question 3

Is

$$
C \perp D
$$

?

### Answer

**No.**

D depends on A.

A influences C.

Therefore,

information can travel

$$
D \leftarrow A \rightarrow B \rightarrow C
$$

so C and D remain dependent.


## Question 4

Is

$$
C \perp D \mid A
$$

?

### Answer

**Yes.**

Once A is known,

both C and D are determined only through A.

Learning D cannot tell us anything more about C.

The influence is blocked.


## Question 5

Is

$$
E \perp C \mid D
$$

?

### Answer

**Yes.**

The lecture states that knowing D blocks the remaining influence between C and E.

---

# Important Observation

Knowing an intermediate variable often blocks information flow.

This is one of the central ideas behind D-Separation.

---

# Example 2

Now consider another network.

```

A      B
\    /
▼  ▼
C
|
▼
E

```

The lecture asks:

## Question 1

Is

$$
A \perp E
$$

?

### Answer

**No.**

There is a path

$$
A \rightarrow C \rightarrow E
$$

Therefore,

A influences E.


## Question 2

Is

$$
A \perp E \mid B
$$

?

### Answer

**No.**

Knowing B does not block

A → C → E.

The influence from A still exists.

## Question 3

Is

$$
A \perp E \mid C
$$

?

### Answer

**Yes.**

Once C is known,

the path is blocked.

Knowing A gives no additional information about E.

## Question 4

Is

$$
A \perp B
$$

?

### Answer

**Yes.**

They are separate root nodes.

There is no path connecting them.

## Question 5

Is

$$
A \perp B \mid C
$$

?

### Answer

**No.**

This is exactly the **Explaining Away** phenomenon.

Originally,

A and B are independent.

After observing C,

they become dependent.

Knowing A changes our belief about B.

---

# Connection to Explaining Away

This is the same phenomenon studied earlier.

Without observing the effect,

the causes remain independent.

After observing the effect,

the causes compete to explain it.

Therefore,

conditioning creates dependence.

---

# Key Takeaways

- D-Separation determines independence directly from the graph.
- Knowing intermediate variables can block information flow.
- Root variables are independent unless evidence connects them.
- Explaining Away is a special case where conditioning creates dependence.

# Probabilistic Inference with Bayes Networks

# From Representation to Inference

In the previous lecture, we learned **how Bayes Networks represent probability distributions compactly**.

This lecture answers the next question:

> Once we have a Bayes Network, **how do we actually answer probability questions using it?**

This process is called **probabilistic inference**.

---

# Example Bayes Network

The lecture uses the classic **Burglary–Earthquake–Alarm** network.

```text
Burglary      Earthquake
     \         /
      \       /
       Alarm
      /     \
John Calls  Mary Calls
```

Variables:

- **Burglary (B)** — Did a burglary occur?
- **Earthquake (E)** — Did an earthquake occur?
- **Alarm (A)** — Did the alarm ring?
- **John Calls (J)** — Did John call?
- **Mary Calls (M)** — Did Mary call?

The relationships are causal:

```text
Burglary ─┐
          ├──► Alarm ───► John Calls
Earthquake┘         │
                    └──► Mary Calls
```

---
Next: [[Lecture 6 - Bayesian Networks V - Probabilistic Inference]]