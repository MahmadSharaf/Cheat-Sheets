# Machine Learning models

- [Machine Learning models](#machine-learning-models)
  - [Supervised Machine Learning Algorithms](#supervised-machine-learning-algorithms)
    - [Linear Models](#linear-models)
      - [Linear Regression](#linear-regression)
        - [Model equation](#model-equation)
        - [Cost functions](#cost-functions)
        - [Estimating parameters $\hat{b},\hat{w}$](#estimating-parameters-hatbhatw)
        - [Linear Regression Cons](#linear-regression-cons)
      - [Polynomial Regression](#polynomial-regression)
      - [Logistic Regression](#logistic-regression)
      - [Support Vector Machines (SVM)](#support-vector-machines-svm)
        - [SVM Error function](#svm-error-function)
        - [Kernelized Support Vector Machines (KSVMs) (Polynomial kernel)](#kernelized-support-vector-machines-ksvms-polynomial-kernel)
        - [Radial Basis Functions (RBF) kernel](#radial-basis-functions-rbf-kernel)
        - [SVM Hyperparameters](#svm-hyperparameters)
        - [SVM python libraries](#svm-python-libraries)
        - [SVM Pros and Cons](#svm-pros-and-cons)
        - [SVM extra resources](#svm-extra-resources)
      - [Decision tree](#decision-tree)
      - [Random Forest](#random-forest)
    - [Neural Networks](#neural-networks)
      - [Perceptron](#perceptron)
      - [Neural network architecture](#neural-network-architecture)
      - [Convolutional Neural Networks](#convolutional-neural-networks)
      - [Recurrent neural networks](#recurrent-neural-networks)
    - [K-nearest neighbor](#k-nearest-neighbor)
    - [Naive Bayes](#naive-bayes)
      - [Bayes Theorem](#bayes-theorem)

## Supervised Machine Learning Algorithms

The supervised aspect refers to the need for each training example to have a label in order for the algorithm to learn how to make accurate predictions on future examples.
This is in contrast to unsupervised machine learning where we don't have labels for the training data examples, and we'll cover unsupervised learning in a later part of this course.

### Linear Models

- Linear models make strong assumptions about the structure of the data.
- The target value can be predicted just using a weighted sum of the input variables, a linear function.
- It can get stable, but potentially inaccurate predictions.

#### Linear Regression

##### Model equation

$$\begin{align*}
f_{w,b}(x) &= \hat{y} \newline
f_{w,b}(x) &= \hat{w_1}x_1 + \hat{w_2} x_2 + ... \hat{w_n} x_n + \hat{b} \newline
f_{w,b}(x) &= \sum_{j=1}^{n}(w_jx_j)+\hat{b} \newline
f_{w,b}(x) &= \overrightarrow{w} . \overrightarrow{x} + \hat{b} \newline
\end{align*}$$

- Notations:
  - The hat(^) is an indication that the parameter is estimated during training process.  
  - **$f(x)$**: The hypothesis or the model function that used to predict an estimated output $\hat{y}$ of the input features $x$.
  - **$\hat{y}$**: the predicted output.  
  - **$x$**: the input features.  
  - **$\hat{w}$**: parameter: the model coefficients or feature weights.  
  - **$\hat{b}$**: parameter: the biased term or intercept of the model.
  - **$n$**: the number of features.  
  - **$x_j,w_j$**: the value and weight of $j^{th}$ feature.
  - $\overrightarrow{w} = [w_1 \space w_2 \space w_3 ... w_n] \newline$
  - $\overrightarrow{x} = [x_1 \space x_2 \space x_3 ... x_n] \newline$
  - **$\overrightarrow{w} . \overrightarrow{x}$**: It is the dot product of vectors $w$ and $x$.

- Impact of changing the values:
  - If we increase $\hat{w}$, we increase the slope so the line rotates counterclockwise.
  - If we decrease $\hat{w}$, we decrease the slope so the line rotates clockwise.
  - If we increase $\hat{b}$, the line maintains its slope but moves up.
  - If we decrease $\hat{b}$, the line maintains its slope but moves down.

- It can be coded using loop or vectorization.
  - `numpy` function uses parallel hardware to efficiently calculate the dot product.

  ```py
  # For loop
  f=0

  for j in range(n):
    f = f + w[j] * x[j]
    f = f + b

  # Vectorization
  import numpy as np
  f = np.dot(w,x) + b
  ```

##### Cost functions

- **MSE** (Mean Squared Error)
  $$J(w,b) = \frac{1}{2m}\sum_{i=1}^{m}​(\hat{y}^{(i)}−y^{(i)}​)^2$$

  - Notations:
    - $J(w,b)$: Cost function
    - $m$: number of points in dataset
    - $y^{(i)}$: actual target value
    - $\hat{y}^{(i)}$: predicted target value

  ```py
  def compute_cost(X, y, w, b): 
    """
    compute cost
    Args:
      X (ndarray (m,n)): Data, m examples with n features
      y (ndarray (m,)) : target values
      w (ndarray (n,)) : model parameters  
      b (scalar)       : model parameter
      
    Returns:
      cost (scalar): cost
    """
    m = X.shape[0]
    cost = 0.0
    for i in range(m):                                
        f_wb_i = np.dot(X[i], w) + b           #(n,)(n,) = scalar (see np.dot)
        cost = cost + (f_wb_i - y[i])**2       #scalar
    cost = cost / (2 * m)                      #scalar    
    return cost
  ```

##### Estimating parameters $\hat{b},\hat{w}$

- They are estimated from training the data.
- There are different methods correspond to different 'fit' criteria and goals and ways to control complexity.
- `Squared loss function` returns the squared difference between the target value and the  actual value as the penalty.
- The learning algorithm then computes or searches for the set of $\hat{w},\hat{b}$ parameters that optimize an objective function, typically to minimize the total of this loss function over all training points.
- Ways to estimate the parameters:
  
  1. Gradient descent:
  $$
  \begin{align*}
  \text{repeat}&\text{ until convergence:} \; \lbrace \newline\;
  & w_j = w_j -  \alpha \frac{\partial J(\mathbf{w},b)}{\partial w_j}  \; & \text{for j = 1..n}\newline
  &b\ \ = b -  \alpha \frac{\partial J(\mathbf{w},b)}{\partial b}  \newline \rbrace \\ \\
  \frac{\partial J(\mathbf{w},b)}{\partial w_j}  & = \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})x_{j}^{(i)} \\
  \frac{\partial J(\mathbf{w},b)}{\partial b} & = \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})
  \end{align*}
  $$
     - where:
       - $f_{\mathbf{w},b}(\mathbf{x}^{(i)})$ is the model's prediction
       - $y^{(i)}$ is the target value
       - $m$ is the number of training examples in the data et
       - $n$ is the number of features.
       - parameters $w_j$,  $b$, are updated simultaneously parameter.
       - $\alpha$: the learning rate.
       - $\frac{\partial f}{\partial w}J(w,b)$: derivative of the cost function.
     - It is the searching for the Minima by taking a step into the direction where the point on the graph with negative gradient. Until it finds a positive gradient, then it reverses the direction to another point where has negative gradient. This process repeats until convergence (the Minima is found).
     - In other words, an equation is calculated which is the derivative of the plot when it is equals to zero. Which is the point where the slope of the tangent line is neither increases nor decreases.
     - Minima is the minimum point between loss and parameters or the point with the least amount of error.
     ![Minima](ML%20images/Error_Parameter_plot.png)
     - It is often that there might more than one local Minima, in which the model might get stuck in local Minima instead of the Global Minima.
   ![Global Minima](ML%20images/Error_Parameter_plot_Global_Minima.png)
     - Ways to find the Global Minima:
       - Comparing all possible values which is inefficient way.
       - (Batch) Gradient Descent  
       ![Gradient Descent](ML%20images/Gradient%20Descent.png)
         - Learning Rate:
           - It is how big is the step to be taken.
           - If it too big, the local Minima will be hard to be found.
           - If it too small, it will take too much time to be found.
         - How to choose the learning rate $\alpha$.
           - The objective is to choose the learning rate that decreases the cost function rapidly and consistently.
           1. Start with a small value. Ex: 0.001
           2. Run the gradient descent for a handful of iterations (steps). ex: 10 or 50
           3. Check that the gradient descent is working properly.
              1. [Recommended] By either plotting the value of cost in each iteration.
              2. By automatic convergence test. In which if the the cost function decreases by $\epsilon$ or less, then declare convergence and no further improvement is required. $\epsilon$ can be chosen as 1% of the acceptable cost function (tolerance for prediction error).
           4. Update the learning rate till convergence.
              1. If the cost function is increasing, we know that gradient descent is diverging, so we need a lower learning rate.
              2. While if the cost function is decreasing slowly, we need to increase the learning rate by 3 times. Ex: 0.003
         - Drawbacks:
           - Updates the parameters only after a pass through all the data (one epoch)
           - Can't be used when data is too large to fit entirely in memory.
           - Can get stuck at local Minima or fail to reach Global Minima.
       - Stochastic Gradient Descent:
         - It is the same as gradient descent except that the weights is updated at every data point.
         - It is very fast to converge.
         - The drawback is that it is very noisy, in such that the steps might be in several directions.
       - Mini-Batch Gradient Descent:
         - It uses mini batch of records, and then the parameters is updated.
         - It is slower than SGD but faster than Gradient Descent.
         - It doesn't consume much memory as SGD
       - Gradient Descent Variations:  
       ![Gradient Descent Variations](ML%20images/Gradient_Descent_Variations.png)

      ```py
      from sklearn.linear_model import SGDRegressor
      from sklearn.preprocessing import StandardScaler

      scaler = StandardScaler()
      X_norm = scaler.fit_transform(X_train)

      sgdr = SGDRegressor(max_iter=1000)
      sgdr.fit(X_norm, y_train)
      ```

  2. Ordinary Least Squares (OLS):
      $$
      RSS(w, b) = \sum_{i=1}^N(y_i - (w . x_i + b))^2
      $$
      - The most popular way to estimate $w$ and $b$ parameters is using what's called least-squares linear regression or ordinary least-squares.
      - Least-squares finds the values of $w$ and $b$ that minimize the total sum of squared differences between the predicted $\hat{y}$ value and the actual $y$ value in the training set. Or equivalently it minimizes the mean squared error of the model.
      - This technique is designed to find the slope, the $w$ value, and the $b$ value of the y-intercept, that minimize this squared error, this mean squared error.
      - The mean squared error is the square difference between predicted and actual values, and then all these are added up, and then divided by the number of training points, take the average, that will be the mean squared error of the model.
      - One thing to note about this linear regression model is that there are no parameters to control the model complexity. No matter what the value of $w$ and $b$, the result is always going to be a straight line. This is both a strength and a weakness of the model.

        ```python
        from sklearn.linear_model import LinearRegression

        X_train, X_test, y_train, y_test=train_test_split(X, y, random_state=0)

        linreg = LinearRegression().fit(X_train,y_train)

        # w_i: coefficients
        linreg.coef_
        # b: the intercept term
        linreg.intercept_

        # In Scikit-Learn object attribute ends with an underscore, 
        # this means that this attribute is derived from the training data,
        # not quantities that set by the user.
        ```

  3. Ridge Regression:
      $$
      RSS_{RIDGE}(w,b) = \sum_{i=1}^N (y_i - (w . x_i + b))^2 + \alpha \sum_{j=1}^p w_j^2
      $$
      - Ridge regression uses the same least-squares criterion, but with one difference. During the training phase, it adds a penalty for large feature weights in w parameters.
      - Once the parameters are learned, its prediction formula is the same as ordinary least-squares.
      - The addition of a parameter penalty is called regularization. Regularization prevents overfitting by restricting the model, typically to reduce its complexity.
      - It uses L2 regularization: minimize sum of squares of w entries.
      - If ridge regression finds two possible linear models that predict the training data values equally well, it will prefer the linear model that has a smaller overall sum of squared feature weights.
      - The amount of regularization to apply is controlled by the alpha parameter. Larger alpha means more regularization and simpler linear models with weights closer to zero.(default 1.0)

        ```python
        from sklearn.preprocessing import MinMaxScaler
        scaler = MinMaxScaler()

        from sklearn.linear_model import Ridge
        X_train, X_test, y_train, y_test =train_test_split(X_crime, y_crime,random_state=0)

        X_train_scaled = scaler.fit_transform(X_train)
        X_test_scaled = scaler.transform(X_test)

        linridge = Ridge(alpha = 20.0).fit(X_train_scaled, y_train)
        ```

  4. Lasso Regression
      $$
      RSS_{LASSO}(w,b) = \sum_{i=1}^N (y_i - (w . x_i + b))^2 + \alpha \sum_{j=1}^p |w_j|
      $$
      - Like ridge regression, lasso regression adds a regularization penalty term to the ordinary least-squares  objective, that causes the model W-coefficients to shrink towards zero.
      - Lasso regression is another form of regularized linear regression that uses an L1 regularization penalty  for training (instead of ridge's L2 penalty).
      - L1 Penalty: minimizes the sum of the absolute values of the coefficients.
      - This has the effect of setting parameter weights in w to zero for the least influential variables. This  called a sparse solution: a kind of feature selection.
      - The parameter alpha controls the amount of L1 regularization (default = 1.0).
      - The prediction formula is the same as ordinary least-squares.

        ```python
        from sklearn.preprocessing import MinMaxScaler
        scaler = MinMaxScaler()

        from sklearn.linear_model import Lasso
        X_train, X_test, y_train, y_test = train_test_split(X_crime, y_crime,random_state=0)

        X_train_scaled = scaler.fit_transform(X_train)
        X_test_scaled = scaler.transform(X_test)

        linlasso = Lasso(alpha = 2.0, max_iter =10000) .fit(X-train_scaled, y_train)
        ```

- When to use ridge vs lasso:
  - Many small/medium sized effects: use ridge.
  - Only a few variables with medium/large effect: use lasso.

##### Linear Regression Cons

1. Linear Regression Works Best When the Data is Linear:
   - Linear regression produces a straight line model from the training data. If the relationship in the training data is not really linear, you'll need to either make adjustments (transform your training data), add features (we'll come to this next), or use another kind of model.
2. Linear Regression is Sensitive to Outliers
   - Linear regression tries to find a 'best fit' line among the training data. If your dataset has some outlying extreme values that don't fit a general pattern, they can have a surprisingly large effect.

#### Polynomial Regression

$$
\hat{y} = \hat{w_0}x_0^{n-1} + \hat{w_1} x_1^{n-2} + ... + \hat{w_n} x_n^{n-n} + \hat{b}
$$

- Notations:
  - The hat(^) is an indication that the parameter is estimated during training process.  
  - **$\hat{y}$**: the predicted output.  
  - **$\hat{w_i}$**: the model coefficients or feature weights.  
  - **$\hat{b}$**: the biased term or intercept of the model.

- It is used when the data requires a curve to be fit. Instead of considering lines, we consider higher degree polynomials. This would give us more weights to solve our problem.

#### Logistic Regression

- Model equation:

$$
\begin{align*}
z &= \overrightarrow{w} . \overrightarrow{x} + \hat{b} \newline
g(z) &= \frac{1}{1+e^{-z}} \newline
\hat{y} &= \frac{1}{1+e^{-(\overrightarrow{w} . \overrightarrow{x} + \hat{b})}}
\end{align*}
$$

- Overview:
  - It is a kind of generalized linear model.
  - In spite of being called a regression measure, it is actually used for classification
  - like ordinary least squares and other regression methods, logistic regression takes a set input variables, the features, and estimates a target value.
  - Unlike ordinary linear regression, in it's most basic form logistic repressions target value is a binary variable instead of a continuous value.
  - There are flavors of logistic regression that can also be used in cases where the target value to be predicted is a multi class categorical variable, not just binary.
  - Logistic regression is similar to linear regression, but with one critical addition. The logistic regression model still computes a weighted sum of the input features $\hat{x}_i$ and the intercept term $\hat{b}$ (like in linear regression), but it runs this result through a special non-linear function, sigmoid function $g(z)$.
  - The effect of applying the logistic function is to compress the output of the linear function so that it's limited to a range between 0 and 1.
  - The formula for the predicted output $\hat{y}$ which first computes the same linear combination $z$ of the inputs $\hat{x}_i$, model coefficient weights $\hat{w}_i$ and intercept $\hat{b}$, but runs it through the additional step of applying the logistic function $g(z)$ to produce $\hat{y}$.
  ![Flowchart box](ML%20images/Logistic%20Regression%20flow%20chart.jpg)
  - If we pick different values for $\hat{b}$ and the $\hat{w}$ coefficients, we'll get different variants of this S shaped logistic function, which again is always between 0 and 1. If $z$ value is a large positive number then $g(z)$ will be near 1, while if its value is a large negative number then $g(z)$ will be near 0.
- Interpretation of the output
  - The value of the logistic function $y$ is the probability in which the target equals to 1.
  - If $\hat{y} = 0.7$, then the target is 70% to be 1.
- Decision boundary:
  - It is the value on which decided to be 0 or 1. For example, if the $g(z)=0.5$, does this considered as class 0 or class 1.
  - So, a threshold is chosen above which identified as 1. For example, if the threshold is >= 0.5, then our prediction in the previous example $g(z)=0.5$ is equal to 1.
  - But $g(z) >= 0.5$ whenever $z>=0$ or when $(\overrightarrow{w} . \overrightarrow{x} + \hat{b}) >= 0$
  ![Decision boundary](ML%20images\logistic_regression_decission_boundry.png)

- Cost function:
  - Squared error cost used in Linear Regression is not suitable for Logistic Regression because the model equation $g(z)$ when applied to the cost function is non-convex, meaning it will have multiple local Minima.
![Logistic Regression loss function](ml%20images/C1_W3_SqErrorVsLogistic.png)
  - Instead this loss function can reach the global minimum.
    $$
    \begin{equation*}
      loss(f_{\mathbf{w},b}(\mathbf{x}^{(i)}), y^{(i)}) = \begin{cases}
        - \log\left(f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right) & \text{if $y^{(i)}=1$} \\
        - \log \left( 1 - f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right) & \text{if $y^{(i)}=0$}
      \end{cases}
    \end{equation*}
    $$
    ![Logistic Regression loss function](ml%20images/Logistic_regression_loss_function.png)

  - As shown in the above plot, the blue line, $-log(f)$, represents the cost for $y=1$. In such that, when the predicted value $f=1$, the cost equals zero. And when $f=0$, the cost equals to infinity. Same for orange line, $-log(1-f)$, which represents the cost for $y=0$.
  - The loss function above can be rewritten to be easier to implement:
    $$
    loss(f_{\mathbf{w},b}(\mathbf{x}^{(i)}), y^{(i)}) = (-y^{(i)} \log\left(f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right) - \left( 1 - y^{(i)}\right) \log \left( 1 - f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right)
    $$
  - The cost function using the above loss function
  $$
  J(\overrightarrow{w},b) = - \frac{1}{m}\sum^m_{i=1}[y^{(i)}\log(f(x))+(1-y{(i)})\log(1-f(x))]
  $$
- Estimating parameters $\hat{b},\hat{w}$:
  - Same gradient descent used in Linear Regression can be used for Logistic Regression.
  $$\begin{align*}
  &\text{repeat until convergence:} \; \lbrace \\
  &  \; \; \;w_j = w_j -  \alpha \frac{\partial J(\mathbf{w},b)}{\partial w_j}  \; & \text{for j := 0..n-1} \\
  &  \; \; \;  \; \;b = b -  \alpha \frac{\partial J(\mathbf{w},b)}{\partial b} \\
  &\rbrace
  \end{align*}$$
  - But the cost function, $J(\mathbf{w},b)$, will be for Logistic Regression instead.
  $$
  \frac{\partial J(\mathbf{w},b)}{\partial w_j}  = \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})x_{j}^{(i)}
  $$
  $$
  \frac{\partial J(\mathbf{w},b)}{\partial b}  = \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})
  $$
  - Although the derivative of the cost function is exactly the same for the one in Linear Regression, but the model equation $f_{\mathbf{w},b}(\mathbf{x}^{(i)})$ used is different. It has the sigmoid function $g(z) = \frac{1}{1+e^{-z}}$
- Implementation:
  - To perform logistic, regression in `Scikit-Learn`, you import the logistic regression class from the sklearn. linear model module, then create the object and call the fit method using the training data.

      ```python
      from sklearn.linear_model import LogisticRegression

      X_train, X_test, y_train, y_test = train_test_split(X, y, random_state = 0)
      
      clf = LogisticRegression(C=1).fit(X_train, y_train)
      ```

    - L2 regularization is 'on' by default (like ridge regression)
    - Parameter C controls amount of regularization (default 1.0)
    - As with regularized linear regression, it can be important to normalize all features so that they are on the same scale.

#### Support Vector Machines (SVM)

- Binary classification supervised algorithm
- Linear models are also used for classification, starting with binary classification.
- This approach uses the same linear functional form as for regression. But instead of predicting a continuous target value, we take the output of the linear function and apply the sine function to produce a binary output with two possible values, corresponding to the two possible class labels.
- Model quality can be measured in two ways:
  - By how many points it misclassifies or by rewarding classifiers for the amount of separation that can provide between the two classes (classifier margin). We can 'punish' the misclassified points, which means make them part of our **Classification Error**.
  - By how wide the margin is. The margin is the width that the decision boundary can be increased perpendicularly before hitting a data point. We also do not want any points in the margin, so we would 'punish' those points as well and include them in the **Margin Error**.

##### SVM Error function

- The total error is the Classification Error + Margin Error

- Classification Error can be measured as below:
  - The equation of the line is $Wx + b = 0$.
  - Since we don't just want a single line, we want the line with two extra lines that create the margin. And the equations for these lines are going to be $Wx + b = 1$ and $Wx + b = -1$
  - We look at the values of $Wx + b$. As we go up, it's going to be 1, 2, 3, 4, etc . And as we go down, it's going to be -1, -2, -3, etc. In order to build the error, we take the absolute value of those errors and translate it by one.
  - And we want to punish the points that are within the margin. So we will start at the margin line not the fitting line.
  ![Classification Error](ML%20images/svm-classification-error.png)

- Margin Error can be measured as below:
  - The margin is 2 divided by the norm of the vector W $\frac{2}{|W|}$. The norm of $W$ is the square root of the sum of the squares of the components of the vector.
  - The norm is in the denominator, which means that it is inversely proportion with to the margin.
  - The margin error is $|W|^2$. This is the exact same error that is given by the regularization term in L2 regularization.
  - So, the norm $|W|$ is the square root of the margin error.
  - Large margin means small margin error. And small margin means large margin error.

- The total error can be minimized using gradient descent.

##### Kernelized Support Vector Machines (KSVMs) (Polynomial kernel)

- It is a very powerful extension of linear support vector machines, it can provide more complex models that can go beyond linear decision boundaries.
- SVMs can be used for both classification and regression.
- One way to think about what kernelized SVMs do, is they take the original input data space and transform it to a new higher dimensional feature space, where it becomes much easier to classify the transform to data using a linear classifier. (eg. instead of $y(x)$ it became $y(x^2)$ like polynomial feature).  
![example](ML%20images/SVM&#32;1-dim&#32;to&#32;2-dim.jpg)  
The above figure shows at the right that the points can be separated by a straight line after converting it to a two dimensional space, while on the left is the original one dimensional points in which the straight line is converted to a parabola.

##### Radial Basis Functions (RBF) kernel

- It is a kernel function that is used to find a non-linear classifier or regression line.
- Kernel Function is used to transform n-dimensional input to m-dimensional input, where m is much higher than n, then find the dot product in higher dimensional efficiently.
- The purpose of a ‘kernel trick’ is to project the original points into some new dimensionality such that it becomes easier to separate through simple linear methods.
- RBF kernels are the most generalized form of kernelization and is one of the most widely used kernels due to its similarity to the Gaussian distribution.
- A good explanation in [Medium article](https://towardsdatascience.com/radial-basis-function-rbf-kernel-the-go-to-kernel-acf0d22c798a)

##### SVM Hyperparameters

- **C regularization parameter**:
  - How tolerant the support vector machine is of misclassifying training points, as compared to its objective of minimizing the margin between classes is controlled by a regularization parameter called C which by default is set to 1.0.
  - The C parameter is just a constant that attaches itself to the classification error by multiplying the classification error by the constant.
  - Larger values of C represent less regularization and will cause the model to fit the training set with these few errors as possible, even if it means using a small immersion decision boundary. (Large C, small margin, small classification error)
  - Very small values of C on the other hand use more regularization that encourages the classifier to find a large marge on decision boundary, even if that decision boundary leads to more points being misclassified. (Small C, Large margin, more classification error)
- **Gamma RBF parameter**:
  - It controls the wideness of the curve.
  - A large gamma will move us to a narrow curve. A small gamma would give us a wide curve.
  - Small gamma means a larger similarity radius (give broader, smoother decision regions). So that points farther apart are considered similar which results in more points being group together. While larger values of gamma give smaller, more complex decision regions, tightly constrained decision boundaries.
  - The gamma matters a lot in the algorithm. Large values of gamma tend to overfit, and small ones tend to underfit.
- **kernel**:
  - The most common ones are 'linear', 'poly', and 'rbf'.

  ![Gamma](ML%20images/RBF-large-gamma.png)
  ![Gamma](ML%20images/RBF-small-gamma.png)

##### SVM python libraries

- scikit-learn.

    ```python
    from sklearn.svm import SVC
    from adspy_shared_utilities import plot_class_regions_for_classifier

    X_train, X_test, y_train, y_test = train_test_split(X_D2, y_D2, random_state = 0)

    # The default SVC kernel is radial basis function (RBF)
    model = SVC(kernel = 'rbf', gamma=1, C=1)

    plot_class_regions_for_classifier(SVC().fit(X_train, y_train), X_train, y_train, None, None, 'Support Vector Classifier: RBF kernel')

    # Compare decision boundaries with polynomial kernel, degree = 3
    plot_class_regions_for_classifier(SVC(kernel = 'poly', degree = 3).fit(X_train, y_train), X_train, y_train, None, None, 'Support Vector Classifier: Polynomial kernel, degree = 3')
    ```

  - Calling the fit method with the training data to train the model.
  - There is an SVC parameter called kernel, that allows us to set the kernel function used by the SVM. The polynomial kernel takes additional parameter degree that controls the model complexity and the computational cost of this transformation.
  - Small gamma means a larger similarity radius (give broader, smoother decision regions). So that points farther apart are considered similar which results in more points being group together. While larger values of gamma give smaller, more complex decision regions, tightly constrained decision boundaries.
  - SVMs also have a regularization parameter, C, that controls the tradeoff between satisfying the maximum margin criterion to find the simple decision boundary, and avoiding misclassification errors on the training set. The C parameter is also an important one for kernelized SVMs, and it interacts with the gamma parameter.

##### SVM Pros and Cons

- **Linear Model Pros**:
  - Simple and easy to train.
  - Fast prediction.
  - Scales well to very large dataset.
  - Works well with sparse data.
  - Reasons for prediction are relatively easy to interpret.
- **Linear Model Cons**:
  - For lower-dimensional data, other models may have superior generalization performance.
  - For classification, data may not be linearly separable.

- **Kernelized model Pros**:
  - Can perform well on a range of datasets.
  - Versatile: different kernel functions can be specified, or custom kernels can be defined for specific data types.
  - Works well for both low-and high-dimensional data.
- **Kernelized model Cons**:
  - Efficiency (runtime speed and memory usage) decreases as training set size increases (e.g. over 50000 samples).
  - Needs careful normalization of input data and parameter tuning.
  - Does not provide direct probability estimates (but can be estimated using e.g. Platt scaling).
  - Difficult to interpret why a prediction was made.

##### SVM extra resources

- [The chapter discusses the support vector machine (SVM) algorithm and explains and demonstrates why they are often considered one of the best “out of the box” classifiers](https://static1.squarespace.com/static/5ff2adbe3fe4fe33db902812/t/6062a083acbfe82c7195b27d/1617076404560/ISLR%2BSeventh%2BPrinting.pdf)
- [Wikipedia goes into depth on how and why SVMs are one of the most robust prediction methods, being based on statistical learning frameworks or VC theory proposed by Vapnik (1982, 1995) and Chervonenkis (1974).](https://en.wikipedia.org/wiki/Support_vector_machine)
- [Starting on page 11, Andrew Ng talks about margins and the idea of separating data with a large “gap, ” the optimal margin classifier, and kernels.](http://cs229.stanford.edu/notes2020fall/notes2020fall/cs229-notes3.pdf)

#### Decision tree

![Decision Tree Example](ML%20images/Descision&#32;Tree&#32;Example.jpg)

- It can be used for both regression and classification.
- How it works:
  - Nodes are split based on the feature that has the largest information gain (IG) between parent and its split nodes.
  - One metric to quantify IG is to compare entropy before and after splitting.
  - Entropy:
    - Entropy is a measure of disorder.
    - Entropy is an indicator of how messy your data is.
    - The more knowledge one has about the inputs, the less entropy, and vice versa.
    - Logarithms commonly used when working with entropy, entropy can be estimated as the sum of the logs of probabilities of all labels a dataset has.
    - $\text{Entropy} = -\sum_{i=1}^n{p_i}\log_2(p_i)$ Where $p_i$ is the probability of randomly selecting an example in class $i$
    - In a binary case:
      - Entropy is 0 if all samples belong to the same class for a node (i.e., pure)
      - Entropy is 1 if samples contains both classes with equal proportion (i.e., 50% for each class, chaos)
  - Information Gain:
    - It is measure of how much information a feature provides about a class.
    - Information gain helps to determine the order of attributes in the nodes of a decision tree.
    - $\text{GAIN} = E_{parent} - E_{children}$ Where $E_{parent}$ is the entropy of the parent node and $E_{children}$ is the average entropy of the child nodes.
  - The splitting procedure can go iteratively at each child node until the end-nodes (or leaves) are pure  (i.e., there is only one class in each node).
    - But the splitting procedure usually stops at certain criteria to prevent overfitting.
- **Hyperparameters** (Splitting stop criteria):
  - Maximum Depth:
    - `max_depth` is the largest possible length between the root to a leaf.
    - A tree of maximum length $k$ can have at most $2^k$ leaves.
    - Small maximum depth causes UNDERFITTING, and Large maximum depth causes OVERFITTING.
  - Minimum number of samples to split:
    - A node must have at least `min_samples_split` samples in order to be large enough to split. If a node has fewer samples than `min_samples_split` samples, it will not be split, and the splitting process stops.
    - `min_samples_split` doesn't control the minimum size of leaves.
    - Small minimum samples per split causes OVERFITTING, and Large minimum samples per split causes UNDERFITTING
  - Minimum number of samples per leaf
    - `min_samples_leaf` is minimum number of samples allowed on each leaf.
    - If the number's an integer, it's the minimum number of samples allowed in a leaf.
    - If it's a float, it's the minimum percentage of samples allowed in a leaf.
- Python Libraries:
  - Scikit-learn

    ```python
    # Classifier version
    from sklearn.tree import DecisionTreeClassifier
    # Regression version
    from sklearn.tree import DecisionTreeRegressor

    Model = DecisionTreeClassifier(max_depth = 3, min_samples_leaf = 8)
    ```

    - `max_depth`: controls maximum depth (number of split points). Most common way to reduce tree complexity and overfitting.
    - `min_samples_leaf`: threshold for the minimum # of data instances a leaf can have to avoid further splitting.
    - `max_leaf_nodes`: limits total number of leaves in the tree.
    - In practice, adjusting only one of these (e.g. max_depth) is enough to reduce overfitting.
- **Over Fitting**
  - There is a problem with decision tree which is overfitting, due to its complexity and essentially memorizing the training data.
  - One strategy to prevent overfitting is to prevent the tree from becoming really detailed and complex by stopping its growth early. This is called pre-pruning.
  - Another strategy is to build a complete tree with pure leaves but then to prune back the tree into a simpler form. This is called post-pruning or sometimes just pruning.
- **Feature Importance**
  - Another way of analyzing the tree instead of looking at the whole tree at once is to do what's called a feature important calculation.
  - one of the most useful and widely used types of summary analysis you can perform on a supervised learning model.
  - typically a number between 0 and 1 that's assigned to an individual feature.
  - It indicates how important that feature is to the overall prediction accuracy.
  - A feature importance of zero means that the feature is not used at all in the prediction. A feature importance of one, means the feature perfectly predicts the target.
  - Typically, feature importance numbers are always positive and they're normalized so they sum to one.
  - In `scikit-learn`, feature importance values are stored as a list in an estimated property called `feature_importances_`.
- **Pros**:  
  - Easily visualized and interpreted.
  - No feature normalization or scaling typically needed.
  - Work well with datasets using a mixture of feature types (continuous, categorical, binary)
- **Cons**:
  - Even after tuning, decision trees can often still overfit.
  - Usually need an ensemble of trees for better generalization performance.

#### Random Forest

- Set of decision trees, each learned from a different randomly sampled subset with replacement.
- Features to split on for each tree, randomly selected subset from original features.
- Prediction: Average output probabilities
- Increases diversity through random selection of training dataset and subset of features for each tree
- Reduces variance through averaging
- Each tree typically does not need to be pruned
- More expensive to train and run
- scikit-learn: `sklearn.ensemble.RandomForestClassifier`
- scikit-learn: `sklearn.ensemble.RandomForestRegressor`

### Neural Networks

#### Perceptron

- It is the simplest neural network.
- It is a single layer neural network that uses one layer of a list of input features and one output.
- One of the features is a bias, same as intercept in linear regression, that gets combined a long with the other features.
- After having this linear combination, an activation function is applied. This function is usually non-linear and depends on the problem being tried to solve.

#### Neural network architecture

- Layers of nodes connected together
- Each node is one multivariate linear function, with an univariate nonlinear transformation.
- Trained via stochastic gradient descent
- Can represent any non-linear function (very expressive)
- Generally hard to interpret.
- Expensive to train, fast to predict
- Scikit-learn: `sklearn.neural_network.MLPClassifier`.
- Deep Learning Frameworks:
  - MXNet
  - TensorFlow
  - Caffe
  - PyTorch

#### Convolutional Neural Networks

- It is very useful in image analysis
- The input is an image or a sequence of images.
- Kernel is used as filter to extract local features.

#### Recurrent neural networks

- It consists of multiple inputs layer, multiple hidden layers and multiple output layer.
- Each node outputs to the next input node.

### K-nearest neighbor

- It is a type of machine learning algorithm.
- It can be used for classification and regression.
- It is an example of what's called instance based or memory based supervised learning.
- It Non-parametric, instance based, lazy:
  - Non-parametric: Model is not defined by fixed set of parameters.
  - Instance-based or lazy learning: Model is the result of effectively memorizing training data.
- Requires keeping the original dataset.
- It returns a classifier that classifies the input with respect to the nearest n_neighbors neighbors that is the most predominant.  
K-nearest neighbors doesn't make a lot of assumptions about the structure of the data and gives potentially accurate, but sometimes unstable predictions
- Space complexity and prediction-time complexity grow with size of training data.
- Suffers from curse of dimensionality: points became increasingly isolated with more dimensions, for a fixed-size training dataset.
- It can be sensitive to small changes in the training data.
- It can be used in python as below:
    1. Initiate a variable

        ```python
        from sklearn.neighbors import KNeighborsClassifier
        knn = KNeighborsClassifier(n_neighbors)
        ```

    2. Train the model to memorize all its features and labels

        ```python
        knn.fit()
        ```

    3. To predict a label use the below function with 1 parameter that has the same number of feature as the trained data

        ```python
        knn.predict(param)
        ```

    4. The accuracy can be tested by passing testing data and testing labels

        ```python
        knn.score(X_test, y_test)
        ```

### Naive Bayes

- Naive Bayes is a supervised machine learning algorithm that can be trained to classify data into multi-class categories.
- In the heart of the Naive Bayes algorithm is the probabilistic model that computes the conditional probabilities of the input features and assigns the probability distributions to each of the possible classes.
- This algorithm has great benefits such as being easy to implement and very fast to train.
- One of the major advantages that Naive Bayes has over other classification algorithms is its ability to handle an extremely large number of features.
- It performs well even with the presence of irrelevant features and is relatively unaffected by them. It has is its relative simplicity.
- It works well right out of the box and tuning its parameters is rarely ever necessary, except usually in cases where the distribution of the data is known.
- It rarely ever overfits the data.
- Its model training and prediction times are very fast for the amount of data it can handle.

#### Bayes Theorem

- The main idea of the Bayes theorem is that it switches from what we know to what we infer.
- Initially, we start with an event A. The probability of $A$ is $P(A)$, it is the prior probability. Another event $B$ that can happen or not happen, also a prior probability.
  - Prior refers to guesses we make before having complete information.
  - Posterior refers to guesses we've inferred after the new information has arrived.
- The probability of $A$ given $B$, noted as $P(A|B)$, and the probability of $B$ complement (B not happened) given $A$, noted as $P(B^c|A)$.
  - $P(B∩A)=P(A)P(B∣A)$
- Because these probabilities do not add to one, we divide them both by their sum so that the new normalized probabilities now do add to one.
- Normalized Bayes Theorem (Posterior Probabilities):
  - $P(A|B) = \frac{P(B∩A)}{P(B)} = \frac{P(A)P(B∣A)}{P(B)}$
  - $P(B) = [P(A) * \text{Sensitivity}] + [P(A^c) * (1-\text{Specificity}))]$
  - $\text{Sensitivity} = P(B|A)$
  - $\text{Specificity} = P(B^c|A^c)$
