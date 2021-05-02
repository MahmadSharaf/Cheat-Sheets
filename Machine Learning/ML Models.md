#### Supervised Machine Learning Algorithms

The supervised aspect refers to the need for each training example to have a label in order for the algorithm to learn how to make accurate predictions on future examples.
This is in contrast to unsupervised machine learning where we don't have labels for the training data examples, and we'll cover unsupervised learning in a later part of this course.

##### Neural Networks

###### Perceptron

- It is the simplest neural network.
- It is a single layer neural network that uses one layer of a list of input features and one output.
- One of the features is a bias, same as intercept in linear regression, that gets combined a long with the other features.
- After having this linear combination, an activation function is applied. This function is usually non-linear and depends on the problem being tried to solve.

###### Neural network architecture

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

###### Convolutional Neural Networks

- It is very useful in image analysis
- The input is an image or a sequence of images.
- Kernel is used as filter to extract local features.

###### Recurrent neural networks

- It consists of multiple inputs layer, multiple hidden layers and multiple output layer.
- Each node outputs to the next input node.

##### K-nearest neighbor

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

##### Linear Model

- Linear models make strong assumptions about the structure of the data.
- The target value can be predicted just using a weighted sum of the input variables, a linear function.
- It can get stable, but potentially inaccurate predictions.

1. Linear Regression  

    $$
    \hat{y} = \hat{w_0}x_0 + \hat{w_1} x_1 + ... \hat{w_n} x_n + \hat{b}
    $$
    The hat(^) is an indication that the parameter is estimated during training process.  
    **$\hat{y}$**: the predicted output.  
    **$\hat{w_i}$**: the model coefficients or feature weights.  
    **$\hat{b}$**: the biased term or intercept of the model.

    $\hat{b},\hat{w}$ parameters are estimated by:

    - They are estimated from training the data.
    - There are different methods correspond to different 'fit' criteria and goals and ways to control complexity.
    - `Squared loss function` returns the squared difference between the target value and the  actual value as the penalty.
    - The learning algorithm then computes or searches for the set of $\hat{w},\hat{b}$ parameters that optimize an objective function, typically to minimize the total of this loss function over all training points.

    1. Least Squares:
        $$
        RSS(w, b) = \sum_{i=1}^N(y_i - (w . x_i + b))^2
        $$
        - The most popular way to estimate w and b parameters is using what's called least-squares linear regression or ordinary least-squares.
        - Least-squares finds the values of w and b that minimize the total sum of squared differences between the predicted y value and the actual y value in the training set. Or equivalently it minimizes the mean squared error of the model.
        - This technique is designed to find the slope, the w value, and the b value of the y intercept, that minimize this squared error, this mean squared error.
        - The mean squared error is the square difference between predicted and actual values, and then all these are added up, and then divided by the number of training points, take the average, that will be the mean squared error of the model.
        - One thing to note about this linear regression model is that there are no parameters to control the model complexity. No matter what the value of w and b, the result is always going to be a straight line. This is both a strength and a weakness of the model.

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

    2. Ridge Regression:
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

    3. Lasso Regression
        $$
        RSS_{LASSO}(w,b) = \sum_{i=1}^N (y_i - (w . x_i + b))^2 + \alpha \sum_{j=1}^p |w_j|
        $$
        - Like ridge regression, lasso regression adds a regularization penalty term to the ordinary least-squares objective, that causes the model W-coefficients to shrink towards zero.
        - Lasso regression is another form of regularized linear regression that uses an L1 regularization penalty for training (instead of ridge's L2 penalty).
        - L1 Penalty: minimizes the sum of the absolute values of the coefficients.
        - This has the effect of setting parameter weights in w to zero for the least influential variables. This called a sparse solution: a kind of feature selection.
        - The parameter alpha controls the amount of L1 regularization (default = 1.0).
        - The prediction formula is the same as ordinary least-squares.

            ```python
            from sklearn.preprocessing import MinMaxScaler
            scaler = MinMaxScaler()

            from sklearn.linear_model import Ridge
            X_train, X_test, y_train, y_test = train_test_split(X_crime, y_crime,random_state=0)

            X_train_scaled = scaler.fit_transfor(X_train)
            X_test_scaled = scaler.transform(X_test)

            linlasso = Lasso(alpha = 2.0, max_iter =10000) .fit(X-train_scaled, y_train)
            ```

            - When to use ridge vs lasso:
              - Many small/medium sized effects: use ridge.
              - Only a few variables with medium/large effect: use lasso.

2. Logistic Regression  
    ![Flowchart box](ML%20images/Logistic&#32;Regression&#32;flow&#32;chart.jpg)  
    ![Logistic fn](ML%20images/Logistic&#32;Regression&#32;function.jpg)
   - It is a kind of generalized linear model.
   - In spite of being called a regression measure, it is actually used for classification
   - like ordinary least squares and other regression methods, logistic regression takes a set input variables, the features, and estimates a target value.
   - Unlike ordinary linear regression, in it's most basic form logistic repressions target value is a binary variable instead of a continuous value.
   - There are flavors of logistic regression that can also be used in cases where the target value to be predicted is a multi class categorical variable, not just binary.
   - Logistic regression is similar to linear regression, but with one critical addition. The logistic regression model still computes a weighted sum of the input features xi and the intercept term b (like in linear regression), but it runs this result through a special non-linear function f, the logistic function represented by this new box in the middle of the diagram to produce the output y. The effect of applying the logistic function is to compress the output of the linear function so that it's limited to a range between 0 and 1. Below the diagram, you can see the formula for the predicted output y hat which first computes the same linear combination of the inputs xi, model coefficient weights wi hat and intercept b hat, but runs it through the additional step of applying the logistic function to produce y hat.
   - If we pick different values for b hat and the w hat coefficients, we'll get different variants of this s shaped logistic function, which again is always between 0 and 1.
   - To perform logistic, regression in Scikit-Learn, you import the logistic regression class from the sklearn.linear model module, then create the object and call the fit method using the training data just as you did for other class files like k nearest neighbors.

        ```python
        from sklearn.linear_model import LogisticRegression

        X_train, X_test, y_train, y_test = train_test_split(X_C2,   y_C2,random_state = 0)
        clf = LogisticRegression(C=1).fit(X_train, y_train)
        ```

     - L2 regularization is 'on' by default (like ridge regression)
     - Parameter C controls amount of regularization (default 1.0)
     - As with regularized linear regression, it can be important to normalize all features so that they are on the same scale.

3. Linear Support Vector Machines (LSVM):
   - Linear models are also used for classification, starting with binary classification.
   - This approach uses the same linear functional form as for regression. But instead of predicting a continuous target value, we take the output of the linear function and apply the sine function to produce a binary output with two possible values, corresponding to the two possible class labels.
   - One way to define a good classifier is to reward classifiers for the amount of separation that can provide between the two classes (classifier margin). The margin is the width that the decision boundary can be increased perpendicularly before hitting a data point. The classifier that has the maximum margin is called the Linear Support Vector Machine, also known as an LSVM or a support vector machine with linear kernel.
   - How tolerant the support vector machine is of misclassifying training points, as compared to its objective of minimizing the margin between classes is controlled by a regularization parameter called C which by default is set to 1.0. Larger values of C represent less regularization and will cause the model to fit the training set with these few errors as possible, even if it means using a small immersion decision boundary. Very small values of C on the other hand use more regularization that encourages the classifier to find a large marge on decision boundary, even if that decision boundary leads to more points being misclassified.
   - scikit-learn: `sklearn.svm.SVC`

   - **Linear Model Pros**:
     - Simple and easy to train.
     - Fast prediction.
     - Scales well to very large dataset.
     - Works well with sparse data.
     - Reasons for prediction are relatively easy to interpret.
   - **Linear Model Cons**:
     - For lower-dimensional data, other models may have superior generalization performance.
     - For classification, data may not be linearly separable.

4. Kernelized Support Vector Machines (KSVMs)
   - It is a very powerful extension of linear support vector machines, it can provide more complex models that can go beyond linear decision boundaries.
   - SVMs can be used for both classification and regression.
   - One way to think about what kernelized SVMs do, is they take the original input data space and transform it to a new higher dimensional feature space, where it becomes much easier to classify the transform to data using a linear classifier. (eg. instead of $y(x)$ it became $y(x,x^2)$ like polynomial feature).  
   ![example](ML%20images/SVM&#32;1-dim&#32;to&#32;2-dim.jpg)  
   The above figure shows at the right that the points can be separated by a straight line after converting it to a two dimensional space, while on the left is the original one dimensional points in which the straight line is converted to a parabola.
   - An example of how it can be done using scikit-learn in Python.

        ```python
        from sklearn.svm import SVC
        from adspy_shared_utilities import plot_class_regions_for_classifier

        X_train, X_test, y_train, y_test = train_test_split(X_D2, y_D2, random_state = 0)

        # The default SVC kernel is radial basis function (RBF)
        #! SVC() = SVC(kernel = 'rbf', gamma=1, C=1)

        plot_class_regions_for_classifier(SVC().fit(X_train, y_train), X_train, y_train, None, None, 'Support Vector Classifier: RBF kernel')

        # Compare decision boundaries with polynomial kernel, degree = 3
        plot_class_regions_for_classifier(SVC(kernel = 'poly', degree = 3).fit(X_train, y_train), X_train, y_train, None, None, 'Support Vector Classifier: Polynomial kernel, degree = 3')
        ```

        - Calling the fit method with the training data to train the model.
        - There is an SVC parameter called kernel, that allows us to set the kernel function used by the SVM. The polynomial kernel takes additional parameter degree that controls the model complexity and the computational cost of this transformation.
        - Small gamma means a larger similarity radius (give broader, smoother decision regions). So that points farther apart are considered similar . Which results in more points being group together. Small values of gamma. While larger values of gamma give smaller, more complex decision regions, tightly constrained decision boundaries.
        - SVMs also have a regularization parameter, C, that controls the tradeoff between satisfying the maximum margin criterion to find the simple decision boundary, and avoiding misclassification errors on the training set. The C parameter is also an important one for kernelized SVMs, and it interacts with the gamma parameter.

   - Pros:
      - Can perform well on a range of datasets.
      - Versatile: different kernel functions can be specified, or custom kernels can be defined for specific data types.
      - Works well for both low-and high-dimensional data.
   - Cons:
     - Efficiency (runtime speed and memory usage) decreases as training set size increases (e.g. over 50000 samples).
     - Needs careful normalization of input data and parameter tuning.
     - Does not provide direct probability estimates (but can be estimated using e.g. Platt scaling).
     - Difficult to interpret why a prediction was made.

5. Decision tree

    ![Decision Tree Example](ML%20images/Descision&#32;Tree&#32;Example.jpg)
    - It can be used for both regression and classification.
    - How it works:
      - Nodes are split based on the feature that has the largest information gain (IG) between parent and its split nodes.
      - One metric to quantify IG is to compare entropy before and after splitting.
      - In a binary case:
        - Entropy is 0 if all samples belong to the same class for a node (i.e., pure)
        - Entropy is 1 if samples contains both classes with equal proportion (i.e., 50% for each class, chaos)
      - The splitting procedure can go iteratively at each child node until the end-nodes (or leaves) are pure  (i.e., there is only one class in each node).
        - But the splitting procedure usually stops at certain criteria to prevent overfitting.
    - How to implement it:

        ```python
        from sklearn.tree import DecisionTreeClassifier

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

6. Random Forest:
   - Set of decision trees, each learned from a different randomly sampled subset with replacement.
   - Features to split on for each tree, randomly selected subset from original features.
   - Prediction: Average output probabilities
   - Increases diversity through random selection of training dataset and subset of features for each tree
   - Reduces variance through averaging
   - Each tree typically does not need to be pruned
   - More expensive to train and run
   - scikit-learn: `sklearn.ensemble.RandomForestClassifier`
