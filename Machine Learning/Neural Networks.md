# Neural Networks

- [Neural Networks](#neural-networks)
  - [Neural Network Architecture](#neural-network-architecture)
  - [Neural networks pros and cons](#neural-networks-pros-and-cons)
  - [Build and Train a Neural Network](#build-and-train-a-neural-network)
    - [1. Forward Propagation/Pass](#1-forward-propagationpass)
    - [2. Cost (error) functions](#2-cost-error-functions)
    - [3. Back Propagation](#3-back-propagation)
    - [4. Update network weights by applying the optimization algorithm method](#4-update-network-weights-by-applying-the-optimization-algorithm-method)
    - [5. Repeat](#5-repeat)
  - [Implementation](#implementation)
    - [NumPy library](#numpy-library)
    - [TensorFlow Framework](#tensorflow-framework)
  - [Debugging a neural network](#debugging-a-neural-network)
  - [Types of Neural Networks](#types-of-neural-networks)
    - [Perceptron](#perceptron)
    - [Convolutional Neural Networks](#convolutional-neural-networks)
    - [Recurrent Neural networks](#recurrent-neural-networks)
  - [Deep Learning Frameworks](#deep-learning-frameworks)
  - [References](#references)

## Neural Network Architecture

![Neural Network](NN%20images/Neural-Network-Architecture.png)

Function:

$$
a_j^{[l]} = \sigma(z^l) = \sigma(\sum_k w_{jk}^{[l]}.a_k^{[l-1]}+b_j^{[l]}) \\
a_j^{[l]} = \sigma(z^l) = \sigma(\overrightarrow{w}_j^{[l]}.\overrightarrow{a}^{[l-1]}+b_j^{[l]}) \tag{vectorized}
$$

Notations:

- $a$: Activation function
- $\sigma$: Nonlinear function. Like sigmoid.
- $z^l$: The weighted input to the neurons in layer $l$
- $l$: Layer number and denoted by a Superscript number between squared brackets
- $j$: Node number of $l^{th}$ layer and denoted by a subscript.
- $k$: Node number of $(l-1)^{th}$ layer and denoted by a subscript.
- $a_j^{[l]}$: Input vector of node $j$ in layer $l$.
- $a^{[l-1]}$: Output vector of layer $(l-1)$.
- $w$ & $b$: Parameters of layer $l$ node $j$
- If network has $s_{in}$ units in a layer and $s_{out}$ units in the next layer, then
  - $W$ will be of dimension $s_{in} \times s_{out}$.
  - $b$ will a vector with $s_{out}$ elements

Overview:

- A neural network consisting of input, hidden and output layers.
- Each layer is connected to the next layer.
- Input layer is a vector of numbers that are fed to the network.
- Hidden layers are one or more layers. Each layer contains number of nodes/neurons/units.
- Each node is one multivariate linear function, with an univariate nonlinear transformation (activation function).
- An activation function is applied on each hidden layer (and output layer).
- Activation Functions:
  - Rectified Linear Unit (ReLU):
    $$\displaystyle f(x) = \begin{cases}0, & \text{if $x < 0$} \\ x, & \text{if $x \geq 0$}\end{cases}$$
    - Most popular for hidden layers.
    - For Regression ML problems.
    - Anything less than 0, results in zero activation.
    - Faster in calculation.
    - Used for hidden and output layers.
  - Logistic (sigmoid):
    $$f(x) = \frac{1}{1+e^{-x}}$$
    - Popular for binary classification ML problems.
    - Slow due to exponential.
    - Squashes input to (0,1)
    - Cost function: Binary Cross Entropy
    - Used for hidden and output layers.
  - Softmax:
    $$a_j = f(x_j) = \frac{e^{x_j}}{{\sum}_{k=1}^N e^{x_k}}$$
    - Notations:
      - $N$: number of classes
      - $j$: class number
    - For Multi-class classification ML problems
    - Outputs probability for each class, in (0,1)
    - Sum of outputs of all classes are equal to 1 (probability distribution)
    - Cost function: Cross Entropy
    - Training drives target class values up, others down
    - Used for output layer. #Units/Nodes = #classes
  - Hyperbolic tangent (tanh):
    $$f(x) = \frac{e^x - e^{-x}}{e^x+e^{-x}}$$
    - Squashes input to (-1, 1).
    - Used for hidden layers
- Types of layers:
  - Dense layer
    - Every neuron/node/unit in the layer gets its inputs from all the previous layer's output.
  - Convolutional layer:
    - Each neuron only takes a part of the previous layer's output
    - It leads to faster computation and need less training data (less prone to overfitting)

## Neural networks pros and cons

- Can represent any non-linear function (very expressive)
- Generally hard to interpret.
- Expensive to train, fast to predict

## Build and Train a Neural Network

- Different activation/output functions can be chosen for different layers, don’t need to be the same, although all neurons in same layer will use same activation
- The activation functions are also hyperparameters of the NN, and need to be tuned by using a validation set, to figure out what choices perform best.
- The network is initialized with initial values for the neurons weights and biases.

### 1. Forward Propagation/Pass
  
- It is the step in which the inputs $X$ are passed through each layer of the network and get computed using layer's activation function, until it reaches the output.

### 2. Cost (error) functions

- It is where the outputs are compared to the true values to measure the performance of the NN with the current weights and biases.
- Cost function is selected according to the problem: Binary/Multi-class Classification or Regression.
  - Binary Cross entropy for logistic.
    - For Binary Classification problems:
    - A numeric value that measures the performance of a binary classifier when model output is a probability between 0 and 1
    $$
    J(\mathbf{w},b) = -\frac{1}{m} \left[ \sum_{i=1}^{m} \sum_{j=1}^{N}  1\left\{y^{(i)} == j\right\} \log \frac{e^{z^{(i)}_j}}{\sum_{k=1}^N e^{z^{(i)}_k} }\right]
    $$
    - Where $m$ is the number of examples, $N$ is the number of outputs. This is the average of all the losses.
  - Cross entropy for Softmax is used:
    - For Multi-class classification problems
    - Extends the cross entropy for sigmoid loss beyond two classes to multi-class classification
    - $C = -\frac{1}{n}{\sum_{examples}}\,{\sum_{classes} y_i \ln(p_i)}$
  - For Regression problems:
    - Mean Squared Error is used
    - $C = \frac{1}{n}{\sum_{examples}}(y-p)^2$

### 3. Back Propagation

- The goal of back-propagation is to adjust the weights and biases, of each layer, so that the NN output $a^L$ equals the true values $y$ or the cost function equals zero.
- This is done by going through each layer of the NN in reverse order. And then adjust the layer's weights and biases with a small amount that minimizes the error of the cost function.
- This can be done by understanding how a change in the weights will affect the cost. For example, if we increased $w^{[1]}$ with 1, how the cost will be affected. Will it increase or decrease and by how much?
- In other words, we need the derivative of the cost $C$ with respect to each parameter $w$ and $b$; $∂C/∂w$ and $∂C/∂b$. This can be achieved by two ways, direct derivative or chain rule
- Using direct derivative requires finding an equation that has a direct relation between the cost and the parameter and apply partial derivative to it. This way is too complex, especially with complex NNs.
  - To give some intuition, let's calculate the partial derivative to the below equations:
    $$
    \begin{align*}
    \frac{\partial{C}}{\partial{w^{[L]}}} &= \frac{1}{1+e^{-(w^La^{[L-1]}+b^L)}} \\
    \frac{\partial{C}}{\partial{w^{[L-1]}}} &= \frac{1}{1+e^{-(w^L (w^{L-1} a^{[L-2]}+b^{L-1})+b^L)}}
    \end{align*}
    $$
- While using chain rule, eliminates the need to find an equation with direct relation between the cost and the parameter. Instead, the derivative is split into intermediate ones that get multiplied together.
  - In the chain rule examples below (1),(2), they show that the derivative is chained together using intermediate relations.
  - By knowing the relations as:
    - Cost function: $C^l = \frac{1}{2}(y-a^L)^2$,
    - Activation function: $a^L = \sigma(z^L)$
    - and $z^{[L]}=w^{[L]}a^{[L-1]}+b^{[L]}$

    $$
    \begin{align}
    \frac{\partial{C}}{\partial{w^{[L]}}} & = \frac{\partial{C}}{\partial{a^{[L]}}} *\frac{\partial{a^{[L]}}}{\partial{z^{[L]}}}* \frac{\partial{z^{[L]}}}{\partial{w^{[L]}}} \\
    \frac{\partial{C}}{\partial{w^{[L-1]}}} & = \frac{\partial{C}}{\partial{a^{[L]}}} *\frac{\partial{a^{[L]}}}{\partial{z^{[L]}}}* \frac{\partial{z^{[L]}}}{\partial{a^{[L-1]}}}* \frac{\partial{a^{[L-1]}}}{\partial{z^{[L-1]}}}* \frac{\partial{z^{[L-1]}}}{\partial{w^{[L-1]}}}
    \end{align}
    $$

    - In the first equation, we need to find $\frac{\partial{C}}{\partial{w^{[L]}}}$, and by using the chain relation, C -> $a^{[L]}$ -> $z^{[L]}$ -> $w^{[L]}$.
    - In the second equation, we need to find $\frac{\partial{C}}{\partial{w^{[L-1]}}}$, and by using the chain relation, C -> $a^{[L]}$ -> $z^{[L]}$ -> $a^{[L-1]}$ -> $z^{[L-1]}$ -> $w^{[L-1]}$.
    - You may noticed that in the second equation, we didn't use $z^{[L]}$ -> $w^{[L]}$, instead we used $z^{[L]}$ -> $a^{[L-1]}$ as not to be blocked by $w$ and reach the weights of the previous layer through $a^{[L-1]}$.
    - You may also noticed that expression $\frac{\partial{C}}{\partial{a^{[L]}}} *\frac{\partial{a^{[L]}}}{\partial{z^{[L]}}}$ is duplicated in both equations. That is will give us a hint that already calculated derivatives will be reused again while calculating weights of a previous layer. This term is called error of $j$ neuron in $l$ layer and donated as $\delta^l_j$.
    - Moreover, since $z^{[L]}=w^{[L]}a^{[L-1]}+b^{[L]}$, then $\frac{\partial{z^{[L]}}}{\partial{w^{[L]}}}=a^{[L-1]}$
    - So, we could replace the above equations as

    $$
    \begin{align}
    \frac{\partial{C}}{\partial{w^{[L]}}} & = \delta^L * a^{[L-1]} \\
    \frac{\partial{C}}{\partial{w^{[L-1]}}} & = \delta^{L-1} * a^{[L-2]}
    \end{align}
    $$

    - Where $\delta^{[L-1]} = \delta^L *\frac{\partial{z^{[L]}}}{\partial{a^{[L-1]}}}* \frac{\partial{a^{[L-1]}}}{\partial{z^{[L-1]}}}$.
    - All these will be applied to the biases as well
  - So, using the chain rule we can deduce these important equations:
    $$
    \begin{align*}
    \delta^{[L]} & = (a^{[L]} - y^T) \\
    \delta^{[l]} & = ((w^{[l+1]})^T \cdot \delta^{[l+1]})*\sigma^\prime(z^{[l]}) \\
    \frac{\partial J}{\partial w^{[l]}} & = \sum^L_{l=1} \delta^{[l]} \cdot (a^{[l-1]})^T \\
    \frac{\partial J}{\partial b^{[l]}} & = \sum^L_{l=1} \delta^{[l]}
    \end{align*}
    $$

### 4. Update network weights by applying the optimization algorithm method

- Adjust the old value of a weight to a new value of the weight, by using optimization algorithm.
  - Optimization algorithms:
    - Gradient Descent
    - [Recommended] Adam: Adaptive Moment estimation
      - It uses same algorithm as Gradient Descent but adjusting the learning rate while training.
      - If cost is decreasing in a steady rate, then increase the learning rate to speed up the convergence.
      - If the cost is oscillating, then decrease the learning rate.
- Each weight will be updated based on its derivative according to this equation:
  - ${w}_{new} = {w}_{old} - learning\_rate * \frac{\partial{C}}{\partial{w}}$
  - ${b}_{new} = {b}_{old} - learning\_rate * \frac{\partial{C}}{\partial{b}}$
- Then moves backward through the network, slightly adjusting each of the weights in a direction that reduces the size of the error by a small degree.

### 5. Repeat

- Both forward and back propagation are re-run hundred/thousands of times on each input combination until the network can accurately predict the expected output of the possible inputs using forward propagation.

## Implementation

![Neural Network example](NN%20images/C2_W1_RoastingNetwork.PNG)

Steps:

1. Specify the model
2. Specify loss and cost functions
3. Train on data to minimize the cost function.

### NumPy library

```py
# Import libraries
import numpy as np

# Normalizing the data
def norm_l(x):
    units = W.shape[1]
    for j in range(units):    
        mu = np.mean(x[:,j])
        sigma = np.std(x[:,j])
        x[:,j] = (x[:,j] - mu)/sigma
    return x

Xn = norm_l(X)

# Define activation function Sigmoid
def g(z):
    return 1.0/(1.0+np.exp(-z))

# Create NN model

## Define the `my_dense()` forward propagation function which computes the activations of a dense layer.

### Using for loop
x = np.array([200, 17])
W = np.array([[1, -3, 5],
             [-2, 4, -6]])
b = np.array([-1, 1, 2])
def my_dense(a_in, W, b, act_fn):
    units = W.shape[1]
    a_out = np.zeros(units)
    for j in range(units):               
        w = W[:,j]                                    
        z = np.dot(w, a_in) + b[j]         
        a_out[j] = act_fn(z)               
    return a_out

### [More efficient] Using vectorization
x = np.array([[200, 17]]) # 2D array
W = np.array([[1, -3, 5],
             [-2, 4, -6]])
b = np.array([[-1, 1, 2]]) # 2D array
def my_dense(a_in, W, b, act_fn):
  z = np.matmul(A_in,W) + b # Matrix Multiplication
  a_out = act_fn(z)
  return a_out

## Define the `sequential` function that connects layers
def my_sequential(x, W1, b1, W2, b2):
    a1 = my_dense(x,  W1, b1, g)
    a2 = my_dense(a1, W2, b2, g)
    return(a2)

# Loss and cost functions

def compute_cost_logistic(X, y, w, b):
    m = X.shape[0]
    cost = 0.0
    for i in range(m):
        z_i = np.dot(X[i],w) + b
        f_wb_i = g(z_i)
        cost +=  -y[i]*np.log(f_wb_i) - (1-y[i])*np.log(1-f_wb_i)
             
    cost = cost / m
    return cost

# Training the model

def my_predict(X, W1, b1, W2, b2):
    m = X.shape[0]
    p = np.zeros((m,1))
    for i in range(m):
        p[i,0] = my_sequential(X[i], W1, b1, W2, b2)
    return(p)
```

### TensorFlow Framework

```py
# Import libraries
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

# Normalizing the data

## create a "Normalization Layer"
norm_l = tf.keras.layers.Normalization(axis=-1)

## learns the mean and variance of the data set and saves the values internally.
norm_l.adapt(X)

## normalize the data
Xn = norm_l(X)

# Create TensorFlow model

## The `tf.keras.Input(shape=(2,)),` specifies the expected shape of the input. This allows Tensorflow to size the weights and bias parameters at this point.  This is useful when exploring Tensorflow models. This statement can be omitted in practice and Tensorflow will size the network parameters when the input data is specified in the `model.fit` statement.

model = Sequential(
    [
        tf.keras.Input(shape=(2,)),
        Dense(3, activation='sigmoid', name = 'layer1'),
        Dense(1, activation='sigmoid', name = 'layer2')
     ]
)

# provides a description of the network
model.summary()

# Get layers weights initiated by Tensorflow model
W1, b1 = model.get_layer("layer1").get_weights()
W2, b2 = model.get_layer("layer2").get_weights()

# define a loss function and specifies compile optimization
model.compile(
    loss = tf.keras.losses.BinaryCrossentropy(),
    optimizer = tf.keras.optimizers.Adam(learning_rate=0.01),
)

# runs gradient descent and fits the weights to the data
## Epochs is the number of steps in gradient descent.
model.fit(Xn,y,epochs=10)

# Check layers weights after fitting
W1, b1 = model.get_layer("layer1").get_weights()
W2, b2 = model.get_layer("layer2").get_weights()

# Predictions
## Normalize the test data `X_test`
X_testn = norm_l(X_test)
## Predict
predictions = model.predict(X_testn)
```

## Debugging a neural network

- A quick trick that is not always applicable
  - If the model is not doing well on the training set $J_{train}$, then enlarge the network.
  - If the model is not doing well on the cross validation set $J_{cv}$, then get more data.
- Large neural networks, with a **well-chosen regularization**, will usually do as well as or better than a smaller one. The only caveat is the computation cost.
- Regularization in TensorFlow `tf.Dense(units=10,activation='relu',kernel_regularizer=L2(0.01))`

## Types of Neural Networks

### Perceptron

- It is the simplest neural network.
- It is a single layer neural network that uses one layer of a list of input features and one output.
- One of the features is a bias, same as intercept in linear regression, that gets combined a long with the other features.
- After having this linear combination, an activation function is applied. This function is usually non-linear and depends on the problem being tried to solve.

### Convolutional Neural Networks

- It is very useful in image analysis
- The input is an image or a sequence of images.
- Kernel is used as filter to extract local features.

### Recurrent Neural networks

- It consists of multiple inputs layer, multiple hidden layers and multiple output layer.
- Each node outputs to the next input node.

## Deep Learning Frameworks

- MXNet
- TensorFlow
- Caffe
- PyTorch

## References

- [AWS ML University](https://www.youtube.com/watch?v=xUxw6C_z2kA&list=PL8P_Z6C4GcuWfAq8Pt6PBYlck4OprHXsw&index=8) and its [repo](https://github.com/aws-samples/aws-machine-learning-university-accelerated-nlp)
- Machine learning specialization by Andrew Ng
- [Backpropagation calculus | Chapter 4, Deep learning - YouTube](https://www.youtube.com/watch?v=tIeHLnjs5U8)
- [Lecture 12 - Backprop & Improving Neural Networks | Stanford CS229: Machine Learning (Autumn 2018) - YouTube](https://www.youtube.com/watch?v=zUazLXZZA2U)
- [Neural networks and deep learning](http://neuralnetworksanddeeplearning.com/chap2.html)
- [Proof of derivative for the sigmoid function](https://math.stackexchange.com/questions/78575/derivative-of-sigmoid-function-sigma-x-frac11e-x)
