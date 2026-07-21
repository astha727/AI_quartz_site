
Previous: [[Lecture 6 – Bayesian Networks VI - Exact Inference]]
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
Next:[[Lecture 7 - Machine Learning Part I]]