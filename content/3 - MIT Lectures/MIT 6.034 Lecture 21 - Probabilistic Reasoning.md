

> **Lecture:** MIT 6.034 Artificial Intelligence – Patrick Winston
>
> **Related Georgia Tech Notes**
> - [[Lecture 6 - Bayesian Networks I — Foundations & Bayes Rule]]
> - [[Lecture 6 - Bayesian Networks II - Bayesian Inference In Simple Networks]]
> - [[3 - Probability]]
> - [[4 - Conditional Probability]]
> - [[6 - Bayes' Theorem]]

---

# Why Study Probability in AI?

Up to this point, many AI techniques we have studied assume that the world is **certain**.

For example,

- Search algorithms assume actions have predictable outcomes.
- Logic assumes statements are either true or false.
- Constraint Satisfaction assumes constraints are fixed.

However, the real world is rarely so clean.

AI systems often need to make decisions with **incomplete information**.

Examples include:

- A doctor diagnosing a disease from symptoms.
- A robot deciding whether an obstacle is a person or a chair.
- A self-driving car deciding whether a pedestrian intends to cross the road.
- An email filter deciding whether a message is spam.

In all of these situations, the AI **cannot know the truth with certainty**.

Instead, it must reason using **probabilities**.

---

# Probability is One Tool Among Many

Patrick Winston makes an important point early in the lecture.

> Probability is **not** the solution to every AI problem.

Many topics in AI have enthusiastic supporters who believe their method solves everything.

For example,

- symbolic reasoning,
- neural networks,
- reinforcement learning,
- probabilistic reasoning.

In reality, each technique solves a different class of problems. Probability is most useful when

- the world is uncertain,
- outcomes cannot be predicted exactly,
- or complete information is unavailable.

---

# A Motivating Example

Imagine driving through campus one morning. Suddenly you notice that a **new statue** has appeared.

Your immediate reaction might be:

> "Someone hacked the campus."

But after thinking for a moment, another explanation occurs.

Perhaps there is an

- art exhibition,
- sculpture installation,
- or public event.

Now there are multiple possible explanations for the same observation.

Instead of immediately concluding

```
Statue

↓

Hack
```

you begin considering several competing possibilities.

---

# Possible Explanations

Patrick Winston considers three binary variables.

| Variable | Meaning |
|-----------|---------|
| Statue | A statue has appeared |
| Hack | Someone carried out a campus hack |
| Art Show | An official art exhibition is occurring |

Each variable can be either

- **True**
- **False**

---

# Representing Every Possible Situation

Since every variable has only two possible values,

```
True

or

False
```

we can list every possible combination. For three binary variables,

the total number of possible worlds is

$$
2^3 = 8
$$

## Joint Probability Table

| Statue | Hack | Art Show |
|---------|------|-----------|
| F | F | F |
| F | F | T |
| F | T | F |
| F | T | T |
| T | F | F |
| T | F | T |
| T | T | F |
| T | T | T |

Each row represents

> **one complete description of the world.**

For example,

```
Statue = True

Hack = False

Art Show = True
```

means

- there really is a statue,
- nobody hacked the campus,
- an art show explains its appearance.

Another row might represent

```
Statue = True

Hack = True

Art Show = False
```

meaning the statue really is the result of a prank.

---

# Every Row Represents One Possible World

This idea is extremely important. Rather than storing information separately, a **joint probability table** stores probabilities for

> **every possible combination of every variable simultaneously.**

In other words, each row answers the question:

> "If the world looked exactly like this, how likely would it be?"

---

# Estimating the Probabilities

Suppose we observed the campus for many years.

Each day we record

- Was there a statue?
- Was there a hack?
- Was there an art show?

Eventually, our observations might look like this.

| Combination | Frequency |
|-------------|-----------|
| F F F | 405 |
| F F T | 45 |
| F T F | 225 |
| F T T | 40 |
| ... | ... |

These are simply **counts**. They tell us

> how often each possible world actually occurred.

---

# From Frequencies to Probabilities

Probability can be estimated using

$$
P(\text{event})
=
\frac{\text{Number of times event occurred}}
{\text{Total observations}}
$$

For example,

if

```
405

out of

1000
```

observations correspond to

```
No statue

No hack

No art show
```

then

$$
P(\text{No Statue},\text{No Hack},\text{No Art Show})
=
\frac{405}{1000}
=
0.405
$$

Each row of the table receives its own probability. Together, these probabilities form the

> **Joint Probability Distribution**

---

# What Does "Joint" Mean?

The word **joint** means

> **all variables are considered together simultaneously.**

Instead of asking

> "How likely is a hack?"

we ask

> "How likely is this entire situation?"

For example,

$$
P(\text{Statue},\text{Hack},\text{Art Show})
$$

is a **joint probability** because it refers to all three variables at once.

---

# Why Is This So Powerful?

Once every possible world has been assigned a probability, we can answer almost any probability question.

For example,

- How likely is there a statue?
- How likely is there a hack?
- How likely is there an art show?
- How likely is there a hack if a statue appears?
- How likely is there an art show if a statue appears?

Remarkably, all of these can be computed from the same table. Patrick Winston calls this the "miracle" of probabilistic inference.

The only problem is that this miracle comes with a cost...

---

# The First Big Problem

The table grows **exponentially**.

For

```
3 variables
```

we need

$$
2^3 = 8
$$

rows.

For

```
10 variables
```

we need

$$
2^{10}=1024
$$

rows.

For

```
20 variables
```

we need

$$
2^{20}
=
1,048,576
$$

rows.

Each additional binary variable **doubles** the size of the table.

---

# Why This Doesn't Scale

Imagine trying to model a medical diagnosis.

Variables might include

- Fever
- Cough
- Fatigue
- COVID
- Flu
- Pneumonia
- Age
- Smoking
- Blood Pressure
- Oxygen Level

Even this small problem already requires thousands of possible combinations. Real AI systems often contain hundreds or thousands of variables, making a complete joint probability table impossible to store.

---

# Key Takeaways

- AI often operates under uncertainty rather than certainty.
- Probability helps an agent reason about uncertain situations.
- A **joint probability table** lists every possible combination of variables.
- For **n** binary variables, the table contains $2^n$ rows.
- Each row stores the probability of one complete possible world.
- Once the joint probability table is known, many different probability questions can be answered.
- Unfortunately, the table grows **exponentially**, motivating the need for more efficient representations—namely **Bayesian (Belief) Networks**.

## Using a Joint Probability Table

> **Related Notes**
>
> - [[Lecture 6 - Bayesian Networks II - Bayesian Inference In Simple Networks]]
> - [[4 - Conditional Probability]]
> - [[6 - Bayes' Theorem]]


## The Power of the Joint Probability Table

Although a joint probability table can become enormous,

it has one remarkable advantage.

> **Once we know the probability of every possible world, we can answer almost any probability question.**

For example,

we can calculate

- the probability that a statue appears,
- the probability that a hack occurred,
- the probability that an art show is taking place,
- the probability of a hack given a statue,
- the probability of an art show given a statue,
- and many more.

All of these are derived from **the same table**.

---

# Marginal Probability

Suppose we want to know

> What is the probability that a statue appears?

Notice that this question says **nothing** about hacks or art shows.

We therefore need to consider **every row** where

```
Statue = True
```

regardless of the values of the other variables.

Graphically,

```
Statue   Hack   Art Show

 T         F        F
 T         F        T
 T         T        F
 T         T        T
```

The marginal probability is simply

$$
P(\text{Statue})
=
\sum_{\text{rows where Statue=True}}
P(\text{row})
$$


## Why Is It Called "Marginal"?

Historically, when probability tables were written in books, the totals were written in the **margin** of the table. Those totals became known as

> **Marginal probabilities**

A marginal probability is therefore obtained by

> **adding together all rows consistent with the event of interest.**

---

# Conditional Probability

Now suppose we learn new information. Instead of asking

> What is the probability of a statue?

we ask

> What is the probability of a statue **given** that there is an art show?

Now we no longer consider every row.

Instead, we restrict ourselves to only those rows where

```
Art Show = True
```

Within this smaller set, we calculate

$$
P(\text{Statue}\mid\text{Art Show})
$$

This is exactly the idea of **conditional probability**.

---

# Conditioning Changes Probabilities

An important lesson from the lecture is that

> **Learning new information changes our beliefs.**

Initially,

```
Statue
```

may be relatively unlikely. However, once we discover there is an

```
Art Show
```

the probability of seeing a statue increases dramatically.

Nothing about the world has changed.

Only **our knowledge** has changed.

---

# Adding More Evidence

Now suppose we also learn

```
Hack = True
```

Our question becomes

$$
P(\text{Statue}\mid
\text{Art Show},
\text{Hack})
$$

Again, the joint probability table answers this simply by considering only the rows satisfying both conditions.

---

# A Second Example

Patrick Winston introduces another example. Instead of statues, consider a neighbor's dog.

The dog may bark because

- a burglar is present,
- a raccoon is outside,
- both,
- or neither.

The variables become

| Variable | Meaning |
|-----------|---------|
| Dog Barking | The dog is barking |
| Burglar | A burglar is present |
| Raccoon | A raccoon is present |

Again,

there are

$$
2^3=8
$$

possible worlds.

Exactly the same joint probability framework applies.

---

# Example Question

Initially,

suppose we ask

> What is the probability of a raccoon?

We simply sum all rows where

```
Raccoon = True
```

Next, suppose we hear the dog barking.

Now we ask

$$
P(\text{Raccoon}\mid\text{Dog Barking})
$$

Because barking is evidence that something is outside, the probability of a raccoon increases.

---

# Explaining Away

Now suppose we discover something else. The police confirm

```
Burglar = True
```

Our question becomes

$$
P(\text{Raccoon}
\mid
\text{Dog Barking},
\text{Burglar})
$$

Surprisingly, the probability of a raccoon **decreases**.

---

# Why Does It Decrease?

Initially, the barking needs an explanation.

Possible explanations include

```
Dog Barking

↓

Burglar

or

Raccoon
```

Once we already know

```
Burglar = True
```

the barking is already explained.

Therefore, the raccoon becomes less necessary as an explanation. This phenomenon is known as **Explaining Away**

---

# Explaining Away in Bayesian Networks

This idea appears repeatedly in Bayesian Networks.

Two independent causes

```
Burglary

↓

Alarm

↑

Earthquake
```

become **dependent once we observe their common effect**.

If we hear the alarm, both burglary and earthquake become more likely.

However, once we discover a burglary actually occurred, the earthquake becomes less likely. Exactly the same reasoning appears in the Dog–Burglar–Raccoon example.

---

# Key Takeaways

- Marginal probabilities are computed by summing appropriate rows.
- Conditional probabilities restrict attention to rows satisfying known evidence.
- Evidence changes beliefs.
- One explanation can reduce the probability of competing explanations.
- This phenomenon is called **explaining away** and is one of the most important ideas in Bayesian Networks.

## Why Joint Probability Tables Don't Scale

> **Related Notes**
>
> - [[Lecture 6 - Bayesian Networks IV — Bayesian Network Structure]]
> - [[Lecture 6 - Bayesian Networks VII - Approximate Inference]]

---

# The Miracle—and the Problem

Patrick Winston describes the joint probability table as almost miraculous.

Why?

Because once the table is known, it can answer nearly every probability question.

Unfortunately, this miracle comes with a serious limitation. The table becomes impossibly large.

---

# Exponential Growth

Suppose every variable is binary. Each new variable doubles the number of possible worlds.

The number of rows becomes

$$
2^n
$$

where

- \(n\) = number of variables.


## Example

| Variables | Number of Rows |
|-----------:|---------------:|
| 3 | 8 |
| 5 | 32 |
| 10 | 1024 |
| 20 | 1,048,576 |
| 30 | More than 1 billion |

Notice how quickly the table explodes.

---

# Why Does This Happen?

Each variable can be

```
True

or

False
```

Every new variable doubles the combinations.

For example,

```
Weather

↓

2 possibilities
```

Add

```
Traffic
```

Now we have

```
4 possibilities
```

Add

```
Late for Work
```

Now

```
8 possibilities
```

The growth is exponential rather than linear.

---

# Collecting the Probabilities

Even if storage were free, there is another problem. Where do all these probabilities come from? Patrick Winston suggests two possibilities.

---

# 1. Frequentist Interpretation

One approach is to estimate probabilities using observations.

For example,

observe

- 1000 days,
- 10000 patients,
- millions of emails.

Probability becomes

$$
P(A)
=
\frac{\text{Number of occurrences of }A}
{\text{Total observations}}
$$

This is called the

> **Frequentist interpretation of probability.**

---

# 2. Subjective Interpretation

Sometimes there simply is not enough data. Instead, an expert estimates the probabilities.

Examples include

- doctors,
- engineers,
- weather forecasters.

These probabilities reflect

> **expert belief rather than measured frequency.**

This is called the

> **Subjective interpretation of probability.**

---

# Probability Is Not the Answer to Everything

Patrick Winston pauses to make an important philosophical point.

Probability is an extremely useful AI tool, but it is **not** the only tool. Sometimes, there already exists an exact scientific model.

---

# The Floating Objects Example

Imagine trying to determine

> Which objects float?

One approach would be purely statistical. Observe thousands of objects.

Record

- wood,
- metal,
- plastic,
- rocks,
- paper,
- pencils,
- coins.

Estimate probabilities for everything.

## But Physics Already Solves It

Instead, physics provides a direct explanation. Whether something floats depends on

- density,
- displaced water,
- buoyancy.

No probability table is necessary. The correct model comes from **Archimedes' Principle**, not statistics.

---

# When Probability Is Appropriate

Probability becomes useful when there is **no complete physical model**.

Examples include

- Will someone vote for a particular political party?
- Will a customer buy a product?
- Does a patient have cancer?
- Is an email spam?

These involve many hidden influences that cannot easily be modeled using deterministic equations.

---

# The Need for a Better Representation

At this point, Patrick Winston concludes

> Joint probability tables are theoretically perfect...

...but practically impossible.

We therefore need a representation that

- stores far fewer probabilities,
- avoids exponential explosion,
- still allows probabilistic inference.

This motivates the invention of

# Bayesian (Belief) Networks

Rather than storing probabilities for **every possible world**,

Bayesian Networks exploit

> **conditional independence**

to represent the same information much more efficiently.

This is why Bayesian Networks became one of the most important probabilistic models in Artificial Intelligence.

---

# Connection to Your Georgia Tech Notes

This is exactly the motivation behind

[[Lecture 6 - Bayesian Networks I — Foundations & Bayes Rule]]

and

[[Lecture 6 - Bayesian Networks IV — Bayesian Network Structures]]

Instead of storing

$$
2^n
$$

joint probabilities,

Bayesian Networks store only

- prior probabilities,
- conditional probability tables,

making inference tractable even for very large systems.

---

# Key Takeaways

- Joint probability tables are mathematically complete.
- Their size grows exponentially as $2^n$
- Probabilities may come from data (frequentist) or expert knowledge (subjective).
- Probability is one AI tool among many—not every problem requires probabilistic reasoning.
- The exponential growth of joint probability tables motivates Bayesian Networks, which compress the representation by exploiting conditional independence.

## Why Joint Probability Tables Do Not Scale

Up to this point, we have assumed that we can answer probabilistic questions simply by building a **Joint Probability Table (JPT)**.

The problem is that this approach becomes impossible as the number of variables increases.


## The Size of a Joint Probability Table

Suppose our world contains only three binary variables.

For example,

- Statue
- Hack
- Art Show

Each variable has two possible values:

- True
- False

Therefore, the table contains

$$
2^3 = 8
$$

possible combinations. This is manageable.

---

# What Happens When We Add More Variables?

Now suppose we decide that another variable might influence the situation.

Examples might include:

- Day of the week
- Weather
- Whether there is a football game
- What I ate for breakfast

Every new **binary** variable doubles the number of rows.

If we have four variables,

$$
2^4 = 16
$$

rows.

Five variables require

$$
2^5 = 32
$$

rows.

Ten variables require

$$
2^{10}=1024
$$

rows. Already, we need over one thousand probabilities.

---

# Exponential Growth

The size of the table grows **exponentially**, not linearly.

| Number of Variables | Rows Required |
|---------------------:|--------------:|
| 3 | 8 |
| 4 | 16 |
| 5 | 32 |
| 10 | 1,024 |
| 20 | 1,048,576 |
| 30 | More than 1 billion |

This is known as the **curse of dimensionality**.

Adding only a few variables quickly makes the table impossible to construct or store.

---

# Why Is This a Problem?

Patrick Winston points out two practical difficulties.

## 1. Collecting the Data

To estimate every probability, we would need enough observations for **every possible combination**.

For large tables, many combinations might never occur in our dataset.

Example:

Suppose we have 20 variables.

There are

$$
2^{20}=1,048,576
$$

possible worlds.

Collecting enough data for every one of them is unrealistic.

## 2. Guessing the Probabilities

Even if we do not collect data and instead estimate the probabilities ourselves, the task becomes impossible.

Estimating

- 8 probabilities is reasonable.
- 32 probabilities is tedious.
- 1,024 probabilities is impractical.
- Millions of probabilities are impossible.

---

# The Central Limitation of Joint Probability Tables

A Joint Probability Table is mathematically complete.

If we had one, we could answer virtually **any probabilistic query**.

However, its size grows exponentially with the number of variables.

Therefore,

> **Joint Probability Tables are theoretically powerful but computationally impractical for realistic AI problems.**

---

# Why This Matters

This limitation motivates the development of **Bayesian Networks**.

Instead of storing one gigantic table, Bayesian Networks exploit **conditional independence** to store only the probabilities that are actually needed.

This dramatically reduces the number of parameters required.

For example, instead of storing millions of probabilities, a Bayesian Network may only require a few dozen conditional probability tables.

This is the major reason Bayesian Networks became one of the most important probabilistic models in Artificial Intelligence.

---

# Key Takeaways

- A Joint Probability Table represents the complete probability distribution.
- Every additional binary variable doubles the number of rows.
- The number of probabilities grows exponentially.
- Large Joint Probability Tables become impossible to construct or store.
- Bayesian Networks were developed to solve exactly this scalability problem.

## Where Do Probabilities Come From?

Once we decide to use probabilities, an important question arises.

> **Where do the probability values actually come from?**

Patrick Winston discusses several possible interpretations.

---

# 1. Frequentist Interpretation

The first approach is the **Frequentist** view.

Here, probabilities come directly from observed data.

We repeatedly observe the world and record how often events occur.

For example, suppose we observe the Student Center over many years. If a statue appears on 355 out of 1000 observations,

then

$$
P(\text{Statue})=\frac{355}{1000}=0.355
$$

The probability is simply the observed frequency.

## Characteristics

- Based on measurements.
- Requires historical data.
- Objective and repeatable.
- Common in statistics and machine learning.

---

# 2. Subjective Interpretation

Sometimes, we do **not** have enough data. Instead, an expert estimates the probabilities.

For example, a doctor might estimate

> "There is about a 20% chance this patient has Disease X."

No large dataset is required. Instead, the probability reflects the expert's belief. This is called the **Subjective** interpretation of probability.

## Characteristics

- Based on expert knowledge.
- Represents degree of belief.
- Frequently used in Bayesian reasoning.

---

# 3. Natural Propensity

Patrick Winston briefly mentions another interpretation, mainly used in physics. Some events appear to possess an inherent randomness.

For example,radioactive decay or certain quantum events. Here, probability is treated as a natural property of the physical world rather than something estimated from data.

---

# Which Interpretation Does AI Use?

Artificial Intelligence generally uses either

- observed frequencies, or
- subjective beliefs.

The exact philosophical interpretation is usually less important than having reasonable probability estimates.

---

# The Real Problem

Regardless of where the probabilities come from, the main difficulty remains the same. Even if we know every probability, we still cannot practically build a massive Joint Probability Table. The representation itself is too large.

---

# A Huge Research Area

Because Joint Probability Tables do not scale, an enormous amount of AI research has focused on finding better representations.

Patrick Winston describes this as an entire industry devoted to representing probabilities **without storing the full Joint Probability Table**.

These methods include:

- Bayesian Networks
- Belief Networks
- Factor Graphs
- Markov Networks
- Hidden Markov Models
- Dynamic Bayesian Networks

Each represents probabilities much more efficiently than a full Joint Probability Table.

---

# The Road Ahead

Patrick Winston outlines the roadmap for the remainder of the lecture.

The progression is

```
Basic Probability

↓

Conditional Probability

↓

Bayes' Rule

↓

Belief Networks (Bayesian Networks)
```

Each topic builds on the previous one.

The ultimate goal is to replace the impractical Joint Probability Table with a compact graphical representation that still allows efficient probabilistic reasoning.

---

# Key Takeaways

- Probabilities may come from observed data (**Frequentist**) or expert belief (**Subjective**).
- Regardless of their source, storing all probabilities in a Joint Probability Table is impractical.
- This scalability problem motivated the development of Bayesian (Belief) Networks.
- The rest of the lecture focuses on the mathematical tools needed to understand these networks.

---

# Part 6 — Conditional Probability and the Chain Rule

In the previous section, we introduced the three basic axioms of probability.

Those axioms tell us what probabilities **must satisfy**, but they are not enough for reasoning under uncertainty.

In Artificial Intelligence, we are usually interested in questions like:

> *If I know one event has happened, how does that change the probability of another event?*

For example,

- If the dog is barking, what is the probability of a burglar?
- If there is an art show, what is the probability that a statue appears?
- If a medical test is positive, what is the probability that the patient has a disease?

Questions like these require **conditional probability**.

---

# What is Conditional Probability?

Conditional probability answers the question:

> **What is the probability of an event, assuming that another event has already occurred?**

Instead of asking

> What is the probability of A?

we ask

> What is the probability of A **given** B?

Mathematically, we write this as

$$
P(A \mid B)
$$

which is read as

> "The probability of A given B."

---

# Definition of Conditional Probability

Patrick Winston defines conditional probability as

$$
P(A \mid B)
=
\frac{P(A \cap B)}{P(B)}
$$

where

- $P(A \cap B)$ is the probability that **both A and B occur**, and
- $P(B)$ is the probability that **B occurs**.

---

# Why Does This Formula Make Sense?

Imagine the following Venn diagram.

```
+------------------------------------+
|                                                                 |
|                         Universe                         |
|                                                                 |
|      _________                                             |
|     /              \                                            |
|    /     A         \                                          |
|   /   _____        \                                         |
|  |   /        \        |                                        |
|  |  |  A∩B  |       |                                        |
|   \  \_____/      /                                          |
|    \         B     /                                           |
|     \_________/                                            |
|                                                                   |
+------------------------------------+
```

Normally, the probability of A is measured relative to the **entire universe**. However, once we know that **B is true**, the universe changes.

Instead of considering every possible outcome, we only consider the outcomes inside B. Our new sample space becomes

```
Only B
```

Within this smaller world, we ask:

> What fraction also belongs to A?

That fraction is exactly

$$
\frac{P(A \cap B)}{P(B)}
$$

---

# Intuition

Think of the denominator,

$$
P(B)
$$

as creating a **new universe**.

Originally,

```
Entire Universe
```

After learning B,

```
Only B matters.
```

Within this restricted world,

we simply ask

> **How much of B also belongs to A?**

---

# Example

Suppose

- 30% of people own a dog.
- 10% own both a dog and a cat.

Then

$$
P(\text{Dog})=0.30
$$

$$
P(\text{Dog and Cat})=0.10
$$

The probability that someone owns a cat **given that they already own a dog** is

$$
P(\text{Cat} \mid \text{Dog})
=
\frac{0.10}{0.30}
=
0.333
$$

So, among dog owners, approximately **33% also own a cat**.

---

# Rearranging the Formula

We can rearrange the definition algebraically. Starting from

$$
P(A \mid B)
=
\frac{P(A \cap B)}{P(B)}
$$

multiply both sides by

$$
P(B)
$$

to obtain

$$
P(A \cap B)
=
P(A \mid B)\,P(B)
$$

This form is often called the **Product Rule** (or Multiplication Rule).

---

# Why Is the Product Rule Useful?

Instead of directly estimating

$$
P(A \cap B)
$$

we can compute it from

1. the probability of B occurring, and
2. the probability of A after B has occurred.

This idea becomes extremely important when many variables are involved.

---

# Extending to Three Variables

Suppose we now have three events:

- A
- B
- C

We want the probability that **all three occur simultaneously**.

That is,

$$
P(A \cap B \cap C)
$$

Instead of estimating this directly, we again apply the Product Rule.

Treat

$$
(B \cap C)
$$

as one combined event.

Then

$$
P(A \cap B \cap C)
=
P(A \mid B,C)\,P(B \cap C)
$$

Notice that

$$
P(B \cap C)
$$

can itself be expanded using the same Product Rule. Specifically,

$$
P(B \cap C)
=
P(B \mid C)\,P(C)
$$

Substituting this back gives

$$
P(A \cap B \cap C)
=
P(A \mid B,C)\,
P(B \mid C)\,
P(C)
$$

---

# A Pattern Begins to Emerge

Look carefully at the structure.

$$
P(A \cap B \cap C)
=
P(A \mid B,C)
P(B \mid C)
P(C)
$$

Notice what happens from left to right. The conditioning becomes smaller.

First,

$$
P(A \mid B,C)
$$

depends on **two variables**.

Next,

$$
P(B \mid C)
$$

depends on **one variable**.

Finally,

$$
P(C)
$$

depends on **nothing**.

Each step removes one conditioning variable. Patrick Winston points out that this is not an accident. It is the beginning of a very powerful general rule.

---

# The Chain Rule

For any collection of random variables

$$
X_1,X_2,\ldots,X_n
$$

their complete joint probability can always be written as

$$
P(X_1,X_2,\ldots,X_n)
=
\prod_{i=1}^{n}
P\!\left(
X_i
\mid
X_{i-1},X_{i-2},\ldots,X_1
\right)
$$

Equivalently, writing it out explicitly,

$$
P(X_1,\ldots,X_n)
=
P(X_n\mid X_{n-1},\ldots,X_1)
\cdots
P(X_2\mid X_1)
P(X_1)
$$

This identity is known as the **Chain Rule of Probability**.

---

# What Does the Chain Rule Do?

The Chain Rule converts one large joint probability

$$
P(X_1,X_2,\ldots,X_n)
$$

into a product of simpler conditional probabilities. Instead of estimating one enormous probability directly, we estimate several smaller probabilities. This decomposition is mathematically exact—it does **not** make any approximations.

---

# Why Is This Important?

The Chain Rule is one of the foundations of Bayesian Networks.

Later, Bayesian Networks will exploit **conditional independence** to simplify these conditional probabilities even further.

Instead of conditioning on *every previous variable*, most variables only depend on a small number of **parents**. This is what allows Bayesian Networks to represent complex probability distributions efficiently.

---

# Key Takeaways

- Conditional probability asks how likely an event is after observing another event.
- It is defined as

$$
P(A \mid B)
=
\frac{P(A \cap B)}{P(B)}
$$

- Rearranging gives the Product Rule

$$
P(A \cap B)
=
P(A \mid B)\,P(B)
$$

- Applying the Product Rule repeatedly leads to the **Chain Rule**.
- The Chain Rule decomposes a large joint probability into a product of conditional probabilities.
- This decomposition is the mathematical foundation on which Bayesian Networks are built.

## Independence and Conditional Independence

In the previous section, we learned that the **Chain Rule** allows us to decompose any joint probability into a product of conditional probabilities.

Although this is mathematically elegant, it still has a major problem.

Consider three variables:

$$
P(A,B,C)
=
P(A\mid B,C)\,P(B\mid C)\,P(C)
$$

Notice that the first term still depends on **both** \(B\) and \(C\).

If we had 20 variables, the first conditional probability would have to depend on **19 other variables**.

As the number of variables increases, estimating all these conditional probabilities quickly becomes impossible.

The key idea that makes Bayesian Networks practical is that **many variables are actually independent of one another**.

This allows us to simplify these conditional probabilities dramatically.

---

# What is Independence?

Two events are **independent** if knowing one event tells us **nothing** about the other.

For example, Suppose we toss

- one coin
- and roll one die.

The result of the coin toss does **not** affect the die roll.

Similarly, the die roll does not affect the coin toss.

These are independent events.

---

# Formal Definition

Patrick Winston defines independence as

$$
P(A\mid B)=P(A)
$$

This means

> Knowing that **B occurred** does not change the probability of **A**.

Equivalently,

$$
P(B\mid A)=P(B)
$$

Both statements express exactly the same idea.

---

# Intuition

Suppose we already know

```
Event B happened.
```

Normally, learning new information changes our beliefs.

However, if A and B are independent, then learning B changes **nothing**.

```
Before observing B

Probability(A)

↓

After observing B

Exactly the same Probability(A)
```

B provides **no useful information** about A.

---

# Visual Interpretation

Imagine the familiar probability space.

```
+--------------------------------------+
|                                      |
|             Universe                 |
|                                      |
|      _________                       |
|     /         \                      |
|    /     A     \                     |
|   /      ___    \                    |
|  |      /   \    |                   |
|  |     |A∩B|     |                   |
|   \     \_/     /                    |
|    \         B /                     |
|     \_________/                      |
|                                      |
+--------------------------------------+
```

Recall that

$$
P(A\mid B)
=
\frac{P(A\cap B)}{P(B)}
$$

If A and B are independent, this ratio should equal

$$
P(A)
$$

In other words, the **fraction of B occupied by A** must be exactly the same as the **fraction of the entire universe occupied by A**.

Learning B does not change the proportion.

---

# Product Rule for Independent Events

Recall the Product Rule

$$
P(A\cap B)
=
P(A\mid B)\,P(B)
$$

If A and B are independent,

then

$$
P(A\mid B)=P(A)
$$

Substituting this into the Product Rule gives

$$
P(A\cap B)
=
P(A)\,P(B)
$$

This is probably the most commonly used formula for independent events.

---

# Why Independence Matters

Imagine three completely unrelated events.

Instead of estimating

$$
P(A\mid B,C)
$$

we simply write

$$
P(A)
$$

because A does not depend on B or C.

This removes enormous amounts of complexity.

Unfortunately, completely independent variables are actually quite rare in real-world problems. Most variables influence one another in some way. This leads us to a much more useful concept.

---

# Conditional Independence

Conditional independence is one of the most important ideas in Bayesian Networks. Two variables may appear dependent, but once we know a third variable, they become independent.

---

# Formal Definition

Patrick Winston defines conditional independence as

$$
P(A\mid B,Z)
=
P(A\mid Z)
$$

This says

> Once we know **Z**, learning **B** provides no additional information about **A**.

Notice the difference.

Ordinary independence says

$$
P(A\mid B)=P(A)
$$

Conditional independence says

$$
P(A\mid B,Z)
=
P(A\mid Z)
$$

B only becomes irrelevant **after** Z is known.

---

# Intuition

Suppose

- A = Patient has pneumonia
- B = Patient has a cough
- Z = Chest X-ray result

Initially, a cough provides useful evidence about pneumonia.

However, once we already have the X-ray, the cough adds very little additional information. The X-ray explains the relationship.

So,

```
Without X-ray

Cough

↓

More evidence for pneumonia

----------------------------

With X-ray

Cough

↓

Almost no extra information
```

This is conditional independence.

---

# Visual Interpretation

Imagine restricting our universe to only those situations where

```
Z is true.
```

Within this smaller world,

we compare

- the proportion of A inside B,
- with the proportion of A inside all of Z.

If those proportions are equal, then B provides no additional information once Z is known.

---

# Product Rule for Conditionally Independent Events

From the definition,

we obtain

$$
P(A\mid B,Z)
=
P(A\mid Z)
$$

Substituting this into the Product Rule,

$$
P(A,B\mid Z)
=
P(A\mid Z)\,P(B\mid Z)
$$

This is the conditional version of

$$
P(A,B)
=
P(A)\,P(B)
$$

Notice that both probabilities are now conditioned on Z.

---

# Why Is Conditional Independence So Important?

Imagine a medical diagnosis system. Without conditional independence, the probability of every disease would depend on every symptom.

The probability tables would become enormous. Instead, Bayesian Networks exploit statements like

> Once we know the disease, two symptoms become independent.

or

> Once we know whether it is raining, wet grass and people carrying umbrellas become independent.

These simplifications reduce massive probability tables into much smaller ones.

This is the fundamental reason Bayesian Networks are computationally efficient.

---

# Comparing the Concepts

| Independence | Conditional Independence |
|--------------|--------------------------|
| Variables never influence each other. | Variables may influence each other until another variable is known. |
| $$P(A\mid B)=P(A)$$ | $$P(A\mid B,Z)=P(A\mid Z)$$ |
| Rare in practice. | Extremely common in Bayesian Networks. |
| Removes all dependence. | Removes dependence only after conditioning on another variable. |

---

# Key Takeaways

- Independence means learning one event never changes the probability of another.

$$
P(A\mid B)=P(A)
$$

- Independent events satisfy

$$
P(A\cap B)=P(A)P(B)
$$

- Conditional independence is much more powerful.

$$
P(A\mid B,Z)=P(A\mid Z)
$$

- Once the conditioning variable is known, the second variable becomes irrelevant.
- Bayesian Networks rely heavily on conditional independence to simplify otherwise enormous probability distributions.
- The next step is to see **how Bayesian Networks use conditional independence to replace massive joint probability tables with compact graphical models.**

## Belief Networks (Bayesian Networks): Representing Probabilistic Knowledge

So far, we have introduced the mathematical tools needed for probabilistic reasoning:

- Joint Probability Distributions
- Conditional Probability
- The Chain Rule
- Independence
- Conditional Independence

Patrick Winston now introduces the idea that makes probabilistic reasoning practical:

> **Belief Networks**, more commonly known today as **Bayesian Networks (Bayes Nets)**.

Instead of storing one enormous joint probability table, we represent relationships using a **graph**.

This dramatically reduces the number of probabilities we need to specify.

---

# Motivation: The Dog–Burglar–Raccoon Example

Consider a familiar scenario. A neighbor's dog sometimes barks.

Why might it bark? Several explanations are possible:

- A burglar is nearby.
- A raccoon is outside.
- Sometimes the dog simply barks for no reason.

Immediately, we notice something important: The causes of barking are **not all equally related**.

The burglar does **not** cause raccoons.

The raccoon does **not** cause burglars.

Instead, both independently influence the dog.

---

# Thinking in Terms of Cause and Effect

Rather than asking

> "What combinations of variables are possible?"

Winston asks

> **"Who influences whom?"**

The relationships become

```
Burglar
      \
       \
        ---> Dog Barking
       /
      /
Raccoon
```

Notice the direction of the arrows. They represent **causal influence**.

```
Cause

↓

Effect
```

The dog barks **because** of the burglar or raccoon.

The burglar does **not** appear because the dog barked.

---

# Extending the Example

Now suppose two additional events exist.

If the dog barks, the neighbors may

```
Call the police.
```

If a raccoon appears, it may

```
Knock over the trash can.
```

Our graph now becomes

```text
          Burglar
              \
               \
                \
                 ▼
             Dog Barking
             /          \
            ▼            ▼
 Call Police      (Effect)

Raccoon
    \
     \
      ▼
Dog Barking

Raccoon
    │
    ▼
Trash Can Knocked Over
```

Or more compactly,

```text
      Burglar          Raccoon
          \              /   \
           \            /     \
            ▼          ▼       ▼
           Dog Barking      Trash Can
                 │
                 ▼
          Call Police
```

---

# What Does an Arrow Mean?

An arrow

```
A → B
```

does **not** simply mean

> "A and B are related."

Instead, it means

> **A directly influences B.**

For example,

```
Burglar → Dog Barking
```

means the probability that the dog barks depends on whether a burglar is present.

Likewise,

```
Dog Barking → Call Police
```

means the decision to call the police depends on whether the dog is barking.

---

# The Local Markov Property

This is the most important idea in Bayesian Networks. Patrick Winston states it as

> **Every node depends only on its parents and is conditionally independent of all its non-descendants given its parents.**

Although the wording sounds intimidating, the intuition is simple.

## Example 1 — Calling the Police

```
Dog Barking
      │
      ▼
Call Police
```

Suppose we already know whether the dog is barking.

Does it matter whether a burglar is present?

No.

Once we know

```
Dog Barking
```

additional information about

- Burglar
- Raccoon
- Trash Can

does not affect the probability that someone calls the police.

Mathematically,

```
Call Police

depends only on

Dog Barking
```


## Example 2 — Trash Can

```
Raccoon

↓

Trash Can
```

Once we know whether a raccoon is present,

it no longer matters

- whether a burglar appeared,
- whether the dog barked,
- whether the police were called.

The trash can only depends on

```
Raccoon
```


## Example 3 — Dog Barking

```
Burglar

↓

Dog Barking

↑

Raccoon
```

The probability that the dog barks depends only on

- Burglar
- Raccoon

It does **not** directly depend on

```
Call Police
```

because calling the police happens **after** the dog barks.

---

# Why Is This Useful?

Imagine describing the world using a Joint Probability Table. With 5 binary variables, we would need

$$
2^5 = 32
$$

possible rows.

Every additional binary variable doubles the size of the table. Very quickly, this becomes impossible.

Instead, Bayesian Networks describe only the **local dependencies**. Each variable only needs probabilities involving its parents. This is far smaller than storing every possible combination.

---

# Conditional Probability Tables (CPTs)

Each node stores a **Conditional Probability Table (CPT).**

A CPT answers the question

> **Given my parents, what is the probability that I am true?**

For example,

Dog Barking has two parents.

```
Burglar

↓

Dog

↑

Raccoon
```

Since each parent is binary, there are only four possible parent combinations.

| Burglar | Raccoon | P(Dog Barking=True) |
|---------|----------|--------------------:|
| False | False | 0.10 |
| False | True | 0.50 |
| True | False | 1.00 |
| True | True | 1.00 |

Notice something remarkable. Instead of describing every possible world, we only describe

> **How the dog behaves under each combination of its parents.**

---

# Root Nodes

Some variables have **no parents**.

For example,

```
Burglar
```

and

```
Raccoon
```

These are called **root nodes**. They simply store prior probabilities.

For example,

$$
P(\text{Burglar})=0.10
$$

$$
P(\text{Raccoon})=0.50
$$

No conditioning is required because nothing influences them.

---

# Child Nodes

Variables with parents use conditional probabilities.

For example,

Dog Barking stores

$$
P(Dog \mid Burglar,Raccoon)
$$

Call Police stores

$$
P(CallPolice \mid Dog)
$$

Trash Can stores

$$
P(TrashCan \mid Raccoon)
$$

Each node only stores information about its **immediate causes**.

---

# Why Bayesian Networks Save Space

Suppose our network contains

5 binary variables.

A Joint Probability Table requires

$$
2^5=32
$$

rows.

A Bayesian Network stores

- Burglar prior
- Raccoon prior
- Dog CPT (4 rows)
- Call Police CPT (2 rows)
- Trash Can CPT (2 rows)

Only

```
10 probabilities
```

need to be specified.

Instead of

```
32 numbers
```

we only store

```
10 numbers.
```

As the number of variables grows, this saving becomes enormous.

---

# Key Insight

A Bayesian Network is **not** just a graph. It combines

1. **Graph Structure**
   - shows causal or dependency relationships

2. **Conditional Probability Tables**
   - quantify those relationships

Together, they completely describe the underlying probability distribution.

---

# Connection to Previous Concepts

Notice how all the ideas fit together.

- The **Chain Rule** tells us every joint distribution can be decomposed.
- **Conditional Independence** tells us many conditioning variables can be removed.
- A **Bayesian Network** encodes exactly which variables can be ignored.

In other words, the graph is a compact representation of conditional independence assumptions.

---

# Key Takeaways

- A **Bayesian Network (Belief Network)** is a directed graph representing probabilistic dependencies.
- Nodes represent random variables.
- Directed edges represent direct causal or probabilistic influence.
- Every node stores a **Conditional Probability Table (CPT)** based only on its parents.
- Root nodes store prior probabilities.
- Child nodes store conditional probabilities.
- The graph encodes **conditional independence**, allowing large joint probability distributions to be represented compactly.
- Instead of storing every possible world, Bayesian Networks only store **local relationships**, making probabilistic inference computationally feasible.

## From Bayesian Networks to the Full Joint Probability Distribution

In the previous section, we saw that a Bayesian Network stores only a small number of **local probability tables**.

For the Dog–Burglar example, we only needed around **10 probabilities** instead of the **32 probabilities** required by the full Joint Probability Table.

A natural question now arises:

> **How can a handful of local probabilities represent the entire joint probability distribution?**

The answer combines **two ideas** we learned earlier:

1. The **Chain Rule**
2. **Conditional Independence**

Together, they allow us to reconstruct the full joint probability distribution from the Bayesian Network.

---

# Step 1 — Start with the Joint Probability

Suppose our network contains the following variables:

- Burglar (B)
- Raccoon (R)
- Dog Barking (D)
- Trash Can Knocked Over (T)
- Call Police (P)

The joint probability of one complete world is

$$
P(P,D,B,T,R)
$$

For example, one row of the joint distribution might represent

- Burglar = True
- Raccoon = False
- Dog Barking = True
- Trash Can = False
- Police Called = True

The joint probability assigns a probability to **every such combination**.

---

# Step 2 — Apply the Chain Rule

The Chain Rule tells us that **any** joint probability can be decomposed into a product of conditional probabilities.

Expanding the variables in an appropriate order gives

$$
P(P,D,B,T,R)
=
P(P\mid D,B,T,R)
\;
P(D\mid B,T,R)
\;
P(B\mid T,R)
\;
P(T\mid R)
\;
P(R)
$$

At this stage, nothing has been simplified.

We have simply rewritten one large probability as a product of smaller ones.

---

# Step 3 — Use Conditional Independence

Now comes the key idea.

The Bayesian Network tells us that many of these conditional probabilities contain **unnecessary variables**.

We can remove them using the conditional independence assumptions encoded by the graph.


## Example 1 — Police

From the network,

```text
Dog Barking
      │
      ▼
Call Police
```

The probability of calling the police depends **only** on whether the dog is barking.

It does **not** directly depend on

- Burglar
- Raccoon
- Trash Can

Therefore,

$$
P(P\mid D,B,T,R)
=
P(P\mid D)
$$

All the extra variables disappear.

## Example 2 — Dog Barking

The network tells us

```text
Burglar ─┐
         ▼
     Dog Barking
         ▲
Raccoon ─┘
```

Dog Barking depends only on

- Burglar
- Raccoon

It does **not** directly depend on

```
Trash Can
```

because Trash Can is a **descendant** of Raccoon.

Therefore,

$$
P(D\mid B,T,R)
=
P(D\mid B,R)
$$

Again, one unnecessary variable disappears.

## Example 3 — Burglar

Burglar is a **root node**. Nothing causes a burglar.

Therefore,

$$
P(B\mid T,R)
=
P(B)
$$

The conditioning variables disappear entirely.

## Example 4 — Trash Can

Trash Can depends only on

```
Raccoon
```

Therefore,

$$
P(T\mid R)
$$

already has exactly the correct form. Nothing changes.

## Example 5 — Raccoon

Raccoon is another root node.

Therefore,

$$
P(R)
$$

remains unchanged.

---

# The Simplified Factorization

After applying all these conditional independence assumptions,

the large Chain Rule expression becomes

$$
P(P,D,B,T,R)
=
P(P\mid D)
\;
P(D\mid B,R)
\;
P(B)
\;
P(T\mid R)
\;
P(R)
$$

Notice what happened.

The enormous conditional probabilities have become **small local probabilities**, each involving only a variable and its parents.

This is exactly the information stored inside the Bayesian Network.

---

# General Rule for Bayesian Networks

For a Bayesian Network with variables

$$
X_1,X_2,\ldots,X_n
$$

the complete joint probability distribution factorizes as

$$
P(X_1,X_2,\ldots,X_n)
=
\prod_{i=1}^{n}
P(X_i\mid Parents(X_i))
$$

This is one of the most important equations in probabilistic AI.

Instead of conditioning on **all previous variables** (as in the Chain Rule),

each variable is conditioned **only on its parents**.

---

# Why This Works

The graph encodes a set of conditional independence assumptions. These assumptions allow us to replace large conditional probabilities such as

$$
P(D\mid B,T,R)
$$

with much smaller ones like

$$
P(D\mid B,R)
$$

As a result, the Bayesian Network stores only the probabilities that are actually needed.

---

# Example: Number of Parameters

Consider our five-variable network. Without a Bayesian Network, a Joint Probability Table requires

$$
2^5 = 32
$$

possible rows.

With the Bayesian Network, we only specify:

- Prior for Burglar
- Prior for Raccoon
- CPT for Dog Barking
- CPT for Call Police
- CPT for Trash Can

This requires only about

```
10 probabilities
```

instead of

```
32 probabilities.
```

---

# Why the Savings Become Huge

The difference becomes dramatic as the number of variables grows.

Suppose we have

```
20 binary variables.
```

A Joint Probability Table would require

$$
2^{20}
=
1,\!048,\!576
$$

entries.

If each variable only has two or three parents, a Bayesian Network might require only a few dozen probabilities. This exponential reduction is why Bayesian Networks are practical for real-world AI systems.

---

# The Complete Workflow

A Bayesian Network performs probabilistic reasoning in three steps.

### Step 1

Design the graph.

```
Nodes

↓

Variables

Edges

↓

Dependencies
```

---

### Step 2

Specify a Conditional Probability Table (CPT) for every node.

Each CPT only involves

```
Parents → Child
```

---

### Step 3

Recover the full Joint Probability Distribution by combining

- the Chain Rule, and
- the conditional independence assumptions encoded in the graph.

The resulting distribution is mathematically identical to the original joint distribution but is represented much more compactly.

---

# Why Bayesian Networks Are So Powerful

Patrick Winston emphasizes that we **never explicitly write down the enormous Joint Probability Table**.

Instead, we construct a graph and specify only local probability tables. From these, the complete probability distribution can always be reconstructed.

This is what makes Bayesian Networks one of the most successful probabilistic representations in Artificial Intelligence.

---

# Key Takeaways

- The **Chain Rule** decomposes any joint probability into conditional probabilities.
- Bayesian Networks use **conditional independence** to simplify those conditional probabilities.
- Every variable depends only on its **parents**, not on every other variable.
- The complete joint distribution is recovered using

$$
P(X_1,\ldots,X_n)
=
\prod_i P(X_i\mid Parents(X_i))
$$

- Bayesian Networks represent the same probability distribution as a Joint Probability Table but require exponentially fewer parameters.
- This compact representation is what makes probabilistic reasoning feasible for large, complex AI systems.