Previous: [[Lecture 6 - Bayesian Networks IV — Bayesian Network Structures]]
Next: [[Lecture 6 – Bayesian Networks VI - Exact Inference]]
# What is Probabilistic Inference?

Probabilistic inference means:

> Using the Bayes Network to compute probabilities after observing evidence.

Instead of simply storing probabilities, we now **reason with them**.

For example:

> Mary calls and says the alarm is ringing.

We may want to know:

> How likely is it that there was actually a burglary?

The Bayes Network lets us answer this mathematically.

---

# Three Types of Variables

During inference, every variable belongs to one of three categories.

## 1. Evidence Variables

These are variables whose values are already known.

Example:

```text
Mary Calls = True
```

We already observed this fact.

These variables become the **input** to our inference problem.


## 2. Query Variables

These are the variables whose probabilities we want to compute.

Example:

```text
Burglary = ?
```

We do not know whether a burglary occurred.

The purpose of inference is to estimate its probability.

## 3. Hidden Variables

These are variables that are neither observed nor directly asked for.

However, they still influence the computation.

Example:

```text
Earthquake
Alarm
```

Even if we are not interested in these variables themselves, they affect the probability of burglary and therefore cannot simply be ignored.

---

# Example Classification

Suppose:

> Mary calls to report that the alarm has gone off.

We want to know whether there was a burglary.

Then:

| Variable | Type |
|----------|------|
| Burglary | Query |
| Mary Calls | Evidence |
| Alarm | Hidden |
| Earthquake | Hidden |
| John Calls | Hidden |

Notice that the hidden variables are **not discarded**.

They must still be considered during inference because they influence the query.

---

# Posterior Distribution

The answer produced by probabilistic inference is called the **posterior distribution**.

It is written as

$$
P(\text{Query} \mid \text{Evidence})
$$

Meaning:

> The probability of the query variable **after incorporating the observed evidence**.

Example:

$$
P(B \mid M)
$$

This reads:

> Probability of a burglary given that Mary called.

---

# General Form

If there are multiple query variables,

$$
P(Q_1,Q_2,\ldots \mid E_1,E_2,\ldots)
$$

Examples:

$$
P(B,E \mid M)
$$

Probability of burglary and earthquake given Mary called.

---

$$
P(B,J \mid M)
$$

Probability of burglary and John calling given Mary called.

---

# Evidence Can Be Anywhere

Unlike ordinary programming functions, Bayes Networks are **not limited to one direction**.

In a normal function:

```text
Inputs
   │
   ▼
Function
   │
   ▼
Outputs
```

Information only flows one way.

---

In a Bayes Network, evidence can be supplied anywhere.

For example:

### Causal reasoning

Known:

```text
Burglary
Earthquake
```

Infer:

```text
Alarm
John Calls
Mary Calls
```

Reasoning follows the direction of the arrows.

---

### Diagnostic reasoning

Known:

```text
John Calls
Mary Calls
```

Infer:

```text
Burglary
Earthquake
```

Reasoning goes **against** the arrows.

This is exactly the type of reasoning made possible by Bayes' Rule.

---

### Mixed reasoning

Known:

```text
Mary Calls
```

Infer:

```text
Burglary
John Calls
```

Evidence and queries can be placed anywhere in the network.

---

# Most Likely Explanation (MLE)

Sometimes we are not interested in the full probability distribution.

Instead, we ask:

> Which combination of variable values is most likely?

Instead of computing

$$
P(Q \mid E)
$$

we compute

$$
\arg\max_Q P(Q \mid E)
$$

This means:

> Find the assignment of the query variables with the highest posterior probability.

For example:

Mary called.

Possible explanations:

| Burglary | Earthquake | Probability |
|-----------|------------|------------|
| True | False | 0.28 |
| False | True | 0.12 |
| False | False | 0.55 |
| True | True | 0.05 |

The **Most Likely Explanation (MLE)** is simply the row with the highest probability.

---

# Key Ideas from This Section

- Bayes Networks are not just representations—they are tools for **probabilistic inference**.
- During inference, variables are classified as:
  - Evidence
  - Query
  - Hidden
- The result of inference is the **posterior distribution**

$$
P(\text{Query} \mid \text{Evidence})
$$

- Evidence can appear anywhere in the network.
- Bayes Networks support both **causal reasoning** and **diagnostic reasoning**.
- Sometimes we want the full posterior distribution, while other times we only want the **most likely explanation (MLE)**.

---

# Summary

This section introduces **probabilistic inference**, the process of answering probability questions using a Bayes Network. Every inference problem is defined by **evidence variables** (known observations), **query variables** (what we want to infer), and **hidden variables** (unknown intermediate variables). The goal is usually to compute the **posterior distribution**, $P(\text{Query}\mid\text{Evidence})$, although sometimes we seek only the **most likely explanation**. Unlike traditional programs, Bayes Networks allow reasoning in both causal and diagnostic directions, making them powerful tools for uncertain reasoning.

Next: [[Lecture 6 – Bayesian Networks VI - Exact Inference]]