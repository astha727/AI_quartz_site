# Deep Learning

> [!insight]  
> Deep Learning extends traditional neural networks by stacking many hidden layers, allowing the network to automatically learn increasingly abstract representations of data. Modern breakthroughs in computer vision, speech recognition, natural language processing, and generative AI are all built upon this principle.

Related Notes: 
[[Lecture 7 - Machine Learning Part I]]
[[Lecture 7 - Machine Learning Part II]]
[[Lecture 7 - Machine Learning Part III]]

# 1. What is Deep Learning?

**Deep Learning** is a subset of Machine Learning that uses **deep (multi-layer) artificial neural networks** to automatically learn hierarchical representations from data.

Unlike traditional ML algorithms that often require manually engineered features, deep learning **learns useful features directly from raw data**.

## Why is it called "Deep"?

A neural network is considered **deep** when it contains multiple hidden layers.

```text
Input
   │
   ▼
Hidden Layer 1
   │
   ▼
Hidden Layer 2
   │
   ▼
Hidden Layer 3
   │
   ▼
...
   │
   ▼
Output
```

The term **depth** refers to the number of learnable layers between the input and the output.

## Traditional ML vs Deep Learning

|Traditional Machine Learning|Deep Learning|
|---|---|
|Manual feature engineering|Learns features automatically|
|Works well with smaller datasets|Excels with large datasets|
|Simpler models|Many hidden layers|
|Easier to interpret|Often behaves as a "black box"|
|Less computationally intensive|Requires powerful hardware (GPUs/TPUs)|

---

# 2. Hierarchical Representation Learning

One of the most important ideas in Deep Learning is **hierarchical feature learning**.

Each layer learns increasingly abstract representations of the data.

For example, in image recognition:

```text
Raw Image
    │
    ▼
Pixels
    │
    ▼
Edges
    │
    ▼
Corners
    │
    ▼
Shapes
    │
    ▼
Object Parts
    │
    ▼
Entire Object
```

The lecture emphasizes that each layer builds upon the representations learned by the previous layer.

## Example: Dog Image Classification

Consider a neural network trained to recognize dogs.

### Layer 1

Learns

- Pixel intensities
    
- Brightness
    
- Simple gradients
    

---

### Layer 2

Learns

- Horizontal edges
    
- Vertical edges
    
- Curves
    

---

### Layer 3

Combines edges into

- Eyes
    
- Nose
    
- Legs
    
- Tail
    

---

### Layer 4

Learns

- Fur texture
    
- Face shape
    
- Body structure
    

---

### Final Layer

Combines all learned features to predict

```
Dog
```

---

> [!example]  
> This hierarchical representation is why deep learning performs remarkably well on complex perception tasks such as image classification and speech recognition.

---

# 3. Learning from Experience

Deep neural networks improve by continuously adjusting the strengths of the connections (weights) between neurons.

During training:

1. Input data is passed through the network.
    
2. Predictions are made.
    
3. Error is calculated.
    
4. Backpropagation adjusts the weights.
    
5. The network gradually improves.
    

This process is repeated over many epochs.

## Representation Learning

Unlike classical algorithms, deep networks discover useful features automatically.

For example,

Instead of manually programming

- edges
    
- textures
    
- corners
    

the network learns these representations directly from data.

> [!tip]  
> Feature engineering becomes **feature learning**.

This is one of the biggest paradigm shifts introduced by Deep Learning.

---

# 4. Why Did Deep Learning Become Successful?

Neural networks were proposed in the 1950s.

However, they only became practical during the last decade because of three major developments.

## ① Large Datasets

Deep networks require enormous amounts of labeled data.

Examples include

- ImageNet
    
- Common Crawl
    
- Wikipedia
    
- LAION
    

Large datasets allow millions or billions of parameters to be trained effectively.

## ② Faster Hardware

Modern GPUs perform thousands of matrix operations simultaneously.

This dramatically reduces training time.

Examples include

- NVIDIA GPUs
    
- Google TPUs
    
- AMD Accelerators
    

Without specialized hardware, training deep models would take months or years.

## ③ Improved Algorithms

Several algorithmic improvements made deep networks train reliably.

Examples include

- Backpropagation
    
- Better initialization
    
- ReLU activation
    
- Batch Normalization
    
- Adam Optimizer
    

---

# 5. Advantages of Deep Learning

Deep Learning excels when dealing with highly complex, high-dimensional data.

Advantages include:

- Automatic feature extraction
    
- Excellent predictive performance
    
- Handles unstructured data
    
- Learns complex nonlinear relationships
    
- Scales with larger datasets
    

Applications include

- Computer Vision
    
- Speech Recognition
    
- Machine Translation
    
- Medical Imaging
    
- Robotics
    
- Autonomous Driving
    
- Generative AI
    

# 6. Limitations of Deep Learning

Despite its success, Deep Learning has several drawbacks.

## High Computational Cost

Training requires

- GPUs
    
- Large memory
    
- Significant electricity
    

Some large models require weeks of training.

## Large Data Requirements

Deep models generally require much more data than traditional ML algorithms.

Small datasets often lead to overfitting.

## Poor Interpretability

Decision Trees produce explicit rules.

Neural Networks distribute knowledge across millions of weights.

As a result,

it is often difficult to explain **why** a prediction was made.

---

> [!warning]  
> Neural Networks are frequently described as **black-box models**.

Understanding their internal reasoning remains an active area of research called **Explainable AI (XAI)**.

## Hyperparameter Sensitivity

Performance depends heavily on choices such as

- Learning rate
    
- Network depth
    
- Number of neurons
    
- Batch size
    
- Activation function
    
- Optimizer
    

Poor choices may prevent convergence.

---

# 7. Explainability vs Performance

The lecture highlights an important trade-off.

|Decision Trees|Deep Neural Networks|
|---|---|
|Easy to understand|Difficult to interpret|
|Explicit decision rules|Distributed representations|
|Lower accuracy on complex tasks|State-of-the-art accuracy|
|Human-readable|Black-box behavior|


> [!important]  
> For many real-world applications, practitioners prioritize **prediction accuracy** over interpretability.

However, in fields such as healthcare or finance, explainability may be legally or ethically required.

---

# 8. Deep Learning in Practice

Modern Deep Learning systems have transformed AI.

Examples include

### Computer Vision

- Image Classification
    
- Face Recognition
    
- Object Detection
    
- Medical Diagnosis
    

---

### Natural Language Processing

- ChatGPT
    
- Machine Translation
    
- Text Summarization
    
- Question Answering
    

---

### Speech

- Speech Recognition
    
- Voice Assistants
    
- Speaker Identification
    

---

### Robotics

- Self-driving cars
    
- Industrial automation
    
- Drone navigation
    

---

### Scientific Discovery

- Protein folding
    
- Drug discovery
    
- Climate modeling
    

---

# 9. Human Brain vs Artificial Neural Networks

Deep Learning is inspired by biology but is **not** an accurate simulation of the human brain.

|Human Brain|Artificial Neural Network|
|---|---|
|~86 billion neurons|Thousands to billions of artificial neurons|
|Electrochemical signaling|Numerical computation|
|Highly energy efficient (~20W)|Requires powerful hardware|
|Learns continuously|Usually trained offline|


> [!note]  
> Artificial Neural Networks are **biologically inspired**, not biologically identical.

---

# 10. Modern Deep Learning Architectures

Today's AI systems use specialized neural network architectures.

Examples include

- Feedforward Neural Networks
    
- [[2.6 Convolutional Neural Networks]]
    
- [[2.7 Recurrent Neural Networks]]
    
- [[2.8 Transformers]]
    
- [[2.9 Autoencoders]]
    
- [[2.10 Graph Neural Networks]]
    

Each architecture is designed for a different class of problems.

---

# 11. Future Directions

The lecture suggests that increasingly deep networks can discover meaningful hierarchical structures with minimal supervision.

Modern research is moving toward

- Self-Supervised Learning
    
- Foundation Models
    
- Multimodal AI
    
- Reinforcement Learning from Human Feedback (RLHF)
    
- Explainable AI
    
- Efficient Deep Learning
    

These advances are enabling models to generalize across multiple tasks and domains.

---

# Summary

|Concept|Key Idea|
|---|---|
|**Deep Learning**|Uses many hidden layers to learn hierarchical representations|
|**Representation Learning**|Automatically discovers useful features from raw data|
|**Hierarchical Features**|Lower layers learn simple patterns; higher layers learn abstract concepts|
|**Advantages**|High accuracy, automatic feature learning, scalable|
|**Limitations**|Requires large datasets, computation, and is difficult to interpret|
|**Modern Applications**|Vision, NLP, speech, robotics, healthcare, generative AI|
|**Explainability**|Deep models are powerful but often behave as black boxes|


## Related Notes

- [[2.2 Neural Networks]]
    
- [[2.3 Gradient Descent]]
    
- [[2.4 Backpropagation]]
    
- [[2.5 Deep Learning]]
    
- [[2.6 Convolutional Neural Networks]]
    
- [[2.7 Recurrent Neural Networks]]
    
- [[2.8 Transformers]]
    
- [[6.1 Explainable AI]]
    
- [[1.2 Ensemble Learning]]