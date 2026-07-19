
> [!summary]
> **Deep Learning (DL)** is a subset of **Machine Learning (ML)** that uses **artificial neural networks with multiple hidden layers** to automatically learn hierarchical representations from data.
>
> Unlike traditional machine learning, deep learning learns both the **features** and the **decision function** directly from raw data.

## Relationship to Artificial Intelligence

```text
Artificial Intelligence (AI)
│
├── Symbolic AI
│
└── Machine Learning (ML)
      │
      ├── Supervised Learning
      ├── Unsupervised Learning
      ├── Reinforcement Learning
      │
      └── Deep Learning (DL)
             │
             ├── Neural Networks
             ├── CNNs
             ├── RNNs
             ├── Transformers
             └── Large Language Models
```

## Evolution of Machine Learning

```text
Traditional Programming

Rules + Data
        │
        ▼
     Output


         ↓

    Machine Learning

    Data + Labels
        │
        ▼
      Model

     New Data
        │
        ▼
     Prediction


         ↓

     Deep Learning

    Raw Data
      │
      ▼
Neural Network

Automatically learns

• Features
• Representations
• Decision Function

      ↓

Prediction
```

## Key Idea

Traditional machine learning usually requires humans to decide **what information (features) is important**.

Deep learning removes much of this manual work by allowing neural networks to automatically discover useful patterns directly from raw data.

## Characteristics

- Uses artificial neural networks.
- Contains multiple hidden layers.
- Learns hierarchical representations.
- Trained using gradient descent and backpropagation.
- Scales well with large datasets and compute.

## Why is it called "Deep"?

The word **deep** refers to the **number of hidden layers** inside a neural network.

```text
Input

↓

Hidden Layer

↓

Output

= Shallow Network


Input

↓

Hidden Layer

↓

Hidden Layer

↓

Hidden Layer

↓

Output

= Deep Network
```


## Deep Learning vs Traditional Machine Learning

| Traditional ML | Deep Learning |
|----------------|---------------|
| Handcrafted features | Learns features automatically |
| Smaller models | Very large neural networks |
| Works with limited data | Benefits from massive datasets |
| Easier to interpret | Often behaves like a black box |
| Less computationally expensive | Requires GPUs/TPUs |

## Examples

| Task | Deep Learning Model |
|------|----------------------|
| Image Classification | CNN |
| Speech Recognition | Transformer |
| Machine Translation | Transformer |
| Object Detection | CNN |
| Text Generation | Large Language Model |
| Recommendation Systems | Deep Neural Network |
# Why Deep Learning

> [!summary]
> Deep learning became the dominant paradigm in Artificial Intelligence because it can automatically learn complex representations from raw data and continues to improve as datasets and computational power increase.


## Why was Deep Learning Needed?

Traditional machine learning performs well on many structured problems but struggles with highly complex tasks such as:

- Computer Vision
- Speech Recognition
- Natural Language Processing
- Autonomous Driving
- Protein Structure Prediction

These tasks involve enormous amounts of high-dimensional data that are difficult to model using handcrafted rules or manually engineered features.

## Why Deep Learning Works

### 1. Representation Learning

Unlike traditional machine learning, deep learning automatically learns useful representations directly from raw data.

Instead of designing features manually,

```text
Raw Data

↓

Neural Network

↓

Learned Features

↓

Prediction
```

This dramatically reduces the need for feature engineering.

→ [[Representation Learning]]

---

### 2. Universal Approximation

According to the **Universal Approximation Theorem**, even a neural network with a single hidden layer can approximate any continuous function given enough neurons.

This provides the theoretical foundation explaining why neural networks can model extremely complex relationships.

→ [[Universal Approximation Theorem]]

---

### 3. Hierarchical Learning

Deep neural networks build increasingly abstract representations.

```text
Image

↓

Edges

↓

Corners

↓

Shapes

↓

Object Parts

↓

Objects
```

Each layer learns features from the previous layer.

---

### 4. Scalability

Many traditional machine learning algorithms eventually plateau as dataset size increases.

Deep learning typically continues improving with:

- More data
- More parameters
- Larger models
- Better hardware (GPUs)

This scaling behavior is one of its greatest strengths.

---

### 5. Groundbreaking Performance

Deep learning has produced major breakthroughs across AI.

Examples include:

- ImageNet image recognition
- Speech recognition
- Machine translation
- AlphaGo
- ChatGPT and Large Language Models

Many of these achievements dramatically outperformed previous machine learning methods.

## Why Traditional Machine Learning Was Not Enough

Deep learning emerged because classical machine learning suffers from several important limitations.

```text
Traditional ML

↓

Requires Feature Engineering

↓

Limited Model Capacity

↓

Poor Performance on Raw High-Dimensional Data

↓

Deep Learning
```

## Key Takeaway

> Deep learning succeeds because it automatically learns rich hierarchical representations that traditional machine learning requires humans to design manually.