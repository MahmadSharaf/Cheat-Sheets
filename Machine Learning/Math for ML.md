# Mathematics for machine learning

- [Mathematics for machine learning](#mathematics-for-machine-learning)
  - [Phase 1: Data Processing](#phase-1-data-processing)
  - [Phase 2: Feature Engineering and Selection](#phase-2-feature-engineering-and-selection)
    - [Vectors and Matrices](#vectors-and-matrices)
      - [Vector/Matrix Addition/Subtraction](#vectormatrix-additionsubtraction)
      - [Scalar Multiplication](#scalar-multiplication)
      - [Vector/Matrix Transpose](#vectormatrix-transpose)
      - [Vector Dot Product](#vector-dot-product)
      - [Dot Product for Matrix by Vector](#dot-product-for-matrix-by-vector)
      - [Dot Product for Matrices](#dot-product-for-matrices)
      - [Hadamard Multiplication](#hadamard-multiplication)
    - [Vectors in code](#vectors-in-code)
      - [Python example](#python-example)
    - [Product Properties](#product-properties)
      - [Original Matrix Properties](#original-matrix-properties)
        - [Identity Matrix](#identity-matrix)
      - [Hadamard Matrix Properties](#hadamard-matrix-properties)
  - [Phase 3: Modeling](#phase-3-modeling)
    - [Geometry of Column Vectors](#geometry-of-column-vectors)
      - [Angel between vectors](#angel-between-vectors)
    - [Measures of Magnitude](#measures-of-magnitude)
      - [Definition of Norm](#definition-of-norm)
      - [Properties of Norm](#properties-of-norm)
      - [Types of Norm](#types-of-norm)
    - [Probability](#probability)
      - [Probability Terminologies](#probability-terminologies)
      - [Axioms of probability](#axioms-of-probability)
      - [Conditional probability](#conditional-probability)
      - [Bayes’ rule](#bayes-rule)
      - [Independent events](#independent-events)
      - [Random variables](#random-variables)
        - [Discrete Random Variables](#discrete-random-variables)
        - [Expected Value](#expected-value)
        - [Variance](#variance)
        - [Standard Deviation](#standard-deviation)
      - [Chebyshev’s inequality](#chebyshevs-inequality)
      - [Entropy](#entropy)
      - [Continuous random variables and probability density function](#continuous-random-variables-and-probability-density-function)
      - [Building machine learning models](#building-machine-learning-models)
  - [Phase 4: Optimization](#phase-4-optimization)
    - [Maximum Likelihood Estimation](#maximum-likelihood-estimation)
    - [Derivatives](#derivatives)
    - [Common Derivatives](#common-derivatives)
    - [Derivative Rules](#derivative-rules)
      - [Sum Rule](#sum-rule)
      - [Product Rule](#product-rule)
      - [Chain Rule](#chain-rule)
    - [Second Derivative](#second-derivative)
    - [Gradient Descent](#gradient-descent)
    - [Newton's method](#newtons-method)
    - [Multivariate Derivative](#multivariate-derivative)
      - [Partial Derivative](#partial-derivative)
      - [Gradient](#gradient)
  - [References](#references)

## Phase 1: Data Processing

Data is formatted in a way that algorithms can ingest. Uses Linear Algebra.

## Phase 2: Feature Engineering and Selection

Data is transformed to make it easy for algorithms to understand. Uses vectors and matrices.

### Vectors and Matrices

#### Vector/Matrix Addition/Subtraction

Given $v$ and $k$ are same length/size then we can operate on them.

- Column Vector addition

$$  v=\begin{bmatrix} v_1 \\ v_2 \\ v_3\end{bmatrix};
    k=\begin{bmatrix} k_1 \\ k_2 \\ k_3\end{bmatrix}$$
$$v + k = \begin{bmatrix} v_1+k_1 \\ v_2+k_2 \\ v_3+k_3 \end{bmatrix}$$
$$v - k = \begin{bmatrix} v_1-k_1 \\ v_2-k_2 \\ v_3-k_3 \end{bmatrix}$$

- Row Vector addition

$$  v=\begin{bmatrix} v_1 & v_2 & v_3\end{bmatrix};
    k=\begin{bmatrix} k_1 & k_2 & k_3\end{bmatrix}$$
$$v + k = \begin{bmatrix} v_1+k_1 & v_2+k_2 & v_3+k_3 \end{bmatrix}$$
$$v - k = \begin{bmatrix} v_1-k_1 & v_2-k_2 & v_3-k_3 \end{bmatrix}$$

- Matrix addition

$$  v=\begin{bmatrix} v_{11} & v_{12} \\ v_{21} & v_{22} \\ v_{31} & v_{32}\end{bmatrix};
    k=\begin{bmatrix} k_{11} & k_{12} \\ k_{21} & k_{22} \\ k_{31} & k_{32}\end{bmatrix}$$
$$v + k = \begin{bmatrix} v_{11}+k_{11} & v_{12}+ k_{12} \\ v_{21}+k_{21} & v_{22}+k_{22} \\ v_{31}+k_{31} & v_{32}+k_{32}\end{bmatrix}$$
$$v - k = \begin{bmatrix} v_{11}-k_{11} & v_{12}-k_{12} \\ v_{21}-k_{21} & v_{22}-k_{22} \\ v_{31}-k_{31} & v_{32}-k_{32}\end{bmatrix}$$

#### Scalar Multiplication

$$ a => R_{real}; \overrightarrow{v} \& \overrightarrow{k} \text{are vectors} $$
$$ a(\overrightarrow{v} + \overrightarrow{k}) = a\overrightarrow{v} + a\overrightarrow{k} = \begin{bmatrix} av_1 \\ av_2 \\ av_3\end{bmatrix} +  \begin{bmatrix} ak_1 \\ ak_2 \\ ak_3\end{bmatrix}$$

#### Vector/Matrix Transpose

It is the diagonal inverse of vector/matrix

$$ \text{if } v=\begin{bmatrix} v_1 \\ v_2 \\ v_3\end{bmatrix}\text{,then } v^T=\begin{bmatrix} v_1 & v_2 & v_3\end{bmatrix}$$
$$ \text{if } v=\begin{bmatrix} v_{11} & v_{12} \\ v_{21} & v_{22} \\ v_{31} & v_{32}\end{bmatrix}\text{,then } v^T=\begin{bmatrix} v_{11} & v_{21} & v_{31} \\ v_{12} & v_{22} & v_{32}\end{bmatrix} $$

#### Vector Dot Product

$$ \overrightarrow{v} = \begin{bmatrix}
    v_1 \\
    v_2 \\
    .. \\
    v_n
\end{bmatrix}
, \overrightarrow{w} = \begin{bmatrix}
    w_1 \\
    w_2 \\
    ..  \\
    w_n
\end{bmatrix}
\\ \overrightarrow{v} . \overrightarrow{w} = \overrightarrow{v}^T\overrightarrow{w} =
\begin{bmatrix}
v_1 & .. & v_n
\end{bmatrix}
\begin{bmatrix}
    w_1 \\
    w_2 \\
    ..  \\
    w_n
\end{bmatrix} = \sum_{i=1}^n v_i w_i
$$

#### Dot Product for Matrix by Vector

$$
w = \begin{bmatrix}
    \overrightarrow{w_1} \\
    ... \\
    \overrightarrow{w_m} \\
\end{bmatrix}, \overrightarrow{v} =\begin{bmatrix}
    v_1 \\
    ... \\
    v_n \\
\end{bmatrix}
\\
w.\overrightarrow{v} = \begin{bmatrix}
    \overrightarrow{w_1} \\
    ... \\
    \overrightarrow{w_m} \\
\end{bmatrix}\begin{bmatrix}
    v_1 \\
    ... \\
    v_n \\
\end{bmatrix} = \begin{bmatrix}
    \overrightarrow{w_1}\overrightarrow{v} \\
    ... \\
    \overrightarrow{w_m}\overrightarrow{v} \\
\end{bmatrix}
\\
\\ \begin{bmatrix}
    1 & 0 & 1 \\
    2 & 0 & -1 \\
    0 & 1 & 1 \\
\end{bmatrix}
\begin{bmatrix}
    4 \\
    -1 \\
    5 \\
\end{bmatrix} =
\begin{bmatrix}
    8 \\
    3 \\
    4 \\
\end{bmatrix}
$$

#### Dot Product for Matrices

In Formulae: If $C=AB$, where $A$ is an $n × m$ matrix and $B$ is a $m × k$ matrix, then $C$ is a $n × k$ matrix where
$$c_{i,j} = \sum_l a_{i,l} b_{l,j}$$

Example:

$$
\begin{bmatrix}
    1 & 2 \\
    -1 & 1
\end{bmatrix}
\begin{bmatrix}
    1 & 1 & 0 \\
    0 & 1 & 2
\end{bmatrix} =
\begin{bmatrix}
    1*1+2*0 & 1*1 +2*1 & 1*0+2*2 \\
    -1*1+1*0 & -1*1+1*1 & -1*0+1*2
\end{bmatrix} =
\begin{bmatrix}
    1 & 3 & 4 \\
    -1 & 0 & 2
\end{bmatrix}
$$

#### Hadamard Multiplication

Definition: An (often less useful) method of multiplying matrices is element-wise.

$$
A = \begin{bmatrix}
    1 & 0 \\
    3 & 2 \\
    8 & 5 \\
\end{bmatrix},
B = \begin{bmatrix}
    2 & 1 \\
    0 & 3 \\
    1 & 1 \\
\end{bmatrix}
\\ A \circ B = \begin{bmatrix}
    1*2 & 0*1 \\
    3*0 & 2*3 \\
    8*1 & 5*1 \\
\end{bmatrix} =
\begin{bmatrix}
    2 & 0 \\
    0 & 6 \\
    8 & 5 \\
\end{bmatrix}
$$

### Vectors in code

#### Python example

```py
import numpy as np

# This defines a row vector
v = [1,2,3]

# This defines a matrix
A = [[1,2,3][4,5,6][7,8,9]]

# L_P-Norms of vectors are done by the following

print('L1 Norm: ',np.linalg.norm(v,ord=1))
print('L2 Norm: ',np.linalg.norm(v,ord=2))
print('L∞ Norm: ',np.linalg.norm(v,ord=np.inf))

# Python, in general, takes a different convention for matrix norms.
# Most will not do what you think they will from our notation.
# However, you can type the following for L_2 norms:

print(np.linalg.norm(A))
```

### Product Properties

Verify the fundamental algebraic laws of Distributivity, Associativity, and Commutativity, with regard to regular Matrix multiplication and the Hadamard product

#### Original Matrix Properties

- Distributivity

$$A(B+C) = AB + AC$$

- Associativity

$$A(BC) = (AB)C$$

- Not Commutativity

$$
A = \begin{bmatrix}
    1 \\ 1
\end{bmatrix}, B =
\begin{bmatrix}
    1 & 1
\end{bmatrix}
\\
AB = \begin{bmatrix}
    1\\ 1
\end{bmatrix}
\begin{bmatrix}
    1 & 1
\end{bmatrix} =
\begin{bmatrix}
    1 & 1 \\
    1 & 1 \\
\end{bmatrix}
\\
BA = \begin{bmatrix}
    1 & 1
\end{bmatrix}
\begin{bmatrix}
    1\\ 1
\end{bmatrix} = 2
\\
AB \neq BA
$$

##### Identity Matrix

$$
\begin{bmatrix}
    1 & 0 & .. & 0  & 0 \\
    0 & 1 & .. & 0 & 0 \\
    ..& .. & .. & .. & ..\\
    0 & 0 &  .. & 1 & 0 \\
    0 & 0 &  .. & 0 & 1 \\
\end{bmatrix}
$$

#### Hadamard Matrix Properties

- Distributivity

$$A \circ (B+C) = A \circ B + A \circ C$$

- Associativity

$$A \circ (B \circ C) = (A \circ B) \circ C$$

- Commutativity

$$
A \circ B = B \circ A
$$

## Phase 3: Modeling

Problem is defined in a way that the algorithm can optimize. Uses geometry, probability, norms, and statistics. (Loss Functions)

### Geometry of Column Vectors

$\begin{bmatrix} v_1 \\ v_2\end{bmatrix}$ means moving $v_1$ in x-axis and moving $v_2$ in y-axis

#### Angel between vectors

$$
\theta = \text{arcos} \frac{\overrightarrow{v_1}.\overrightarrow{v_2}}{||v_1||_2.||v_2||_2}
$$
Example:
$$
\overrightarrow{v_1} = \begin{bmatrix}
    1 \\ 0 \\ -1 \\ 2
\end{bmatrix},
\overrightarrow{v_2} = \begin{bmatrix}
    3 \\ 1 \\ 0 \\ 1
\end{bmatrix}
\\ \theta = \frac{5}{\sqrt{6}.\sqrt{11}}= \frac{5}{\sqrt{66}}
$$

### Measures of Magnitude

#### Definition of Norm

It is the measure of distance for moving from one point to the other.

#### Properties of Norm

- All distances are non-negative.
    $$||\overrightarrow{v}||\geq0$$
- Distances multiply with scalar multiplication.
    $$||a\overrightarrow{v}||=||a||.||\overrightarrow{v}||$$
- Triangle Inequality. If I travel from A to B ($\overrightarrow{v}$) then B to C ($\overrightarrow{w}$), that is at least as far as going from A to C ($\overrightarrow{v}+\overrightarrow{w}$).
    $$||\overrightarrow{v}+\overrightarrow{w}|| \leq ||\overrightarrow{v}||+||\overrightarrow{w}||$$

#### Types of Norm

1. Euclidean ($L_2$ norm) Norm:
    $$\text{if }\overrightarrow{v} =\begin{bmatrix}
        v_1 \\
        v_2 \\
        ..\\
        v_n
    \end{bmatrix}
    \\ \text{Then, the length of }||\overrightarrow{v}||_2 = \sqrt{v_1^2+v_2^2+..+v_n^2} = \sqrt{\sum_{i=1}^n v_i^2}
    \\ \overrightarrow{v} = \begin{bmatrix} 4 \\ 3\end{bmatrix}
    \\ ||\overrightarrow{v}||_2 = \sqrt{4^2 + 3^2} = \sqrt{17}$$
2. $L_p$ norm:
    $$||\overrightarrow{v}||_p  = ({\sum_{i=1}^n |v_i|^p})^{1/p}; \text{where }|v_i|^p\geq0 , p\geq1
    \\ \overrightarrow{v} = \begin{bmatrix} 4 \\ 3\end{bmatrix}
    \\ ||\overrightarrow{v}||_p = (4^p + 3^p)^{1/p}$$
3. $L_1$ norm:  
    $$\text{for} L_p \text{where } p=1
    \\ ||\overrightarrow{v}||_1  = ({\sum_{i=1}^n |v_i|^1})^{1/1} = {\sum_{i=1}^n |v_i|}
    \\ \overrightarrow{v} = \begin{bmatrix} 4 \\ 3\end{bmatrix}
    \\ ||\overrightarrow{v}||_1 = {4 + 3} = 7$$
4. $L_\infin$ norm:
    $$\text{for} L_p \text{where } p=\infin
    \\ ||\overrightarrow{v}||_\infin  = ({\sum_{i=1}^n |v_i|^\infin})^{1/\infin}
    \\ \text{for} L_p \text{where } p\rightarrow \infin
    \\ ||\overrightarrow{v}||_\infin = \lim_{p \rightarrow \infin} ||\overrightarrow{v}||_p  = \lim_{p \rightarrow \infin}({\sum_{i=1}^n |v_i|^p})^{1/p}
    \\ ||\overrightarrow{v}||_\infin \approxeq max_i |v_i|
    \\ \overrightarrow{v} = \begin{bmatrix} 5 \\ 10 \\ -2\end{bmatrix}
    \\ ||\overrightarrow{v}||_\infin = 10$$
5. $L_0$ norm:  
    Despite the name, this is not a norm. It is the number of non-zero elements in of the vector.
    $$ \overrightarrow{v} = \begin{bmatrix} 1 \\ 0 \\ 0\\-2 \\-5 \\ 0 \\10 \end{bmatrix}
    \\ ||\overrightarrow{v}||_0 = 4$$

### Probability

Probability enables machines to manage outcomes and outputs.

- The probability theory is used in machine learning models where the outcomes are:
  - Inherently random
  - Simply to be complex to be completely known
- In theory, outcomes can be predicted, but in real-time there are a huge number of factors that influence those outcomes.
- Intuition: The probability of an event is the expected fraction of time that the outcome would occur with repeated experiments.

#### Probability Terminologies

- Outcome: A single possibility of the experiment.
- Sample Space ($\Omega$) : The set of all possible outcomes.
- Event (E): Something that can be observed in the world with yes and no answer.
- Probability (P): Fraction of an Experiment where event occurs.

#### Axioms of probability

The three basic rules that every probability function satisfies

- Axiom #1:
  - The fraction of the times an event occurs is between 0 and 1.  
  $$
  P\{E\} \in [0,1]
  $$
- Axiom #2:
  - Something always happens.  
  $$
  P\{\Omega\} = 1
  $$
- Axiom #3:
  - If two events can't happen at the same time, then the fraction of the time that at least one of them occurs is the sum of the fraction of the time either one occurs separately.  
  $$
  P\{E_1 \cup E_2\} = P\{E_1\} + P\{E_2\}
  \\
  \text{when} E_1 \cap E_2 = \phi
  $$
  - Also works for any number of events (including countably infinite)
  $$
  P\{ \bigcup_i E_i \} = \sum_i{E_i}
  \\
  \text{when} E_1 \cap E_2 = \phi
  $$

#### Conditional probability

When you’re certain about the outcome of one event, conditional probability helps identify the fractional outcome of a second event.

- Definition
  - The probability of $E_1$ given $E_2$ is:
  $$
  P \{ E_1|E_2 \} = \frac{P \{E_1 \cap E_2\}}{P\{E_2\}}
  $$

#### Bayes’ rule

It describes the probability of an event, based on prior knowledge of conditions that might be related to the event.

$$
\frac{P(H_1 | D)}{P(H_2 | D)} = \frac{P(D | H_1)}{P(D | H_2)} . \frac{P(H_1)}{P(H_2)}
$$

#### Independent events

In machine learning, the model’s dependency can make it challenging to apply mathematical principles so it’s best to assume independence where possible

Definition: Two event are independent if one event doesn't influence the other.

#### Random variables

##### Discrete Random Variables

A function X that takes in an outcome and gives a number back. X takes at most countable many values. X will take only a finite set of values.

##### Expected Value

$$
\mu_x = E[X] = \sum_x x.P\{X=x\} = \sum_w X(w).P\{w\}
$$

Example: Flipping 4 coins and H is the random variable which gives the number of Heads. $H \in \{0,1,2,3,4\}$

$$
E[4]=\sum_x x.P\{H=x\}
\\ = 1.P\{H=1\} + 2.P\{H=2\} + 3.P\{H=3\} + 4.P\{H=4\}
\\= 1.\frac{4}{16} + 2.\frac{6}{16} + 3.\frac{4}{16} + 4.\frac{1}{16} = 2
$$

##### Variance

It is the difference between the random variable and the mean of the whole population

$\sigma_x^2=E[(X-\mu_x)^2]=...=E[X^2]+\mu^2$

Flaw of variance is that its unit is not the same as the sample units.

##### Standard Deviation

$\sigma_x=\sqrt{\sigma_x^2}$

#### Chebyshev’s inequality

For any random variable X (no assumptions) at least 99% of the time $X \in [\mu_x-10\sigma_x,\mu_x+10\sigma_x$]

#### Entropy

How to define the randomness of a random variable using entropy, and how entropy changes when bit size is altered.

Example:

A coin flipped, if the outcome is Head then no more flipping but if the outcome is Tails then one more flip occurs. As to be all possible as below:

$$
\Omega =\{H, TH, TT \},
\\ P\{H\} = \frac{1}{2},
\\ P\{TH\} = \frac{1}{4},
\\ P\{TT\} = \frac{1}{4}
$$
So we can get number of coin flips from the probabilities. In such that $P=\frac{1}{2^n}$, therefore $n = - \log_2(p)$
$$
\text{Entropy} = E[ \text{no. coin flips}] = H = - \sum_i p_i \log_2(p_i)
$$
And for units more than 2 sides (coins):

$$
H = \frac{1}{\log_2(k)}. (- \sum_i p_i \log_2(p_i));
$$
where $k$ is the number of possible outcomes, 2 for coins, 6 for die

#### Continuous random variables and probability density function

Whether you’re rolling a die or flipping a coin, you have a finite set of outcomes—but that’s not the case in the real world. So describe continuous random variables by using the probability distribution function.

#### Building machine learning models

## Phase 4: Optimization

This is where you iterate until certain conditions are met, and then you choose the best Model. Uses vector calculus.

### Maximum Likelihood Estimation

It finds the maxima which is the probability of the data at parameter D is maximized. In other words, what is the highest probability.

### Derivatives

It measures how much you change your inputs, gets amplified in change of the output.

### Common Derivatives

- Most ML tasks thankfully need comparatively few derivatives.

| Value           | Derivative                                                    |
| --------------- | ------------------------------------------------------------- |
| $f$             | $f\prime = \frac{df}{dx} = \frac{d}{dx}f = \partial_xf = f_x$ |
| $(n\neq 0) x^n$ | $nx^{n-1}$                                                    |
| $e^x$           | $e^x$                                                         |
| $(x>0) \log(x)$ | $\frac{1}{x}$                                                 |

### Derivative Rules

#### Sum Rule

$$[f(x) + g(x)]\prime = f\prime(x)+g\prime(x)$$

- Example:

$$\frac{d}{dx}[x^2+e^x]=2x+e^x$$

#### Product Rule

$$[f(x) . g(x)]\prime = f(x)g\prime(x)+f\prime(x)g(x)$$

- Example:

$$\frac{d}{dx}[x^2e^x]=2xe^x+x^2e^x$$

#### Chain Rule

$$[f(g(x))]\prime = f\prime(g(x)) g\prime(x)$$
$$\frac{df}{dx}=\frac{df}{dg}.\frac{dg}{dx}$$

- Example:

$$\frac{d}{dx}[e^{x^2}]=e^{x^2}2x$$

### Second Derivative

It shows how the slope is changing at the function position

$$
 f\prime > 0, f \text{ is locally increasing}
\\ f\prime < 0, f \text{ is locally decreasing}
\\ f\prime = 0, \text{ then if }
\\ f\prime\prime > 0 , f \text{ has a local minimum}
\\ f\prime\prime < 0 , f \text{ has a local maximum}
\\ f\prime\prime = 0 , \text{ can't tell}
$$

### Gradient Descent

Definition:

- To Minimize $f(x)$
  - Start with a given $x_0$
  - Iterate $x_{i+1}=x_i-\eta f\prime(x_1)$
  - Stop after some condition is met
    - If the value of x doesn't change by more than 0.001.
    - After a fixed number of steps.
    - Fancier things to.

Example:

Let's minimize $f(x) = e^x-x$ with an initial guess of $x_0 = 1$ and learning rate of $\eta = \frac{1}{2}$

$$
f\prime(x_1) = e^x-1 \text{ when it will be zero, } e^x=1, x=\log(1)=0
\\x_{i+1}=x_i-\eta f\prime(x_1) =x_i-\eta (e^{x_i}-1)
\\x_1 = x_0 - \eta (e^{x_0}-1) = 1 - \frac{1}{2}(e^{x_0}-1) = 1
\\x_0 = 1
\\x_1 \approx 0.14
\\x_2 \approx 0.065
\\x_3 \approx 0.032
\\x_4 \approx 0.016
$$

Note: The error is cut roughly in half each time, which means that each step essentially gives one more correct digit

The issue is in choosing the proper learning rate $\eta$ as improper chosen learning rate will cause the entire optimization procedure to either fail or operate too slowly to be of practical use

### Newton's method

- Same of objective of Gradient Descent is to minimize $f$
  - Look for an algorithm to find the zero of some function $g(x)$
  - Apply that algorithm to $f\prime(x)$
  - To find Zero of function $x_{i+1} = x_i - \frac{g(x_i)}{g\prime(x_i)}$
  - To find minimize a function $x_{i+1} = x_i - \frac{f\prime(x_i)}{f\prime\prime(x_i)}$

Example:

Let's minimize $f(x) = e^x-x$ with an initial guess of $x_0 = 1$

$$
f\prime(x_1) = e^x-1, f\prime\prime=e^x
\\x_{i+1} = x_i - \frac{f\prime(x_i)}{f\prime\prime(x_i)} = x_i - \frac{e^{x_i}-1}{e^{x_i}} = x_i - 1 + e^{-x_i}
\\x_1 = x_0 - 1 + e^{-x_0} = 1 -1 + 0.36
\\x_0 = 1
\\x_1 \approx 0.35
\\x_2 \approx 0.060
\\x_3 \approx 0.0018
\\x_4 \approx 0.0000016
$$

Note: in this case, the number of correct digits approximately doubles.

### Multivariate Derivative

This about how to apply derivative to a multivariate function

#### Partial Derivative

It is the derivative of one variable while considering the other variables as constant

Example:

$$
f(x,y) = e^{x^2+\sqrt{y}}
\\ \frac{\partial f}{\partial x} = e^{x^2+\sqrt{y}} .2x
\\ \frac{\partial f}{\partial y} = e^{x^2+\sqrt{y}} . \frac{1}{2\sqrt{y}}
$$

#### Gradient



## References

1. [LaTex reference](https://en.wikipedia.org/wiki/List_of_mathematical_symbols_by_subject)