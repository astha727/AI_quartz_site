# Perceptrons & Backpropagation

> [!insight]  
> This section introduces the **Perceptron**, the simplest artificial neural network capable of learning linear decision boundaries. It then extends the idea to **Multilayer Perceptrons (MLPs)** and the **Backpropagation algorithm**, which made training deep neural networks practical. These concepts form the mathematical foundation of modern Deep Learning.

Related Notes: 
[[Lecture 7 - Machine Learning Part I]]
[[Lecture 7 - Machine Learning Part II]]

---

# 1. Perceptron Learning

The **Perceptron** is one of the earliest learning algorithms for neural networks.

It consists of:

- Input features
    
- Learnable weights
    
- A bias
    
- An activation function
    
- An output neuron
    

Unlike previous examples, the **input layer is not counted** as part of the neural network because it performs no computation.

## Single Layer Perceptron

```text
      x₁ ── w₁ ─┐
                │
      x₂ ── w₂ ─┤
                │
      x₃ ── w₃ ─┤── Σ ──> g(.) ──> Output
                │
      ...       │
                │
      xₙ ── wₙ ─┘

            + Bias
```

The neuron computes a weighted sum of its inputs followed by an activation function.

## Mathematical Model

The weighted input is

$$  
z=\sum_{i=1}^{n}w_i x_i+b  
$$

The output activation is

$$  
a=g(z)  
$$

where

- $x_i$ = input feature
    
- $w_i$ = weight
    
- $b$ = bias
    
- $g(\cdot)$ = activation function
    

## Activation Function

The lecture assumes a **sigmoid activation function**.

$$  
g(z)=\frac{1}{1+e^{-z}}  
$$

Properties

- Output between 0 and 1
    
- Smooth and differentiable
    
- Suitable for gradient-based optimization
    

---

> [!note]  
> Earlier neural networks often used **step functions**, while modern deep learning primarily uses **ReLU**, **GELU**, or related activations because they train faster.

---

# 2. Learning from Data

The goal is to adjust the weights so that the network's predictions become increasingly accurate.

Learning follows four steps:

1. Compute prediction
    
2. Measure error
    
3. Compute gradient
    
4. Update weights
    

This process repeats until convergence.

## Error Function

The lecture uses **Squared Error Loss**.

For one training example:

$$  
E=  
\left(  
y-h_w(x)  
\right)^2  
$$

where

- $y$ = desired output
    
- $h_w(x)$ = neural network prediction
    

---

For an entire dataset

$$  
J(w)=  
\sum_{i=1}^{m}  
\left(  
y^{(i)}-  
h_w(x^{(i)})  
\right)^2  
$$

This is called the **cost function**.

## Why Squared Error?

Squaring ensures

- Positive errors remain positive
    
- Larger errors receive larger penalties
    
- The function is differentiable
    

making optimization easier.

---

# 3. Gradient Descent

The objective is to minimize the cost function.

Rather than searching randomly, Gradient Descent moves in the direction of **steepest decrease**.

## Weight Update Rule

For each weight

$$  
w_i  
\leftarrow  
w_i

\alpha  
\frac{\partial J}{\partial w_i}  
$$

where

- $\alpha$ = learning rate
    
- $\frac{\partial J}{\partial w_i}$ = gradient
    

## Learning Rate

The learning rate determines how quickly weights change.

Small α

- Stable
    
- Slow convergence
    

Large α

- Faster learning
    
- May overshoot the minimum
    
- Can diverge completely
    

---

> [!important]  
> Choosing an appropriate learning rate is one of the most important hyperparameter tuning tasks in Machine Learning.


---

# 4. Why Update Slowly?

Suppose we train an OCR system to recognize

- H
    
- I
    
- T
    

If we completely optimize weights for only one letter, we may damage performance on previously learned letters.

Instead, each training example contributes **small updates**.

Eventually the weights converge to values that work well across the entire dataset. This is an example of **iterative optimization**.

---

# 5. Epochs

One complete pass through the training dataset is called an **Epoch**.

Training typically consists of many epochs.

```text
Training Data

↓

Epoch 1

↓

Epoch 2

↓

Epoch 3

↓

...

↓

Converged Weights
```

During each epoch

- Predictions improve
    
- Error decreases
    
- Gradients become smaller
    
- Weights stabilize
    

---

# 6. Expressiveness of a Perceptron

A single-layer perceptron is limited.

It can only learn **linear decision boundaries**.

For example

```text
Positive      Negative

+++++++|-------

```


## Problems It Can Solve

- AND
    
- OR
    
- Majority Function
    
- Threshold Functions
    

## Problems It Cannot Solve

The classic example is **XOR**.

```text
+     -

   X

-     +
```

No straight line separates the two classes.

Therefore

> A single-layer perceptron cannot represent XOR.

## Why?

A perceptron computes

$$  
w^Tx+b  
$$

which is a linear function.

Linear functions can only produce linear boundaries.

> [!warning]  
> This limitation became known as the **XOR problem**, one of the major reasons neural network research slowed during the 1970s until multilayer networks and backpropagation were rediscovered.

---

# 7. Multilayer Perceptrons (MLPs)

Adding hidden layers dramatically increases the expressive power of neural networks.

```text
Input

↓

Hidden Layer

↓

Hidden Layer

↓

Output
```

Each hidden neuron creates its own nonlinear transformation.

These transformations combine to create highly complex decision boundaries.

## Universal Approximation

One hidden layer allows neural networks to approximate **any continuous function** given sufficient neurons.

Two hidden layers allow approximation of even more complex functions efficiently.

> [!tip]  
> Hidden neurons do not directly correspond to human-defined features.
> 
> They automatically learn intermediate representations useful for solving the task.

See:

- [[2.2 Neural Networks]]
    

# 8. Why Hidden Layers Help

The lecture explains this intuitively.

A single neuron creates a "cliff-like" decision surface.

Combining multiple neurons creates

- Ridges
    
- Valleys
    
- Peaks
    

Eventually these combine into arbitrarily complex nonlinear functions.

This is closely related to

- Kernel Methods
    
- Gaussian Mixture Models
    
- Radial Basis Functions
    

All are methods for approximating complex decision boundaries.

---

# 9. Backpropagation

Training multilayer networks requires propagating error backwards through the network.

This algorithm is called **Backpropagation**.

## High-Level Algorithm

### Step 1

Forward Pass

Compute predictions.

---

### Step 2

Compute Output Error

Compare prediction with true label.

---

### Step 3

Backpropagate Error

Distribute responsibility for the error backward through hidden layers.

---

### Step 4

Update Weights

Adjust every weight using Gradient Descent.


Repeat until convergence.

---

# 10. Output Error

Output neurons compute

$$  
\delta_i

(y_i-a_i)  
g'(z_i)  
$$

where

- $a_i$ = prediction
    
- $y_i$ = target
    
- $g'$ = derivative of activation function
    

---

# 11. Hidden Layer Error

Hidden neurons do not have target labels.

Instead, their error depends on how much they contributed to downstream errors.

The lecture gives

$$  
\delta_j

g'(z_j)  
\sum_i  
w_{ji}  
\delta_i  
$$

This is the essence of **Backpropagation**.

---

# 12. Weight Update Rule

Once hidden errors are known, weights update exactly like Gradient Descent.

$$  
w_{kj}  
\leftarrow  
w_{kj}  
+  
\alpha  
a_k  
\delta_j  
$$

where

- $a_k$ = activation from previous layer
    
- $\delta_j$ = propagated error
    
- $\alpha$ = learning rate
    

## Complete Training Cycle

```text
Input

↓

Forward Pass

↓

Prediction

↓

Loss

↓

Backpropagation

↓

Gradient Computation

↓

Weight Update

↓

Next Epoch
```

---

# 13. Comparing Decision Trees and Neural Networks

|Decision Trees|Neural Networks|
|---|---|
|Learn quickly|Require many epochs|
|Highly interpretable|Difficult to interpret|
|Good with small datasets|Excel with large datasets|
|Explicit rules|Distributed representations|
|Fast training|Computationally expensive|

---

> [!important]  
> Decision Trees often outperform neural networks on **small datasets**, while neural networks generally improve as more data becomes available.

---

# Exam Takeaways

> [!success]  
> Remember these key ideas:
> 
> - Perceptrons learn **linear decision boundaries**.
>     
> - Single-layer perceptrons cannot solve XOR.
>     
> - Hidden layers dramatically increase expressive power.
>     
> - Backpropagation propagates error from outputs to hidden layers.
>     
> - Gradient Descent updates weights iteratively.
>     
> - One complete pass through the dataset is called an **Epoch**.
>     
> - Multilayer Perceptrons are the foundation of modern Deep Learning.
>     


## Related Notes

- [[2.2 Neural Networks]]
    
- [[2.3 Gradient Descent]]
    
- [[2.4 Backpropagation]]
    
- [[2.5 Deep Learning]]
    
- [[1.2 Ensemble Learning]]
    
- [[4.2 Bayesian Inference]]