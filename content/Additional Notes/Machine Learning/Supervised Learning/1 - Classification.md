# Classification

> [!insight]
> **Classification** is a supervised machine learning task in which the goal is to assign an input instance to one of several predefined categories (classes) based on its features.

The model learns from **labelled training data** and predicts the correct class for previously unseen examples.

## What is Classification?

Classification attempts to learn a mapping

$$
f:X\rightarrow Y
$$

where

- $X$ = feature space (inputs)
- $Y$ = finite set of class labels

Unlike regression, which predicts continuous values, classification predicts **discrete categories**.

> **Figure:** Classification Example
>
> *![[Pasted image 20260709230715.png|509]]

The blue and orange points represent two classes. Each point corresponds to one student described by two features: Math Score and Interview Score. The objective of a classifier is to learn a decision rule that separates these classes and correctly predicts the label of new students.
## Examples

Classification problems appear throughout Artificial Intelligence and Data Science.

Examples include

| Problem | Classes |
|----------|----------|
| Email Filtering | Spam / Not Spam |
| Medical Diagnosis | Disease / Healthy |
| Image Recognition | Cat / Dog / Bird |
| Credit Risk | Default / No Default |
| Sentiment Analysis | Positive / Neutral / Negative |
| Fraud Detection | Fraudulent / Legitimate |


## Classification Pipeline

A typical classification workflow consists of five stages.

### 1. Training Data

A labelled dataset is collected.

Each training example contains

- Feature vector
- Known class label

Example

| Features | Label |
|----------|-------|
| Age, Income | High Income |
| Age, Income | Medium Income |

---

### 2. Feature Extraction

Relevant characteristics of each observation are selected or engineered.

Good features improve classifier performance by providing informative descriptions of the data.

Examples include

- Age
- Income
- Pixel intensity
- Word frequency
- Sensor measurements

---

### 3. Model Training

A classification algorithm learns the relationship between the features and their corresponding labels.

The objective is to discover a decision rule that generalizes beyond the training data.

---

### 4. Model Evaluation

The trained classifier is tested on previously unseen examples.

Common evaluation metrics include

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC

---

### 5. Prediction

Once trained, the classifier predicts the most likely class for new observations.

## Example

Suppose household income is grouped into three categories.

| Income | Class |
|----------|--------|
| Less than \$60,000 | Low Income |
| \$60,000 – \$99,999 | Middle Income |
| \$100,000+ | High Income |

The classifier may use additional information such as

- Education
- Age
- Occupation
- Geographic location
- Years of experience

to predict which income category a person belongs to.

## Decision Boundary

A classifier separates different classes using a **decision boundary**.

The complexity of this boundary depends on both the data and the learning algorithm.

Simple datasets may require only a linear boundary, whereas more complex datasets require nonlinear decision boundaries.

> [!important]
> Real-world datasets rarely exhibit perfect class separation. As a result, selecting an appropriate classifier and decision boundary is an important part of the learning process.

The figure below illustrates how Logistic Regression separates the two classes using a single straight decision boundary.

>**Figure:** Decision Boundary (Logistic Regression). 
>Logistic Regression learns a **linear decision boundary** that separates the feature space into two regions. Points on one side of the boundary are classified as _Rejected_, while points on the other side are classified as _Admitted_
>![[Pasted image 20260709231441.png|530]]

Different classification algorithms learn different types of decision boundaries. Some, such as Logistic Regression, produce linear boundaries, while others, such as Decision Trees or Neural Networks, can learn much more complex nonlinear boundaries.

---

# Classifiers

A **classifier** is the machine learning model that performs classification.

It learns patterns from labelled examples and uses those patterns to predict labels for unseen observations.

## How Classifiers Learn

During training, the classifier

1. Observes labelled examples.
2. Learns relationships between features and labels.
3. Constructs a decision rule or decision boundary.
4. Applies this rule to future observations.

## Characteristics of a Good Classifier

A good classifier should

- Generalize well to unseen data.
- Resist overfitting.
- Handle noisy observations.
- Produce accurate predictions.
- Be computationally efficient.

## Common Classification Algorithms

Some of the most widely used classifiers include

- [[1. Decision Trees]]
- [[2. k-Nearest Neighbors]]
- [[3. Naïve Bayes]]
- [[4. Logistic Regression]]
- [[5. Support Vector Machines]]
- [[6. Random Forests]]
- [[7. Gradient Boosting]]
- [[2.2 Neural Networks]]

Each algorithm has different assumptions, strengths, and limitations.

---
# Hard vs Soft Classification

Classification models generally produce predictions in one of two forms.

## Hard Classification

Hard classification assigns exactly one class to every observation.

Example

```text
Email → Spam
```

or

```text
Tumor → Benign
```

There is no measure of uncertainty.

## Soft Classification

Soft classification predicts the probability that an observation belongs to each class.

Example

| Class | Probability |
|---------|------------:|
| Spam | 0.82 |
| Not Spam | 0.18 |

The predicted class is usually the one with the highest probability.

---

### Advantages of Soft Classification

Soft classification

- Quantifies uncertainty.
- Handles overlapping classes.
- Supports threshold adjustment.
- Provides confidence estimates.

This is particularly useful in medical diagnosis, fraud detection, and risk assessment.

---
Example:

| Hard Classification      | Soft Classification |
| ------------------------ | ------------------- |
| **Student X**            | **Student X**       |
| **Prediction:** Admitted | Admitted → **87%**  |
|                          | Rejected → **13%**  |

**Table:** Comparison of hard and soft classification. Hard classification assigns only the most likely class label (e.g., _Admitted_), whereas soft classification estimates the probability of belonging to each class before selecting the most likely prediction. The probability estimates provide a measure of confidence in the prediction.

# Choosing a Classification Threshold

Many classifiers output probabilities.

A threshold determines the final prediction.

For example

$$
P(\text{Spam}|x) > 0.5
$$

may classify an email as spam.

However, the threshold does **not** have to be 0.5.

## Cost-Sensitive Classification

Different mistakes may have different consequences.

Example

Explosive detection

Predicting

- Safe when explosive → catastrophic

Predicting

- Explosive when safe → inconvenience

Therefore the classifier should prefer **false alarms** over missed explosives.

This illustrates the importance of selecting an appropriate decision threshold.

---

# Axis-Aligned Decision Boundaries

Sometimes a classifier depends on only one feature.

If the decision boundary is

- **Vertical**, only the **x-axis feature** affects classification.

- **Horizontal**, only the **y-axis feature** affects classification.

More sophisticated classifiers combine information from multiple features to produce diagonal or nonlinear decision boundaries.

## Summary

| Concept | Description |
|----------|-------------|
| Classification | Predicts discrete categories |
| Classifier | Learns decision rules from labelled data |
| Feature Extraction | Represents observations numerically |
| Decision Boundary | Separates classes in feature space |
| Hard Classification | Predicts one class only |
| Soft Classification | Predicts class probabilities |
| Threshold | Converts probabilities into class labels |
| Cost-sensitive Classification | Adjusts decisions based on error costs |