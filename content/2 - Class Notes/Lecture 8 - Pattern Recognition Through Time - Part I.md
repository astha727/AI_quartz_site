
>[!info] **From Static Machine Learning to Sequential AI**
>Traditional machine learning assumes that each observation is independent of the others. However, many real-world problems involve **ordered sequences**, where the timing and order of observations are essential for understanding their meaning. This branch of AI is known as **Pattern Recognition Through Time** or **Sequential Pattern Recognition**. Before the rise of deep learning, algorithms such as **Dynamic Time Warping (DTW)** and **Hidden Markov Models (HMMs)** were the dominant approaches for modeling temporal data like speech, handwriting, gestures, and sign language. These methods laid the foundation for modern sequence models such as **Recurrent Neural Networks (RNNs), LSTMs, and Transformers**.

> [!insight]  
> Pattern Recognition Through Time studies data whose meaning depends not only on **what** is observed, but also **when** it is observed.
> 
> Unlike traditional machine learning problems where each observation is independent, temporal pattern recognition analyzes sequences of observations whose order carries important information.
> 
> This area forms the foundation of many Artificial Intelligence applications including speech recognition, handwriting recognition, gesture recognition, sign language recognition, biological signal analysis, and human activity recognition.

---

# Why Time Matters

Many machine learning algorithms assume that every observation is independent.

For example

- Predicting house prices
    
- Predicting diabetes
    
- Spam detection
    

Each example can be considered individually.

However, many real-world problems involve **sequences**.

Examples include

- Speech
    
- Handwriting
    
- Sign language
    
- Music
    
- Human motion
    
- Dolphin whistles
    

In these problems, the **order of observations** is essential.

Changing the order changes the meaning.

---

## Static vs Temporal Recognition

|Static Recognition|Pattern Recognition Through Time|
|---|---|
|Single observation|Sequence of observations|
|Order not important|Order is critical|
|Image classification|Speech recognition|
|Credit approval|Gesture recognition|
|Face image|Face video|


> [!example]  
> Recognizing a person's face from a **video** is generally easier than recognizing it from a single image.
> 
> If one frame is blurred, poorly lit, or partially occluded, other frames often provide enough information for correct recognition.

---

# Language-like Structure

Many temporal problems share a common hierarchical structure.

Small units combine into larger units.

```text
Small units
      │
      ▼
Letters / Phonemes / Gestures
      │
      ▼
Words
      │
      ▼
Sentences
      │
      ▼
Complete Meaning
```

Examples

|Domain|Small Unit|Larger Structure|
|---|---|---|
|Speech|Phoneme|Word|
|Handwriting|Letter|Word|
|Sign Language|Gesture|Sentence|
|Music|Note|Melody|
|Human Activity|Motion|Activity|

The lecture argues that many human activities naturally possess this language-like organization.

Examples include

- Driving
    
- Playing basketball
    
- Vacuuming
    
- Walking
    

Each activity is composed of reusable movement patterns arranged according to statistical rules.

---

> [!insight]  
> Pattern Recognition Through Time is fundamentally about recognizing **ordered sequences** rather than isolated observations.

---

# Dolphin Whistles

The lecture introduces dolphin whistle recognition as a motivating problem.

Marine biologists collect thousands of underwater recordings.

The goal is to automatically recognize different whistle types.

Doing so allows researchers to

- identify dolphins
    
- track communication
    
- automatically annotate large databases
    

## Spectrogram

Instead of viewing sound as a waveform, we convert it into a **spectrogram**.

A spectrogram displays

- time
    
- frequency
    
- signal power
    

```text
Frequency ↑

17 kHz |                                   ███
        |                          ███
12 kHz |                           ███
        |                ███
 7 kHz |                ███
        |      ███
 5 kHz |____________________________
    0------------------------→ Time

Brightness = Signal Power
```

The lecture notes

- x-axis → time
    
- y-axis → frequency
    
- brighter pixels indicate greater energy
    

## Noise

Ocean recordings contain substantial background noise.

Typical low-frequency sources include

- waves
    
- boats
    
- ocean movement
    

Fortunately,

Atlantic spotted dolphin whistles typically occur between

**5 kHz – 17 kHz**

making them easier to isolate.

## Signature Whistles

Dolphins possess **signature whistles**, which function similarly to human names.

A dolphin entering a new area may emit its signature whistle so nearby dolphins can identify and locate it.

---

> [!example]  
> Human:
> 
> "Astha!"
> 
> Dolphin:
> 
> Unique signature whistle

---

# The Recognition Problem

The lecture presents two recordings of the **same whistle**.

Although they represent the same whistle,

one is

- faster
    

while the other is

- stretched over time.
    

```text
Whistle A

/\____/\_

Whistle B

/ \__________/ \__
```

Humans easily recognize them as identical.

A computer must learn to do the same.

---

# Feature Representation

Choosing appropriate features is one of the most important parts of machine learning.

The obvious choice would be

- absolute frequency
    

Example

|Time|Frequency (kHz)|
|---|--:|
|t₁|5|
|t₂|14|
|t₃|10|
|t₄|7|
|t₅|10|
|t₆|14|

However,

different dolphins may whistle at slightly different base frequencies.

The absolute pitch is less important than the **shape** of the whistle.

## Delta Frequency

Instead of storing the frequency itself,

the lecture suggests storing the **change in frequency** between consecutive samples.

Example

|Frequency|Delta Frequency|
|---|--:|
|5|—|
|14|+9|
|10|−4|
|7|−3|
|10|+3|
|14|+4|

The overall pattern

```text
+9
↓
-4
↓
-3
↑
+3
↑
+4
```

remains similar even if the whistle starts at a different frequency.

> [!important]  
> Delta Frequency captures the **shape** of the whistle instead of its absolute pitch.

---

# Why Euclidean Distance Fails

Suppose two whistles contain identical patterns but are spoken at different speeds.

```text
Fast

■■■■■■■■

Slow

■■■■■■■■■■■■■■■■
```

The two sequences have different lengths.

A simple Euclidean Distance comparison requires observations to align perfectly.

To compare unequal lengths,

one sequence must be padded.

Unfortunately,

this produces large errors even though both whistles represent the same signal.

---

```text
Fast

A B C D

Slow

A A B B C C D D
```

Humans recognize these as identical.

Euclidean Distance does not.

---

> [!warning]  
> Ordinary distance metrics assume that observations occur at exactly the same time.
> 
> Temporal signals rarely satisfy this assumption.

---

# Summary

|Concept|Key Idea|
|---|---|
|Pattern Recognition Through Time|Studies sequential data|
|Sequence|Order carries information|
|Language-like Structure|Small units combine into larger structures|
|Spectrogram|Visual representation of sound|
|Signature Whistle|Dolphin identity signal|
|Delta Frequency|Represents changes rather than absolute pitch|
|Euclidean Distance|Performs poorly when sequences differ in speed|


## See Also

- [[1 - Classification]]
    
- [[Distance Metrics]]
    
- [[Hidden Markov Models (HMM)]]

# Dynamic Time Warping (DTW)

> [!insight]  
> **Dynamic Time Warping (DTW)** is an algorithm used to measure the similarity between two sequences that may vary in speed or duration.
> 
> Rather than comparing observations at identical time steps, DTW **warps the time axis** so that similar portions of two sequences are aligned before computing their distance.
> 
> It is widely used in speech recognition, handwriting recognition, gesture recognition, bioinformatics, financial time series, and many other sequence matching problems.

---

# Motivation

Suppose two people say the same word.

Person A speaks slowly.

Person B speaks quickly.

Although both words are identical, the corresponding samples occur at different times.

```text
Slow

A────B────C────D

Fast

A──B──C──D
```

Humans immediately recognize both as the same word.

A computer comparing samples one-by-one may conclude they are very different.

---

# The Time Warping Problem

Many real-world signals are **not produced at a constant speed**.

Examples include

- Speech
    
- Dolphin whistles
    
- Handwriting
    
- Sign language
    
- Walking
    
- ECG signals
    

The important information is usually

> **the shape of the signal**

rather than

> **exact timing of every sample**


## Example

Imagine saying your own name.

```text
Fast

Alexa

████████

Slow

Aaaallllllleeeexxaaaa

██████████████████
```

The pronunciation is identical.

Only the timing changes.

---

# Why Euclidean Distance Fails

Euclidean Distance assumes

- same number of samples
    
- one-to-one alignment
    

Example

```text
Signal A

0 2 3 3 2 1

Signal B

0 5 2 0
```

To compare them,

one sequence is padded

```text
0 5 2 0 0 0
```

The Euclidean Distance becomes

$$  
d(x,y)=\sqrt{\sum_i(x_i-y_i)^2}  
$$

Even though both signals have similar overall shapes,

the distance becomes unnecessarily large because corresponding features occur at different times.

---

> [!warning]  
> Euclidean Distance assumes every observation occurs at exactly the same time.
> 
> Temporal signals rarely satisfy this assumption.

---

# Dynamic Time Warping

Instead of comparing observations directly,

DTW first aligns similar portions of the sequences.

The time axis is allowed to stretch or compress.

```text
Signal A

A B C D

Signal B

A A B B C C D
```

Instead of forcing

```text
A↔A
B↔A
C↔B
D↔B
```

DTW aligns

```text
A ↔ A A

B ↔ B B

C ↔ C C

D ↔ D
```

The resulting distance is much smaller.

---

# Visual Intuition

Without DTW

```text
Signal 1

/\____/\_

Signal 2

/ \__________/ \__

↓

Compare point-by-point

❌ Poor alignment
```

With DTW

```text
Stretch time

/\________/\_

/\________/\_

↓

Features now align

✔ Good match
```

---

# Alignment Matrix

DTW compares every point in one sequence with every point in the other.

```text
          Sequence X

    ● ● ● ● ●

Y  ●  □ □ □ □ □

   ●  □ □ □ □ □

   ●  □ □ □ □ □

   ●  □ □ □ □ □

   ●  □ □ □ □ □
```

Each square stores

- local distance
    
- cumulative distance
    

The optimal path travels through the matrix.

## Warping Path

The algorithm searches for the lowest-cost path.

```text
Start

●══════╗
        ║
        ╚══╗
            ║
            ╚════●

                 Finish
```

Unlike Euclidean Distance,

the path does **not** have to remain perfectly diagonal.

---

# DTW Cost Function

At every cell,

DTW computes

$$  
DTW(i,j)=d(i,j)+\min  
\begin{cases}  
DTW(i-1,j)\  
DTW(i,j-1)\  
DTW(i-1,j-1)  
\end{cases}  
$$

where

- $d(i,j)$ is the local distance
    
- the minimum selects the cheapest previous alignment
    

This is a classic **Dynamic Programming** recurrence.

---

> [!tip]  
> DTW is called **Dynamic Time Warping** because it uses **Dynamic Programming** to determine the optimal time alignment.

---

# Example

Suppose

```text
Signal A

0 0 2 3 3 2 1

Signal B

0 5 2 0
```

A direct comparison produces a large Euclidean Distance.

DTW instead matches

```text
0 ↔ 0

0 ↔ 0

2 ↔ 5

3 ↔ 5

3 ↔ 2

2 ↔ 2

1 ↔ 0
```

allowing repeated matches where necessary.

The overall distance becomes much smaller.

---

# Sakoe–Chiba Bounds

DTW is very flexible.

Sometimes

too flexible.

A poor match could still produce an artificially small distance by excessively stretching the alignment.

```text
Without bounds

●══════════════════════╗
                       ║
                       ╚══════●
```

The lecture introduces **Sakoe–Chiba Bounds**.

These restrict how far the alignment may deviate from the main diagonal.

```text
Allowed Region

///////////////////

////██████████////

///////////////////
```

Only paths inside the band are considered.

## Why Use Bounds?

Advantages

- Prevent unrealistic alignments
    
- Reduce computation
    
- Improve recognition accuracy
    
- Limit excessive time warping
    

---

> [!important]  
> The optimal width of the Sakoe–Chiba Band is usually chosen empirically using cross-validation.

---

# Advantages of DTW

✔ Handles sequences with different speeds

✔ Matches similar patterns

✔ Robust to local stretching

✔ Works well for temporal signals

---

# Limitations

✘ Computationally expensive

✘ Can over-warp unrelated signals

✘ Requires constraints for realistic alignments

✘ Does not explicitly model temporal states

---

# Applications

Dynamic Time Warping is commonly used in

- Speech Recognition
    
- Handwriting Recognition
    
- Sign Language Recognition
    
- Gesture Recognition
    
- Dolphin Whistle Recognition
    
- ECG Analysis
    
- Financial Time Series
    
- Motion Capture Analysis
    

---

# DTW vs Euclidean Distance

|Euclidean Distance|Dynamic Time Warping|
|---|---|
|One-to-one comparison|Flexible alignment|
|Same length preferred|Different lengths allowed|
|No stretching|Time stretching permitted|
|Fast|More computationally expensive|
|Sensitive to timing|Robust to timing differences|

---

# Summary

|Concept|Description|
|---|---|
|Dynamic Time Warping|Aligns temporal sequences before comparison|
|Warping|Stretches or compresses time|
|Alignment Matrix|Stores cumulative distances|
|Warping Path|Lowest-cost alignment|
|Dynamic Programming|Computes optimal path efficiently|
|Sakoe–Chiba Bounds|Restrict excessive warping|

