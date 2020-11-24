# NLP Cheat Sheet

## NLP Terms

- Corpus: Large collection of words or phrases - can come from different sources: documents, web sources, database
  - [Common Crawl Corpus](http://aws.amazon.com/de/datasets/common-crawl-corpus/): web crawl data composed of over 5 billion web pages (541 TB)
  - [Reddit Submission Corpus](https://www.reddit.com/r/datasets/comments/3mg812/full_reddit_submission_corpus_now_available_2006/): publicly available Reddit submissions (42 GB)
  - [Wikipedia XML Data](http://aws.amazon.com/de/datasets/wikipedia-xml-data/): complete copy of all Wikimedia wikis, in the form of wikitext source and metadata embedded in XML. (500 GB)
  - Etc.
- Token: Words or phrases extracted from documents
- Feature vector: A numeric array that ML models use for different tasks such as training and prediction

## NLP Pipeline

1. Text Data
2. Text Preprocessing (Cleaning and formatting)
   - Stop words removal, Stemming, Lemmatization
3. Vectorization (Convert to numbers)
4. Train ML Model using numerical data
    - K Nearest Neighbors (KNN), Neural Network, etc.

### Text Preprocessing

- Tokenization:
  - Splits text/document into small parts by white space and punctuation.
  - These tokens will be used in the next steps in the pipeline.
  - EX: “I don’t like eggs.” to “I”, “do”, “n’t”, “like”, “eggs”, “.”
- Stop Words Removal:
  - Stop words: Some words that frequently appear in texts, but they don’t contribute too much to the overall meaning.
  - Common stop words: “a”, “the”, “so”, “is”, “it”, “at”, “in”, “this”, “there”, “that”, “my”
  - EX: “There is a tree near the house” to “tree near house”
  - There stop words precreated in the Natural Language Tool Kit ([NLTK](https://www.nltk.org/)) library.
- Stemming:
  - Set of rules to slice a string to a substring that usually refers to a more general meaning.
  - The goal is to remove word affixes (particularly suffixes) such as “s”, “es”, “ing”, “ed”, etc.
  - The issue: It doesn’t usually work with irregular forms such as irregular verbs: “taught”, “brought”, etc.
- Lemmatization:
  - Similar to stemming, but more advanced. It uses a look-up dictionary.
  - Handles more situations and usually works better than stemming.
  - For the best results, correct word position tags should be provided: “adjective”, “noun”, “verb” etc.
- Stemming vs. Lemmatization
  - Original sentence: "the children are playing outside. the weather was better yesterday."
  - Stemming => “the children are play outside. the weather was better yesterday”
  - Lemmatization => “the child be play outside. the weather be good yesterday”

### Text Vectorization

- Bag of Words (BoW):
  - Bag of Words method converts text data into numbers.
  - It does this by
    - Creating a vocabulary from the words in all documents
    - Calculating the occurrences of words:
      - binary (present or not)
      - word counts
      - word frequency
- Term Frequency (TF):
  - It increases the weight for common words in a document.
  - 𝑡𝑓(𝑡𝑒𝑟𝑚, 𝑑𝑜𝑐) = $\frac{\text{𝑛𝑢𝑚𝑏𝑒𝑟 𝑜𝑓 𝑡𝑖𝑚𝑒𝑠 𝑡ℎ𝑒 𝑡𝑒𝑟𝑚 𝑜𝑐𝑐𝑢𝑟𝑠 𝑖𝑛 𝑡ℎ𝑒 𝑑𝑜𝑐}}{\text{𝑡𝑜𝑡𝑎𝑙 𝑛𝑢𝑚𝑏𝑒𝑟 𝑜𝑓 𝑡𝑒𝑟𝑚𝑠 𝑖𝑛 𝑡ℎ𝑒 𝑑𝑜𝑐}}$
- Inverse Document Frequency (IDF):
  - It decreases the weights for commonly used words and increases weights for rare words in the vocabulary.
  - id𝑓(𝑡𝑒𝑟𝑚, 𝑑𝑜𝑐) = $log(\frac{\text{𝑛𝑢𝑚𝑏𝑒𝑟 𝑜𝑓 documents}}{\text{number of documents containing the term }+1})+1$
- Term Frequency-Inverse Document Frequency (TF-IDF):
  - Combines term frequency and inverse document frequency.
  - tf-idf(term, doc) = 𝑡𝑓(𝑡𝑒𝑟𝑚, 𝑑𝑜𝑐)∗𝑖𝑑𝑓(𝑡𝑒𝑟𝑚)
- N-gram:
  - An n-gram is a sequence of n tokens from a given sample of text or speech.
  - We can include n-grams in our term frequencies too.
  - Used in words Suggestions.

### Train ML Model

#### K Nearest Neighbors (KNN)

- KNN predicts new data points based on K similar records from a dataset.
- How it works:
  - Choose K, which is the number of nearest neighbors for the data point
  - Calculate the distances from the data point to all data points.
  - Find the K nearest neighbors
  - Pick the majority class
- KNN in SciKit learn: KNeighborsClassifier(n_neighbors=5, metric='minkowski’, p=2)
  - How to choose K (n_neighbors):
    - Use a validation set to select an appropriate value for K.
  - What is the effect of K on the model?
    - Low K (like K=1): predictions based on only one data sample could be greatly impacted by noise in the data (outliers, mislabeling)
    - Large K: more robust to noise, but the nearest “neighborhood” can get too inclusive, breaking the “locality”, and a class with only a few samples in it will always be outvoted by the other classes
    - Rule of thumb in selecting K:
      - K = $\sqrt{n}$, where $n$ is the number of data samples.
  - Choosing the Distance Metric (metric):
    - Data samples are considered similar to each other if they are close to each other, as determined by a specific distance metric.
    - How to choose the distance metric?
      - Real-valued features: Minkowski
        - Similar types: p = 2, Euclidean
        - Mixed types (lengths, ages, salaries): p = 1, Manhattan (taxi-cab)
      - Binary-valued features: Hamming
        - Number of positions where the values of two vectors are different
      - Boolean-valued features: Jaccard
        - Ratio of shared values to the total number of values of two vectors
      - High dimensional feature space: cosine similarity
        - The angle between two vectors (similarity irrespective of their sizes)
- Curse of Dimensionality:
  - With too many features, KNN becomes computationally expensive and difficult to solve.
- Feature Scaling:
  - Features should be on the same scale when using KNN.

### Decision Trees

- Decision Trees are flowchart-like structures that can be used for classification or regression tasks.
- Steps to do:
  - Select “the best feature” to split (we will see how to select)
  - Separate the training samples according to the selected feature
  - Stop if we have samples from a single class or if we used all features, and note it as a leaf node
- Top down approach: Grow the tree from root node to leaf nodes.
- A good split results in overall less uncertainty (impurity).
- How to Measure Uncertainty:
  - Gini impurity:
    - $i(p_{1},...,p_{k}) = \sum_{k=1}^{n}p_{k}(1-p_{k})$
    - If we have only + samples or only - samples then it is Low Uncertainty.
    - If we have mix of + and - samples then it is High uncertainty
    - ![Gini Impurity Curve](NLP%20images/Gini%20Impurity%20Curve.png)
    - Information Gain:
      - Expected reduction in uncertainty due to selected feature.
      - Gini gain is calculated when building a decision tree to help determine which attribute gives us the most information about which class a new data point belongs to.
      - $i(p_{1},...,p_{k})_{before} - i(p_{1},...,p_{k})_{after}$
      - EX:
        - ![Gini information gain](NLP%20images/Gini%20information%20gain%20example.png)
        - Overcast leaf = pure. A leaf node is said to be pure if all of its examples belong to the same class.
        - $i_{before} = \frac{9}{14}*\frac{5}{14} + \frac{5}{14}*\frac{9}{14} = 0.46$
        - $i_{sunny} = \frac{2}{5}*\frac{3}{5}+\frac{3}{5}*\frac{2}{5} = 0.48$
        - $i_{overcast} = \frac{4}{4}*\frac{0}{4}+\frac{0}{4}*\frac{4}{4} = 0$
        - $i_{rainy} = \frac{3}{5}*\frac{2}{5}+\frac{2}{5}*\frac{3}{5} = 0.48$
        - $i_{weather} = \frac{5}{14}*i_{sunny} + \frac{4}{14}*i_{overcast} + \frac{5}{14}*i_{rainy}=0.34$
        - $gain_{weather} = 0.46-0.34=0.12$
  - [Entropy](https://d2l.ai/chapter_appendix-mathematics-for-deep-learning/information-theory.html#entropy)

### Ensemble Learning

- Ensembles can be applied to both regression and classification problems
- Ensemble methods create a strong model by combining the predictions of multiple weak models (aka weak learners or base estimators) built with a given dataset and a given learning algorithm.
- As the same model is trained on the same dataset, there are some techniques are applied to get a different model.
  - Bagging (**B**ootstrap **Agg**regat**ing**):
    - Randomly draw N samples of a fix size from the training set (with replacement) - bootstrap technique.
    - Usually 63.2% of the original dataset would be in the sample, the rest would be repeats.
    - Example: given data [1, 2, 3, 4, 5, 6, 7, 8, 9], samples of size 6 are: [ 1, 1, 2, 4, 9, 9]; [ 2, 4, 5, 5, 7, 7]; [ 1, 1, 1, 1, 1, 1]; [ 1, 2, 4, 5, 7,9]
    - Build independent estimators of same type on each subset.
      - Note the ”independent” estimators here, which implies that bagging could easily be parallelized for speed and functionality!
    - Majority vote or average the predictions from all estimators
    - The most popular bagging model is bagging trees, known as Random Forest
    - Bagging reduces the variance, does not increase bias, therefore the test error goes down.

    ```py
    BaggingClassifier(
        base_estimator=None, # Any base_estimator – classifier or regressor
        n_estimators=10, # The number of trees to be modeled
        max_samples=1.0, # The number of samples to draw from X to train each base estimator (with replacement by default, see bootstrap for more details).
        bootstrap=True # That is, When random subsets of the dataset are drawn as random subsets with replacement, then the method implementing is Bagging a discussed previously.
        )

    ```

  - Boosting: building estimators sequentially, each subsequent one attempting to boost performance overall, by overcoming/reducing the errors of the previous one.
  - Voting
  - Stacking

#### Random Forest

- Draw random subsets (with replacement) from the original dataset
- Build a decision tree on each bootstrapped subset
- Combine predictions from each tree for final prediction
- SciKit Learn: `RandomForestClassifier`
  
    ```py
    RandomForestClassifier(
      n_estimators=100, #the number of trees to be modeled
      max_samples =None, # the number of samples to draw from original data to train each tree (the size of the bootstrapped subsets)
      criterion='gini', # what to use to decide the splits (entropy as well)
      max_depth=None, # The maximum depth of a tree. Used to control over-fitting as Higher depth will allow model to learn relations very specific to a particular sample.
      min_samples_split=2, # Defines the minimum number of samples (or observations) which are required in a node to be considered for splitting. Used to control over-fitting as Higher values prevent a model from learning relations which might be highly specific to the particular sample selected for a tree. Too high values can lead to under-fitting hence, it should be tuned using CV.
      min_samples_leaf=1, # Defines the minimum samples (or observations) required in a terminal node or leaf. Used to control over-fitting similar to min_samples_split. Generally lower values should be chosen for imbalanced class problems because the regions in which the minority class will be in majority will be very small.
      class_weight=None # Weights associated with classes in the form: {class_label: weight} The “balanced” mode uses the values of y to automatically adjust weights inversely proportional to class frequencies in the input data
      )
    ```

#### Linear Regression

- It is used for regression problems
- It models the relationship between two variables x and y with a “line”.
- Linear regression formula: $y=w_0+w_1 x$, where x: feature, attribute; y: target, outcome; w0: intercept; w1: slope
- The vertical offset for each data point from the regression line is the error between the true label y and the prediction based on x
- The “best” line minimizes the sum of the squared errors (SSE):  $∑(y_i−\hat{y}_i )^2$

#### Logistic Regression

- It used for classification problems
- A sigmoid function is applied to the Linear Regression equation
- sigmoid function $(y)=\frac{1}{1+e^{-y}}$
- Can define a “threshold” at 0.5:
  - if sigmoid(y)< 0.5, class 0
  - if sigmoid(y)≥ 0.5, class 1
- Log-loss (Binary Cross-Entropy):
  - A numeric value that measures the performance of a binary classifier when model output is a probability between 0 and 1
  - To improve model learning from the data, we want to minimize it
  - LogLoss=$−(y∗log(p)+(1−y)∗log⁡(1−p))$ where y: true class ∈{0, 1}, p: probability of class

### Optimization

- In ML, use optimization to minimize an error function of the ML model.
- Gradient Optimization
  - It is the direction and rate of the fastest increase of a function.
  - It can be calculated with partial derivatives of the function f with respect to each input variable in w: $\frac{\partial f(w)}{\partial w}$
  - Because it has a direction, the gradient is a “vector”.
- Gradient Descent method:
  - Gradient Descent method uses gradients to find the minimum of a function iteratively.
  - Taking steps (proportional to the gradient size) towards the minimum, in the opposite direction of the gradient.
  - Gradient Descent Algorithm:
    - Start at an initial point $w$.
    - Update: $w_{new} = w_{current} -$ step_size * gradient
    - The size of the update, is controlled by this step_size parameter, also known in ML as the learning rate.

### Regularization

- Underfitting: Model too simple, fewer features, smaller weights, weak learning.
- Overfitting: Model too complex, too many features, larger weights, weak generalization.
- ‘Good Fit’ Model: Compromise between fit and complexity (drop features, reduce weights).
- Regularization does both: penalizes large weights, sometimes reduced all the way to zero
- It a ML technique that helps over/underfitting models adjust to be more useful on both training and validation sets.
- Most of the time regularization is used to control overfitting, by penalizing large weights, sometimes reducing some all the way to zero (in which case, the corresponding features are dropped all together!)
- It tunes model complexity by adding a penalty score for complexity to the cost function.
- $C_{regularized} (w) = C(w) + \alpha * penalty(w)$
- Calibrate regularization strength by using a regularizer parameter, 𝛂
- Standard regularization types:
  - L2 regularization (Ridge):
    - It is a popular regularization choice, penalizes the model by minimizing the sum of the squared values of all features weights.
  - L1 regularization (LASSO) (short for Least Absolute Shrinkage and Selection Operator)
    - Is penalizing the sum of the absolute values of all features weights, shrinking some weights all the way to 0, due to the geometry of the L1 norm/abs value.
    - Useful as feature selection, since most weights shrink to 0 - sparsity
  - Both L2 and L1 (ElasticNet):
    - It’s applying both penalties, usually with the effect of a compromise between the two.
- Features must be scaled before regularization, to avoid any scaling issues.

#### Regression in SciKit Learn

- LinearRegression: sklearn Linear Regression (and regularization)
  - `LinearRegression()`
  - `Ridge(alpha=1.0)`: regression addresses some of the problems of LinearRegression by imposing a L2 penalty.
    - The regularizer parameter α≥0 controls the amount of regularization: the larger the value of α, the greater the amount of regularization/shrinkage and thus the coefficients become more robust to collinearity.
  - `RidgeCV(alpha=1.0, cv=5)`: implements ridge regression with built-in cross-validation of the alpha parameter (cv=5)
  - `Lasso(alpha=1.0)`, `LassoCV(alpha=1.0, cv=5)`
  - `ElasticNet(alpha=1.0, l1_ratio=0.5)`, `ElasticNetCV(cv=5)`

- LogisticRegression: sklearn Logistic Regression (and regularization)
  - `LogisticRegression(penalty='l2', C=1.0, l1_ratio=None)`
  - `LogisticRegressionCV(penalty='l2', C=1.0, l1_ratio=None, cv=5)`
  - Note that regularization is applied by default, and is using a slightly different regularizer parameter attached to the cost function not the penalty.
  - C = 1/alpha
  - The larger the value of C, the lower the amount of regularization

### Hyperparameters

- Hyperparameters are ML algorithms parameters that affect the structure of the algorithms and the performance of the models.
- Examples of hyperparameters:
  - K Nearest Neighbors: n_neighbors, metric
  - Decision trees: max_depth, min_samples_leaf, class_weight, criterion
  - Random Forest: n_estimators, max_samples
  - Ensemble Bagging: base_estimator, n_estimators
  - Hyperparameter tuning looks for the best combination of hyperparameters (combination that maximizes model performance).
- Hyperparameter tuning is the search for this best combination of hyperparameters, to improve a desired performance metric.

#### Grid Search

- It finds the optimum combination of hyperparameters by exhaustive search over specified parameter values.
- GridSearchCV(estimator, param_grid, scoring=None):
  - `estimator` is the ML model types. ex: `tree` for decision tree
  - `scoring` is your choice of model performance metric
  - `param_grid` is the hyperparameters values
    - ex: `param_grid ={ max_depth: [5, 10, 50, 100, 250], min_samples_leaf: [15, 20, 25, 30, 35]}`
  - `GridSearchCV` can be used as an estimator, with a fit and predict methods, it is also performing 5-fold Cross Validation by default for each combination of hyperparameters.
  - For the above example, 25 combinations of hyperparameters and with 5-fold CV for each combination, that would train 125 models. That will take time to complete.
  - Once all the combinations are evaluated, the model with the set of parameters which give the top metric is considered to be the best.
  - `GridSearchCV` returns the best combination of the hyperparameters, the best estimator equipped with these best hyperparameters, and will also report the performance metric of this best estimator.

#### Randomized Search

- A more efficient implementation of hyperparameter tuning.
- `RandomizedSearchCV(estimator, param_distributions, n_iter=10, scoring=None)`
  - `estimator` is the ML model types. ex: `tree` for decision tree
  - `scoring` is your choice of model performance metric
  - `param_grid` is the hyperparameters values
    - ex: `param_grid ={max_depth: [5, 10, 50, 100, 250], min_samples_leaf: uniform(15,35,5)}`
  - `n_tier` (default 10) is the number of random parameter settings that are sampled. It trades off runtime vs quality of the solution.
- In contrast to `GridSearchCV`, not all parameter values are tried out, but rather a fixed number of parameter settings is sampled from the specified distributions. The number of parameter settings that are tried is given by `n_iter`.
- `RandomizedSearchCV` also performs 5-fold CV by default for each combination of hyperparameters.
- Can sample from distributions (sampling with replacement is used), if at least one parameter is given as a distribution.
- If all parameters are presented as a list, sampling without replacement is performed.
- If at least one parameter is given as a distribution, sampling with replacement is used.
- It is highly recommended to use continuous distributions for continuous parameters.

#### Bayesian Search

- Bayesian Search method keeps track of previous hyperparameter evaluations and builds a probabilistic model.
- It tries to balance exploration (uncertain hyperparameter set) and exploitation (hyperparameters with a good chance of being optimum)
- It prefers points near the ones that worked well.
- AWS SageMaker uses Bayesian Search for hyperparameter optimization.

### Neural Networks

#### Perceptron

- It is the simplest neural network.
- It is a single layer neural network that uses one layer of a list of input features and one output.
- One of the features is a bias, same as intercept in linear regression, that gets combined a long with the other features.
- After having this linear combination, an activation function is applied. This function is usually non-linear and depends on the problem being tried to solve.

#### Neural Network Architecture

- Generally hard to interpret.
- Expensive to train, fast to predict
- A neural network consisting of input, hidden and output layers.
- Each layer is connected to the next layer.
- An activation function is applied on each hidden layer (and output layer).
- Activation Functions:
  - Logistic (sigmoid):
    - The most common activation function. Squashes input to (0,1).
    - $$f(x) = \frac{1}{1+e^{-x}}$$
  - Hyperbolic tangent (tanh):
    - Squashes input to (-1, 1).
    - $$f(x) = \frac{e^x - e^{-x}}{e^x+e^{-x}}$$
  - Rectified Linear Unit (ReLU):
    - Popular activation function. Anything less than 0, results in zero activation.
    - $$\displaystyle f(x) = \begin{cases}0, & \text{if $x < 0$} \\ x, & \text{if $x \geq 0$}\end{cases}$$
- Output Activations/Functions:
  - Sigmoid:
    - For binary classification ML problems
    - Output probability for each class, in (0,1)
    - Logistic regression of output of last layer
    - $$f(x) = \frac{1}{1+e^{-x}}$$
  - Softmax:
    - For Multi-class classification ML problems
    - Output probability for each class, in (0,1)
    - Sum of outputs to be 1 (probability distribution)
    - Training drives target class values up, others down
    - $$f(x_i) = \frac{\exp(x_i)}{{\sum}_i \exp(x_i)}   $$
  - Linear/ ReLU:
    - For Regression ML problems
    - $$\displaystyle f(x) = \begin{cases}0, & \text{if $x < 0$} \\ x, & \text{if $x \geq 0$}\end{cases}$$
- Scikit-learn: `sklearn.neural_network.MLPClassifier`.
- Deep Learning Frameworks:
  - MXNet
  - TensorFlow
  - Caffe
  - PyTorch

#### Build and Train a Neural Network

- Different activation/output functions can be chosen for different layers, don’t need to be the same, although all neurons in same layer will use same activation
- The activation functions are also hyperparameters of the NN, and need to be tuned by using a validation set, to figure out what choices perform best.
- Steps to train the NN:
  - The network is initialized with initial values for the neurons weights.
  - Forward Pass:
    - It is the step in which the inputs are passed through each layer of the network and get computed, until it reaches the output.
  - Cost (error) functions:
    - It is where the outputs are compared to the true values.
    - Cross entropy for logistic.
      - For Binary Classification problems:
      - A numeric value that measures the performance of a binary classifier when model output is a probability between 0 and 1
      - $C = -\frac{1}{n}{\sum_{examples} y \ln(p) + (1-y) \ln(1-p)}$
    - Cross entropy for Softmax is used:
      - For Multi-class classification problems
      - Extends the cross entropy for sigmoid loss beyond two classes to multi-class classification
      - $C = -\frac{1}{n}{\sum_{examples}}\,{\sum_{classes} y_i \ln(p_i)}$
    - For Regression problems:
      - Mean Squared Error is used
      - $C = \frac{1}{n}{\sum_{examples}}(y-p)^2$
    - Cost function is selected according to problem: Binary, Multi-class Classification or Regression.
    - Update network weights by applying the gradient descent method and back propagation.
    - Adjust the old value of a weight to a new value of the weight, by using a so-called learning rate and the gradient of the cost fct with respect to that weight.
    - ${w}_{new} = {w}_{old} - learning\_rate * \frac{\partial{C}}{\partial{w}}$
  - Back Propagation:
    - The back propagation algorithm begins by comparing the actual NN output by the forward pass/forward propagation process to the expected value (target).
    - Then moves backward through the network, slightly adjusting each of the weights in a direction that reduces the size of the error by a small degree.
- Both forward and back propagation are re-run hundred/thousands of times on each input combination until the network can accurately predict the expected output of the possible inputs using forward propagation.

#### Convolutional Neural Networks

- It is very useful in image analysis
- The input is an image or a sequence of images.
- Kernel is used as filter to extract local features.

#### Recurrent Neural networks

- It consists of multiple inputs layer, multiple hidden layers and multiple output layer.
- Each node outputs to the next input node.

## References

- [AWS ML University](https://www.youtube.com/watch?v=xUxw6C_z2kA&list=PL8P_Z6C4GcuWfAq8Pt6PBYlck4OprHXsw&index=8) and its [repo](https://github.com/aws-samples/aws-machine-learning-university-accelerated-nlp)