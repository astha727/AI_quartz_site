# Data Types & Data Processing

---

# 1. Structured Data

> [!definition]
> **Structured Data** is data that is organized according to a predefined schema, making it easy to store, retrieve, and analyze.

### Characteristics
- Organized into **rows** (records) and **columns** (features/attributes)
- Stored in databases or spreadsheets
- Easy to query using SQL
- Highly organized

### Examples
- Excel spreadsheets
- SQL databases
- Customer records
- Employee information

| Advantages | Disadvantages |
|------------|---------------|
| Easy to search | Less flexible |
| Fast querying | Fixed schema required |
| Efficient storage | Difficult to store complex objects |

---

# 2. Unstructured Data

> [!definition]
> **Unstructured Data** has no predefined format or schema.

### Characteristics
- Cannot be organized neatly into tables
- Requires preprocessing before analysis
- Usually much larger than structured data

### Examples
- Text documents
- Emails
- PDFs
- Images
- Videos
- Audio recordings
- Social media posts
- Sensor data

### Processing Methods
- Natural Language Processing (NLP)
- Computer Vision
- Speech Recognition

---

# 3. Quantitative Data

> [!definition]
> **Quantitative Data** consists of numerical values representing measurable quantities.

### Examples
- Height
- Weight
- Age
- Temperature
- Salary
- Sales revenue

## Types

### Discrete Data
Countable values.

Examples:
- Number of students
- Number of cars
- Number of emails

### Continuous Data
Measured on a continuous scale.

Examples:
- Height
- Weight
- Time
- Distance
- Temperature

---

# 4. Categorical Data

> [!definition]
> **Categorical Data** consists of labels or categories rather than numerical measurements.

### Examples
- Gender
- Country
- Eye color
- Blood type

## Types

### Nominal Data

No inherent ordering.

Examples:
- Country
- Color
- Brand

### Ordinal Data

Categories have a meaningful order.

Examples:
- Education level
- Customer satisfaction
- Movie ratings

Example:

Poor < Fair < Good < Excellent

---

# 5. Binary Data

> [!definition]
> **Binary Data** is a special case of categorical data with only two possible values.

### Examples
- Yes / No
- True / False
- Pass / Fail
- Success / Failure
- Spam / Not Spam

---

# 6. Unrelated Data

> [!definition]
> **Unrelated Data** consists of independent observations with no relationship between them.

### Characteristics
- One observation does not affect another.
- Independent samples.

### Example

Player statistics from different sports teams.

Each player's information is unrelated to players from other teams.

---

# 7. Time Series Data

> [!definition]
> **Time Series Data** consists of observations collected over time in chronological order.

### Characteristics
- Ordered by time
- Captures trends and seasonality
- Used for forecasting

### Examples
- Stock prices
- Daily temperatures
- Website traffic
- Electricity usage
- Monthly sales

---

# 8. Scaling Data

> [!definition]
> **Scaling** transforms numerical features into a comparable range.

## Why Scale?

Without scaling:

- Age: 18–90
- Salary: \$30,000–\$200,000

Salary dominates most machine learning algorithms.

Scaling places features on similar ranges.

## Common Techniques

### Min-Max Scaling

Transforms values to a fixed range (usually 0–1).

Formula:

\[
x'=\frac{x-\min(x)}{\max(x)-\min(x)}
\]

Advantages
- Preserves original distribution
- Keeps values between 0 and 1

---

### Z-Score Scaling (Standardization)

Transforms data so that:

- Mean = 0
- Standard deviation = 1

Formula:

\[
z=\frac{x-\mu}{\sigma}
\]

Advantages
- Handles different units
- Widely used in ML algorithms

---

# 9. Standardizing Data

> [!definition]
> **Standardization** is a specific scaling technique that converts data to have:
>
> - Mean = 0
> - Standard deviation = 1

### Why Standardize?

Allows fair comparison between variables measured in different units.

### Common Uses

- Logistic Regression
- Linear Regression
- Support Vector Machines
- Principal Component Analysis (PCA)
- Neural Networks

---

# Scaling vs Standardization

| Scaling | Standardization |
|----------|-----------------|
| General concept | Specific technique |
| Often 0–1 range | Mean = 0, SD = 1 |
| Uses Min-Max Scaling | Uses Z-score |
| Preserves relative spacing | Centers data around zero |

---

# 10. Validation

> [!definition]
> **Validation** is the process of evaluating how well a machine learning model performs on unseen data.

## Purpose

- Estimate real-world performance
- Detect overfitting
- Compare models
- Improve generalization

---

## Common Validation Techniques

### Train-Test Split

Split dataset into:

- Training Set
- Testing Set

Example:

- 80% Training
- 20% Testing

---

### Cross-Validation

Repeatedly splits data into different training/testing subsets.

Most common:

- k-Fold Cross Validation

Advantages:
- Better performance estimate
- Uses all available data

---

## Evaluation Metrics

Common validation metrics include:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC
- Mean Squared Error (Regression)

---

# Summary Table

| Data Type | Description | Examples |
|-----------|-------------|----------|
| Structured | Organized into rows and columns | SQL database, Excel |
| Unstructured | No predefined format | Images, text, video |
| Quantitative | Numerical measurements | Height, salary |
| Categorical | Labels or groups | Gender, country |
| Binary | Two possible values | Yes/No |
| Unrelated | Independent observations | Players from different teams |
| Time Series | Data collected over time | Stock prices |
| Scaling | Rescales values to similar range | Min-Max Scaling |
| Standardization | Mean = 0, SD = 1 | Z-score |
| Validation | Evaluates model performance | Train-test split, Cross-validation |

---

> [!tip] Quick Revision
>
> - **Structured** → Tables & databases
> - **Unstructured** → Text, images, videos
> - **Quantitative** → Numbers
> - **Categorical** → Labels
> - **Binary** → Two classes
> - **Time Series** → Ordered by time
> - **Scaling** → Rescale values
> - **Standardization** → Mean = 0, SD = 1
> - **Validation** → Test model on unseen data