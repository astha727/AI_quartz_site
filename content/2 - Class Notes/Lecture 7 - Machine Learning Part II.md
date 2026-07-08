# Ensemble Learning, Boosting & Neural Networks

> [!insight]
> This section continues the Machine Learning lecture by introducing **ensemble methods**, **Naïve Bayes**, **Maximum Likelihood**, **Random Forests**, **Boosting**, and the foundations of **Neural Networks**. These methods illustrate different approaches to classification and reinforce the **No Free Lunch Theorem**—no single algorithm performs best for every problem.

---
Related Notes: 
[[Lecture 7 - Machine Learning Part I]]
# 1. Random Forests

Random Forests are an **ensemble learning** technique that combines multiple decision trees.

Instead of relying on a single tree, many trees are trained independently and then **vote** on the final prediction.

## Key Idea

> [!tip]
> Instead of trusting one decision tree, train many diverse trees and aggregate their predictions.


## How does a Random Forest work?

1. Randomly sample the training data (**bootstrap sampling**).
2. Randomly choose a subset of features for each tree.
3. Train a decision tree on the sampled data.
4. Repeat many times.
5. Each tree predicts a class.
6. The final prediction is the **majority vote** (classification) or **average** (regression).

## Why does it work?

A single decision tree often **overfits** the training data.

Random Forests reduce overfitting because:

- Each tree sees different training examples.
- Each tree uses different subsets of features.
- Individual tree errors tend to cancel one another.

Advantages:

- Lower variance
- Better generalization
- Resistant to overfitting
- Works well on high-dimensional datasets

See:

- [[1.2 Ensemble Learning]]

---

# 2. Boosting

Boosting combines many **weak classifiers** into a **strong classifier**.

Unlike Random Forests, Boosting trains classifiers **sequentially**, where each new classifier focuses on examples that previous classifiers misclassified.

## Core Idea

After each weak classifier:

- Increase the weights of incorrectly classified examples.
- Decrease the weights of correctly classified examples.
- Train the next classifier using the updated weights.

Each classifier specializes in correcting previous mistakes.

## AdaBoost

One of the most famous boosting algorithms is **AdaBoost (Adaptive Boosting).**

Each weak classifier receives a voting weight:

$$
\alpha_t=\frac12\ln\left(\frac{1-\epsilon_t}{\epsilon_t}\right)
$$

where

- $\epsilon_t$ = classification error
- $\alpha_t$ = voting weight

Properties:

- Small error → larger weight
- Large error → smaller weight

## Final Prediction

Each classifier casts a weighted vote.

The ensemble prediction is determined by the weighted sum of all classifier votes.

## Advantages

Boosting can:

- Improve weak learners dramatically.
- Focus learning on difficult examples.
- Produce highly accurate classifiers.
- Perform automatic feature selection.

See:

- [[1.2 Ensemble Learning]]

# 3. No Free Lunch Theorem

> [!important]
> No Machine Learning algorithm is optimal for every problem.

Every algorithm makes assumptions about the underlying data.

Algorithms that perform well on one class of problems will perform worse on another.

Examples include:

- Decision Trees
- k-Nearest Neighbors
- Naïve Bayes
- Support Vector Machines
- Neural Networks
- Random Forests
- Boosting
- Gaussian Mixture Models

The choice of algorithm should depend on:

- Data distribution
- Noise
- Number of features
- Computational resources
- Interpretability requirements

---

# 4. Maximum Likelihood

In Naïve Bayes, if all classes are assumed equally likely, we assign an example to the class that maximizes the likelihood.

$$
P(D|C_j)=\prod_{i=1}^{n}P(d_i|C_j)
$$

where

- $d_i$= feature i
- $C_j$ = class

This approach is called **Maximum Likelihood (ML).**

## Maximum Likelihood vs MAP

| Method                     | Uses Prior Probability? |
| -------------------------- | ----------------------- |
| Maximum Likelihood (ML)    | No                      |
| Maximum A Posteriori (MAP) | Yes                     |

MAP computes

$$
P(C_j|D)\propto P(D|C_j)P(C_j)
$$

Thus,

> **Maximum Likelihood is simply MAP assuming equal class priors.**

---

# 5. Naïve Bayes

Naïve Bayes assumes that features are **conditionally independent given the class.**

Instead of estimating one large joint probability distribution, it estimates many small conditional probabilities.

## Bayesian Network Representation

```text
        Class
          /   |   \
         /    |    \
 Feature1 Feature2 Feature3
```

The class influences each feature.

Once the class is known, the features are assumed to be independent.

## Advantages

- Extremely fast
- Memory efficient
- Easy to train
- Performs surprisingly well on text classification
- Robust to many irrelevant features

## Why doesn't irrelevant features hurt much?

Suppose eye color is unrelated to gender.

Then

$$
P(\text{Brown Eyes}|\text{Male})
\approx
P(\text{Brown Eyes}|\text{Female})
$$

These probabilities nearly cancel during Bayes computation.

The informative features dominate the final decision.

See:

- [[4.2 Bayesian Inference]]

---

# 6. Gaussian Classification

Many real-world variables approximately follow a **Gaussian (Normal) Distribution**.

Examples include:

- Human height
- Sensor noise
- Biological measurements
- Exam scores (approximately)

## Gaussian Probability Density Function

$$
f(x)=
\frac{1}{\sqrt{2\pi\sigma^2}}
e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$

where

- $\mu$ = mean
- $\sigma^2$ = variance
- $\sigma$ = standard deviation

## Empirical Rule

| Interval | Probability |
|-----------|------------|
| μ ± 1σ | 68% |
| μ ± 2σ | 95% |
| μ ± 3σ | 99.7% |


## Decision Boundary

For two Gaussian classes,

the **decision boundary** occurs where

$$
P(C_1|x)=P(C_2|x)
$$

Properties:

- Equal variance → one threshold
- Different variances → possibly multiple thresholds

---

# 7. Recognition Accuracy & Class Imbalance

Accuracy alone can be misleading.

Example:

- Positive examples = 10%
- Negative examples = 90%

A classifier that always predicts **negative**

achieves

**90% accuracy**

while learning absolutely nothing.

---

> [!warning]
> Always compare model accuracy against the **baseline class distribution**.

Accuracy should be interpreted alongside:

- Precision
- Recall
- F1-score
- ROC-AUC

---

# 8. Generalization

The true objective of Machine Learning is **generalization**.

A model should perform well on **previously unseen data**.

Good generalization requires:

- Representative training data
- Appropriate model complexity
- Cross Validation
- Independent Test Set

> [!important]
> High training accuracy does **not** imply good generalization.

---

# 9. Neural Networks

Artificial Neural Networks were inspired by biological neurons.

Each artificial neuron receives

- Inputs
- Weights
- Bias
- Activation Function

and produces an output.

![[Pasted image 20260708182506.png]]
                       Creator: Natalie Wolchover
## Artificial Neuron

```text
x₁ ----\
         \
x₂ -----> Σ ----> g(.) ----> Output
         /
x₃ ----/

Bias ----/
```


## Mathematical Form

$$
a=g\left(\sum_i w_ix_i+b\right)
$$

where

- \(w_i\) = weights
- \(x_i\) = inputs
- \(b\) = bias
- \(g\) = activation function

## Common Activation Functions

| Function | Purpose |
|----------|---------|
| Step | Binary logic |
| Sigmoid | Probability estimation |
| Tanh | Zero-centered activation |
| ReLU | Deep learning |

---

# 10. Multilayer Neural Networks

A **Feed-Forward Neural Network** contains:

- Input Layer
- Hidden Layer(s)
- Output Layer

Information moves in only one direction.

## Forward Pass

For one output neuron,

$$a_5
=
g(w_{35}a_3+w_{45}a_4+b)
$$

Each hidden neuron performs the same computation.

## Why Nonlinear Activations Matter

If every activation were linear,

multiple layers would collapse into one linear equation.

Nonlinear activation functions allow neural networks to learn:

- Curved decision boundaries
- Complex feature interactions
- Highly nonlinear functions

See:

- [[2.2 Neural Networks]]

---

# Summary

| Concept | Key Idea |
|----------|----------|
| ==Random Forests== | Ensemble of decision trees using majority voting |
| ==Boosting== | Sequentially improves weak classifiers |
| ==Maximum Likelihood== | Selects class with highest likelihood |
| ==Maximum A Posteriori (MAP)== | Uses likelihood and prior probabilities |
| ==Naïve Bayes== | Assumes conditional independence between features |
| ==Gaussian Classification== | Models classes using Gaussian distributions |
| ==Decision Boundary== | Region where class probabilities are equal |
| ==Class Imbalance== | Accuracy alone may be misleading |
| ==Generalization== | Perform well on unseen data |
| ==Neural Networks== | Learn nonlinear decision boundaries using weighted neurons |
| ==Multilayer Networks== | Stack nonlinear neurons to learn complex functions |