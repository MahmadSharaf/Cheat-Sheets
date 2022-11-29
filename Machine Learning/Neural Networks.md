# Neural Networks

- [Neural Networks](#neural-networks)
  - [Neural Network Architecture](#neural-network-architecture)
  - [Neural networks pros and cons](#neural-networks-pros-and-cons)
  - [Build and Train a Neural Network](#build-and-train-a-neural-network)
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

## Neural networks pros and cons

- Can represent any non-linear function (very expressive)
- Generally hard to interpret.
- Expensive to train, fast to predict

## Build and Train a Neural Network

- Different activation/output functions can be chosen for different layers, don’t need to be the same, although all neurons in same layer will use same activation
- The activation functions are also hyperparameters of the NN, and need to be tuned by using a validation set, to figure out what choices perform best.
- Steps to train the NN:
  - The network is initialized with initial values for the neurons weights.
  - Forward Propagation/Pass:
    - It is the step in which the inputs are passed through each layer of the network and get computed, until it reaches the output.
  - Cost (error) functions:
    - It is where the outputs are compared to the true values.
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
    - Cost function is selected according to problem: Binary/Multi-class Classification or Regression.
  - Back Propagation:
    - The goal of back-propagation is to compute the partial derivatives $∂C/∂w$ and $∂C/∂b$ of the cost function C with respect to any weight w or bias b in the network.
    - The back propagation algorithm begins by comparing the actual NN output by the forward pass/forward propagation process to the expected value (target).
    - Calculate new weights to minimize the cost.
      - Adjust the old value of a weight to a new value of the weight, by using optimization algorithm.
        - Optimization algorithms:
          - Gradient Descent
          - [Recommended] Adam: Adaptive Moment estimation
            - It uses same algorithm as Gradient Descent but adjusting the learning rate while training.
            - If cost is decreasing in a steady rate, then increase the learning rate to speed up the convergence.
            - If the cost is oscillating, then decrease the learning rate.
      - This can be done by understanding how a change in the weights will affect the cost. For example, if we increased $w^{[1]}$ with 1, how the cost will be affected. Will it increase or decrease and by how much?
      - In other words, we need the derivative of the cost with respect to each parameter. This can be achieved by two ways, direct derivative or chain rule
      - Using direct derivative requires finding an equation that has a direct relation between the cost and the parameter and apply partial derivative to it. This way is too complex, especially with complex NNs.
        - To give some intuition, do partial derivative to the below equations:
        $$
        \begin{align*}
        \frac{\partial{C}}{\partial{w^{[L]}}} &= \frac{1}{1+e^{-(w^La^{[L-1]}+b^L)}} \\
        \frac{\partial{C}}{\partial{w^{[L-1]}}} &= \frac{1}{1+e^{-(w^L (w^{L-1} a^{[L-2]}+b^{L-1})+b^L)}}
        \end{align*}
        $$
      - While using chain rule, eliminates the need to find an equation with direct relation between the cost and the parameter.
      - Instead, the derivative is split into intermediate ones that get multiplied together.
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

      - In the first equation, we need to find $\frac{\partial{C}}{\partial{w^{[L]}}}$, and by using the chain relation, C -> $a^{[L]}=\hat{y}$ -> $z^{[L]}$ -> $w^{[L]}$.
      - In the second equation, we need to find $\frac{\partial{C}}{\partial{w^{[L-1]}}}$, and by using the chain relation, C -> $a^{[L]}=\hat{y}$ -> $z^{[L]}$ -> $a^{[L-1]}$ -> $z^{[L-1]}$ -> $w^{[L-1]}$.
      - You may noticed that in the next equation, we didn't use $z^{[L]}$ -> $w^{[L]}$, instead we used $z^{[L]}$ -> $a^{[L-1]}$ as not to be blocked be $w$ and reach the weights of the previous layer through $a$.
      - You may also noticed that expression $\frac{\partial{C}}{\partial{a^{[L]}}} *\frac{\partial{a^{[L]}}}{\partial{z^{[L]}}}$ is duplicated in both equations. That is will give us a hint that already calculated derivatives will be reused again while calculating weights of a previous layer. This term is called error of $j$ neuron in $l$ layer and donated as $\delta^l_j$.
      - Moreover, since $z^{[L]}=w^{[L]}a^{[L-1]}+b^{[L]}$, then $\frac{\partial{z^{[L]}}}{\partial{w^{[L]}}}=a^{[L-1]}$
      - So, We could replace the above equations as

      $$
      \begin{align}
      \frac{\partial{C}}{\partial{w^{[L]}}} & = \delta^L * a^{[L-1]} \\
      \frac{\partial{C}}{\partial{w^{[L-1]}}} & = \delta^L * \delta^{L-1} * a^{[L-2]}
      \end{align}
      $$

      - $\delta^l_j = \frac{\partial{C}}{\partial{a^{[L]}}} *\frac{\partial{a^{[L]}}}{\partial{z^{[L]}}} = \nabla_a C \odot \sigma'(z^L)$ This is a more matrix-based form in which $\nabla_a C$ is the rate of change of $C$ with respect to the output activations, and $\sigma'(z^L)$ is exactly the same as $\frac{\partial{a^{[L]}}}{\partial{z^{[L]}}}$ because $a=\sigma(z^L)$ and $`$ means prime or derivative.

    - Update network weights by applying the optimization algorithm method.
      - Each weight will be updated based on its derivative according to this equation: ${w}_{new} = {w}_{old} - learning\_rate * \frac{\partial{C}}{\partial{w}}$
      - All these will be applied to the biases as well
    - Then moves backward through the network, slightly adjusting each of the weights in a direction that reduces the size of the error by a small degree.
- Both forward and back propagation are re-run hundred/thousands of times on each input combination until the network can accurately predict the expected output of the possible inputs using forward propagation.
