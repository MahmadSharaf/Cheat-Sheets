- [Feature Engineering](#feature-engineering)
  - [Feature Engineering Definition](#feature-engineering-definition)
  - [Feature Engineering Techniques](#feature-engineering-techniques)
    - [Feature Selection](#feature-selection)
      - [Feature Selection Methods](#feature-selection-methods)
    - [Feature Learning (Representation Learning)](#feature-learning-representation-learning)
    - [Feature Extraction](#feature-extraction)
    - [Feature Combination](#feature-combination)
    - [Feature Detection](#feature-detection)
    - [Dimensionality Reduction](#dimensionality-reduction)
  - [Data](#data)
    - [Data types](#data-types)
    - [Problems with data](#problems-with-data)
    - [Correlation Coefficient](#correlation-coefficient)
      - [Correlation Coefficient Definition](#correlation-coefficient-definition)
      - [Measures of Correlation](#measures-of-correlation)
      - [Evaluating Correlations](#evaluating-correlations)

# Feature Engineering

## Feature Engineering Definition

- It is engineering the features to get the best out of the model.
- It is not one technique or even a set of techniques that can be used as a whole, it is a block and tackle work which requires iterative working and improving the features of the model.
- There are no set of techniques that apply to all models. It is specific to the problem and data in the problem.

## Feature Engineering Techniques

### Feature Selection

- It is the use of some techniques to select the most relevant features of the model.
- Feature selection technique is a possible solution when the there many variables in the data. Most of which contain little information, some of which are meaningful, or meaningful variables are independent of each other.

#### Feature Selection Methods

1. Filter methods:
   - Apply statistical methods to extract the most relevant features.
   - It is independent on building and training the model.
   - Rely on statistical properties of features, either individually (univariate) or jointly (multivariate).
   - Examples:
     - Chi-Square analysis
     - ANOVA analysis
     - Mutual information
2. Embedded methods:
   - Build a ML model that assigns importance to difference features and select those features that are the most important.
   - The feature selection is embedded within the model training phase.
   - Only specific types of models perform feature selection.
   - Examples:
     - Lasso Regression
     - Decision trees
3. Wrapper methods:
   - They lie between filter methods and embedded methods.
   - It is independent of the model
   - Train a number of different candidate models (same model type), in each model has a different subset of features, and choose that subset of features that produces the best model.
   - Examples:
     - Forward stepwise: It is by adding a new feature to the model, if the model improves, the new feature becomes a part of the model
     - Backward stepwise: It is the same as Forward Stepwise, but by removing a feature.

### Feature Learning (Representation Learning)

- It is the rely on ML algorithms rather than human experts to "learn" the best representations of complex data such as images, videos.
- It is reduces or eliminates the need of domain experts, and provides scalability to the algorithm due to the automated action
- It can use supervised or unsupervised techniques to learn latent features that exist in the data.
- Supervised examples:
  - **Neural networks**, the data just fed into the model, and the model will find out which latent features are more significant.
- Unsupervised examples:
  - **Clustering**, finds patterns in the data
  - **Dictionary learning**, suitable for image data. It learns sparse representations of dense features.
  - **Autoencoders**, suitable for Neural Networks models. It extracts latent significant representations of the data.

### Feature Extraction

- It involves the transformation or reorientation of the features into fundamentally transformed derived features, which often unrecognizable and cannot be interpreted as is.
- Feature extraction usually also leads to dimensionality reduction.
- Examples:
  - Image descriptors for images
  - Principle components for matrices
  - Tf-Idf for documents

### Feature Combination

- It is the combination of features together to get a feature that is more meaningful and has more predictive power.
- Some features naturally work better when considered together. Or the original feature might be raw or too granular.

### Feature Detection

- In the context of image processing, algorithms that detect and extract the appropriate, most interesting, features from images.
- Identify right feature representations of images.
- Starting point of many computer vision algorithms.
- Repeatability is an important factor.
- Whether the same feature will be detected in two or more images.
- Features can be:
  - Abstractions such as: style, texture
  - Content such as: edges, corners
- Interest points: Points in the image that define what is interesting and must be captured in the feature representation of the image. Key points should be:
  - Well defined and Identifiable, such as Edges, intensity maxima or minima, landing points.
  - Should not be affected by operations such as:
    - Rotation
    - Translation
    - Expansion
    - Warping
- Interest regions (blobs): Regions within an image within which points are similar and share properties that are different from surrounding points.
  - They are complementary to points of interest
  - Capture additional information
    - Object recognition
    - Object motion tracking
    - Texture analysis and detection
    - Image segmentation
- Image Descriptors: numeric arrays which give key features of images, such as shape, color, texture (and motion, in the case of videos).
  - Can be computed by different algorithms
    - Scale Invariant Feature Transform (SIFT)
    - Daisy
  - Should be independent of position of associated key points.
  - Should be robust to transformations.
  - Should be scale independent.
  - Used for feature matching or pattern matching across images.
  - Help in comparing key points across images.
  - Can use distance measures to compare. Key points whose descriptors have the smallest distances are matches.

### Dimensionality Reduction

- It is about reducing the complexity of the input data. It also involves reorienting the features along new axes, which better represent the data.
- Excessive number of features leads to severe problems. It is know as Curse of Dimensionality.
- It applies preprocessing algorithms to reduce complexity of raw features. Specifically, it aims to reduce the number of features while preserving as much as information as possible.
- It is a form of unsupervised learning
- Examples:
  - Principle Components Analysis (PCA), works with linear data
  - Manifold Learning, for non-linear data. It involves unrolling complex forms of data in a higher axis to express data in a simpler form.
  - Latent Semantic Analysis: It is a topic modeling and dimensionality reduction technique that used with text data.
  - Autoencoding for images.

## Data

### Data types

1. Numeric
   1. Ratio Scale: ex: 60 KGs are twice the weight of 30 KGs
   2. Interval Scale: ex: 60 Fahrenheit is not twice the temperature of 30 Fahrenheit
2. Categorical
   1. Ordinal: ex: small, medium, large
   2. Nominal: ex: cat, dog

### Problems with data

1. Insufficient data
   1. Models trained with insufficient data perform poorly in prediction.
   2. Paradoxically leads to either
      1. Overfitting: Read too much for too little data
      2. Underfitting: Build overly simplistic model from available data.
2. Too much data
   1. Curse of dimensionality: Too many columns
   2. Outdated historical data: Too many rows
3. Non-representative data
   1. Data not representative of the real world
   2. Leads to biased models that perform poorly in practice
   3. Mitigate using oversampling and undersampling
4. Missing data
   1. Deletion
   2. Imputation
5. Duplicate data
6. Outliers

### Correlation Coefficient

#### Correlation Coefficient Definition

- Any statistical relationship, whether causal or not, between two random variables.
- Correlation doesn't mean causation
- Correlation coefficients provide a measure of the**strength** and**direction** of a**linear** relationship.

#### Measures of Correlation

1. Pearson
   - Most common
   - Most restrictive
   - Provides the Strength and Direction of a linear relationship
   - Assumes normally distributed data
   - Works only with numeric, both ratio and interval scale.
   - Doesn't work with ordinal data
2. Kendall
   - General purpose
   - Rank correlation, that takes into account the difference in order between variables.
   - It works with ratio scale, interval scale, and ordinal data. But not with nominal data.
3. Spearman
   - Rank correlation, that takes into account the difference in order between variables.
   - It works with ratio scale, interval scale, and ordinal data. But not with nominal data.
   - More appropriate for certain cases of associating two variables.
   - Assumes monotonic relationship i.e. either increasing or decreasing

#### Evaluating Correlations

- Strong: $0.7≤∣r∣≤1.0$
- Moderate: $0.3≤∣r∣<0.7$
- Weak: $0.0≤∣r∣<0.3$
