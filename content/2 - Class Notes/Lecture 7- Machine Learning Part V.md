# 14. Unsupervised Learning

Unlike supervised learning, **unsupervised learning** receives **unlabeled data**.

The algorithm attempts to discover hidden structure, patterns, or clusters within the data without knowing the correct answers beforehand.

> [!insight]
> **Goal:** Discover the natural organization of data without class labels.

Related Notes: 
[[Lecture 7 - Machine Learning Part I]]
[[Lecture 7 - Machine Learning Part II]]
[[Lecture 7 - Machine Learning Part III]]
[[Lecture 7 - Machine Learning Part IV]]

## Characteristics

Input:

- Data only
- No labels
- No target outputs

Output:

- Clusters
- Hidden structure
- Latent patterns
- Relationships among observations

## Why is Unsupervised Learning Useful?

Many real-world datasets are enormous and difficult to label manually.

Examples include:

- Images
- Audio recordings
- Sensor measurements
- Customer behavior
- Animal vocalizations
- GPS trajectories

Instead of labeling millions of samples, we allow the algorithm to discover structure automatically.

## Applications

- Customer segmentation
- Image organization
- Speech discovery
- Sign language recognition
- Human activity recognition
- Document clustering
- Recommendation systems
- Bioinformatics

## Challenges

Unlike supervised learning,

there is **no ground truth** during training.

Evaluating performance is therefore much harder.

---

See:

- [[4.4 Clustering]]
- [[4.5 Unsupervised Learning]]

---

# 15. K-Means Clustering

K-Means is one of the simplest and most widely used clustering algorithms.

The number of clusters, **K**, is specified before training.

The algorithm then groups observations into **K clusters**.

## Objective

Partition the data into clusters such that observations inside a cluster are as similar as possible.

## Algorithm

### Step 1

Randomly initialize **K centroids**.

---

### Step 2 — Expectation (Assignment)

Assign every data point to its nearest centroid.

---

### Step 3 — Maximization (Update)

Recompute each centroid as the average of all assigned points.

The centroid becomes

$$
\mu_k
=
\frac{1}{|C_k|}
\sum_{x_i\in C_k}x_i
$$

where

- $C_k$ = cluster $k$
- $\mu_k$ = updated centroid

---

### Step 4

Repeat Assignment → Update until convergence.

---

> [!tip]
> K-Means alternates between assigning data points to clusters (**Expectation**) and updating cluster centers (**Maximization**).


## Objective Function

K-Means minimizes the total within-cluster squared error.

$$
J
=
\sum_{k=1}^{K}
\sum_{x_i\in C_k}
\|x_i-\mu_k\|^2
$$

where

- $\mu_k$ = cluster centroid
- $x_i$ = observation

Lower values indicate tighter clusters.

## Convergence

The algorithm stops when:

- Cluster assignments stop changing.
- Centroids stop moving.
- Maximum iterations are reached.


## Complexity

Each iteration requires assigning every point to every centroid.

Time complexity:

$$
O(nkd)
$$

where

- $n$ = number of samples
- $k$ = number of clusters
- $d$ = number of features


## Advantages

- Simple
- Fast
- Scalable
- Easy to implement


## Limitations

- Must choose **K** beforehand.
- Sensitive to initialization.
- Assumes approximately spherical clusters.
- Sensitive to outliers.

## Random Restart

Because initialization is random,

K-Means may converge to a poor local optimum.

A common strategy is **Random Restart**:

1. Run K-Means multiple times.
2. Use different random initial centroids.
3. Select the clustering with the lowest objective value.

> [!important]
> Random Restart greatly improves stability and is standard practice in K-Means.

## Good Clustering

A desirable clustering has:

- High **inter-cluster variance**
- Low **intra-cluster variance**

Meaning:

- Different clusters are well separated.
- Points inside each cluster are similar.

See:

- [[4.4 Clustering]]

---

# 16. Expectation Maximization (EM)

Expectation Maximization (EM) is a general optimization algorithm for models containing hidden (latent) variables.

K-Means is actually a simplified form of EM.


## Core Idea

EM alternates between two steps:

### Expectation Step (E-Step)

Estimate hidden variables using the current model parameters.

---

### Maximization Step (M-Step)

Update the model parameters using the estimated hidden variables.


Repeat until convergence.


## Generic EM Algorithm

Initialize parameters

↓

Expectation

↓

Maximization

↓

Repeat

↓

Converged


## Why EM Works

Each iteration improves (or leaves unchanged) the data likelihood.

Eventually,

the algorithm converges to a **local optimum**.

## EM Characteristics

Advantages

- Works with hidden variables.
- Flexible framework.
- Applicable to many probabilistic models.

Limitations

- Can converge to local optima.
- Sensitive to initialization.
- Often slower than K-Means.

See:

- [[4.6 Expectation Maximization (EM)]]

---

# 17. EM for Gaussian Mixture Models (GMMs)

EM is commonly used to estimate the parameters of a **Gaussian Mixture Model (GMM)**.

Instead of assigning every point to exactly one cluster,

each point receives a **probabilistic membership** in every Gaussian.

## Gaussian Mixture Model

The probability density is

$$
P(x)
=
\sum_{k=1}^{K}
\pi_k
\,
\mathcal{N}(x\mid\mu_k,\Sigma_k)
$$

where

- $\pi_k$ = mixture weight
- $\mu_k$ = mean
- $\Sigma_k$ = covariance matrix


## E-Step

Compute the probability (responsibility) that Gaussian $k$ generated point $x_i$.

$$
\gamma(z_{ik})
=
P(z_i=k\mid x_i)
$$

These are called **responsibilities**.

## M-Step

Update

- Means
- Covariance matrices
- Mixture weights

using the responsibilities computed in the E-Step.

Unlike K-Means,

clusters are **soft assignments** rather than hard assignments.

Each point can belong partially to multiple clusters.


## K-Means vs GMM

| Property | K-Means | Gaussian Mixture Model |
|-----------|----------|------------------------|
| Assignment | Hard | Soft |
| Cluster Shape | Spherical | Elliptical |
| Covariance | Ignored | Estimated |
| Probability Output | No | Yes |
| Optimization | Distance | Likelihood |


## Why GMM is More Flexible

K-Means assumes every cluster has:

- Equal size
- Equal variance
- Circular shape

GMM allows:

- Different sizes
- Different orientations
- Different covariance structures

making it significantly more expressive.

## Computational Cost

Because GMM estimates additional parameters,

training is more computationally expensive than K-Means.

More dimensions and more Gaussians require:

- More data
- More iterations
- More computation

> [!note]
> In practice, K-Means often converges in only a few iterations, whereas EM for Gaussian Mixture Models may require many more because it must estimate both cluster centers and covariance matrices.


See:

- [[4.6 Expectation Maximization (EM)]]
- [[5.2 Gaussian Mixture Models]]

---

# Summary

| Concept | Key Idea |
|----------|----------|
| ==Unsupervised Learning== | Learn hidden structure without labels |
| ==K-Means== | Partition data into K clusters using nearest centroids |
| ==Expectation Step== | Assign data to clusters using current parameters |
| ==Maximization Step== | Update parameters from assigned data |
| ==Objective Function== | Minimize within-cluster squared distance |
| ==Random Restart== | Improve clustering by using multiple initializations |
| ==Expectation Maximization== | Alternate between estimating hidden variables and updating parameters |
| ==Gaussian Mixture Models== | Probabilistic clustering using multiple Gaussians |
| ==Soft Clustering== | Points belong to clusters with probabilities |
| ==Hard Clustering== | Points belong to exactly one cluster |