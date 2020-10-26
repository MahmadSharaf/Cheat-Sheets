# Applied Machine Learning with Python

- [Applied Machine Learning with Python](#applied-machine-learning-with-python)
  - [About this course](#about-this-course)
  - [What is covered in this course](#what-is-covered-in-this-course)
  - [What is not covered](#what-is-not-covered)
  - [Setting up environment](#setting-up-environment)
  - [Introduction](#introduction)
    - [Definition Machine Learning (ML)](#definition-machine-learning-ml)
    - [Types of Machine Learning](#types-of-machine-learning)
      - [1. Supervised ML](#1-supervised-ml)
      - [2. Unsupervised ML](#2-unsupervised-ml)
    - [Basic Machine Learning Workflow](#basic-machine-learning-workflow)
  - [Getting Started](#getting-started)
    - [Preprocessing](#preprocessing)
    - [Splitting dataset](#splitting-dataset)
    - [Choosing the ML model](#choosing-the-ml-model)
      - [Supervised Machine Learning Algorithms](#supervised-machine-learning-algorithms)
        - [Neural Networks](#neural-networks)
          - [Perceptron](#perceptron)
          - [Neural network architecture](#neural-network-architecture)
          - [Convolutional Neural Networks](#convolutional-neural-networks)
          - [Recurrent neural networks](#recurrent-neural-networks)
        - [K-nearest neighbor](#k-nearest-neighbor)
        - [Linear Model](#linear-model)
    - [Model Training/Tunning](#model-trainingtunning)
      - [Bias Variance Tradeoff](#bias-variance-tradeoff)
      - [Learning Curve](#learning-curve)
      - [Model Debugging](#model-debugging)
      - [Regularization](#regularization)
      - [Hyperparameter tuning](#hyperparameter-tuning)
        - [Grid Search](#grid-search)
        - [Random Search](#random-search)
      - [Model Tuning](#model-tuning)
        - [Training Data Tuning](#training-data-tuning)
        - [Feature Set Tuning](#feature-set-tuning)
        - [Feature Extraction](#feature-extraction)
        - [Model Tuning: Bagging/Boosting](#model-tuning-baggingboosting)
  - [Aspects to be considered](#aspects-to-be-considered)
  - [ML Data Readiness](#ml-data-readiness)
  - [Productizing a ML Model](#productizing-a-ml-model)
    - [Aspects to consider](#aspects-to-consider)
    - [Types of Production environments](#types-of-production-environments)
      - [Batch predictions](#batch-predictions)
      - [Online Predictions](#online-predictions)
      - [Online training](#online-training)
    - [Business metrics vs Model Metrics](#business-metrics-vs-model-metrics)
      - [Metrics for Logistic Regression](#metrics-for-logistic-regression)
        - [Confusion Matrix](#confusion-matrix)
        - [Metrics for Linear Regression](#metrics-for-linear-regression)
    - [Storage](#storage)
    - [Model and Pipeline Persistence](#model-and-pipeline-persistence)
    - [Model Deployment](#model-deployment)
    - [Monitoring](#monitoring)
    - [Maintenance](#maintenance)
  - [Common Mistakes](#common-mistakes)

## About this course

This course will introduce the learner to applied machine learning, focusing more on the techniques and methods than on the statistics behind these methods. The course will start with a discussion of how machine learning is different than descriptive statistics, and introduce the scikit learn toolkit through a tutorial. The issue of dimensionality of data will be discussed, and the task of clustering data, as well as evaluating those clusters, will be tackled. Supervised approaches for creating predictive models will be described, and learners will be able to apply the scikit learn predictive modelling methods while understanding process issues related to data generalizability (e.g. cross validation, overfitting). The course will end with a look at more advanced techniques, such as building ensembles, and practical limitations of predictive models. By the end of this course, students will be able to identify the difference between a supervised (classification) and unsupervised (clustering) technique, identify which technique they need to apply for a particular dataset and need, engineer features to meet that need, and write python code to carry out an analysis.

## What is covered in this course

- Understand basic ML concepts and workflow
- How to properly apply 'black-box' machine learning
components and features
- Learn how to apply machine learning algorithms in
Python using the scikit-learn package

## What is not covered

- Underlying theory of statistical machine learning
- Lower-level details of how particular ML components work
- In-depth material on more advanced concepts like deep learning.

## Setting up environment

1. ### `scikit-learn`: Python Machine Learning Library

    1. scikit-learn Homepage: <http://scikit-learn.org/>
    2. scikit-learn User Guide: <http://scikit-learn.org/stable/user_guide.html>
    3. scikit-learn API reference: <http://scikit-learn.org/stable/modules/classes.html>

        ```python
        from sklearn.model_selection import train_test_split
        from sklearn.tree import DecisionTreeClassifier
        ```

2. ### Python Environment with below libraries

    1. `SciPy` Library: Scientific Computing Tools

        - Provides a variety of useful scientific computing     tools, including statistical distributions,     optimization of functions, linear algebra, and a    variety of specialized mathematical functions.
        - With scikit-learn, it provides support for sparse     matrices, a way to store large tables that consist  mostly of zeros.

            ```python
            import scipy as sp
            ```

    2. `NumPy`: Scientific Computing Library

        - Provides fundamental data structures used by  scikit-learn, particularly multi-dimensional arrays.
        - Typically, data that is input to scikit-learn will    be in the form of a NumPy array.
        hat consist  mostly of zeros.

            ```python
            import numpy as np
            ```

    3. `Pandas`: Data Manipulation and Analysis

        - Provides key data structures like DataFrame
        - Also, support for reading/writing data in different   formats
        hat consist  mostly of zeros.

            ```python
            import pandas as pd
            ```

    4. `matplotlib` and other plotting libraries

        - We typically use matplotlib's pyplot module:

            ```python
            import matplotlib.pyplot as plt
            ```

        - We also sometimes use the seaborn visualization
        library (<http://seaborn.pydata.org/)>

            ```python
            import seaborn as sn
            ```

        - And sometimes the graphviz plotting library:

            ```python
            import graphviz
            ```

    5. Libraries versions used in this course

        | Library name | Minimum version |
        | ------------ | --------------- |
        | scikit-learn | 0.18.1          |
        | scipy        | 0.19.0          |
        | numpy        | 1.12.1          |
        | pandas       | 0.19.2          |
        | matplotlib   | 2.0.1           |
        | seaborn      | 0.7.1           |
        | graphviz     | 0.7             |

## Introduction

### Definition Machine Learning (ML)

- The study of computer programs (algorithms)
that can learn by example
- ML algorithms can generalize from existing
examples of a task

### Types of Machine Learning

#### 1. Supervised ML

Learn to predict target values from labelled data.

1. Classification: Target values with discrete classes  
    eg: Differentiate between fruit types
2. Regression: Target values are continuous values.  
    eg: Predict house price

#### 2. Unsupervised ML

Find structure in unlabeled data

1. Clustering: Find groups of similar instances in the data.  
  eg: Finding clusters of similar users.
2. Outlier detection: Detecting abnormal server access patterns.  
  eg: Predict house price

### Basic Machine Learning Workflow

1. Representation  
    Choose:
    - A feature representation
    - Type of classifier to use  
        e.g. image pixels, with k-nearest neighbor classifier
2. Evaluation  
    Choose:
    - What criterion distinguishes good vs. bad classifiers?  
        e.g. % correct predictions on test set
3. Optimization  
    Choose:
    - How to search for the settings/parameters that give the best classifier for this evaluation criterion.  
        e.g. try a range of values for "k" parameter in k-nearest neighbor classifier

## Getting Started

### Preprocessing

Look at what kind of feature preprocessing is typically needed.

- Missing data.
  - Check for missing values by using pandas functions `df.isnull()`.
  - If there are missing values, the below can be done:
    - Drop missing values by `df.dropna()`.
      - Risks of dropping rows:
        - Losing too much data, Overfitting, wider confidence intervals, etc.
        - May bias sample
      - Risks of dropping columns:
        - May lose information in features (Underfitting)
    - Impute the missing values:
      - It can be replaced by using an estimated value such as Mean, Median, Most Frequent(for categoricals), etc.
      - Evaluate the cause of missingness to determine the best imputation process.

        ```py
        from sklearn.preprocessing import Imputer
        import numpy as np

        arr = np.array([[5,3,2,2],[3,None,1,9],[5,2,7,None]])

        imputer = Imputer(strategy = 'mean')
        imp = imputer.fit(arr)
        imputer.transform(arr)

        # array([[5,3,2,2],
        #        [3,2.5,1,9],
        #        [5,2,7,5.5]])
        ```

      - Advanced methods for Imputation:
        - MICE (Multiple Imputation by chained Equations).
        `sklearn.impute.MICEImpute` (v0.20)
        - Python (not sklearn) `fancyimpute` package (KNN impute, SoftImpute, MICE, etc..)
- Gain insight on what machine learning model might be appropriate, if any.
- Get a sense of how difficult the program might be.
- Encoding Labels:
  - It is converting categorical variable into a numerical variable.
  - Ordinal:
    - SciKit Learn library, LabelEncoder, converts categorical variable to numerical variable that starts with 0 and increase with 1. But if this applied to non-nominal categorical type, may lead to wrong computations or wrong usages. So, it is recommended to be used with Ordinal type that has relationships with each other.

      ```py
      from sklearn.preprocessing import LabelEncoder

      loan_enc = LabelEncoder()
      y = group_enc.fit_transform(df['loan_approved'])
      ```

  - Nominal:
    - While library OneHotEncoder is more likely to be used for Nominal variables.

      ```py
      from sklearn.preprocessing import OneHotEncoder

      df = pd.DataFrame({"Fruits":["Apple","Banana","Banana","Mango","Banana"]})
      num_type = group_enc.fit_transform(df['Fruits'])
      type_enc = OneHotEncoder()
      type_enc.fit(num_type.reshape(-1,1))
      ```

    - Pandas library has get_dummies() function to do the same as OneHotEncoder

      ```py
      import pandas as pd

      df = pd.DataFrame({"Fruits":["Apple","Banana","Banana","Mango","Banana"]})

      pd.get_dummies(df)
      ```

    - Encoding with many classes:
      - Define a hierarchy structure.
      - Try to group the levels by similarity to reduce the overall number of groups.

- Feature Engineering
  - Scaling Transformation:

    Critical aspects to Feature Engineering:
    - The scalar is fit to training data only, then transform both train and validation data.
    1. Apply the same scalar object to both training and testing data.
    2. Training the scalar object on the training data and not on the test data. If it trained on the test data, it will cause a phenomena called Data Leakage, where the training phase has information that is leaked from the test set.

    - Mean/variance standardization:
      - Centering the values around mean $\mu_j = 0$ with standard deviation $\sigma_j = 1$ for each column.
      - This can be achieved by removing the mean from the variable and divide it with the standard variance.

        $$x_{i,j}^* = \frac{x_{i,j} - \mu_j}{\sigma_j}$$

        ```py
        from sklearn.preprocessing import StandardScalar

        scale = StandardScalar()
        arr = np.array([[5,3,2,2],[2,3,1,9],[5,2,7,6]],dtype=float)
        print(scale.fit_transform(arr))
        print(scale.scale_)
        ```

        - Advantages:
          - Many algorithms behave better with smaller values
          - Keeps outlier information, but reduces impact.

    - MinMax Scaling: transform all the input variables, so they're all on the same scale between zero and one.

        $$x_{i,j}^* = \frac{x_{i} - \min x_j}{\max x_j - \min x_j}$$

      ```python
      from sklearn.preprocessing import MinMaxScaler
      scaler = MinMaxScaler()
      scaler.fit(x_train)   # compute the min and max feature   values for each feature in this training dataset.
      X_trained_scaled = scaler.transform(X_train)
      X_test_scaled = scaler.transform(X_test)
      clf = Ridge().fit(X_train_scaled, y_train)
      r2_score = clf.score(X_test_scaled, y_test)
      # or more efficiently fit and transform in one step
      X_train_scaled = scaler.fit_transform(X_train)
      ```

      - Advantages:
        - Robust to small standard deviations

    - MaxAbs scaling:
      - Diving each element by the maximum absolute value in the feature.
        $$x_{i,j}^* = \frac{x_{i,j}}{\max (|x_j|)}$$
      - scikit-learn: `sklearn.preprocessing.MaxAbsScaler`
      - Advantages:
        - It doesn't destroy sparsity, because there observations are not centered around any measurement

    - Robust scaling
      - It is applied to particle features
        $$x_{i}^* = \frac{x_{i} - Q_{50}(x)}{Q_{75}(x) - Q_{25}(x)}$$
      - scikit-learn: `sklearn.preprocessing.RobustScaler`
      - Advantages:
        - After transformation, it will be robust outliers
  - Normalizer:
    - It is applied to rows.
    - Scaled values are scaled with standard deviation $\sigma_j = 1$
      $$x_{i,j}^* = \frac{x_{i,j}}{\sigma_j}$$
    - scikit-learn: `sklearn.preprocessing.Normalizer`
    - Rescales $x_j$ to unit norm based on:
      - L1 norm
      - L2 norm
      - Max norm
    - It is widely used in text analysis.
  - Polynomial Transformation
    - Polynomial Features
      ![Polynomial-Features_equation](images/Polynomial&#32;features&#32;equation.jpg)
      - Generate new features consisting of all polynomial combinations of the original two features 𝑥0,𝑥1.
      - The degree of the polynomial specifies how many variables participate at a time in each new feature (above example: degree 2).
      - This is still a weighted linear combination of features, so it's still a linear model, and can use same least-squares estimation method for w and b.
      - Adding these extra polynomial features allows us a much richer set of complex functions that we can use to fit to the data.
      - This intuitively as allowing polynomials to be fit to the training data instead of simply a straight line, but using the same least-squares criterion that minimizes mean squared error.
      - We want to transform the data this way to capture interactions between the original features by adding them as features to the linear model.
      - Polynomial feature expansion with high as this can lead to complex models that over-fit.
      - Polynomial feature expansion is often combined with a regularized learning method like ridge regression.

        ```python
        from sklearn.linear_model import LinearRegression
        from sklearn.linear_model import Ridge
        from sklearn.preprocessing import PolynomialFeatures

        X_train, X_test, y_train, y_test =  train_test_split(x    y, random_state = 0)

        linreg = LinearRegression().fit(X_train, y_train)

        poly = PolynomialFeatures(degree=2)
        X_poly = poly.fit_transform(x)

        X_train, X_test, y_train, y_test =  train_test_split(X_poly,y, random_state = 0)

        linreg = LinearRegression().fit(X_train, y_train)
        ```

  - Radial Basis Function
    - Transform: $f(x) = f(||x - c||)$
    - Widely used in Support Vector Machine as a kernel and in Radial Basis Networks (RBNNs)
    - Gaussian RBF is the most common RBF used.
  - Text-based Features
    - Bag-of-words model
      - Represent document as vector of numbers, one for each word (tokenize, count, and normalize)
      - Note:
        - Sparse matrix implementation is typically used, ignores relative position of words.
        - Can be extended to bag of n-grams of words or of characters
    - Count Vectorizer
      - Per-word value is count (also called term frequency)
      - Note: Includes lowercasing and tokenization on white space and punctuation
      - scikit-learn: `sklearn.feature_extraction.text.CountVectorizer`
    - TfidfVectorizer
      - Term-Frequency times Inverse Document-Frequency
      - Per-word value is downweighted for terms common across documents (eg. "the")
      - scikit-learn: `sklearn.feature_extraction.text.TfidfVectorizer`
    - Hashing Vectorizer
      - Stateless mapper from text to term index
      - scikit-learn: `sklearn.feature_extraction.text.HashingVectorizer`

### Splitting dataset

Split dataset into features X and labels y

1. Split X and y

   - With a percentage for training the algorithm and the remaining for testing its accuracy

       ```python
       from sklearn.model_selection import train_test_split

       X_train, X_test, y_train, y_test =
       train_test_split(X, y, random_state=0)
       ```

2. Cross Validation:
   - Cross-validation is a method that goes beyond evaluating a single model using a single Train/Test split of the data by using multiple Train/Test splits, each of which is used to train and evaluate a separate model.
   - So why is this better than our original method of a single Train/Test split? Bec. the accuracy score you get from running a classifier can vary quite a bit just by chance depending on the specific samples that happen to end up in the training set.
   - Cross-validation basically gives more stable and reliable estimates of how the classifiers likely to perform on average by running multiple different training test splits and then averaging the results.
   - The most common type of cross-validation is k-fold cross-validation most commonly with K set to 5 or 10. For example, to do five-fold cross-validation, the original dataset is partitioned into five parts of equal or close to equal size. Each of these parts is called a "fold". Then a series of five models is trained one per fold. The first model: Model one, is trained using folds 2 through 5 as the training set and evaluated using fold 1 as the test set. The second model: Model 2, is trained using Folds 1, 3, 4, and 5 as the training set, and evaluated using Fold 2 as the test set, and so on. When this process is done, we have five accuracy values, one per fold.
   - One benefit of computing the accuracy of a model on multiple splits instead of a single split, is that it gives us potentially useful information about how sensitive the model is to the nature of the specific training set. It does take more time and computation to do cross-validation.
   - One problem with this is that the records are sorted or at least show some bias in the ordering by class label. For example, the first 20% of the data has the same label. `scikit-learn` do cross-validation for a classification task, it actually does instead what's called "Stratified K-fold Cross-validation". The Stratified Cross-validation means that when splitting the data, the proportions of classes in each fold are made as close as possible to the actual proportions of the classes in the overall data set as shown here. While for regression, `scikit-learn` uses regular k-fold cross-validation.

    ```python
    from sklearn.model_selection import cross_val_score

    clf = KNeighborsClassifier(n_neighbors = 5)
    X = X_fruits_2d.as_matrix()
    y = y_fruits_2d.as_matrix()
    cv_scores = cross_val_score(clf, X, y, cv = 3)
    # clf: the model you want to evaluate
    # X, y: dataset
    # cv: the corresponding ground truth target labels or values. By default, cross_val_score does threefold cross-validation.
    print('Cross-validation scores (3-fold):', cv_scores)
    print('Mean cross-validation score (3-fold): {:.3f}'.format(np.mean(cv_scores)))
    ```

3. Validation Curve:
    - To evaluate the effect that an important parameter of a model has on the cross-validation scores.
    - Like cross-value score, validation curve will do threefold cross-validation by default but it can be adjusted with the CV parameter as well.
    - Unlike cross_val_score, you can also specify a classifier, parameter name, and set of parameter values, you want to sweep across.
    - So you first pass in the estimator object, or that is the classifier or regression object to use, followed by the data set samples X and target values Y, the name of the parameter to sweep, and the array of parameter values that that parameter should take on in doing the sweep.
    - It will return two two-dimensional arrays corresponding to evaluation on the training set and the test set. Each array has one row per parameter value in the sweep, and the number of columns is the number of cross-validation folds that are used.

        ```python
        from sklearn.svm import SVC
        from sklearn.model_selection import validation_curve

        param_range = np.logspace(-3, 3, 4)
        train_scores, test_scores = validation_curve(SVC(), X, y,
                                        param_name='gamma',
                                        param_range=param_range, cv=3)
        ```

### Choosing the ML model

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

- Generally hard to interpret.
- Expensive to train, fast to predict
- Scikit-learn: sklearn.neural_network.MLPClassifier.
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
    ![equation](images/Linear&#32;equation.jpg)  
    $$
    \hat{y} = \hat{w_0}x_0 + \hat{w_1} x_1 + ... \hat{w_n} x_n + \hat{b}
    $$
    The hat(^) is an indication that the parameter is estimated during training process.  
    **y**: the predicted output.  
    **w_i**: the model coefficients or feature weights.  
    **b**: the biased term or intercept of the model.

    w, b parameters are estimated by:

    - They are estimated from training the data.
    - There are different methods correspond to different 'fit' criteria and goals and ways to control complexity.
    - `Squared loss function` returns the squared difference between the target value and the  actual value as the penalty.
    - The learning algorithm then computes or searches for the set of w, b parameters that optimize an objective function, typically to minimize the total of this loss function over all training points.

    1. Least Squares:  
        ![Least-squares_equation](images/Least-squares&#32;Equation.jpg)
        - The most popular way to estimate w and b parameters is using what's called least-squares linear regression or ordinary least-squares. Least-squares finds the values of w and b that minimize the total sum of squared differences between the predicted y value and the actual y value in the training set. Or equivalently it minimizes the mean squared error of the model.
        - This technique is designed to find the slope, the w value, and the b value of the y intercept, that minimize this squared error, this mean squared error.
        - The mean squared error is the square difference between predicted and actual values, and then all these are added up, and then divided by the number of training points, take the average, that will be the mean squared error of the model.
        - One thing to note about this linear regression model is that there are no parameters to control the model complexity. No matter what the value of w and b, the result is always going to be a straight line. This is both a strength and a weakness of the model.

            ```python
            from sklearn.linear_model import LinearRegression

            X_train, X_test, y_train, y_test=train_test_split(X_R1, y_R1, random_state=0)

            linreg = LinearRegression().fit(X_train,y_train)

            # w_i: coefficients
            linreg.coef_
            # b: the intercept term
            linreg.intercept_

            #! In Scikit-Learn object attribute endswith an underscore, this means that thisattribute is derived from the trainingdata, not quantities that set by the user.
            ```

    2. Ridge Regression:  
        ![ridge_equation](images/Ridge&#32;Equation.jpg)
        - Ridge regression uses the same least-squares criterion, but with one difference. During the training phase, it adds a penalty for large feature weights in w parameters.
        - Once the parameters are learned, its prediction formula is the same as ordinary least-squares.
        - The addition of a parameter penalty is called regularization. Regularization prevents over fitting by restricting the model, typically to reduce its complexity.
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
        ![Lasso_equation](images/Lasso&#32;Equation.jpg)
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

2. Linear Classification
    1. Support Vector Machines (SVC):
        - Linear models are also used for classification, starting with binary classification.
        - This approach uses the same linear functional form as for regression. But instead of predicting a continuous target value, we take the output of the linear function and apply the sine function to produce a binary output with two possible values, corresponding to the two possible class labels.
        - One way to define a good classifier is to reward classifiers for the amount of separation that can provide between the two classes (classifier margin). The margin is the width that the decision boundary can be increased perpendicularly before hitting a data point. The classifier that has the maximum margin is called the Linear Support Vector Machine, also known as an LSVM or a support vector machine with linear kernel.
        - How tolerant the support vector machine is of misclassifying training points, as compared to its objective of minimizing the margin between classes is controlled by a regularization parameter called C which by default is set to 1.0. Larger values of C represent less regularization and will cause the model to fit the training set with these few errors as possible, even if it means using a small immersion decision boundary. Very small values of C on the other hand use more regularization that encourages the classifier to find a large marge on decision boundary, even if that decision boundary leads to more points being misclassified.

    - **Linear Model Pros**:
      - Simple and easy to train.
      - Fast prediction.
      - Scales well to very large dataset.
      - Works well with sparse data.
      - Reasons for prediction are relatively easy to interpret.
    - **Linear Model Cons**:
      - For lower-dimensional data, other models may have superior generalization performance.
      - For classification, data may not be linearly separable.

3. Logistic Regression  
    ![Flowchart box](images/Logistic&#32;Regression&#32;flow&#32;chart.jpg)  
    ![Logistic fn](images/Logistic&#32;Regression&#32;function.jpg)
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

4. Kernelized Support Vector Machines (SVMs)
   - It is a very powerful extension of linear support vector machines, it can provide more complex models that can go beyond linear decision boundaries.
   - SVMs can be used for both classification and regression.
   - one way to think about what kernelized SVMs do, is they take the original input data space and transform it to a new higher dimensional feature space, where it becomes much easier to classify the transform to data using a linear classifier. (eg. instead of y(x) it became y(x,x^2) like polynomial feature).  
   ![example](images/SVM&#32;1-dim&#32;to&#32;2-dim.jpg)  
   The above figure shows at the right that the points can be separated by a straight line after converting it to a two dimensional space, while on the left is the original one dimensional points in which the straight line is converted to a parabola.
   - An example of how it can be done using scikit-learn in Python.

        ```python
        from sklearn.svm import SVC
        from adspy_shared_utilities import              plot_class_regions_for_classifier

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

    ![Decision Tree Example](images/Descision&#32;Tree&#32;Example.jpg)
    - It can be used for both regression and classification.
    - It learns a series of explicit `if then` rules on feature values that result in a decision that predicts the target value. In this way any given object can be categorized as either matching the target object the first person is thinking of or not, according to its features as determined by asking the series of yes or no questions. We can form these questions into a tree with a node representing one question and the yes or no possible answers as the left and right branches from that node that connect the node to the next level of the tree. One question being answered at each level. At the bottom of the tree are nodes called leaf nodes that represent actual objects as the possible answers. For any object there's a path from the root of the tree to that object that is determined by the answers to the specific yes or no questions at each level.

        ```python
        from sklearn.datasets import load_iris
        from sklearn.tree import DecisionTreeClassifier
        from sklearn.model_selection import train_test_split

        iris = load_iris()

        X_train, X_test, y_train, y_test = train_test_split(iris.data, iris.target, random_state = 3)
        clf = DecisionTreeClassifier(max_depth = 3, min_samples_leaf = 8).fit(X_train, y_train)
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

### Model Training/Tunning

Machine learning models depend on input data, output data, and understanding the relationship between the two. *bias* and *variance* affect the relationship between input and output data.

#### Bias Variance Tradeoff

- Bias:
  - It is an error from flawed assumptions in the algorithm. High bias can cause an algorithm to miss important relationships between features and target outputs resulting in underfitting.
  - Bias = $E[\hat{f}(x)] - f(x)$, Where $f(x)$ is the true model, $\hat{f}(x)$ is the estimated model.
  - Solution:
    - Increase the number of features
    - Decrease degree of regularization

- Variance:
  - It is an error from sensitivity to small variations in the training data. High variance can cause an algorithm to model random noise in the training set, resulting in overfitting.
  - Variance = $E[(\hat{f}(x)-E[\hat{f}(x)])^2]$, Where $f(x)$ is the true model, $\hat{f}(x)$ is the estimated model.
  - Solution:
    - Increase training data
    - Reduce model complexity
      - Decrease the number of features
      - Increase the degree of regularization

- Total Error $(x) = \text{Bias}^2 + \text{Variance} + \text{Irreducible Error}$

#### Learning Curve

- It used to detect if the model is underfitting or overfitting, and impact of training data size the error.
- It plots the training dataset and validation dataset error or accuracy against training set size.
- scikit-learn: `sklearn.learning_curve.learning_curve`
  - Uses stratified k-fold cross-validation by default if output is binary or multiclass (preserves percentage of samples in each class)
  - Note: `sklearn.model_selection.learning_curve` in v0.18

#### Model Debugging

- Filter on failed predictions and manually look for patterns.
  - Data problems (eg, many variants for same word)
  - Labeling errors (eg, data mislabelled)
  - Under/over-represented subclasses (eg, too many examples of one type)
  - Discriminating information is not captured in features (eg, customer location)
- This helps pivot on target, key attributes, and failure type, and build histograms of error counts.

    ```py
    pred = clf.predict(train[col])
    error_df = test[pred != test['target']]
    ```

#### Regularization

- Motivation: Overfitting often caused by overly-complex models capturing idiosyncrasies in training set.
- Regularization: Adding penalty score for complexity to cost function. $\text{cost}_{reg} = \text{cost} + \frac{\alpha}{2}\text{penalty}$
- Idea: Large weights corresponds to higher complexity.
- Two standard types:
  - L1 regularization, Lasso
  - L2 regularization, Ridge

#### Hyperparameter tuning

It is an Estimator parameter that is NOT fitted in the data

- Hyperparameters must be optimized separately
- Techniques:
  - Grid Search
  - Random Search

##### Grid Search

- Allows you to search for the best parameter combination over a set of parameters
- Compute intensive
- scikit-learn: sklearn.grid_search.GridSearchCV

    ```py
    from sklean.datasets import make_classification
    from sklearn import svm
    from sklearn.model_selection import GridSearchCV

    plt.figure(4)
    X2, Y2 = make_classification(n_features = 5, n_redundant = 0, n_informative = 2)

    parameters = {'kernel':('linear','rbf'), 'C':[1,5,10,15], 'degree':[2,3,4,5]}
    svc = svm.SVC()
    clf = GridSearchCV(svc, parameters)
    clf.fit(X2, Y2)

    clf.best_params_

    # {'C': 5, 'degree':2, 'kernel':'rbf'}
    ```

##### Random Search

- Each setting is sampled from a distribution over possible parameter values.

#### Model Tuning

##### Training Data Tuning

- If training set too small, then Sample and Label more data if possible
- If training set biased against or missing some important scenarios, then Sample and Label more data for those scenarios if possible.
- If it is not easy to sample or label more, then consider creating synthetic data (duplication or techniques like SMOTE)
- IMPORTANT: Training data doesn't need to be exactly representative, but yor test set does.

##### Feature Set Tuning

- Add features that help capture pattern classes of errors
- Try different transformations of the same feature.
  - Example: Square the values of a feature.
- Apply dimensionality reduction to reduce impact of weak features.

##### Feature Extraction

- Maps data into smaller feature space that captures the bulk of the information in the data
  - a.k.a data compression
- Motivation:
  - Improves computational efficiency
  - Reduces curse of dimensionality
- Techniques
  - Principle component analysis (PCA)
    - It is unsupervised linear approach to feature extraction
    - Finds pattern based on correlations between features
    - Constructs principal components: orthogonal axes in directions of maximum variance.
    - scikit-learn: `sklearn.decomposition.PCA`

        ```py
        pca = PCA(n_components=2)
        X_train_pca = pca.fit_transform(X_train_std)
        lr = LogisticRegression()
        lr.fit(X_train_pca)
        ```

  - Linear discriminant analysis (LDA)
    - A supervised linear approach to feature extraction
    - Transforms to subspace that maximizes class separability
    - Assumes data is normally distributed
    - Used for dimensionality reduction of features
    - Can reduce to at most #classes-1 components
    - scikit-learn: `sklearn.discriminant_analysis.LinearDiscriminantAnalysis`
  - Kernel versions of these for fundamentally non-linear data

##### Model Tuning: Bagging/Boosting

Feature extraction and selection are relatively manual processes. Bagging and boosting are automated or semi-automated approaches to determining which features to include.

- Bagging (Bootstrapping Aggregation)
  - Generate a group of weak learners that when combined together generate higher accuracy
  - Reduces variance
  - Keeps bias the same
  - sklearn:
    - `sklearn.ensemble.BaggingClassifier`
    - `sklearn.ensemble.BaggingRegressor`

- Boosting
  - Assign strengths to each weak learner
  - Iteratively train learners using misclassified examples by previous weak learners.
  - It is used for models that have a high bias and accepts weights on individual samples
  - sklearn:
    - sklearn.ensemble.AdaBoostClassifier
    - sklearn.ensemble.AdaBoostRegressor
    - sklearn.ensemble.GradientBoostingClassifier
  - XGBoost library

## Aspects to be considered

1. ### Overfitting

    Informally, overfitting typically occurs when we try to fit a complex model with an inadequate amount of training data. And overfitting model uses its ability to capture complex patterns by being great at predicting lots and lots of specific data samples or areas of local variation in the training set. But it often misses seeing global patterns in the training set that would help it generalize well on the unseen test set.

2. ### Underfitting

    The model is too simple for the actual trends that are present in the data. It doesn't even do well on the training data and thus, is not at all likely to generalize well to test data.

- To avoid these, the below points would help:
  1. First, try to draw the data with respect to the labels and try to figure out the relationship between, whether its linear, quadratic, polynomial and so on.
  2. Reduce the number of features.
     1. Manually select which features to keep.
     2. Use a model selection algorithm.
  3. Regularization
     1. Keep all the features, but reduce the magnitude of parameters.
     - It works well when there are a lot of slightly useful features.

## ML Data Readiness

- ML data readiness is the capability to evaluate readiness, or worthiness, of datasets for use in an ML based predictive solution.

- ML data readiness evaluation is typically done prior to embarking on an ML project. It can help:

  - Evaluate the predictive potential of the dataset
  - Identify predictive outcomes that can be supported
  - Build initial ML models and understand relative performance

## Productizing a ML Model

### Aspects to consider

- Model Hosting
- Model deployment
- Pipeline to provide features vectors
- Code to provide low-latency and/or high-volume predictions
- Model and data updating and versioning
- Quality monitoring and alarming
- Data and model security and encryption
- Customer privacy, fairness, and trust
- Data provider contractual constraints (eg., attribution, cross-fertilization)

### Types of Production environments

#### Batch predictions

- Useful if all possible inputs known a priori (eg., all product categories for which demand is to be forecast, all keywords to bid)
- Predictions can still be served real-time, simply read from pre-computed values

#### Online Predictions

- Useful if input space is large (e.g., customer's utterances or photos, detail pages to be translated)
- Low latency requirement (e., at most 100ms)

#### Online training

- Sometimes training data patterns change often, so need to train online (eh., fraud detection)

### Business metrics vs Model Metrics

- Business metrics may not be the same as the performance metrics that are optimized during training. Why?
  - click-through rate
- Ideally, performance metrics are highly correlated with business metrics.

#### Metrics for Logistic Regression

##### Confusion Matrix

- True Positive (TP): When model predicts Positive outcome as Positive
- True Negative (TN): When model predicts Negative Outcome as Negative
- False Positive (FP): When model predicts Positive outcome as Negative
- False Negative (FN): When model predicts Negative outcome as Positive

To determine how well is the Logistic Model, the are some some metrics:

- **Accuracy**:
  - Accuracy (also called Score) is the proportion of correctly labeled rows divided by the total number of rows in data set. There are some cases when Accuracy won't work well, when there are large class imbalances in the dataset.

$$\text{Accuracy} = \frac{TP+TN}{TP+TN+FP+FN}$$

- **Precision**:
  - Out of all the items labeled as positive, how many truly belong to the positive class.

$$\text{Precision} = \frac{TP}{TP+FP}$$

- **Recall**:
  - Out of all the items that are truly positive, how many were correctly classified as positive. Or simply, how many positive items were 'recalled' from the dataset.

$$\text{Recall} = \frac{TP}{TP+FN}$$

##### Metrics for Linear Regression

- Mean Squared Error
  - Average squared error over entire dataset
  - Mean squared error(MSE) = $\frac{1}{N}\sum_{i=1}^N(\widehat{y} - y_i)^2$
  - Very commonly used
  - scikit-learn: sklearn.metrics.mean_squared_error
- $R^2$ error
  - $R^2 = 1 - \frac{\text{Sum of Squared Error (SSE)}}{\text{Var}(y)}$ which is between 0 and 1
  - Interpretation: Fraction of variance accounted for by the model
  - Basically, standardized version of MSE
  - Good $R^2$ are determined by actual problem
  - $R^2$ always increase when more variables are added tp the model
  - Adjusted $R^2 = 1-(1-R^2)\frac{\text{no. of data pts.} -1}{\text{no. of data pts. - no. of variables}-1}$
  - Takes into account of the effect of adding more variables such that it only increases when the added variables have significant effect in prediction
- Confidence Interval
  - An average computed on a sample is merely an estimate of the true population mean.
  - Confidence interval: Quantifies margin-of-error between sample metric and true metric due to sampling randomness
  - Informal interpretation: with x% confidence, true metric lies within the interval.
  - Precisely: If the true distribution is as stated, then with x% probability the observed value is in the interval.
  - Z-score: Quantifies how much the value is above or below the mean in terms of its standard deviation

### Storage

- Row-oriented formats:
  - comma/tab-separated values (CSV/TSV)
  - Read-only DB (RODB): Internal read-only file-based store with fast key-based access
  - Avro: allows schema evolution for Hadoop
- Column-oriented formats:
  - Parquet: Type-aware and indexed for Hadoop
  - Optimized row columnar (ORC): Type-aware, indexed, and with statistics for Hadoop
- User-defined formats:
  - JavaScript object notation (JSON): For key-value objects
  - Hierarchical data format 5 (HDF5): Flexible data model with chunks
- Compression can be applied to all formats
- Usual trad-offs: Read/write speeds, size, platform-dependency, ability for schema to evolve, schema/data separability, type richness

### Model and Pipeline Persistence

- Predictive Model Markup Language (PMML):
  - Vendor-independent XML-based language for storing ML models
  - Support varies in different libraries:
    - KNIME (analytics/ML library): Full Support
    - Scikit-learn: Extensive support
    - Spark MLlib: Limited Support

- Custom methods:
  - Scikit-learn: Uses the Python pickle method to serialize/deserialize Python objects
  - Spark MLlib: Transformers and Estimators implement ML Writable
  - TensorFlow (deep learning library): Allows saving of MetaGraph
  - MxNet (deep learning library): Saves into JSON

### Model Deployment

- Technology transfer: Experimental framework may not suffice for production
  - A/B testing or shadow testing: Helps catch production issues early

### Monitoring

- It is important to monitor quality metrics and business impacts with dashboards, alarms, user feedback, etc.:
  - The real-world domain may change over time.
  - The software environment may change.
  - High profile special cases may fail.
  - There may be a change in business goals.

### Maintenance

- Performance deterioration may require acquire new tuning:
  - Changing goals may require new metrics.
  - A changing domain may require changes to validation set.
  - Your validation set may be replaced over time to avoid overfitting.

## Common Mistakes

- You solved the wrong problem
- The data was flawed
- The solution didn't scale
- Final result doesn't match with the prototype's results.
- It takes too long to fail
- The solution was too complicated
- There weren't enough allocated engineering resources to try out long-term science ideas.
- There was a lack of a true collaboration.
