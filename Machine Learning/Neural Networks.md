# Neural Networks

- [Neural Networks](#neural-networks)
  - [Neural Network Architecture](#neural-network-architecture)
## Neural Network Architecture

![s](NN%20images\Neural-Network-Architecture.png)

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

