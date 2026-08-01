# Machine Learning (AI)

> [!insight]
> Machine Learning is the branch of Artificial Intelligence that enables computers to improve their performance by learning patterns from data rather than relying solely on explicitly programmed rules.
>
> While classical AI often focuses on search, logic, and reasoning, Machine Learning focuses on **learning from examples**.

---

# 1. Introduction

Machine Learning, Pattern Recognition, and Data Mining are closely related fields.

Although these terms are often used interchangeably, there are subtle differences.

* **Machine Learning** focuses on learning predictive models from data.
* **Pattern Recognition** focuses on recognizing regularities and structures within data.
* **Data Mining** emphasizes discovering useful knowledge and relationships from large datasets.

Many algorithms are shared across all three areas.

## What kinds of problems can Machine Learning solve?

Machine Learning is widely used for:

* Optical Character Recognition (OCR)
* Face Recognition
* Speech Recognition
* Handwriting Recognition
* Text Retrieval
* Spam Filtering
* Activity Recognition
* Recommendation Systems
* Medical Diagnosis
* Web Search

> [!tip]
> The same learning algorithms often appear in Artificial Intelligence, Machine Learning, Pattern Recognition, Computer Vision, Robotics, and Data Mining.

---

# 2. Supervised vs Unsupervised Learning

Machine Learning algorithms are broadly divided into two categories.

## Supervised Learning

> [!insight]
> **Supervised Learning** is a machine learning paradigm in which the algorithm learns a mapping from **inputs (features)** to **known outputs (labels)** using labeled training data.
>
> During training, the model repeatedly compares its predictions against the correct answers and adjusts its parameters to minimize prediction error. Once trained, it can generalize to unseen examples.

### Components of Supervised Learning

A supervised learning dataset consists of:

- **Features (Input Variables, X)** — measurable attributes describing each observation.
- **Labels (Target Variable, y)** — the correct output associated with each observation.

The goal is to learn a function

$$
f : X \rightarrow Y
$$

that predicts the correct output for previously unseen data.

---

### Learning Process

1. Collect labeled training data.
2. Learn patterns relating features to labels.
3. Optimize model parameters to minimize prediction error.
4. Evaluate performance on unseen test data.
5. Deploy the trained model for inference.

---

### Types of Supervised Learning

Supervised learning problems are broadly divided into two categories.

#### Classification

The output belongs to one of several **discrete categories**.

Examples:

- Spam vs Not Spam
- Disease diagnosis
- Handwritten digit recognition
- Sentiment analysis
- Fraud detection

Typical algorithms include:

- [[Naïve Bayes]]
- Decision Trees
- Random Forests
- [[Support Vector Machines]]
- [[Neural Networks]]
- [[k-Nearest Neighbors]]

See:

- [[1 - Classification]]

---

#### Regression

The output is a **continuous numerical value**.

Examples:

- House price prediction
- Temperature forecasting
- Stock price estimation
- Patient survival time
- Sales prediction

Typical algorithms include:

- [[Linear Regression]]
- [[Polynomial Regression]]
- Decision Trees
- Random Forest Regression
- Neural Networks

See:

- [[2. Regression]]

---

### Characteristics

Advantages

- High predictive performance when labeled data is available.
- Clear evaluation using ground-truth labels.
- Supports a wide variety of applications.

Limitations

- Requires large amounts of labeled data.
- Label collection can be expensive and time-consuming.
- Performance depends on how representative the training data is.

---

### Common Applications

Healthcare

- Disease diagnosis
- Medical image analysis
- Risk prediction

Natural Language Processing

- Spam detection
- Sentiment analysis
- Language translation

Computer Vision

- Face recognition
- Object detection
- OCR

Finance

- Credit scoring
- Fraud detection
- Loan approval

Engineering

- Predictive maintenance
- Fault detection
- Quality inspection


> [!important]
> Most of the algorithms introduced in this Machine Learning section—including **k-Nearest Neighbors, Naïve Bayes, Decision Trees, Random Forests, Boosting, and Neural Networks**—are examples of **supervised learning algorithms**.

## Unsupervised Learning

> [!insight]
> **Unsupervised Learning** is a machine learning paradigm in which the algorithm is given **unlabeled data** and must discover hidden patterns, relationships, or structure without knowing the correct answers beforehand.

Unlike supervised learning, there are **no target labels** to guide the learning process.

Instead, the algorithm attempts to identify similarities, clusters, latent variables, or lower-dimensional representations directly from the data.

---

### Components of Unsupervised Learning

An unsupervised dataset contains only

- **Features (Input Variables, X)**

There are **no labels (y)**.

The objective is to discover meaningful structure within the feature space.

---

### Learning Process

1. Collect unlabeled data.
2. Measure similarities or distances between observations.
3. Identify hidden patterns or structures.
4. Group similar observations or learn compact representations.
5. Analyze the discovered structure.

---

### Types of Unsupervised Learning

#### Clustering

Clustering partitions observations into groups such that:

- Observations within the same cluster are highly similar.
- Observations in different clusters are significantly different.

Examples:

- Customer segmentation
- Document grouping
- Gene expression analysis
- Image segmentation

Typical algorithms include:

- [[k-Means]]
- [[Hierarchical Clustering]]
- [[Gaussian Mixture Models]]
- [[DBSCAN]]

See:

- [[6. Clustering]]
- [[Lecture 7- Machine Learning Part V]]

---

#### Dimensionality Reduction

Many real-world datasets contain hundreds or thousands of features.

Dimensionality reduction attempts to represent the same information using fewer variables while preserving as much structure as possible.

Applications include:

- Data visualization
- Noise reduction
- Feature extraction
- Faster machine learning

Typical methods include:

- [[Principal Component Analysis (PCA)]]
- [[t-SNE]]
- [[Autoencoders]]

See:

- [[7. Features]]

---

#### Density Estimation

Instead of assigning classes, some algorithms estimate the probability distribution that generated the data.

Examples include:

- [[Gaussian Mixture Models]]
- [[Expectation Maximization (EM)]]
- [[Kernel Density Estimation]]

Density estimation forms the foundation of many probabilistic machine learning methods.

---

### Advantages

- No labeled data required.
- Can discover previously unknown patterns.
- Useful for exploratory data analysis.
- Often serves as preprocessing for supervised learning.

---

### Limitations

- Difficult to evaluate objectively.
- Results may not correspond to meaningful real-world categories.
- Performance often depends heavily on algorithm assumptions.

---

### Common Applications

Business

- Customer segmentation
- Market basket analysis

Healthcare

- Patient subtype discovery
- Disease phenotype identification

Computer Vision

- Image compression
- Feature learning

Natural Language Processing

- Topic modeling
- Word embeddings

Cybersecurity

- Anomaly detection
- Intrusion detection


> [!important]
> Unsupervised learning focuses on **discovering structure**, whereas supervised learning focuses on **predicting labels**.

---
# 3. Choosing the Right Algorithm

> [!note]
> There is **no universally best Machine Learning algorithm**. Every algorithm makes assumptions about the underlying data, and its performance depends on how well those assumptions match the problem.

This principle is formalized by the **No Free Lunch Theorem**, which states that an algorithm performing exceptionally well on one class of problems must perform worse on others.

---

### Factors That Influence Algorithm Selection

Choosing an algorithm depends on several characteristics of the problem.

#### Dataset Size

Small datasets often work well with

- [[k-Nearest Neighbors]]
- [[Decision Trees]]
- [[Naïve Bayes]]

Large datasets often favor

- [[Random Forests]]
- [[Gradient Boosting]]
- [[Neural Networks]]

---

#### Number of Features

High-dimensional datasets often benefit from

- [[Support Vector Machines]]
- [[Naïve Bayes]]
- [[Neural Networks]]

Lower-dimensional datasets may work well with

- [[Decision Trees]]
- [[k-Nearest Neighbors]]

---

#### Noise

Datasets containing significant measurement noise often require algorithms that generalize well.

Examples include

- [[Random Forests]]
- [[Boosting]]
- [[Regularized Models]]

---

#### Interpretability

Some applications require decisions that humans can understand.

Highly interpretable models include

- [[Decision Trees]]
- [[Linear Regression]]
- [[Logistic Regression]]

Less interpretable ("black-box") models include

- [[Neural Networks]]
- [[Boosting]]
- [[Ensemble Methods]]

---

#### Computational Cost

Some algorithms require little computation.

Examples:

- Naïve Bayes
- Decision Trees

Others may require substantial training time.

Examples:

- Deep Neural Networks
- Large Support Vector Machines

---

### Trade-offs

Every machine learning algorithm balances different objectives.

| Property | Simple Models | Complex Models |
|-----------|--------------|---------------|
| Training Speed | High | Lower |
| Interpretability | High | Low |
| Flexibility | Lower | Higher |
| Risk of Overfitting | Lower | Higher |
| Computational Cost | Low | High |

---

> [!important]
> Machine Learning is **not** about finding the "best" algorithm.
>
> It is about choosing the algorithm whose assumptions best match the characteristics of the data and the problem.


# 4. Decision Trees

> [!insight]
> A **Decision Tree** is a supervised learning algorithm that classifies examples by recursively partitioning the feature space using a sequence of decision rules.

Each internal node asks a question about one feature.

Each branch corresponds to one possible answer.

Each leaf node contains the final prediction.

---

### Tree Structure

A decision tree consists of

- Root node
- Internal decision nodes
- Branches
- Leaf nodes

```text
            Outlook?
          /     |      \
      Sunny  Overcast  Rain
        |         |       |
   Humidity?     Play   Wind?
```

---

### Learning Process

Decision trees are constructed recursively.

At each step:

1. Evaluate every candidate feature.
2. Measure how informative each feature is.
3. Select the feature providing the greatest reduction in uncertainty.
4. Split the data.
5. Repeat until stopping criteria are met.

---

### Information Gain

Most decision tree algorithms choose splits using **Information Gain**, which measures how much uncertainty (entropy) decreases after splitting the data.

Algorithms include:

- ID3
- C4.5
- CART

---

### Advantages

- Easy to interpret
- Handles both numerical and categorical features
- Requires little data preprocessing
- Fast prediction
- Naturally performs feature selection

---

### Limitations

- Easily overfits
- Sensitive to noisy data
- Small data changes may produce different trees

These limitations motivate ensemble methods such as

- [[Random Forests]]
- [[Boosting]]

---

### Common Applications

- Medical diagnosis
- Credit approval
- Fraud detection
- Customer segmentation
- Feature importance analysis

---

See:

- [[3 - Decision Trees]]

# 5. k-Nearest Neighbors (k-NN)

> [!note]
> **k-Nearest Neighbors (k-NN)** is a supervised, instance-based learning algorithm that classifies new observations based on the labels of the most similar training examples.

Unlike many machine learning algorithms, k-NN performs **no explicit training**.

Instead, it memorizes the training dataset.

---

### Learning Process

When a new example arrives:

1. Compute the distance to every training example.
2. Identify the **k nearest neighbors**.
3. Retrieve their labels.
4. Predict the majority class.

For regression, the prediction is typically the average of the neighboring values.

---

### Distance Metrics

Common distance measures include

- Euclidean Distance
- Manhattan Distance
- Minkowski Distance
- Cosine Similarity (high-dimensional text)

The choice of distance metric strongly influences performance.

---

### Choosing k

The value of **k** controls model complexity.

Small k

- Flexible decision boundary
- Sensitive to noise
- Higher variance

Large k

- Smoother boundary
- More robust to noise
- Higher bias

Cross-validation is commonly used to determine an appropriate value of **k**.

---

### Advantages

- Simple to understand
- No training phase
- Naturally handles multiclass problems
- Flexible decision boundaries

---

### Limitations

- Slow prediction on large datasets
- Sensitive to irrelevant features
- Requires feature scaling
- Memory intensive

---

### Common Applications

- Pattern recognition
- Image classification
- Recommendation systems
- Medical diagnosis
- Document classification

---

See:

- [[2 - k-Nearest Neighbors]]

# 6. Model Evaluation

A Machine Learning model should be evaluated on data that was **not used during training**.

Testing on the training data often produces overly optimistic results.

This phenomenon is known as **overfitting**.

To estimate real-world performance, the available data is typically divided into:

* Training set
* Validation set
* Test set

## Cross Validation

Cross Validation repeatedly divides the data into different training and testing partitions.

The model is trained multiple times.

The average performance provides a more reliable estimate than a single train-test split.

Benefits include:

* Better performance estimation
* Parameter tuning
* Reduced sampling bias
* Detecting unstable models

Common strategies include:

* k-Fold Cross Validation
* Leave-One-Out Cross Validation (LOOCV)

See:

* [[2. Cross Validation]]

---

# 7. Overfitting

Overfitting occurs when a model memorizes the training data instead of learning general patterns.

An overfitted model performs well on training data but poorly on unseen examples.

Typical causes include:

* Excessively complex models
* Small datasets
* Excessive parameter tuning

Cross Validation helps detect overfitting before deployment.

> [!warning]
> High training accuracy does **not** necessarily imply good real-world performance.

---

# 8. Generalization

The goal of Machine Learning is **generalization**.

A successful model performs well on new, previously unseen examples.

Good generalization requires:

* Representative training data
* Appropriate model complexity
* Proper validation
* Sufficient data diversity

---

# 9. Typical Machine Learning Workflow

```text
Collect Data
      │
      ▼
Preprocess Data
      │
      ▼
Split Dataset
      │
      ▼
Train Model
      │
      ▼
Cross Validation
      │
      ▼
Tune Parameters
      │
      ▼
Final Testing
      │
      ▼
Deployment
```

---

# 10. AI vs Machine Learning

| Artificial Intelligence | Machine Learning |
| ----------------------- | ---------------- |
| Designs intelligent systems | Learns from data |
| Includes search, planning, reasoning, logic | Focuses on prediction and pattern discovery |
| May not require learning | Learning is central |
| Often rule-based | Primarily data-driven |

---

# Summary

| Concept | Description |
| -------- | ----------- |
| ==Machine Learning== | Learning patterns from data |
| ==Supervised Learning== | Learning from labeled examples |
| ==Unsupervised Learning== | Discovering hidden structure without labels |
| ==Decision Trees== | Classification using sequential questions |
| ==k-NN== | Classification using nearby examples |
| ==Cross Validation== | Reliable model evaluation using repeated train-test splits |
| ==Overfitting== | Memorizing training data instead of generalizing |
| ==Generalization== | Performing well on unseen data |


# 11. Gaussian Distributions in Machine Learning

Many Machine Learning algorithms model data using the **Gaussian (Normal) Distribution** because numerous real-world phenomena approximately follow a bell-shaped curve.

A Gaussian distribution is characterized by two parameters:

- Mean (μ)
- Standard Deviation (σ)

These determine the center and spread of the distribution.

Common applications include:

- Probabilistic classification
- Density estimation
- Bayesian learning
- Gaussian Mixture Models (GMMs)

See:

- [[3. Gaussian Distribution]]

## Why are Gaussians Important?

The Gaussian distribution appears naturally in many real-world datasets because of the **Central Limit Theorem**.

When many independent random factors contribute to an observation, the resulting distribution tends toward a Gaussian.

Examples include:

- Human height
- Measurement noise
- Sensor readings
- Exam scores (approximately)
- Biological variation

See:

- [[4. Central Limit Theorem]]

---

> [!tip]
> Many Machine Learning algorithms assume Gaussian-distributed features because it simplifies probability estimation while remaining surprisingly effective in practice.

---

# 12. Gaussian Classification

One way to classify data is by modeling each class as its own probability distribution.

Given an observation:

1. Estimate the probability density under each class distribution.
2. Compare the probabilities.
3. Predict the class with the highest probability.

For example:

- Grasshopper vs Katydid using antenna length
- Medical diagnosis using biomarker measurements
- Fraud detection using transaction statistics

See:

- [[5. Gaussian Classification]]

---

# 13. Decision Boundaries

A **decision boundary** separates regions belonging to different predicted classes.

For Gaussian classifiers:

- The boundary occurs where two class probabilities are equal.
- Equal variances often produce a single threshold.
- Different variances may produce multiple decision boundaries.

Decision boundaries also depend on:

- Class variances
- Prior probabilities
- Feature distributions

See:

- [[6. Decision Boundaries]]

---

# 14. Prior Probabilities

Classification depends not only on the observed data but also on how common each class is.

For example,

Suppose:

- 90% of insects are grasshoppers
- 10% are katydids

Even when the feature value lies near the overlap between both distributions, the classifier is more likely to predict **grasshopper** because that class is more common.

This prior knowledge shifts the decision boundary.

See:

- [[6. Decision Boundaries]]
- [[8. Bayes Classifier]]

---

> [!important]
> A classifier should consider both the observed evidence and the prior likelihood of each class.

---

# 15. Classification Accuracy Can Be Misleading

Overall accuracy does not always reflect classifier quality.

For example,

Suppose:

- 90% Negative
- 10% Positive

A classifier that always predicts **Negative** achieves:

**90% accuracy**

despite never identifying a positive example.

Therefore, classifier performance should always be compared against a simple baseline.

Proper evaluation requires:

- Independent test sets
- Cross Validation
- Class balance analysis

See:

- [[2. Cross Validation]]

---

> [!warning]
> High accuracy does **not** necessarily indicate a useful classifier.

---

# 16. Classification Error

Every classifier makes mistakes.

Classification errors arise because different class distributions often overlap.

Sources of error include:

- Measurement noise
- Similar feature values
- Limited features
- Imperfect models

Theoretical minimum error for a given feature representation is known as the **Bayes Error**.

Sometimes different types of errors have different costs.

Examples:

- Missing a cancer diagnosis
- Incorrectly marking a legitimate email as spam
- Failing to detect fraud

Decision boundaries can be adjusted to reduce more costly errors.

See:

- [[7. Classification Error]]

---

# 17. Bayesian Classification

Bayesian classifiers compute:

> "Given the observed data, what is the probability that this example belongs to each class?"

Rather than making decisions solely from feature similarity, Bayesian methods combine:

- Likelihood
- Prior probability
- Evidence

using **Bayes' Rule**.

This produces a probabilistic prediction instead of only a class label.

See:

- [[8. Bayes Classifier]]

---

# 18. Naive Bayes

Naive Bayes simplifies Bayesian classification by assuming that features are **conditionally independent** given the class.

Although this assumption is rarely perfectly true, Naive Bayes often performs surprisingly well.

Advantages include:

- Extremely fast training
- Fast prediction
- Works well with high-dimensional data
- Effective for text classification and spam filtering

The probabilistic structure of Naive Bayes can also be represented as a simple Bayesian Network where:

- The class variable is the parent.
- Features are conditionally independent children.

See:

- [[9. Naive Bayes]]

---

> [!note]
> Despite its "naive" independence assumption, Naive Bayes remains one of the strongest baseline classifiers in Machine Learning.

---

# Summary

| Concept | Description |
|----------|-------------|
| ==Gaussian Distribution== | Models many real-world feature distributions |
| ==Central Limit Theorem== | Explains why Gaussian distributions frequently arise |
| ==Gaussian Classification== | Models each class using probability distributions |
| ==Decision Boundary== | Separates regions assigned to different classes |
| ==Prior Probability== | Incorporates class frequency into predictions |
| ==Classification Error== | Errors caused by overlapping distributions and uncertainty |
| ==Bayes Classifier== | Uses Bayes' Rule for probabilistic prediction |
| ==Naive Bayes== | Assumes conditional independence between features |


# 19. Maximum Likelihood Estimation (MLE)

Many probabilistic classifiers assign an example to the class that is **most likely to have generated the observed data**.

For a feature vector:

$$
D=(d_1,d_2,\ldots,d_n)
$$

Naive Bayes assumes the features are conditionally independent, allowing the likelihood to be written as

$$
P(D \mid C_j)
=
\prod_{i=1}^{n}
P(d_i \mid C_j)
$$

The predicted class is the one with the **largest likelihood**.

This approach is known as **Maximum Likelihood Estimation (MLE).**

See:

- [[8. Bayes Classifier]]
- [[9. Naive Bayes]]



## Maximum Likelihood vs Maximum A Posteriori (MAP)

Maximum Likelihood assumes all classes are equally probable.

Maximum A Posteriori (MAP) additionally incorporates the prior probability of each class.

MLE chooses

$$
\arg\max P(D \mid C)
$$

whereas MAP chooses

$$
\arg\max P(D \mid C)P(C)
$$

When all priors are equal,

**MAP reduces to MLE.**

See:

- [[8. Bayes Classifier]]

---

> [!note]
> MLE is a special case of MAP when all classes have equal prior probabilities.

## Why is Naive Bayes Efficient?

The conditional independence assumption provides several advantages.

- Requires much less memory
- Fast training
- Fast prediction
- Scales well to many features
- Robust to many irrelevant features

Interestingly, irrelevant features usually contribute nearly equally to every class and therefore have little influence on the final prediction.

This explains why Naive Bayes often performs well despite its simplifying assumptions.

See:

- [[9. Naive Bayes]]

---

# 20. No Free Lunch Theorem

One of the most important principles in Machine Learning is the **No Free Lunch Theorem**.

It states that:

> No single learning algorithm performs best on every possible problem.

Every algorithm makes assumptions about the data.

Algorithms perform well only when those assumptions approximately match reality.

For example,

| Algorithm | Best suited for |
|------------|-----------------|
| Decision Trees | Interpretable rule-based problems |
| k-NN | Complex local decision boundaries |
| Naive Bayes | Independent features |
| Gaussian Models | Approximately Gaussian data |
| Neural Networks | Highly nonlinear relationships |

Choosing the correct algorithm is therefore an important part of Machine Learning.

---

> [!important]
> There is no universally "best" Machine Learning algorithm.

---

# 21. Comparing Learning Algorithms

Different algorithms create different decision boundaries.

For example,

**k-Nearest Neighbors**

- Flexible
- Complex boundaries
- Captures local structure
- Sensitive to noise

**Gaussian Classifiers**

- Smooth boundaries
- Strong probabilistic interpretation
- Better when data is approximately Gaussian

Neither method is always superior.

Performance depends on the underlying data distribution.

See:

- [[5. Gaussian Classification]]
- [[6. Decision Boundaries]]
- [[3. k-Nearest Neighbors]]

---

# 22. Mixture of Gaussians

Real-world data is often too complex to be represented by a single Gaussian.

Instead, each class can be modeled as a combination of multiple Gaussian distributions.

This approach is called a **Gaussian Mixture Model (GMM).**

Increasing the number of Gaussian components allows increasingly complex decision boundaries.

However,

too many components may lead to **overfitting**.

Choosing the appropriate number of components is commonly performed using **Cross Validation**.

See:

- [[Gaussian Mixture Models]]
- [[2. Cross Validation]]

---

# 23. Generalization

The ultimate objective of Machine Learning is **generalization**.

A model should perform well not only on the training data but also on previously unseen examples.

Poor generalization usually results from:

- Overfitting
- Insufficient training data
- Excessively complex models
- Poor feature selection

Simpler decision boundaries often generalize better when training data is limited.

---

> [!tip]
> A slightly simpler model that generalizes well is usually preferable to a highly complex model that memorizes the training data.

---

# 24. Visualizing Data

Before selecting a Machine Learning algorithm, it is often useful to visualize the data.

Visualization can reveal:

- Cluster structure
- Class overlap
- Outliers
- Noise
- Decision boundary complexity

These observations help determine which algorithms are likely to perform well.

For example,

- Compact clusters often suit Gaussian models.
- Irregular boundaries may favor k-NN.
- High-dimensional data may require Decision Trees, PCA, or feature selection.

See:

- [[7. Features]]
- [[6. Clustering]]

---

# 25. Decision Trees

Decision Trees classify data by asking a sequence of questions.

Each question partitions the dataset into smaller subsets until a prediction can be made.

Advantages include:

- Easy to understand
- Fast prediction
- Highly interpretable
- Handles both categorical and continuous features

Continuous attributes are handled by selecting appropriate threshold values.

See:

- [[1 - Classification]]

---

# 26. Simplicity and Minimum Description Length

When multiple decision trees classify the training data equally well, the simpler tree is generally preferred.

This idea is formalized by the **Minimum Description Length (MDL) Principle**.

The best hypothesis minimizes the total complexity required to describe:

- The model
- The remaining unexplained data

This preference for simpler models helps reduce overfitting.

---

> [!important]
> Simpler models often generalize better than unnecessarily complex ones.

---

# 27. Entropy

Decision Trees choose questions that provide the greatest reduction in uncertainty.

This uncertainty is measured using **Entropy**.

Entropy measures how mixed the class labels are.

Properties:

- Entropy = 0
  - All examples belong to one class.
- Maximum entropy
  - Classes are evenly mixed.

Higher entropy indicates greater uncertainty.

See:

- [[3.4.1 Entropy]]

---

# 28. Information Gain

Information Gain measures how much uncertainty is removed after splitting on an attribute.

The attribute with the **highest Information Gain** is selected first by algorithms such as **ID3**.

Good attributes:

- Create pure subsets
- Reduce entropy significantly
- Produce compact trees

Poor attributes:

- Leave class labels highly mixed
- Provide little useful information

See:

- [[1.1.2 Asking Questions: The ID3 Algorithm]]
- [[3.4.1 Entropy]]

