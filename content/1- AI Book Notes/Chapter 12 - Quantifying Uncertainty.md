
> [!insight]
> This chapter explains **why probability is needed in Artificial Intelligence**. Rather than replacing logic, probability extends reasoning to situations where an agent lacks complete knowledge. Instead of asking *"Is this statement true?"*, the agent asks *"How strongly should I believe this statement?"*

# Related Notes

- [[3 - Probability]]
- [[4 - Conditional Porbability]]
- [[6 - Bayes' Theorem]]
- [[2 - Expected Value (Expectation) and LOTUS]]
- [[Lecture 6 - Bayesian Networks I — Foundations & Bayes Rule]], [[Lecture 6 – Bayesian Networks V -  Probabilistic Inference]], [[Lecture 6 – Bayesian Networks VI - Exact Inference]]

---

# Why AI Needs Probability

Real-world agents rarely have complete information.

An AI agent must often make decisions under uncertainty because of:

- Partial observability
- Nondeterminism
- Adversaries

An agent may never know

- its exact current state
- what future state its actions will lead to

---

# Earlier Approach: Belief States

Earlier AI approaches represented uncertainty using a **belief state**.

A belief state contains

> every possible world that could currently be true.

The agent then creates a **contingency plan** that handles every possible situation.

---

# Problems with Belief States

The book identifies three major drawbacks.

## 1. Every possibility must be considered

Even extremely unlikely explanations remain inside the belief state.

The agent cannot ignore them.

This causes the belief state to become very large.

---

## 2. Contingency plans become enormous

A correct plan must prepare for every possible future.

Even incredibly unlikely situations require their own branch of the plan.

The plan can therefore grow arbitrarily large.

---

## 3. Sometimes no guaranteed plan exists

Sometimes every available action carries risk.

No plan can guarantee success.

The agent must still choose one.

Therefore it must compare plans that have different chances of success.

---

# Airport Example

Suppose an automated taxi must take a passenger to the airport.

One possible plan is

> **A90**

Leave home 90 minutes before departure.

Logic cannot prove

> "A90 will definitely succeed."

Instead, logic only concludes

> "A90 succeeds **if** nothing unusual happens."

Examples include

- the car does not break down
- there is no accident
- the road is open
- no meteorite hits the car

Since none of these can be guaranteed, logical reasoning alone cannot prove the plan succeeds.

---

# Qualification Problem

This is another example of the **Qualification Problem** discussed earlier.

A logical rule requires an almost endless list of conditions to guarantee success.

The agent therefore cannot conclude with certainty that the plan will work.

---

# Choosing the Best Plan

Although logic cannot guarantee success, some plans are still better than others.

For example

- A90 may arrive on time with high probability.
- A180 leaves much earlier, making lateness even less likely.
- However, A180 also increases unnecessary waiting.

Different plans involve different trade-offs.

The agent therefore needs a way to compare them.

---

# Performance Measure

The quality of a plan depends on the agent's **performance measure**.

For the taxi example, this includes

- arriving before the flight
- avoiding unnecessary waiting
- avoiding speeding tickets

The best plan is the one expected to perform best according to these goals.

---

# Degree of Belief

Instead of certainty, the agent maintains a

> **degree of belief**

about possible outcomes.

Its knowledge cannot guarantee what will happen.

Instead, it estimates how likely each outcome is.

This prepares the foundation for probability theory.

---

# Key Idea

Logic asks

> Is this statement certainly true?

Probability asks

> How strongly should I believe this statement given everything I currently know?

This shift allows an intelligent agent to act even when certainty is impossible.

---
# 12.2 Basic Probability Notation
*Artificial Intelligence: A Modern Approach (AIMA)*

> [!abstract]
> This section introduces the formal language used in probability theory. Like logic, probability reasons about **possible worlds**, but instead of declaring worlds as simply possible or impossible, it assigns each world a numerical probability.

---

# Related Notes

- [[Probability]]
- [[NCERT - Probability]]
- [[Conditional Probability]]
- [[Bayes' Theorem]]
- [[Bayes Networks]]

---

# Why a Formal Language?

An intelligent agent must represent uncertain knowledge mathematically.

Probability theory provides a formal language for

- representing uncertainty
- asking probability queries
- performing probabilistic inference

Unlike traditional mathematical notation, AI connects probability notation directly with concepts from logic.

---

# Probability is About Possible Worlds

Just like propositional logic, probability theory reasons about **possible worlds**.

The difference is:

| Logic | Probability |
|--------|------------|
| Rules out impossible worlds | Assigns probabilities to possible worlds |

Instead of asking

> Is this world possible?

Probability asks

> How likely is each possible world?

---

# Sample Space

> [!definition]
> **Sample Space ($\Omega$)** is the set of all possible worlds.

Properties:

- mutually exclusive
- exhaustive

This means

- only one possible world can actually occur
- one of them must occur

---

## Example: Rolling Two Dice

Possible worlds are

```
(1,1)
(1,2)
...
(6,6)
```

Total possible worlds

$$
6 \times 6 = 36
$$

Notation

- $\Omega$ → sample space
- $\omega$ → one possible world

---

# Probability Model

A **probability model** assigns a probability to every possible world.

Notation

$$
P(\omega)
$$

---

# Probability Axioms

Every possible world satisfies

$$
0 \le P(\omega) \le 1
$$

The probabilities of all possible worlds sum to 1.

$$
\sum_{\omega \in \Omega} P(\omega)=1
$$

---

## Fair Dice Example

Every world has probability

$$
\frac{1}{36}
$$

If the dice are loaded

- probabilities change
- but still satisfy

$$
\sum P(\omega)=1
$$

---

# Events

Most probability questions are **not** about individual worlds.

Instead, they concern **sets of worlds**.

> [!definition]
> An **event** is a set of possible worlds.

In logic

- propositions correspond to sets of worlds

Therefore

> Event ≈ Proposition

---

## Example

Event

```
Total = 11
```

corresponds to worlds

```
(5,6)

(6,5)
```

---

# Probability of a Proposition

The probability of a proposition equals the sum of probabilities of every world where it is true.

$$
P(\phi)=\sum_{\omega\in\phi}P(\omega)
$$

---

## Example

For fair dice

```
Total = 11
```

Possible worlds

```
(5,6)

(6,5)
```

Therefore

$$
P(\text{Total}=11)
=
\frac1{36}
+
\frac1{36}
=
\frac1{18}
$$

---

# Partial Knowledge

Probability theory does **not** require complete knowledge of every possible world.

Example

Suppose we only know

```
P(Doubles)=1/4
```

We do **not** need to know

- probability of (1,1)
- probability of (2,2)
- probability of (6,6)

individually.

Just like logic, probability assertions constrain the model without fully specifying it.

---

# Unconditional (Prior) Probability

> [!definition]
> An **unconditional probability** (or **prior probability**) is the probability of a proposition before observing any evidence.

Examples

```
P(Cavity)

P(Total=11)

P(Doubles)
```

These represent belief **without additional information**.

---

# Evidence

Often, some information has already been observed.

This observed information is called **evidence**.

Example

The first die already shows

```
5
```

Now the question changes.

Instead of asking

```
P(Doubles)
```

we ask

```
P(Doubles | Die1 = 5)
```

---

# Conditional (Posterior) Probability

> [!definition]
> A **conditional probability** (posterior probability) is the probability of a proposition after incorporating evidence.

Notation

$$
P(A|B)
$$

reads

> Probability of A **given** B.

---

## Dental Example

Prior belief

```
P(Cavity)=0.2
```

After observing toothache

```
P(Cavity | Toothache)=0.6
```

The new evidence changes the belief.

---

# Prior Probability Still Exists

An important point made by the book:

Observing evidence **does not invalidate** the prior probability.

Even after observing a toothache,

```
P(Cavity)=0.2
```

remains a correct statement.

It is simply no longer the most useful quantity for decision making.

Instead, the agent uses

```
P(Cavity | Toothache)
```

because decisions should condition on all available evidence.

---

# Conditioning ≠ Logical Implication

The statement

$$
P(Cavity|Toothache)=0.6
$$

does **not** mean

> Whenever Toothache is true, conclude Cavity with probability 0.6.

Instead it means

> Given only the evidence "Toothache," the probability of Cavity is 0.6.

Additional evidence changes the probability.

Example

If the dentist later confirms

```
No Cavity
```

then

```
P(Cavity | Toothache ∧ ¬Cavity)=0
```

Thus conditional probabilities always depend on the complete knowledge state.

---

# Definition of Conditional Probability

Conditional probability is defined as

$$
P(A|B)
=
\frac{P(A\land B)}
{P(B)}
$$

provided

$$
P(B)>0
$$

---

## Dice Example

$$
P(Doubles|Die1=5)
=
\frac
{P(Doubles \land Die1=5)}
{P(Die1=5)}
$$

---

# Interpretation

Observing evidence

```
B
```

eliminates every world where

```
B
```

is false.

Among the remaining worlds,

the probability of

```
A
```

is simply

$$
\frac{P(A\land B)}
{P(B)}
$$

---

# Product Rule

The definition can be rearranged into the **Product Rule**.

$$
P(A\land B)
=
P(A|B)P(B)
$$

Interpretation:

For both events to occur

1. B must occur.
2. Given B, A must occur.

---

# Random Variables

Probability theory describes worlds using **random variables**.

Notation

- Variable names begin with uppercase letters.

Examples

```
Weather

Total

Die1

Age
```

---

# Range

Every random variable has a **range**.

Examples

```
Total
=
{2,...,12}

Die1
=
{1,...,6}

Weather
=
{sun,rain,cloud,snow}
```

Values are written in lowercase.

---

# Boolean Variables

Boolean variables have two values.

```
true

false
```

Example

```
Doubles = true
```

By convention

```
A = true
```

is abbreviated as

```
a
```

and

```
A = false
```

as

```
¬a
```

---

# Other Variable Types

Ranges may be

- categorical

```
Weather
=
{sun,rain,cloud,snow}
```

- ordered

```
Age
```

- infinite discrete

```
Integers
```

- continuous

```
Real numbers
```

Inequalities are also allowed.

Example

```
NumberOfAtoms ≥ 10^70
```

---

# Combining Propositions

Elementary propositions may be combined using propositional logic.

Example

$$
P(Cavity|\neg Toothache \land Teen)=0.1
$$

Probability notation also allows commas instead of conjunction.

Equivalent notation

$$
P(Cavity|\neg Toothache,\ Teen)
$$

---

# Probability Distribution

Instead of writing every probability separately,

```
P(Weather=sun)=0.6

P(Weather=rain)=0.1

P(Weather=cloud)=0.29

P(Weather=snow)=0.01
```

we write

$$
\mathbf{P}(Weather)
=
\langle0.6,\ 0.1,\ 0.29,\ 0.01\rangle
$$

This vector is called a **probability distribution**.

---

# Conditional Distributions

Conditional distributions use the same notation.

Example

$$
\mathbf{P}(X|Y)
$$

represents the probabilities

$$
P(X=x_i|Y=y_j)
$$

for every combination of values.

---

# Continuous Variables

Continuous variables have infinitely many values.

Instead of listing probabilities,

we define a **probability density function (pdf).**

Example

$$
P(NoonTemp=x)
=
Uniform(x,18^\circ C,26^\circ C)
$$

---

# Probability Density

Uniform distribution

$$
P(x)
=
\begin{cases}
1/8^\circ C,&18^\circ C\le x\le26^\circ C\\
0,&\text{otherwise}
\end{cases}
$$

Important distinction

- probability density is **not** probability.
- probability of one exact continuous value is zero.

---

# Joint Probability Distribution

Multiple variables are written together.

Example

$$
\mathbf{P}(Weather,\ Cavity)
$$

This represents the probability of every combination of

- Weather
- Cavity

For Weather (4 values) and Cavity (2 values),

the joint distribution is a

```
4 × 2
```

table.

---

# Product Rule for Distributions

The product rule extends naturally.

$$
\mathbf{P}(Weather,Cavity)
=
\mathbf{P}(Weather|Cavity)\mathbf{P}(Cavity)
$$

Instead of writing eight separate equations,

the vector notation represents them compactly.

---

# Possible Worlds Revisited

A possible world is

> a complete assignment of values to every random variable.

Example

Variables

```
Cavity

Toothache

Weather
```

Possible worlds

$$
2 \times 2 \times 4 = 16
$$

Every proposition can be evaluated in exactly the same way as propositional logic by checking whether it is true in each world.

---

# Redundant Variables

Some variables are completely determined by others.

Example

```
Doubles
```

is completely determined by

```
Die1

Die2
```

Such variables do not create genuinely new possible worlds.

Impossible combinations simply receive probability

$$
0
$$

---

# Full Joint Probability Distribution

> [!definition]
> The **full joint probability distribution** specifies the probability of every possible world.

Example

```
P(Cavity, Toothache, Weather)
```

For

- Cavity (2 values)
- Toothache (2 values)
- Weather (4 values)

there are

$$
2\times2\times4=16
$$

entries.

Since every proposition is a sum over possible worlds,

the full joint distribution is sufficient, in principle, to compute the probability of **any** proposition.

---

# Key Takeaways

- Probability assigns numerical belief to possible worlds.
- Sample space contains all mutually exclusive and exhaustive worlds.
- Events are sets of possible worlds.
- Probability of a proposition equals the sum of probabilities of worlds where it is true.
- Prior probabilities ignore evidence.
- Posterior probabilities condition on evidence.
- Conditioning is not logical implication.
- The Product Rule follows directly from the definition of conditional probability.
- Random variables describe possible worlds.
- Probability distributions summarize beliefs about variable values.
- Continuous variables require probability density functions.
- The full joint probability distribution completely specifies the probability model.

# 12.2 Basic Probability Notation

> [!summary]
> This section introduces the formal language used in probability theory. Like logic, probability reasons about **possible worlds**, but instead of declaring worlds as simply possible or impossible, it assigns each world a numerical probability.

# Why a Formal Language?

An intelligent agent must represent uncertain knowledge mathematically.

Probability theory provides a formal language for

- representing uncertainty
- asking probability queries
- performing probabilistic inference

Unlike traditional mathematical notation, AI connects probability notation directly with concepts from logic.

---

# Probability is About Possible Worlds

Just like propositional logic, probability theory reasons about **possible worlds**.

The difference is:

| Logic | Probability |
|--------|------------|
| Rules out impossible worlds | Assigns probabilities to possible worlds |

Instead of asking

> Is this world possible?

Probability asks

> How likely is each possible world?

---

# Sample Space

> [!definition]
> **Sample Space ($\Omega$)** is the set of all possible worlds.

Properties:

- mutually exclusive
- exhaustive

This means

- only one possible world can actually occur
- one of them must occur

---

## Example: Rolling Two Dice

Possible worlds are

```
(1,1)
(1,2)
...
(6,6)
```

Total possible worlds

$$
6 \times 6 = 36
$$

Notation

- $\Omega$ → sample space
- $\omega$ → one possible world

---

# Probability Model

A **probability model** assigns a probability to every possible world.

Notation

$$
P(\omega)
$$

---

# Probability Axioms

Every possible world satisfies

$$
0 \le P(\omega) \le 1
$$

The probabilities of all possible worlds sum to 1.

$$
\sum_{\omega \in \Omega} P(\omega)=1
$$

## Fair Dice Example

Every world has probability

$$
\frac{1}{36}
$$

If the dice are loaded

- probabilities change
- but still satisfy

$$
\sum P(\omega)=1
$$

---

# Events

Most probability questions are **not** about individual worlds.

Instead, they concern **sets of worlds**.

> [!definition]
> An **event** is a set of possible worlds.

In logic

- propositions correspond to sets of worlds

Therefore

> Event ≈ Proposition

## Example

Event

```
Total = 11
```

corresponds to worlds

```
(5,6)

(6,5)
```

---

# Probability of a Proposition

The probability of a proposition equals the sum of probabilities of every world where it is true.

$$
P(\phi)=\sum_{\omega\in\phi}P(\omega)
$$

## Example

For fair dice

```
Total = 11
```

Possible worlds

```
(5,6)

(6,5)
```

Therefore

$$
P(\text{Total}=11)
=
\frac1{36}
+
\frac1{36}
=
\frac1{18}
$$

---

# Partial Knowledge

Probability theory does **not** require complete knowledge of every possible world.

Example

Suppose we only know

```
P(Doubles)=1/4
```

We do **not** need to know

- probability of (1,1)
- probability of (2,2)
- probability of (6,6)

individually.

Just like logic, probability assertions constrain the model without fully specifying it.

---

# Unconditional (Prior) Probability

> [!definition]
> An **unconditional probability** (or **prior probability**) is the probability of a proposition before observing any evidence.

Examples

```
P(Cavity)

P(Total=11)

P(Doubles)
```

These represent belief **without additional information**.

---

# Evidence

Often, some information has already been observed.

This observed information is called **evidence**.

Example

The first die already shows

```
5
```

Now the question changes.

Instead of asking

```
P(Doubles)
```

we ask

```
P(Doubles | Die1 = 5)
```

---

# Conditional (Posterior) Probability

> [!definition]
> A **conditional probability** (posterior probability) is the probability of a proposition after incorporating evidence.

Notation

$$
P(A|B)
$$

reads

> Probability of A **given** B.


## Dental Example

Prior belief

```
P(Cavity)=0.2
```

After observing toothache

```
P(Cavity | Toothache)=0.6
```

The new evidence changes the belief.

---

# Prior Probability Still Exists

An important point made by the book:

Observing evidence **does not invalidate** the prior probability.

Even after observing a toothache,

```
P(Cavity)=0.2
```

remains a correct statement.

It is simply no longer the most useful quantity for decision making.

Instead, the agent uses

```
P(Cavity | Toothache)
```

because decisions should condition on all available evidence.

---

# Conditioning ≠ Logical Implication

The statement

$$
P(Cavity|Toothache)=0.6
$$

does **not** mean

> Whenever Toothache is true, conclude Cavity with probability 0.6.

Instead it means

> Given only the evidence "Toothache," the probability of Cavity is 0.6.

Additional evidence changes the probability.

Example

If the dentist later confirms

```
No Cavity
```

then

```
P(Cavity | Toothache ∧ ¬Cavity)=0
```

Thus conditional probabilities always depend on the complete knowledge state.

---

# Definition of Conditional Probability

Conditional probability is defined as

$$
P(A|B)
=
\frac{P(A\land B)}
{P(B)}
$$

provided

$$
P(B)>0
$$

## Dice Example

$$
P(Doubles|Die1=5)
=
\frac
{P(Doubles \land Die1=5)}
{P(Die1=5)}
$$

---

# Interpretation

Observing evidence

```
B
```

eliminates every world where

```
B
```

is false.

Among the remaining worlds,

the probability of

```
A
```

is simply

$$
\frac{P(A\land B)}
{P(B)}
$$

---

# Product Rule

The definition can be rearranged into the **Product Rule**.

$$
P(A\land B)
=
P(A|B)P(B)
$$

Interpretation:

For both events to occur

1. B must occur.
2. Given B, A must occur.

---

# Random Variables

Probability theory describes worlds using **random variables**.

Notation

- Variable names begin with uppercase letters.

Examples

```
Weather

Total

Die1

Age
```

---

# Range

Every random variable has a **range**.

Examples

```
Total
=
{2,...,12}

Die1
=
{1,...,6}

Weather
=
{sun,rain,cloud,snow}
```

Values are written in lowercase.

---

# Boolean Variables

Boolean variables have two values.

```
true

false
```

Example

```
Doubles = true
```

By convention

```
A = true
```

is abbreviated as

```
a
```

and

```
A = false
```

as

```
¬a
```

---

# Other Variable Types

Ranges may be

- categorical

```
Weather
=
{sun,rain,cloud,snow}
```

- ordered

```
Age
```

- infinite discrete

```
Integers
```

- continuous

```
Real numbers
```

Inequalities are also allowed.

Example

```
NumberOfAtoms ≥ 10^70
```

---

# Combining Propositions

Elementary propositions may be combined using propositional logic.

Example

$$
P(Cavity|\neg Toothache \land Teen)=0.1
$$

Probability notation also allows commas instead of conjunction.

Equivalent notation

$$
P(Cavity|\neg Toothache,\ Teen)
$$

---

# Probability Distribution

Instead of writing every probability separately,

```
P(Weather=sun)=0.6

P(Weather=rain)=0.1

P(Weather=cloud)=0.29

P(Weather=snow)=0.01
```

we write

$$
\mathbf{P}(Weather)
=
\langle0.6,\ 0.1,\ 0.29,\ 0.01\rangle
$$

This vector is called a **probability distribution**.

---

# Conditional Distributions

Conditional distributions use the same notation.

Example

$$
\mathbf{P}(X|Y)
$$

represents the probabilities

$$
P(X=x_i|Y=y_j)
$$

for every combination of values.

---

# Continuous Variables

Continuous variables have infinitely many values.

Instead of listing probabilities,

we define a **probability density function (pdf).**

Example

$$
P(NoonTemp=x)
=
Uniform(x,18^\circ C,26^\circ C)
$$

---

# Probability Density

Uniform distribution

$$
P(x)
=
\begin{cases}
1/8^\circ C,&18^\circ C\le x\le26^\circ C\\
0,&\text{otherwise}
\end{cases}
$$

Important distinction

- probability density is **not** probability.
- probability of one exact continuous value is zero.

---

# Joint Probability Distribution

Multiple variables are written together.

Example

$$
\mathbf{P}(Weather,\ Cavity)
$$

This represents the probability of every combination of

- Weather
- Cavity

For Weather (4 values) and Cavity (2 values),

the joint distribution is a

```
4 × 2
```

table.

---

# Product Rule for Distributions

The product rule extends naturally.

$$
\mathbf{P}(Weather,Cavity)
=
\mathbf{P}(Weather|Cavity)\mathbf{P}(Cavity)
$$

Instead of writing eight separate equations,

the vector notation represents them compactly.

---

# Possible Worlds Revisited

A possible world is

> a complete assignment of values to every random variable.

Example

Variables

```
Cavity

Toothache

Weather
```

Possible worlds

$$
2 \times 2 \times 4 = 16
$$

Every proposition can be evaluated in exactly the same way as propositional logic by checking whether it is true in each world.

---

# Redundant Variables

Some variables are completely determined by others.

Example

```
Doubles
```

is completely determined by

```
Die1

Die2
```

Such variables do not create genuinely new possible worlds.

Impossible combinations simply receive probability

$$
0
$$

---

# Full Joint Probability Distribution

> [!definition]
> The **full joint probability distribution** specifies the probability of every possible world.

Example

```
P(Cavity, Toothache, Weather)
```

For

- Cavity (2 values)
- Toothache (2 values)
- Weather (4 values)

there are

$$
2\times2\times4=16
$$

entries.

Since every proposition is a sum over possible worlds,

the full joint distribution is sufficient, in principle, to compute the probability of **any** proposition.

---

# Key Takeaways

- Probability assigns numerical belief to possible worlds.
- Sample space contains all mutually exclusive and exhaustive worlds.
- Events are sets of possible worlds.
- Probability of a proposition equals the sum of probabilities of worlds where it is true.
- Prior probabilities ignore evidence.
- Posterior probabilities condition on evidence.
- Conditioning is not logical implication.
- The Product Rule follows directly from the definition of conditional probability.
- Random variables describe possible worlds.
- Probability distributions summarize beliefs about variable values.
- Continuous variables require probability density functions.
- The full joint probability distribution completely specifies the probability model.

# 12.2 Basic Probability Notation

## Why do we need probability notation?

Logical agents represent:
- True
- False
- Unknown

Probabilistic agents instead represent

> Degree of belief.

To do this formally, probability theory provides a mathematical language.

# 12.2.1 What probabilities are about

## Possible Worlds

Like propositional logic,

Probability is defined over **possible worlds**.

Instead of saying

> Which worlds are impossible

Probability says

> How likely each possible world is.

## Sample Space (Ω)

The set of **all possible worlds** is called the

> Sample Space

Notation

- Ω → Sample Space
- ω → one particular possible world

Example

Rolling two distinguishable dice

Possible worlds

```
(1,1)
(1,2)
...
(6,6)
```

Total possible worlds

```
6 × 6 = 36
```

---

### Properties of Sample Space

Possible worlds are

- Mutually Exclusive
- Exhaustive

Meaning

- Two worlds cannot both occur.
- One world must occur.

## Probability Model

A probability model assigns

```
P(ω)
```

to every possible world.

Example

Fair dice

```
P((1,1)) = 1/36
```

Loaded dice

Some worlds receive larger probabilities,

but

```
Σ P(ω) = 1
```

always.

## Probability Axioms

Every possible world satisfies

```
0 ≤ P(ω) ≤ 1
```

and

```
Σ P(ω) = 1
```

---

### Connection to NCERT

Exactly the same idea as

```
Sum of probabilities of all outcomes = 1
```

except

AIMA treats each outcome as an entire **possible world**.

---

# Events

Normally we do **not** ask about one possible world.

Instead,

we ask about a **set of worlds**.

Example

```
Total = 11
```

includes

```
(5,6)

(6,5)
```

This set is called an

> Event

---

### Event vs Proposition

Logic

```
Proposition
```

Probability

```
Event
```

They represent the same idea

> A set of worlds where a statement is true.

## Probability of a Proposition

The probability of a proposition equals

the sum of probabilities of every world where it is true.

Formula

```
P(φ)
=
Σ P(ω)
```

where

```
ω satisfies φ
```

---

Example

```
Total = 11
```

contains

```
(5,6)

(6,5)
```

Therefore

```
P(Total=11)

=
1/36 + 1/36

=
1/18
```


## Important Observation

Sometimes

we know probabilities about events

without knowing probabilities of every world.

Example

```
P(Doubles)=1/4
```

We do **not** need to know

```
P((2,2))
P((4,4))
...
```

individually.

---

# Prior (Unconditional) Probability

Probability with

**no evidence**

Notation

```
P(A)
```

Examples

```
P(Cavity)

P(Total=11)
```

---

# Evidence

New information already observed.

Example

```
Die1 = 5
```

or

```
Toothache
```

---

# Conditional (Posterior) Probability

Probability after incorporating evidence.

Notation

```
P(A | B)
```

Read as

> Probability of A given B

Example

```
P(Doubles | Die1=5)
```

or

```
P(Cavity | Toothache)
```

---

### Connection to NCERT

Exactly the same conditional probability concept.

The notation

```
P(A|B)
```

is identical.

---

# Knowledge-State Interpretation

One of the book's most important ideas.

Probability is **not about reality.**

It is about

> What the agent currently knows.

Example

Initially

```
P(Cavity | Toothache)=0.8
```

Later

New evidence

```
History of Gum Disease
```

Now

```
P(Cavity | Toothache, GumDisease)=0.4
```

Later

Dentist confirms

No cavity

Now

```
P(Cavity)=0
```

These do **not** contradict each other.

Each probability belongs to a **different knowledge state**.

---

### Important Insight

Reality never changes.

Our

> Degree of belief

changes as evidence changes.

---

# Definition of Conditional Probability

Formula

```
P(A|B)

=
P(A ∧ B)
/ P(B)
```

provided

```
P(B)>0
```

---

Interpretation

After observing

```
B
```

we remove every world where

```
B
```

is false.

Among the remaining worlds,

calculate how many satisfy

```
A.
```

---

# Product Rule

Rearranging

```
P(A|B)

=
P(A∧B)
/P(B)
```

gives

```
P(A∧B)

=

P(A|B)

×

P(B)
```

This is called

> Product Rule

---

Meaning

For both A and B to happen

- B must occur.
- Then A must occur given B.

---

# 12.2.2 Probability Language

## Random Variables

Instead of logical propositions,

probability theory uses

> Random Variables.

Convention

Variable names

```
Uppercase
```

Values

```
Lowercase
```

Example

Variables

```
Weather

Die1

Total
```

Values

```
sun

rain

5

11
```

---

## Range

Each random variable has a

Range

Example

```
Die1

→

{1,2,3,4,5,6}
```

```
Weather

→

{sun,rain,cloud,snow}
```

---

## Boolean Random Variables

Range

```
{true,false}
```

Example

```
Doubles
```

Instead of writing

```
Doubles=true
```

the book abbreviates

```
doubles
```

Similarly

```
Doubles=false

↓

:doubles
```

---

### Bernoulli Distribution

A Boolean variable may also use

```
{0,1}
```

This is called a

> Bernoulli Distribution.

---

## Abbreviated Notation

Instead of

```
Weather=sun
```

the book often writes

```
sun
```

when no ambiguity exists.

---

## Continuous Variables

Variables need not be finite.

Example

```
Temperature
```

Possible values

All real numbers.

---

# Probability Distribution

Instead of a single probability,

sometimes we need probabilities for every value.

Example

```
P(Weather)

=

<0.6,0.1,0.29,0.01>
```

Meaning

```
Sun

0.60

Rain

0.10

Cloud

0.29

Snow

0.01
```

---

This is called a

> Probability Distribution.

---

### Categorical Distribution

When the variable has

finite discrete values,

the probability distribution is called

> Categorical Distribution.

---

## Conditional Distribution

Notation

```
P(X|Y)
```

represents

all conditional probabilities

for every value

of X and Y.

---

# Continuous Probability Density Function

Continuous variables cannot list probabilities individually.

Instead

use

> Probability Density Function (PDF)

Example

```
Uniform(18°C,26°C)
```

Meaning

Temperature is equally likely anywhere between

18°C and 26°C.

---

Important

```
Probability Density

≠

Probability
```

For a continuous variable

```
P(X=20.18°C)=0
```

because a single point has width zero.

---

# Joint Probability Distribution

Probability over multiple variables simultaneously.

Notation

```
P(Weather,Cavity)
```

Example

4 weather values

×

2 cavity values

↓

8 probabilities.

---

# Full Joint Distribution

A probability model is completely determined by

the

> Full Joint Probability Distribution

Example

Variables

```
Weather

Toothache

Cavity
```

Then

```
P(Weather,Toothache,Cavity)
```

contains probabilities for

every possible world.

---

### Important Insight

Possible World

↓

Assignment of values

to every random variable.

---

Example

Variables

```
Weather

Cavity

Toothache
```

Possible world

```
Weather=sun

Cavity=true

Toothache=false
```

---

# 12.2.3 Probability Axioms

---

## Complement Rule

From probability axioms

```
P(¬A)

=

1−P(A)
```

Exactly the same rule learned in elementary probability.

---

## Inclusion–Exclusion Principle

Probability of OR

```
P(A∨B)

=

P(A)

+

P(B)

−

P(A∧B)
```

Reason

```
P(A)

+

P(B)
```

counts

```
A∧B
```

twice.

Subtract it once.

---

### Connection to NCERT

Exactly the

Addition Rule

for probability.

---

# Kolmogorov's Axioms

These probability rules originate from

Kolmogorov's axioms,

which form the mathematical foundation of probability theory.

---

# Why must probabilities obey these axioms?

The book presents

De Finetti's Betting Argument.

Idea

If your probabilities violate the axioms,

someone can construct bets that guarantee

you lose money

regardless of the outcome.

Therefore

A rational agent must obey

probability axioms.

---

# 12.3 Inference Using Full Joint Distribution

Goal

Compute

Posterior Probabilities

using the

Full Joint Distribution.

---

## Marginal Probability

To obtain probability of one variable,

add over every value of the remaining variables.

Example

```
P(Cavity)

=

0.108

+

0.012

+

0.072

+

0.008

=

0.2
```

This process is called

> Marginalization

or

> Summing Out.

---

General Rule

```
P(Y)

=

Σ

P(Y,Z)
```

where

we sum over

every value of Z.

---

### Connection to NCERT

Exactly the

Law of Total Probability

appearing as

"summing over all possibilities."

---

# Conditioning Rule

Using Product Rule

Marginalization becomes

```
P(Y)

=

Σ

P(Y|Z)

P(Z)
```

---

# Computing Posterior Probabilities

General Formula

```
P(X|e)

=

α

Σ

P(X,e,y)
```

where

- X = query
- e = evidence
- y = hidden variables

---

# Normalization Constant (α)

Instead of computing the denominator,

calculate

relative values

then normalize.

Example

Unnormalized

```
<0.12,0.08>
```

Sum

```
0.20
```

Normalize

```
0.12/0.20=0.6

0.08/0.20=0.4
```

Result

```
<0.6,0.4>
```

---

### Important Insight

Normalization allows inference

without explicitly computing

the denominator.

---

# Complexity Problem

For

n Boolean variables

Full Joint Distribution requires

```
2ⁿ
```

entries.

Example

100 variables

```
2¹⁰⁰

≈

10³⁰
```

entries.

Impossible in practice.

This motivates more efficient probabilistic models later.

---

# 12.4 Independence

Definition

Two variables are independent if

learning one

does not change

belief about the other.

---

Equivalent Forms

```
P(A|B)=P(A)
```

```
P(B|A)=P(B)
```

```
P(A,B)

=

P(A)

P(B)
```

---

Example

Weather

and

Dental Problems

are independent.

Therefore

```
P(Toothache,Cavity,Weather)

=

P(Toothache,Cavity)

P(Weather)
```

---

### Importance

Independence

greatly reduces

storage

and

computation.

Instead of

one huge joint table,

store

smaller independent tables.

---

# 12.5 Bayes' Rule

Derived from

Product Rule

```
P(A∧B)

=

P(A|B)P(B)

=

P(B|A)P(A)
```

Therefore

```
P(B|A)

=

P(A|B)

P(B)

/P(A)
```

This is

> Bayes' Rule

---

General Form

```
P(Y|X)

=

P(X|Y)

P(Y)

/P(X)
```

---

With Background Evidence

```
P(Y|X,e)

=

P(X|Y,e)

P(Y|e)

/P(X|e)
```

---

# Why Bayes' Rule is Useful

Usually

we know

```
Cause

→

Effect
```

Example

Disease

causes

Symptoms.

But we want

```
Symptoms

→

Disease
```

Bayes' Rule reverses the direction.

---

## Causal vs Diagnostic Probability

Causal

```
P(Symptom|Disease)
```

Diagnostic

```
P(Disease|Symptom)
```

Medical diagnosis uses

Bayes' Rule

to convert

causal knowledge

into

diagnostic reasoning.

---

## Normalized Bayes' Rule

Instead of denominator

```
P(X)
```

the book often writes

```
P(Y|X)

=

α

P(X|Y)

P(Y)
```

where

```
α
```

normalizes the result.

---

# Key Takeaways

- Probability is defined over **possible worlds**.
- **Sample Space (Ω)** contains all possible worlds.
- Events are **sets of possible worlds**.
- Probability of an event is the **sum of probabilities of worlds** in that event.
- **Conditional probability** updates beliefs using evidence.
- **Product Rule** links joint and conditional probabilities.
- **Joint distributions** completely specify a probability model.
- **Marginalization** sums out unwanted variables.
- **Normalization (α)** converts relative probabilities into true probabilities.
- **Independence** allows factorization of large probability tables.
- **Bayes' Rule** converts causal probabilities into diagnostic probabilities and is the foundation of probabilistic inference in AI.

## 12.2.3 Probability Axioms

> [!abstract]  
> This section explains **why probability theory is internally consistent**. The previous sections defined probabilities and notation. Here, the book shows that once we accept the basic probability axioms, many familiar probability formulas follow automatically.
> 
> The section also explains **why rational agents should obey these axioms**, introducing the philosophical justification behind probability theory.

---

# Big Picture

> [!important]  
> Logic constrains **truth values**.
> 
> Probability constrains **degrees of belief**.

Just as logic prevents an agent from simultaneously believing contradictory statements, probability theory prevents an agent from assigning inconsistent numerical beliefs.

The goal of this section is to answer:

> **Why must probabilities obey certain mathematical rules?**

---

# Deriving Probability Rules from the Basic Axioms

Recall the two basic axioms introduced earlier.
$$  
0 \le P(\omega) \le 1  
$$

Every possible world has a probability between 0 and 1.

$$
\sum_{\omega \in \Omega} P(\omega)=1  
$$

The probabilities of all possible worlds sum to 1.

Everything else in elementary probability can be derived from these two principles.

---

# Probability of the Negation

Suppose proposition a is true in some possible worlds.

Its negation $\neg a$ is true in every remaining possible world.

Since together they cover **all** possible worlds,
$$  
P(a)+P(\neg a)=1  
$$

Therefore,

$$  
P(\neg a)=1-P(a)  
$$

---

### Intuition

If there is a

- 70% chance of rain,
    

then there must be

- 30% chance of no rain.
    

The two possibilities partition the sample space.

---

### Connection to NCERT

Exactly the same complement rule appears in NCERT.

If

$$  
P(A)=p  
$$

then

$$  
P(A')=1-p  
$$

AI simply derives this from possible worlds instead of presenting it as an isolated formula.

---

# Probability of a Union

Another familiar result is the probability of

$$  
a \lor b  
$$

or

$$ 
A\cup B  
$$

genui{"probability_statistics_learning_block":{"type_id":"UNION_PROBABILITY_INCLUSION_EXCLUSION"}}

The rule is

$$  
P(a\lor b)$$

P(b)

$$P(a\land b)  
$$


## Why subtract the intersection?

Imagine counting students.

- 20 study AI
    
- 15 study Robotics
    

If 5 study both,

simply adding

20+15

counts those 5 students twice.

Subtracting the overlap fixes the double counting.

---

### AI Interpretation

Possible worlds satisfying

(a)

plus

possible worlds satisfying

(b)

already cover every world satisfying

(a\lor b),

but worlds satisfying both are counted twice.

---
# Kolmogorov's Axioms

The book refers to these probability rules as

**Kolmogorov's Axioms**.

These provide the mathematical foundation for all probability theory.

> [!note]  
> Just as Euclid's axioms generate geometry,
> 
> Kolmogorov's axioms generate probability theory.

The book emphasizes that these few axioms are sufficient to build the rest of probability theory.

---

# Why Can't We Choose Any Numbers We Want?

Suppose someone claims

[  
P(a)=0.4  
]

[  
P(b)=0.3  
]

[  
P(a\land b)=0  
]

[  
P(a\lor b)=0.8  
]

These numbers violate the inclusion–exclusion rule.

The question becomes

> Why can't an agent simply believe these numbers?

---

# Degrees of Belief Must Be Consistent

Unlike logic,

probability talks about

the **agent's knowledge**, not directly about the world.

So why are inconsistent beliefs irrational?

The book answers this using

**de Finetti's betting argument.**

---

# de Finetti's Betting Argument

Imagine two agents.

Agent 1 announces their degrees of belief.

Agent 2 is allowed to construct bets using those beliefs.

If Agent 1's beliefs violate probability axioms,

Agent 2 can always design bets that guarantee Agent 1 loses money,

**regardless of what actually happens.**

## Main Idea

The problem is **not** that the beliefs are false.

The problem is that they are

**internally inconsistent.**

This inconsistency can always be exploited.

---

### Example

Suppose you believe

Rain tomorrow = 60%

No rain tomorrow = 50%

These already total

110%.

Someone can construct bets so that you lose regardless of tomorrow's weather.

---

> [!important]  
> Probability axioms protect an agent from making decisions that can be exploited under every possible outcome.

---

# Why This Matters for AI

AI agents constantly make decisions.

Every decision is effectively a bet.

Examples include:

- taking one road instead of another
    
- diagnosing one disease instead of another
    
- choosing one chess move instead of another
    
- selecting one action in reinforcement learning
    

If an AI's beliefs are inconsistent,

its decisions become systematically irrational.

---

# Refusing to Bet Doesn't Escape the Argument

A natural objection is

> "What if I simply refuse to bet?"

The book argues that this changes nothing.

Every action,

including doing nothing,

is itself a decision.

Time continues,

and consequences still occur.

Therefore,

every rational agent is continuously making implicit bets about the world.

---

# Other Philosophical Justifications

The book briefly mentions several researchers who independently argued that probability is the only consistent framework for reasoning under uncertainty:

- Cox
    
- Carnap
    
- Jaynes
    

Their arguments differ from de Finetti's.

Instead of betting,

they begin with reasonable assumptions about how beliefs should behave.

For example:

- beliefs should not contradict each other
    
- stronger evidence should increase belief
    
- if belief in a proposition increases, belief in its negation should decrease
    
- beliefs should be comparable and ordered consistently
    

From these assumptions,

they prove that probability theory is the unique mathematical system satisfying them.

---

# Practical Perspective

The authors finish with an important observation.

Even though philosophical proofs are interesting,

the strongest argument for probability theory is its success in practice.

Modern AI systems based on probability consistently perform well in:

- diagnosis
    
- robotics
    
- speech recognition
    
- language processing
    
- autonomous systems
    

The practical effectiveness of probabilistic reasoning has convinced far more researchers than philosophical arguments alone.

---

# Connections to Previous Chapters

> [!note] Logical Agent vs Probabilistic Agent
> 
> Earlier chapters:
> 
> - Logic determines what is definitely true or false.
>     
> 
> This chapter:
> 
> - Probability determines how strongly an agent should believe uncertain propositions.
>     
> 
> Probability extends logical reasoning rather than replacing it.

    
---

# Key Takeaways

> [!summary]
> 
> - Probability theory constrains **degrees of belief**, just as logic constrains truth.
>     
> - The complement rule (P(\neg A)=1-P(A)) follows directly from the axioms.
>     
> - The inclusion–exclusion rule avoids double-counting overlapping events.
>     
> - **Kolmogorov's axioms** form the mathematical foundation of probability.
>     
> - Inconsistent probability assignments make an agent vulnerable to guaranteed losses (de Finetti's argument).
>     
> - Other philosophical justifications (Cox, Carnap, Jaynes) also conclude that probability is the unique consistent calculus for reasoning under uncertainty.
>     
> - The success of modern AI systems provides strong practical evidence for using probability as the basis for uncertain reasoning.
>
