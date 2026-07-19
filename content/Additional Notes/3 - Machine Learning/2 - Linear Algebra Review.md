## Introduction

Linear algebra is the branch of mathematics that studies **vectors**, **vector spaces**, **matrices**, and **linear transformations**. It provides the mathematical foundation for many fields including:

- Machine Learning
- Artificial Intelligence
- Computer Vision
- Robotics
- Data Science
- Physics
- Computer Graphics
- Engineering

Almost every modern machine learning algorithm relies heavily on linear algebra because datasets, images, text embeddings, and neural network weights are all represented using **vectors** and **matrices**.

> [!note] Why Learn Linear Algebra for Machine Learning?
>
> Linear algebra allows us to:
>
> - Represent datasets as matrices
> - Represent features as vectors
> - Perform efficient computations
> - Solve systems of equations
> - Train neural networks using matrix operations
> - Understand algorithms like PCA, Linear Regression, SVMs, Transformers, etc.

---

### Mathematical Definition

Let

$$
n\in\mathbb N
$$

be a positive integer and let

$$
\mathbb R
$$

denote the set of **real numbers**.

Then,

$$
\mathbb R^n
$$

represents the set of all ordered **n-tuples** of real numbers.

A vector

$$
\mathbf v\in\mathbb R^n
$$

is an ordered collection (tuple) of **n real numbers**.

The notation

$$
\in
$$

is read as

> "belongs to" or "is an element of."

For example,

$$
\mathbf v=(v_1,v_2,v_3)\in\mathbb R^3
$$

means the vector has three components.

Example:

$$
\mathbf v=(2,-1,5)
$$

---

### Matrices

A matrix is a **rectangular arrangement of numbers**.

If a matrix has

- **m rows**
- **n columns**

then it belongs to

$$
\mathbb R^{m\times n}
$$

A matrix

$$
A\in\mathbb R^{m\times n}
$$

looks like

$$
\color{cyan}
A=
\begin{bmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
a_{21}&a_{22}&\cdots&a_{2n}\\
\vdots&\vdots&\ddots&\vdots\\
a_{m1}&a_{m2}&\cdots&a_{mn}
\end{bmatrix}
$$

Example (3 × 2 Matrix)

$$\color{cyan}
A=
\begin{bmatrix}
1&2\\
3&4\\
5&6
\end{bmatrix}
$$

This matrix has

- 3 rows
- 2 columns

---

> [!info]
>
> Linear algebra is essentially the mathematics of **vectors** and **matrices**.
>
> Everything from solving equations to training deep neural networks depends on these two concepts.

---

## Prerequisites

Before studying linear algebra, you should be comfortable with the following mathematical concepts.

### 1. Real Numbers

You should understand:

- Positive numbers
- Negative numbers
- Fractions
- Decimals
- Irrational numbers

Examples

$$
3,\;
-5,\;
\frac12,\;
\sqrt2,\;
\pi
$$

All belong to

$$
\mathbb R
$$

---

### 2. Variables

Variables represent unknown quantities.

Example

$$
x+5=10
$$

Here,

$$
x=5
$$

---

### 3. Arithmetic Operations

You should know

- Addition
- Subtraction
- Multiplication
- Division

Examples

$$
3+2=5
$$

$$
5-1=4
$$

$$
3\times4=12
$$

$$
12\div3=4
$$

---

### 4. Functions

A function maps one value to another.

Mathematically,

$$
f:\mathbb R\rightarrow\mathbb R
$$

means

> the function accepts a real number and returns another real number.

Example

$$
f(x)=x^2
$$

Input

$$
4
$$

Output

$$
16
$$

---

### 5. Inverse Functions

An inverse function reverses the action of another function.

If

$$
f(x)=\ln(x)
$$

then

$$
f^{-1}(x)=e^x
$$

because

$$
f^{-1}(f(x))=x
$$

Another example

If

$$
g(x)=\sqrt x
$$

then

$$
g^{-1}(x)=x^2
$$

---

> [!note]
>
> Throughout linear algebra, functions are often represented using matrices.
> Understanding functions first makes linear transformations much easier to understand later.


## Scalars vs Vectors

One of the most fundamental ideas in linear algebra is understanding the difference between **scalars** and **vectors**.

### Scalars

A **scalar** is a quantity that has **magnitude only**.

It does **not** have a direction.

Examples include

- Length
- Mass
- Time
- Area
- Volume
- Speed
- Temperature
- Money
- Voltage
- Density

Example

A person's height is

> 1.75 m

Only one numerical value is needed.

Therefore,

**Height is a scalar.**

---

### Vectors

A **vector** is a quantity that has

- Magnitude
- Direction

Both pieces of information are necessary.

Examples include

- Displacement
- Velocity
- Acceleration
- Force
- Momentum
- Weight
- Electric field

Example

A football is kicked

> 20 m/s towards the north-east.

This contains

Magnitude

$$
20\;m/s
$$

Direction

North-East

Therefore it is a vector.

---

### Comparison Table

| Scalar | Vector |
|---------|---------|
| Magnitude only | Magnitude and direction |
| One numerical value | Numerical value + direction |
| Cannot be represented by arrows | Represented by arrows |
| Added using normal arithmetic | Added using vector addition |

---

### Examples

| Quantity | Scalar or Vector |
|------------|-----------------|
| Time | Scalar |
| Distance | Scalar |
| Speed | Scalar |
| Temperature | Scalar |
| Mass | Scalar |
| Area | Scalar |
| Displacement | Vector |
| Velocity | Vector |
| Force | Vector |
| Momentum | Vector |
| Acceleration | Vector |

---

> [!example]
>
> Walking **5 km**
>
> is a scalar.
>
> Walking **5 km east**
>
> is a vector.


## Basic Concepts

### Directed Line

A straight line can point in **two opposite directions**.

Adding an arrow specifies one of these directions.

```text
<------------------------>

------------------------>

<------------------------
```

Such a line is called a **directed line**.

---

### Directed Line Segment

If we restrict a directed line to a finite length, we obtain a **directed line segment**.

```text
A ---------------------> B
```

Unlike a simple line,

a directed line segment has

- Magnitude
- Direction

---

### Vector

**Definition**

A quantity that possesses **both magnitude and direction** is called a **vector**.

A vector is usually represented as

$$
\overrightarrow{AB}
$$

or

$$
\mathbf a
$$

The point

A

is called the **initial point**

while

B

is called the **terminal point**.

---

### Magnitude

The magnitude (or length) of a vector is the distance between its initial and terminal points.

Notation

$$
|\mathbf a|
$$

or

$$
||\mathbf a||
$$

Magnitude is **always non-negative**.

Therefore,

$$
|\mathbf a|<0
$$

has **no meaning**.

---

### Direction

The arrow attached to a vector indicates its direction.

For example,

```text
A -------------> B
```

means

the direction is from

A

towards

B.

---

### Position Vector

Consider a point

$$
P(x,y,z)
$$

with respect to the origin

$$
O(0,0,0).
$$

The vector

$$
\overrightarrow{OP}
$$

is called the **position vector** of the point.

It specifies the location of the point relative to the origin.

Example

If

$$
P=(2,3,5)
$$

then

$$\color{cyan}
\overrightarrow{OP}
=
\begin{bmatrix}
2\\
3\\
5
\end{bmatrix}
$$

The magnitude is

$$
|\overrightarrow{OP}|
=
\sqrt{x^2+y^2+z^2}
$$

Therefore,

$$
|\overrightarrow{OP}|
=
\sqrt{2^2+3^2+5^2}
=
\sqrt{38}
$$
	

> [!tip]
>
> In Machine Learning, every data point is often represented as a **position vector** in a high-dimensional feature space.

---

### Direction Cosines

The angles made by a vector with the positive x-, y-, and z-axes are called the **direction angles**.

These angles are

$$
\alpha,\;
\beta,\;
\gamma
$$

The cosines of these angles are called the **direction cosines**.

They are denoted by

$$
l,\;m,\;n
$$

where

$$
l=\cos\alpha
$$

$$
m=\cos\beta
$$

$$
n=\cos\gamma
$$

An important identity is

$$
l^2+m^2+n^2=1
$$

---

### Direction Ratios

Numbers proportional to the direction cosines are called **direction ratios**.

If

$$
l,m,n
$$

are the direction cosines,

then

$$
a,b,c
$$

are corresponding direction ratios.

Unlike direction cosines,

direction ratios **do not necessarily satisfy**

$$
a^2+b^2+c^2=1
$$

---

> [!important]
>
> **Direction Cosines**
>
> - Unit quantities
> - Satisfy
>
> $$
> l^2+m^2+n^2=1
> $$
>
> **Direction Ratios**
>
> - Any proportional numbers
> - No restriction on their squares

# 5. Types of Vectors

Vectors can be classified into different types based on their magnitude, direction, and relationship with other vectors.

## 5.1 Zero Vector (Null Vector)

>[!definition]
>A **zero vector** (or **null vector**) is a vector whose **initial point and terminal point coincide**.

Mathematically,

$$
\vec{0}=(0,0,0)
$$

### Properties

- Magnitude = **0**
- Direction is **undefined** (or can be considered arbitrary)
- Acts as the **additive identity** of vectors

$$
\vec{a}+\vec{0}=\vec{a}
$$

### Example

Moving 5 meters east and then 5 meters west results in

$$
\vec{0}
$$


## 5.2 Unit Vector

>[!definition]
>A **unit vector** is a vector whose magnitude is **1**.

It specifies **direction only**.

If

$$
\vec{a}
$$

is any non-zero vector, then its unit vector is

$$
\hat{a}=\frac{\vec{a}}{|\vec{a}|}
$$

where

- $\hat{a}$ = unit vector
- $|\vec{a}|$ = magnitude of the vector

### Example

If

$$
\vec{a}=(3,4)
$$

then

$$
|\vec{a}|=\sqrt{3^2+4^2}=5
$$

Hence

$$
\hat{a}=\left(\frac35,\frac45\right)
$$

---

>[!important]
>Machine Learning frequently normalizes vectors into **unit vectors**, especially in:
>
>- Cosine Similarity
>- Word Embeddings
>- Recommendation Systems
>- Feature Normalization


## 5.3 Position Vector

>[!definition]
>A **position vector** specifies the location of a point with respect to the origin.

If

$$
P(x,y,z)
$$

then

$$
\overrightarrow{OP}
=(x,y,z)
$$

where

- Initial point = Origin
- Terminal point = P

Magnitude

$$
|\vec{OP}|=\sqrt{x^2+y^2+z^2}
$$


## 5.4 Coinitial Vectors

>[!definition]
>Two or more vectors having the **same initial point** are called **Coinitial Vectors**.

Example

```
      A
     / \
    /   \
   B     C
```

Both vectors

$$
\overrightarrow{AB}
\quad
\text{and}
\quad
\overrightarrow{AC}
$$

start from point **A**.

## 5.5 Collinear Vectors

>[!definition]
>Vectors are **collinear** if they are parallel to the same straight line.

They may

- have different magnitudes
- point in same direction
- point in opposite directions

Example

```
------->

---------->
```

or

```
------->

<-------
```


>[!tip]
>Every pair of parallel vectors is collinear.


## 5.6 Equal Vectors

>[!definition]
>Two vectors are equal if they have:
>
>- Same magnitude
>- Same direction
>
>irrespective of where they are located.

Example

```
A -----> B


C -----> D
```

Even though they start from different points,

$$
\vec{AB}=\vec{CD}
$$

## 5.7 Negative Vector

>[!definition]
>The **negative** of a vector has the **same magnitude** but **opposite direction**.

If

$$
\vec{a}
$$

then

$$
-\vec{a}
$$

is

```
a →

← -a
```

Property

$$
\vec{a}+(-\vec{a})=\vec{0}
$$


## 5.8 Free Vectors

>[!definition]
>A **free vector** can be shifted anywhere in space **without changing its magnitude or direction**.

Only

- magnitude
- direction

matter.

The starting position does **not**.

Throughout vector algebra and machine learning, we usually work with **free vectors**.

## Summary

| Type | Definition |
|--------|------------|
| Zero Vector | Magnitude = 0 |
| Unit Vector | Magnitude = 1 |
| Position Vector | From Origin to a Point |
| Coinitial Vector | Same starting point |
| Collinear Vector | Parallel vectors |
| Equal Vector | Same magnitude + direction |
| Negative Vector | Same magnitude, opposite direction |
| Free Vector | Can be translated without changing value |

---

# 6. Vector Operations

Linear algebra defines several fundamental operations on vectors. These operations form the foundation of geometry, physics, computer graphics, machine learning, robotics, and artificial intelligence.

Suppose

$$
\vec{u}=(u_1,u_2,u_3)
$$

and

$$
\vec{v}=(v_1,v_2,v_3)
$$

## 6.1 Vector Addition

>[!definition]
>Vector addition combines two vectors to produce a new vector called the **resultant vector**.

For vectors

$$
\vec{u}=(u_1,u_2,u_3)
$$

and

$$
\vec{v}=(v_1,v_2,v_3)
$$

their sum is

$$
\vec{u}+\vec{v}
=
(u_1+v_1,
u_2+v_2,
u_3+v_3)
$$

---

### Example

$$
(2,4)+(3,1)
=
(5,5)
$$

---

### Geometric Interpretation

There are two equivalent ways to visualize addition.

### Triangle Law

Move the second vector so its starting point touches the end of the first vector.

The vector from the start of the first to the end of the second is

$$
\vec{u}+\vec{v}
$$

---

### Parallelogram Law

Place both vectors from the same origin.

The diagonal of the parallelogram represents

$$
\vec{u}+\vec{v}
$$

---

### Properties

Commutative

$$
\vec{u}+\vec{v}
=
\vec{v}+\vec{u}
$$

Associative

$$
(\vec{u}+\vec{v})+\vec{w}
=
\vec{u}+(\vec{v}+\vec{w})
$$

Identity

$$
\vec{u}+\vec{0}
=
\vec{u}
$$


>[!example]
>Adding forces acting on an object produces the **net force**.


## 6.2 Vector Subtraction

>[!definition]
>Subtracting vectors means adding the negative vector.

$$
\vec{u}-\vec{v}
=
\vec{u}+(-\vec{v})
$$

Component-wise

$$
(u_1-v_1,
u_2-v_2,
u_3-v_3)
$$

---

### Example

$$
(5,4)-(2,1)
=
(3,3)
$$

---

### Interpretation

Subtraction tells us

>How do we move from one vector to another?

## 6.3 Scalar Multiplication (Scaling)

>[!definition]
>Multiplying a vector by a real number (scalar) changes its magnitude.

For scalar

$$
k
$$

$$
k\vec{v}
=
(kv_1,
kv_2,
kv_3)
$$

### Example

$$
3(2,-1)
=
(6,-3)
$$


### Effect of Scaling

| Scalar | Effect |
|---------|--------|
| k>1 | Stretches vector |
| 0<k<1 | Shrinks vector |
| k=1 | No change |
| k=0 | Zero vector |
| k<0 | Reverses direction |

---

>[!important]
>Feature scaling in Machine Learning is based on this concept.


## 6.4 Norm (Vector Length)

>[!definition]
>The **norm** measures the length or magnitude of a vector.

Also written as

$$
||\vec{v}||
$$

or

$$
|\vec{v}|
$$

For

$$
(x,y,z)
$$

$$
||\vec{v}||
=
\sqrt{x^2+y^2+z^2}
$$

---

### Example

$$
(3,4)
$$

Magnitude

$$
=
5
$$


>[!note]
>The Euclidean norm is simply the distance from the origin.


## 6.5 Dot Product (Inner Product)

>[!definition]
>The **dot product** measures how much one vector points in the direction of another.

Formula

$$
\vec{u}\cdot\vec{v}
=
u_1v_1+u_2v_2+u_3v_3
$$

Alternative geometric form

$$
\vec{u}\cdot\vec{v}
=
||u||
||v||
\cos\theta
$$

where

- θ = angle between vectors

### Example

$$
(2,3)\cdot(4,5)
=
23
$$

---

### Orthogonal Vectors

If

$$
\theta=90^\circ
$$

then

$$
\cos90^\circ=0
$$

Hence

$$
\vec{u}\cdot\vec{v}=0
$$

Orthogonal vectors are **perpendicular**.

>[!important]
>Dot Product is heavily used in Machine Learning:
>
>- Cosine Similarity
>- Recommendation Systems
>- Neural Networks
>- Linear Regression
>- PCA
>- Embeddings


## 6.6 Cross Product

>[!definition]
>The cross product produces a **new vector** that is perpendicular to both vectors.

Applicable only in **3D**.

Formula

$$\color{cyan}
\vec{u}\times\vec{v}
=
\begin{vmatrix}
\hat{i}&\hat{j}&\hat{k}\\
u_1&u_2&u_3\\
v_1&v_2&v_3
\end{vmatrix}
$$

Magnitude

$$
||\vec{u}\times\vec{v}||
=
||u||
||v||
\sin\theta
$$

---

### Properties

Not commutative

$$
\vec{u}\times\vec{v}
\neq
\vec{v}\times\vec{u}
$$

In fact,

$$
\vec{u}\times\vec{v}
=
-
(\vec{v}\times\vec{u})
$$

---

### Example

$$
(1,0,0)\times(0,1,0)
=
(0,0,1)
$$


>[!warning]
>The Cross Product is **not defined for 2D vectors**.

---

## Summary of Vector Operations

| Operation             | Formula                | Output |
| --------------------- | ---------------------- | ------ |
| Addition              | $\vec{u}+\vec{v}$      | Vector |
| Subtraction           | $\vec{u}-\vec{v}$      | Vector |
| Scalar Multiplication | $k\vec{v}$             | Vector |
| Norm                  | $\vec{v}$              | Scaler |
| Dot Product           | $\vec{u}\cdot\vec{v}$  | Scalar |
| Cross Product         | $\vec{u}\times\vec{v}$ | Vector |

---

>[!success]
>These six operations form the mathematical foundation for nearly every machine learning algorithm. Neural networks, regression, PCA, SVMs, embeddings, transformers, and optimization all rely heavily on these vector operations.


# Matrices

> [!insight]
> Matrices are one of the most important mathematical tools in **Machine Learning**, **Computer Science**, **Data Science**, **Artificial Intelligence**, **Physics**, **Economics**, and **Engineering**.
>
> Nearly every ML algorithm—from Linear Regression to Neural Networks—uses matrices to efficiently represent and manipulate data.

---

# 1. Introduction

Linear algebra consists of **vectors** and **matrices**.

While vectors represent a single collection of values, matrices allow us to organize **multiple vectors together** in a structured form.

A matrix is essentially a **rectangular arrangement of numbers** that allows us to perform calculations much more efficiently than working with individual equations.

Historically, matrices were developed as a compact method for solving **systems of linear equations**, but today they are used in almost every scientific discipline.

## Why are matrices important?

Matrices simplify many mathematical operations that would otherwise require hundreds or thousands of equations.

Some common applications include:

- Solving systems of linear equations
- Computer graphics
- Artificial Intelligence
- Machine Learning
- Neural Networks
- Image Processing
- Robotics
- Economics
- Statistics
- Cryptography
- Genetics
- Engineering
- Data Analysis

---

> [!tip]
> In Machine Learning:
>
> - Every dataset is stored as a **matrix**
> - Every neural network layer performs **matrix multiplication**
> - Images are matrices of pixel values
> - Word embeddings are matrices
> - Recommendation systems rely heavily on matrix operations


## Real-world Examples

Matrices appear in many places without us realizing it.

|Application|Matrix Representation|
|------------|--------------------|
|Excel Spreadsheet|Rows × Columns|
|Student Marks|Students × Subjects|
|Image|Pixels arranged in rows and columns|
|Dataset|Samples × Features|
|Neural Network Weights|Weight Matrix|
|Graph Adjacency|Adjacency Matrix|

---

# 2. What is a Matrix?

According to NCERT,

> **A matrix is an ordered rectangular array of numbers or functions.**

The numbers (or functions) inside a matrix are called its

- **elements**
- **entries**

Matrices are usually represented using **capital letters**.

For example,

$$
\color{cyan}
A=
\begin{bmatrix}
2 & 5\\
7 & 1\\
4 & 8
\end{bmatrix}
$$

This matrix is named **A**.

## Example

Suppose three students own notebooks and pens.

|Student|Notebooks|Pens|
|--------|----------|----|
|Radha|15|6|
|Fauzia|10|2|
|Simran|13|5|

This information can be represented as

$$
\color{cyan}
\begin{bmatrix}
15 & 6\\
10 & 2\\
13 & 5
\end{bmatrix}
$$

Instead of writing separate sentences, everything is stored neatly in one mathematical object.

---

> [!info]
> A matrix is simply a structured way of organizing related data.

---

# 3. Matrix Terminology

Consider

$$
\color{cyan}
A=
\begin{bmatrix}
1 & 4 & 2\\
3 & 5 & 6
\end{bmatrix}
$$

It has

- **2 rows**
- **3 columns**

```text
      Columns
        ↓
      1   2   3

R1 →  1   4   2
R2 →  3   5   6
```

---

Each individual number is called an **element**.

Example

- 4 is an element.
- 6 is an element.

More formally,

The element located in the **$i$-th row** and **$j$-th column** is written as

$$
a_{ij}
$$

For example,

$$
a_{23}=6
$$

because it lies in

- row 2
- column 3

---

# 4. Order of a Matrix

> [!important]
> The **order** of a matrix tells us **how many rows and columns** it contains.

The order is written as

$$
m \times n
$$

where

- **$m$ = number of rows**
- **$n$ = number of columns**

---

Example

$$
\color{cyan}
\begin{bmatrix}
1&2&3\\
4&5&6
\end{bmatrix}
$$

has

- 2 rows
- 3 columns

Therefore,

> Order = **$2 \times 3$**

---

Similarly,

$$
\color{cyan}
\begin{bmatrix}
1\\
4\\
7
\end{bmatrix}
$$

has order

> **$3 \times 1$**

---

### Number of Elements

An $m \times n$ matrix always contains

$$
m \times n
$$

elements.

Examples

|Order|Number of Elements|
|------|-----------------|
|2 × 3|6|
|4 × 5|20|
|10 × 100|1000|

---

# 5. Representation of a General Matrix

A general matrix is written as

$$
A=[a_{ij}]_{m\times n}
$$

where

- $i$ represents the row number.
- $j$ represents the column number.

Equivalently,

$$
\color{cyan}
A=
\begin{bmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
a_{21}&a_{22}&\cdots&a_{2n}\\
\vdots&\vdots&\ddots&\vdots\\
a_{m1}&a_{m2}&\cdots&a_{mn}
\end{bmatrix}
$$

---

# 6. Rows and Columns

The **horizontal arrangement** is called a **row**.

The **vertical arrangement** is called a **column**.

Example

$$
\color{cyan}
\begin{bmatrix}
2&5&7\\
1&4&8
\end{bmatrix}
$$

Rows

- (2 5 7)

- (1 4 8)

Columns

- (2,1)

- (5,4)

- (7,8)

---

# 7. Matrix as Data Storage

A matrix can represent real-world information.

Example

Student Marks

|Student|Math|Physics|Chemistry|
|--------|----|---------|-----------|
|Alice|90|82|88|
|Bob|75|80|79|
|Charlie|95|91|93|

becomes

$$
\color{cyan}
\begin{bmatrix}
90&82&88\\
75&80&79\\
95&91&93
\end{bmatrix}
$$

---

> [!example]
> In Machine Learning, datasets are stored exactly like this.
>
> Rows = observations (samples)
>
> Columns = features (variables)

---

# 8. Position of an Element

Each element has a unique address.

Example

$$
\color{cyan}
\begin{bmatrix}
3&8&5\\
2&7&4
\end{bmatrix}
$$

The number **7** is located at

- Row 2
- Column 2

Therefore

$$
a_{22}=7
$$

---

# 9. Matrix Representation of Coordinates

Points in geometry can also be represented using matrices.

Point

$$
P(2,5)
$$

can be written as

Column Matrix

$$
\color{cyan}
\begin{bmatrix}
2\\
5
\end{bmatrix}
$$

or

Row Matrix

$$
\color{cyan}
\begin{bmatrix}
2&5
\end{bmatrix}
$$

---

Multiple points can also be stored inside one matrix.

Example

Vertices of a rectangle

$$
(0,0),(4,0),(4,3),(0,3)
$$

can be written as

$$
\color{cyan}
\begin{bmatrix}
0&4&4&0\\
0&0&3&3
\end{bmatrix}
$$

> [!note]
> Computer Graphics and Robotics frequently represent geometric shapes using matrices like these.

---

# Summary

| Concept            | Meaning                            |
| ------------------ | ---------------------------------- |
| ==Matrix==         | Rectangular arrangement of numbers |
| ==Element==        | Individual number inside a matrix  |
| ==Row==            | Horizontal arrangement             |
| ==Column==         | Vertical arrangement               |
| ==Order==          | Rows × Columns                     |
| ==Entry $a_{ij}$== | Element in row $i$, column $j$     |
| Total Elements     | Rows × Columns                     |
# 3.4 Operations on Matrices

Matrices are useful not only for storing information but also for performing mathematical operations on that information.

Just as we can perform operations such as addition, subtraction, and multiplication on real numbers, similar operations can also be performed on matrices. However, unlike ordinary numbers, **matrix operations have specific rules**, and not every operation is always possible.

In this section, we shall study the following operations:

- Matrix Addition
- Scalar Multiplication
- Negative of a Matrix
- Difference of Matrices

> [!abstract]
> Matrix operations form the foundation of **Machine Learning**.
>
> Every forward pass in a neural network, every linear regression model, and every image transformation relies heavily on these operations.

---

# 3.4.1 Addition of Matrices

Suppose Fatima owns two factories, **Factory A** and **Factory B**, that manufacture sports shoes.

Each factory produces shoes for:

- Boys
- Girls

under three different price categories.

Their productions are represented by two matrices.

Instead of calculating the totals separately for every category, we simply **add the two matrices**.

For example,

Category 1

- Boys: 80 + 90 = 170
- Girls: 60 + 50 = 110

Category 2

- Boys: 75 + 70 = 145
- Girls: 65 + 55 = 120

Category 3

- Boys: 90 + 75 = 165
- Girls: 85 + 75 = 160

Thus, the resulting matrix is

$$
\color{cyan}
\begin{bmatrix}
170 & 110\\
145 & 120\\
165 & 160
\end{bmatrix}
$$

Notice that **each entry is obtained by adding the corresponding entries** of the two matrices.

---

> [!important]
> Matrix addition is performed **element by element**.
>
> The element in the first row and first column is added only to the element in the first row and first column of the second matrix.
>
> Entries in different positions can never be added together.

---

# Definition

Let

$$
\color{cyan}
A=
\begin{bmatrix}
a_{11}&a_{12}&a_{13}\\
a_{21}&a_{22}&a_{23}
\end{bmatrix}
$$

and

$$
\color{cyan}
B=
\begin{bmatrix}
b_{11}&b_{12}&b_{13}\\
b_{21}&b_{22}&b_{23}
\end{bmatrix}
$$

be two matrices of the **same order**.

Then,

$$
\color{cyan}
A+B=
\begin{bmatrix}
a_{11}+b_{11} & a_{12}+b_{12} & a_{13}+b_{13}\\
a_{21}+b_{21} & a_{22}+b_{22} & a_{23}+b_{23}
\end{bmatrix}
$$

In general,

If

$$
\color{cyan}
A=[a_{ij}],\qquad
B=[b_{ij}]
$$

are matrices of order **m × n**, then

$$
\color{cyan}
C=A+B=[c_{ij}]
$$

where

$$
c_{ij}=a_{ij}+b_{ij}
$$

for every possible value of **i** and **j**.

---

> [!note]
> Matrix addition is only defined when both matrices have **exactly the same order**.

---

# Example 1

Let

$$
\color{cyan}
A=
\begin{bmatrix}
3&1&1\\
2&3&0
\end{bmatrix}
$$

and

$$
\color{cyan}
B=
\begin{bmatrix}
2&5&1\\
-1&2&3
\end{bmatrix}
$$

Find

$$
A+B
$$

### Solution

Add the corresponding entries.

$$
\color{cyan}
A+B=
\begin{bmatrix}
3+2 & 1+5 & 1+1\\
2+(-1) & 3+2 & 0+3
\end{bmatrix}
$$

Therefore,

$$
\color{cyan}
A+B=
\begin{bmatrix}
5&6&2\\
1&5&3
\end{bmatrix}
$$

---

# Matrix Addition Formula

For two matrices

$$
\color{cyan}
A=[a_{ij}]
\qquad
B=[b_{ij}]
$$

their sum is

$$
\color{cyan}
A+B=[a_{ij}+b_{ij}]
$$

This means that every element is added **independently**.

---

> [!tip]
> Think of matrix addition like adding two Excel spreadsheets.
>
> Each cell is added only to the corresponding cell in the other spreadsheet.

---

# Condition for Matrix Addition

Two matrices **can be added only if they have the same order**.

Example

These matrices **can** be added.

$$
\color{cyan}
\begin{bmatrix}
2&3\\
1&0
\end{bmatrix}
+
\begin{bmatrix}
4&5\\
7&8
\end{bmatrix}
$$

Both are **2 × 2** matrices.

---

These matrices **cannot** be added.

$$
\color{cyan}
\begin{bmatrix}
2&3\\
1&0
\end{bmatrix}
+
\begin{bmatrix}
1&2&3\\
1&0&1
\end{bmatrix}
$$

because their orders are

- 2 × 2
- 2 × 3

which are different.

---

> [!warning]
> Matrix addition is **not defined** if the matrices have different dimensions.

---

# 3.4.2 Scalar Multiplication

A **scalar** is simply a real number.

When multiplying a matrix by a scalar, **every element** of the matrix is multiplied by that scalar.

Suppose a factory doubles its production.

If

$$
\color{cyan}
A=
\begin{bmatrix}
80&60\\
75&65\\
90&85
\end{bmatrix}
$$

then

$$
\color{cyan}
2A=
\begin{bmatrix}
160&120\\
150&130\\
180&170
\end{bmatrix}
$$

Every element has been multiplied by **2**.

---

## Definition

If

$$
\color{cyan}
A=[a_{ij}]
$$

is an **m × n** matrix and **k** is a scalar,

then

$$
\color{cyan}
kA=[ka_{ij}]
$$

That is,

every entry of the matrix is multiplied by **k**.

---

# Example

Let

$$
\color{cyan}
A=
\begin{bmatrix}
3&1&1.5\\
5&7&3\\
2&0&5
\end{bmatrix}
$$

Find

$$
3A
$$

Multiply every element by 3.

$$
\color{cyan}
3A=
\begin{bmatrix}
9&3&4.5\\
15&21&9\\
6&0&15
\end{bmatrix}
$$

---

> [!tip]
> Scalar multiplication simply scales every value in the matrix equally.

---

# Negative of a Matrix

The **negative** of a matrix is obtained by multiplying every element by **−1**.

If

$$
\color{cyan}
A=
\begin{bmatrix}
3&1\\
-5&x
\end{bmatrix}
$$

then

$$
\color{cyan}
-A=(-1)A=
\begin{bmatrix}
-3&-1\\
5&-x
\end{bmatrix}
$$

---

> [!note]
> The negative of a matrix changes only the **sign** of every element.
>
> The dimensions remain exactly the same.

---

# Difference of Matrices

Matrix subtraction is defined using **matrix addition**.

Instead of subtracting directly, we first take the negative of the second matrix.

Thus,

$$
\color{cyan}
A-B=A+(-B)
$$

---

## Definition

If

$$
\color{cyan}
A=[a_{ij}],\qquad
B=[b_{ij}]
$$

are matrices of the same order,

then

$$
\color{cyan}
A-B=[a_{ij}-b_{ij}]
$$

where each corresponding element is subtracted.

---

# Example

Let

$$
\color{cyan}
A=
\begin{bmatrix}
1&2&3\\
2&3&1
\end{bmatrix}
$$

and

$$
\color{cyan}
B=
\begin{bmatrix}
3&1&3\\
1&0&2
\end{bmatrix}
$$

Find

$$
2A-B
$$

### Step 1

Multiply A by 2.

$$
\color{cyan}
2A=
\begin{bmatrix}
2&4&6\\
4&6&2
\end{bmatrix}
$$

### Step 2

Subtract corresponding entries.

$$
\color{cyan}
2A-B=
\begin{bmatrix}
2-3&4-1&6-3\\
4-1&6-0&2-2
\end{bmatrix}
$$

Therefore,

$$
\color{cyan}
2A-B=
\begin{bmatrix}
-1&3&3\\
3&6&0
\end{bmatrix}
$$

---

> [!summary]
> **Operations covered in this section**
>
> - Matrix Addition → Add corresponding elements
> - Scalar Multiplication → Multiply every element by the scalar
> - Negative of a Matrix → Multiply every element by −1
> - Difference of Matrices → Subtract corresponding elements (or add the negative matrix)
>
> **Important Rule:** Addition and subtraction are possible **only when the matrices have the same order.**

# 3.4.3 Properties of Matrix Addition

> [!insight]
> Matrix addition behaves very similarly to ordinary addition of real numbers.
>
> If matrices have the **same order**, they satisfy several useful algebraic properties that make calculations simpler.
>
> These properties are frequently used in **Linear Algebra**, **Machine Learning**, **Computer Graphics**, and **Scientific Computing**.

---

# 1. Commutative Property

> [!important]
> The **order** in which two matrices are added **does not matter**.

If

$$
\color{cyan}
A=[a_{ij}], \qquad B=[b_{ij}]
$$

are matrices of the same order, then

$$
A+B=B+A
$$

---

### Proof

Using the definition of matrix addition,

$$
\begin{aligned}
A+B
&=[a_{ij}]+[b_{ij}]\\
&=[a_{ij}+b_{ij}]\\
&=[b_{ij}+a_{ij}]\\
&=[b_{ij}]+[a_{ij}]\\
&=B+A
\end{aligned}
$$

Since addition of real numbers is commutative,

$$
a_{ij}+b_{ij}=b_{ij}+a_{ij}
$$

therefore,

$$
A+B=B+A
$$

---

### Example

Let

$$
\color{cyan}
A=
\begin{bmatrix}
1&2\\
3&4
\end{bmatrix},
\qquad
B=
\begin{bmatrix}
5&6\\
7&8
\end{bmatrix}
$$

Then

$$
\color{cyan}
A+B=
\begin{bmatrix}
6&8\\
10&12
\end{bmatrix}
=
B+A
$$

---

> [!tip]
> Just like
>
> $$
> 2+5=5+2
> $$
>
> matrix addition is also commutative.

---

# 2. Associative Property

> [!important]
> When adding three matrices, it does **not matter** which two are added first.

If

$$
A,\;B,\;C
$$

are matrices of the same order,

then

$$
(A+B)+C=A+(B+C)
$$

---

### Proof

Using the definition of matrix addition,

$$
\begin{aligned}
(A+B)+C
&=([a_{ij}]+[b_{ij}])+[c_{ij}]\\
&=[a_{ij}+b_{ij}]+[c_{ij}]\\
&=[(a_{ij}+b_{ij})+c_{ij}]\\
&=[a_{ij}+(b_{ij}+c_{ij})]\\
&=[a_{ij}]+([b_{ij}]+[c_{ij}])\\
&=A+(B+C)
\end{aligned}
$$

This follows from the associative property of real numbers.

---

### Example

Suppose

$$
\color{cyan}
A=
\begin{bmatrix}
1&0\\
2&1
\end{bmatrix},
\quad
B=
\begin{bmatrix}
2&1\\
0&3
\end{bmatrix},
\quad
C=
\begin{bmatrix}
4&2\\
1&0
\end{bmatrix}
$$

Regardless of how the matrices are grouped,

$$
(A+B)+C=A+(B+C)
$$

Both produce exactly the same matrix.

---

# 3. Additive Identity

> [!important]
> Every matrix has an **identity element** for addition.

For matrix addition, the identity element is the **Zero Matrix**.

If

$$
\color{cyan}
O=
\begin{bmatrix}
0&0\\
0&0
\end{bmatrix}
$$

then

$$
A+O=O+A=A
$$

---

### Why?

Adding zero to any number leaves it unchanged.

Similarly,

adding a zero matrix leaves every element unchanged.

---

### Example

Let

$$
\color{cyan}
A=
\begin{bmatrix}
3&5\\
2&7
\end{bmatrix}
$$

Then

$$
\color{cyan}
A+
\begin{bmatrix}
0&0\\
0&0
\end{bmatrix}
=
\begin{bmatrix}
3&5\\
2&7
\end{bmatrix}
=A
$$

---

> [!note]
> The zero matrix is called the **Additive Identity** because it behaves exactly like the number **0** in ordinary arithmetic.

---

# 4. Additive Inverse

> [!important]
> Every matrix has a **negative matrix** that "cancels it out."

If

$$
A=[a_{ij}]
$$

then its additive inverse is

$$
-A=[-a_{ij}]
$$

and

$$
A+(-A)=O
$$

---

### Example

Let

$$
\color{cyan}
A=
\begin{bmatrix}
3&-2\\
1&5
\end{bmatrix}
$$

Then

$$
\color{cyan}
-A=
\begin{bmatrix}
-3&2\\
-1&-5
\end{bmatrix}
$$

Therefore,

$$
\color{cyan}
A+(-A)=
\begin{bmatrix}
0&0\\
0&0
\end{bmatrix}
=O
$$

---

> [!tip]
> Think of the additive inverse exactly like
>
> $$
> 7+(-7)=0
> $$

---

# 5. Properties of Scalar Multiplication

Suppose

- $A$ and $B$ are matrices of the same order.
- $k$ and $l$ are scalars (ordinary real numbers).

Then scalar multiplication satisfies the following important properties.

## Property 1

A scalar distributes over matrix addition.

$$
k(A+B)=kA+kB
$$

### Proof

$$
\begin{aligned}
k(A+B)
&=k([a_{ij}]+[b_{ij}])\\
&=k[a_{ij}+b_{ij}]\\
&=[k(a_{ij}+b_{ij})]\\
&=[ka_{ij}+kb_{ij}]\\
&=[ka_{ij}]+[kb_{ij}]\\
&=kA+kB
\end{aligned}
$$

---

### Example

Let

$$
k=2
$$

and

$$
\color{cyan}
A=
\begin{bmatrix}
1&2\\
3&4
\end{bmatrix},
\qquad
B=
\begin{bmatrix}
5&6\\
7&8
\end{bmatrix}
$$

Then

$$
2(A+B)=2A+2B
$$


## Property 2

A matrix distributes over scalar addition.

$$
(k+l)A=kA+lA
$$

---

### Proof

$$
\begin{aligned}
(k+l)A
&=(k+l)[a_{ij}]\\
&=[(k+l)a_{ij}]\\
&=[ka_{ij}+la_{ij}]\\
&=k[a_{ij}]+l[a_{ij}]\\
&=kA+lA
\end{aligned}
$$

---

> [!note]
> These two distributive laws are used constantly in Linear Algebra and Machine Learning proofs.

---

# 6. Worked Example 8

> [!example]
> If
>
> $$
> 2A+3X=5B
> $$
>
> where
>
> $$
> \color{cyan}
> A=
> \begin{bmatrix}
> 8&0&-2\\
> 4&2&3\\
> -5&1&6
> \end{bmatrix},
> \qquad
> B=
> \begin{bmatrix}
> 2&2&4\\
> -2&3&6\\
> 5&1&2
> \end{bmatrix}
> $$
>
> Find the matrix $X$.

---

### Step 1

Move $2A$ to the right-hand side.

$$
2A+3X=5B
$$

Subtract $2A$ from both sides.

$$
3X=5B-2A
$$

---

### Step 2

Divide both sides by 3.

$$
X=\frac13(5B-2A)
$$

---

### Step 3

Compute

$$
5B=
\color{cyan}
\begin{bmatrix}
10&10&20\\
-10&15&30\\
25&5&10
\end{bmatrix}
$$

and

$$
2A=
\color{cyan}
\begin{bmatrix}
16&0&-4\\
8&4&6\\
-10&2&12
\end{bmatrix}
$$

---

### Step 4

Subtract the matrices.

$$
5B-2A=
\color{cyan}
\begin{bmatrix}
-6&10&24\\
-18&11&24\\
35&3&-2
\end{bmatrix}
$$

---

### Step 5

Multiply by

$$
\frac13
$$

to obtain

$$
\color{cyan}
X=
\frac13
\begin{bmatrix}
-6&10&24\\
-18&11&24\\
35&3&-2
\end{bmatrix}
$$

or

$$
\color{cyan}
X=
\begin{bmatrix}
-2&\frac{10}{3}&8\\
-6&\frac{11}{3}&8\\
\frac{35}{3}&1&-\frac23
\end{bmatrix}
$$

---

# Summary

|Property|Formula|
|---------|--------|
|Commutative|$A+B=B+A$|
|Associative|$(A+B)+C=A+(B+C)$|
|Additive Identity|$A+O=A$|
|Additive Inverse|$A+(-A)=O$|
|Distributive Property|$k(A+B)=kA+kB$|
|Scalar Addition Property|$(k+l)A=kA+lA$|

---

> [!success]
> These six properties form the foundation of **Matrix Algebra**.
>
> They are used repeatedly throughout **Linear Algebra**, **Machine Learning**, **Optimization**, and **Deep Learning**, especially when simplifying equations involving vectors and matrices.