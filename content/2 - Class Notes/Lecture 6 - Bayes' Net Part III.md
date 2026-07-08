
> **Prerequisites**
>
> - [[3 - Probability]]
> - [[4 - Conditional Porbability]]
> - [[6 - Bayes' Theorem]]
> - [[Lecture 6 - Bayes' Net Part I]]
> - [[Lecture 6 - Bayes' Net Part III]]

# Enumeration

## Goal

Now that we know how Bayes Networks represent probability distributions, the next question is:

> **How do we actually answer probability questions using a Bayes Network?**

This process is called **probabilistic inference**.

The first inference algorithm introduced in the lecture is **Enumeration**.

It is the most direct algorithm and serves as the foundation for later, faster algorithms.

---

# Example Bayes Network

The lecture uses the famous **Burglary–Earthquake–Alarm** network.

```
Burglary ----\
              \
               Alarm -----> John Calls
              /
Earthquake --/ \
               \
                Mary Calls
```

Variables:

- **B** = Burglary
- **E** = Earthquake
- **A** = Alarm
- **J** = John calls
- **M** = Mary calls

---

# Example Query

Suppose:

- John called.
- Mary called.

We want to know:

> What is the probability that a burglary occurred?

Mathematically:

$$
P(B \mid J,M)
$$

---

# Step 1 — Apply Conditional Probability

Use the definition of conditional probability.

$$
P(B\mid J,M)
=
\frac{P(B,J,M)}
{P(J,M)}
$$

The lecture immediately rewrites the problem into:

- numerator = joint probability
- denominator = normalization term

---

# Hidden Variables

Notice that the query mentions only

- B
- J
- M

But the network also contains

- Earthquake
- Alarm

These are **hidden variables**.

We do not know their values.

Therefore we must consider **every possible value** they could take.

---

# Enumeration

Enumeration literally means

> **Try every possible combination of hidden variables.**

For this network:

Hidden variables:

- Earthquake (E)
- Alarm (A)

Both are Boolean.

Therefore there are

$$
2^2 = 4
$$

possible assignments.

| E | A |
|---|---|
| T | T |
| T | F |
| F | T |
| F | F |

We compute the probability for **each row**, then add them together.

---

# Expanding the Joint Probability

Instead of computing

$$
P(B,J,M)
$$

directly, we sum over all hidden variables.

$$
P(B,J,M)
=
\sum_E
\sum_A
P(B,E,A,J,M)
$$

This is exactly the **Law of Total Probability** applied to hidden variables.

---

# Factorizing Using the Bayes Network

Instead of treating the joint probability as one giant table, we use the Bayes Network factorization.

The lecture rewrites

$$
P(B,E,A,J,M)
$$

as

$$
P(B)
P(E)
P(A\mid B,E)
P(J\mid A)
P(M\mid A)
$$

This is possible because of the network structure.

Notice how each node depends **only on its parents**.

---

# Complete Enumeration Formula

Putting everything together:

$$
P(B,J,M)
=
\sum_E
\sum_A
P(B)
P(E)
P(A\mid B,E)
P(J\mid A)
P(M\mid A)
$$

The lecture calls each product

$$
f(E,A)
$$

Then

$$
P(B,J,M)
=
\sum_E
\sum_A
f(E,A)
$$

---

# Example Calculation

Consider one row:

- Burglary = True
- Earthquake = True
- Alarm = True
- John = True
- Mary = True

The CPT values are

$$
P(B)=0.001
$$

$$
P(E)=0.002
$$

$$
P(A\mid B,E)=0.95
$$

$$
P(J\mid A)=0.9
$$

$$
P(M\mid A)=0.7
$$

Multiply them together.

$$
0.001
\times
0.002
\times
0.95
\times
0.9
\times
0.7
=
0.000001197
$$

This is **only one** of the four enumeration rows.

The remaining three rows are computed the same way.

Finally,

- add all four rows,
- normalize using

$$
P(J,M)
$$

to obtain

$$
P(B\mid J,M)
$$

---

# Final Result

The lecture states

$$
P(B\mid J,M)
\approx
0.284
$$

---

# Why Isn't the Probability Higher?

At first glance:

- John called
- Mary called

so burglary might seem almost certain.

However,

the lecture explains that burglary itself is **very rare**.

The prior probability

$$
P(B)=0.001
$$

is extremely small.

Although both phone calls provide strong evidence,

the low prior keeps the posterior probability to

$$
0.284
$$

rather than something close to 1.

---

# Drawback of Enumeration

Enumeration works well for small networks.

However, the number of hidden-variable assignments grows exponentially.

For

$$
n
$$

Boolean hidden variables,

the algorithm must examine

$$
2^n
$$

rows.

This quickly becomes computationally expensive, motivating faster inference methods introduced later in the lecture.

---

# Key Takeaways

- **Inference** answers probability queries using a Bayes Network.
- Enumeration computes probabilities by considering every possible assignment of hidden variables.
- Hidden variables are eliminated by summing over all their possible values.
- The Bayes Network factorizes the joint distribution into local conditional probabilities.
- Each enumeration row multiplies the appropriate CPT entries.
- The final probability is obtained by summing all rows and normalizing.
- Enumeration is conceptually simple but scales exponentially with the number of hidden variables.

# Speeding Up Enumeration & Causal Direction
---

# 1. Constructing Bayes Networks Efficiently

Peter Norvig introduces an important question:

> Suppose we already know the variables of a problem.
> 
> **How should we connect them?**

Different graph structures can represent the same probability distribution, but **some require many more probability tables than others.**

The goal is to maximize conditional independence.

## Example: Alarm Network

Original causal network:

```
Burglary ──►
             \
              Alarm ──► John Calls
             /
Earthquake ─►
              \
               Mary Calls
```

This network is efficient because every arrow follows the **true causal direction**.

---

# 2. Building the Network in a Different Order

Suppose instead we begin constructing the network with:

```
John Calls
Mary Calls
```

Question:

> Are John and Mary independent?

---

Answer:

**No.**

Although they have no arrow between them in the original network,

they are connected through the hidden variable Alarm.

```
John ◄── Alarm ──► Mary
```

Without knowing Alarm,

John calling increases the chance Alarm occurred.

If Alarm becomes more likely,

Mary calling also becomes more likely.

Therefore

```
John ⟂̸ Mary
```

They are dependent.

## Key Principle

Unknown common causes create dependence.

# 3. Adding Alarm

Now Alarm is inserted.

Question:

What variables is Alarm dependent on?

Answer:

Alarm depends on

- John
    
- Mary
    

because

If John calls,

Alarm becomes more likely.

If Mary calls,

Alarm becomes more likely.

If both call,

Alarm becomes even more likely.

Diagram:

```
John
    \
     Alarm
    /
Mary
```

---

# 4. Adding Burglary

Now Burglary is added.

Question:

Which previous variables affect Burglary?

Answer:

Only Alarm.

Diagram:

```
Burglary ◄── Alarm
```

Why not John or Mary?

Because

Once Alarm is known,

John and Mary provide no extra information.

Mathematically,

```
B ⟂ {J,M} | A
```


## Intuition

Imagine:

John called.

Mary called.

Alarm definitely rang.

Once Alarm is already known,

whether John called is irrelevant.

The evidence has already been absorbed into Alarm.

---

# 5. Adding Earthquake

Finally,

Earthquake is inserted.

Question:

Which variables affect Earthquake?

Answer:

Earthquake depends on

- Alarm
    
- Burglary
    

Diagram:

```
Burglary ─► Alarm ◄── Earthquake
```

---

Why Burglary?

Because of **explaining away**.

Suppose Alarm occurred.

Possible explanations:

- burglary
    
- earthquake
    

If burglary becomes known,

earthquake becomes less likely.

If burglary is impossible,

earthquake becomes more likely.

Thus

```
Earthquake
```

depends on

```
Burglary
```

after conditioning on Alarm.

---

# 6. The Moral

Norvig concludes:

> **Bayes Nets are most compact when built in the causal direction.**

Instead of

```
Effects → Causes
```

build

```
Causes → Effects
```

---

Why?

Because causes are usually independent.

Effects become conditionally independent once causes are known.

This produces:

- fewer edges
    
- fewer CPT entries
    
- faster inference
    

## Example

Bad ordering:

```
John
 ↓
Alarm
 ↓
Burglary
 ↓
Earthquake
```

Many unnecessary dependencies appear.

---

Good ordering:

```
Burglary ─► Alarm ◄── Earthquake
               │
          ┌────┴────┐
          ▼                   ▼
       John                  Mary
```

Much simpler.

---

# Key Takeaways (Part 3)

- Build Bayes Nets in the causal direction.
    
- Unknown causes induce dependence.
    
- Conditioning on causes removes dependence between effects.
    
- Better graph structure leads directly to faster inference.
    

# Variable Elimination

# 1. The Problem with Enumeration

Previously we solved inference using
  
P(Q|E) = $\sum_{\text{hidden variables}}  \prod_i P(X_i|\text{Parents}(X_i))$

Enumeration computes **every hidden-variable combination.**

This becomes expensive because many intermediate products are recomputed repeatedly.

---

# Example Network

```
Rain (R)
     │
     ▼
Traffic (T)
     │
     ▼
Late (L)
```

Goal:

Find P(L)

---

Enumeration computes

```
R=True
T=True

R=True
T=False

R=False
T=True

R=False
T=False
```

Every combination is visited.

Many repeated calculations occur.

---

# 2. Variable Elimination Idea

Instead of building one huge table, build several small tables.

Then eliminate variables one at a time.

Think of compressing the network gradually.

The algorithm repeatedly performs two operations:

1. Join factors
    
2. Eliminate variables
    

# 3. What is a Factor?

A factor is simply a table over one or more variables.

Examples:

### Prior

|R|P(R)|
|---|---|
|True|0.1|
|False|0.9|

---

Conditional table

| R   | T   | P(T\|R) |
| --- | --- | ------- |
| T   | T   | 0.8     |
| T   | F   | 0.2     |
| F   | T   | 0.1     |
| F   | F   | 0.9     |

These are factors.

---

# 4. Operation 1 — Join Factors

Join means

multiply matching rows.

Suppose P(R)  and P(T|R) Join them.

Result:  P(R,T)  

---

Example

For

```
R=True
T=True
```

Multiply

```
0.1 × 0.8 = 0.08
```

Do this for every row.

Result:

|R|T|Joint|
|---|---|---|
|T|T|0.08|
|T|F|0.02|
|F|T|0.09|
|F|F|0.81|

This new table is another factor.

---

# 5. Operation 2 — Eliminate Variables

Suppose Rain is hidden.

Remove it.

How?

Add probabilities sharing the same remaining variables.

Example

For Traffic = True

```
0.08 + 0.09 = 0.17
```

For

Traffic = False

```
0.02 + 0.81 = 0.83
```

Result

|T|Probability|
|---|---|
|True|0.17|
|False|0.83|

Rain has disappeared.

---

This operation is called

- elimination
    
- marginalization
    
- summing out
    

All mean exactly the same thing.

---

# 6. Continue Eliminating

Now join

Traffic

with

Late.

Compute P(T,L) by multiplying entries.

Example

```
0.17 × 0.3
=
0.051
```

Continue for all rows.

Result

|T|L|Value|
|---|---|---|
|T|T|0.051|
|T|F|0.119|
|F|T|0.083|
|F|F|0.747|

---

# 7. Eliminate Traffic

Now remove T.

For

Late = True

```
0.051 + 0.083 = 0.134
```

For

Late = False

```
0.119 + 0.747 = 0.866
```

Final table

|L|Probability|
|---|---|
|True|0.134|
|False|0.866|

Therefore P(L = True) = 0.134  

---

# 8. Variable Elimination Algorithm

The process is always:

```
Choose a hidden variable

↓

Join every factor containing it

↓

Eliminate it (sum out)

↓

Repeat
```

Eventually only the query variables remain.

---

# 9. Why Is This Faster?

Enumeration

```
Create gigantic joint table

↓

Then sum
```

Variable Elimination

```
Small table

↓

Join

↓

Eliminate

↓

Smaller table

↓

Repeat
```

Large intermediate tables are avoided.

## Complexity Comparison

### Enumeration

```
Compute everything

↓

Exponential work
```

---

### Variable Elimination

```
Compute only what is necessary

↓

Reuse intermediate results

↓

Much faster in practice
```

Inference is still NP-hard in the worst case, but Variable Elimination dramatically reduces computation for most real-world Bayes Networks.


|Concept|Meaning|
|---|---|
|**Factor**|A probability table over one or more variables|
|**Join**|Multiply compatible factors into a larger factor|
|**Eliminate (Marginalize)**|Sum out a hidden variable from a factor|
|**Variable Elimination**|Alternate joining and eliminating until only the query variables remain|
|**Advantage**|Avoids repeated calculations and is much faster than full enumeration|

>[!Summary]
>- **Good Bayes Net structure matters.** Building networks from **causes → effects** minimizes dependencies and makes inference more efficient.
    >- **Enumeration** is conceptually simple but scales poorly because it recomputes many intermediate values.
    >- **Variable Elimination** improves efficiency by working with **factors**, repeatedly **joining** relevant probability tables and **eliminating** hidden variables through marginalization.
    >- These ideas form the foundation for more advanced exact inference algorithms used in modern probabilistic AI systems.

---

# Approximate Inference & Sampling

# Why Approximate Inference?

So far we've studied **exact inference**:

- Enumeration
    
- Variable Elimination
    

These always produce the exact probability.

Example:

$$  
P(Burglary=True \mid John=True, Mary=True)  
$$

can be computed exactly.

---

The problem is that exact inference becomes computationally expensive.

Large Bayes Nets may contain:

- hundreds of variables
    
- thousands of CPT entries
    
- millions or billions of possible assignments
    

Exact algorithms eventually become too slow.

---

Instead, we can **approximate** the answer.

Rather than computing every possibility,

we generate many random samples.

As the number of samples increases,

our estimate approaches the true probability.


## Big Idea

Instead of computing P(X) exactly, estimate it from observations.

Exactly like estimating the probability of heads by flipping a coin many times.

---

# Sampling Intuition

Suppose we have two fair coins.

Possible outcomes:

|Coin 1|Coin 2|
|---|---|
|H|H|
|H|T|
|T|H|
|T|T|

Instead of calculating probabilities mathematically, flip them repeatedly.

Example:

```
H T
T H
H H
T T
H T
H T
```

Count occurrences.

|Outcome|Count|
|---|---|
|HH|1|
|HT|3|
|TH|1|
|TT|1|

Estimated probabilities:

$$
P(HH)=\frac16  
$$

$$
P(HT)=\frac36  
$$

etc.

---

As more samples are collected,

these frequencies converge to the true probabilities.

This is an application of the **Law of Large Numbers**.

---

# Advantages of Sampling

Advantages over exact inference:

### 1. Faster

No exponential summation.

---

### 2. Works on huge networks

Can handle networks where exact inference is impossible.

---

### 3. Works even without explicit CPTs

If we can simulate the system,

sampling still works.

---

# Example Bayes Net

```
        Cloudy
        /    \
       /          \
Sprinkler       Rain
      \            /
       \        /
      Wet Grass
```

Variables:

- Cloudy (C)
    
- Sprinkler (S)
    
- Rain (R)
    
- Wet Grass (W)
    

---

Dependencies:

```
Cloudy
   ↓
Sprinkler

Cloudy
   ↓
Rain

Sprinkler
      \
       \
        WetGrass
       /
Rain
```

---

# Prior Sampling

Also called **Forward Sampling**.

## Step 1

Sample root nodes first.

Cloudy has no parents.

Suppose

$$
P(C=True)=0.5  
$$

Randomly sample.

Suppose:

```
Cloudy = True
```


## Step 2

Now sample Sprinkler.

Since Cloudy=True,

look only at this row:

|C|P(S=True)|
|---|---|
|True|0.1|

Generate random number.

Suppose:

```
Sprinkler=False
```


## Step 3

Sample Rain.

Parent is Cloudy=True.

Suppose

$$
P(R=True)=0.8  
$$

Sample.

Result:

```
Rain=True
```

## Step 4

Now Wet Grass.

Parents:

```
Sprinkler=False
Rain=True
```

Use corresponding CPT row.

Suppose
$$  
P(W=True)=0.9  
$$

Random draw gives

```
WetGrass=True
```

---

Entire sample:

```
Cloudy=True
Sprinkler=False
Rain=True
WetGrass=True
```

Throw this sample away.

Generate another.

Repeat thousands of times.

Eventually:

```
+C -S +R +W
-C +S -R -W
+C +S +R +W
...
```

---

# Why Prior Sampling Works

Every variable is sampled according to its CPT.

Therefore,

over many samples,

each assignment appears with exactly its true probability.

The sampling process is **consistent**.

---

Consistency means:

As $N\rightarrow\infty$

Estimated probabilities converge to true probabilities.

---

# Conditional Probability Problem

Suppose we want

$$
P(W=True \mid C=False)  
$$

Our samples include both:

```
+C
-C
```

Only samples satisfying

```
Cloudy=False
```

are useful.

The others are discarded.

This leads to...

# Rejection Sampling

Procedure:

Generate complete samples normally.

Reject any sample that doesn't match evidence.

---

Example

Evidence:

```
Cloudy=False
```

Samples:

```
+C -S +R +W ❌ Reject

-C +S +R -W ✔ Keep

+C +S -R -W ❌ Reject

-C -S -R +W ✔ Keep
```

Only retained samples estimate the conditional probability.

## Why it Works

Among the retained samples,

their distribution converges to
$$ 
P(Query|Evidence)  
$$

---

# Problem with Rejection Sampling

Suppose evidence is extremely rare.

Example:

Alarm network.

Evidence:

```
Alarm=True
```

But

Alarm = True

is uncommon.

Generated samples might be:

```
-B -A ❌

-B -A ❌

-B -A ❌

-B -A ❌

+B +A ✔
```

Thousands of samples are discarded.

Very inefficient.

---

# Likelihood Weighting

Idea:

Never reject samples.

Instead,

fix evidence variables from the beginning.

---

Example:

Evidence:

```
Sprinkler=True

WetGrass=True
```

Always force:

```
S=True

W=True
```

Only non-evidence variables are sampled.

Instead of rejecting,

assign each sample a **weight**.

## Example

Suppose:

Cloudy=True

Forced:

```
Sprinkler=True
```

From CPT:

$$
P(S=True|C=True)=0.1  
$$

Current weight:

```
0.1
```

---

Sample Rain.

Suppose

Rain=True.

---

Wet Grass is evidence.

Forced:

```
WetGrass=True
```

From CPT:

$$ 
P(W=True|S=True,R=True)=0.99  
$$

Multiply weight:

$$ 
0.1\times0.99

0.099  
$$

Final sample:

```
+C +S +R +W

Weight = 0.099
```

---

Instead of counting as

```
1 sample
```

it contributes

```
0.099 samples
```

---

# Why Likelihood Weighting Helps

No samples are rejected.

All generated samples contribute.

Far more efficient when evidence is rare.

---

Still consistent.

As samples increase,

weighted estimates converge to true probabilities.

---

# Remaining Problem

Suppose evidence is

```
Sprinkler=True

Rain=True
```

Cloudy is an ancestor.

Cloudy is sampled before seeing evidence.

Sometimes:

```
Cloudy=False
```

is generated,

even though the evidence strongly suggests

```
Cloudy=True.
```

Those samples receive very low weights.

So likelihood weighting still wastes effort.

---

# Gibbs Sampling

Solution:

Instead of generating entire samples,

modify one variable at a time.

---

Suppose evidence is fixed.

Current assignment:

```
Cloudy=True
Sprinkler=True   (Evidence)
Rain=False
WetGrass=True    (Evidence)
```

Choose one hidden variable.

Example:

```
Rain
```

Resample Rain

using every other variable.

Now:

```
Cloudy=True
Sprinkler=True
Rain=True
WetGrass=True
```

Next iteration:

choose Cloudy.

Update only Cloudy.

Repeat forever.


Unlike previous sampling methods:

Adjacent samples differ by only one variable.

---

This forms a **Markov Chain**.

Hence the name **Markov Chain Monte Carlo (MCMC).**

---

Eventually, the chain spends time in each state proportional to its probability.

Thus Gibbs Sampling is also consistent.

---

# Comparison of Sampling Methods

|Method|Reject Samples?|Uses Evidence During Sampling?|Efficiency|
|---|---|---|---|
|Prior Sampling|No|No|Poor for conditional probabilities|
|Rejection Sampling|Yes|After sampling|Poor when evidence is rare|
|Likelihood Weighting|No|Evidence fixed|Better|
|Gibbs Sampling|No|Uses all evidence continuously|Usually best|

---

# Key Exam Takeaways

✔ Approximate inference estimates probabilities using random samples.

✔ More samples → higher accuracy.

✔ Prior sampling generates samples from root to leaves.

✔ Rejection sampling discards samples inconsistent with evidence.

✔ Likelihood weighting fixes evidence and weights samples instead of rejecting them.

✔ Gibbs sampling repeatedly resamples one hidden variable while keeping evidence fixed.

✔ All four methods are **consistent**, meaning they converge to the correct probability as the number of samples approaches infinity.

---

# Cheat Sheet

|Method|Core Idea|
|---|---|
|Prior Sampling|Generate complete samples from the network|
|Rejection Sampling|Keep only samples matching evidence|
|Likelihood Weighting|Fix evidence and weight each sample|
|Gibbs Sampling|Resample one hidden variable at a time using current assignments|
