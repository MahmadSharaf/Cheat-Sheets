# Data Analysis

- [Data Analysis](#data-analysis)
  - [Process Overview](#process-overview)
    - [Step 1: Ask questions (Extract)](#step-1-ask-questions-extract)
    - [Step 2: Wrangle data (Clean)](#step-2-wrangle-data-clean)
    - [Step 3: Perform EDA (Exploratory Data Analysis)](#step-3-perform-eda-exploratory-data-analysis)
    - [Step 4: Draw conclusions (or even make predictions)](#step-4-draw-conclusions-or-even-make-predictions)
    - [Step 5: Communicate your results (Share)](#step-5-communicate-your-results-share)
  - [Data Types](#data-types)
    - [1. Quantitative data](#1-quantitative-data)
      - [Continuous vs. Discrete](#continuous-vs-discrete)
    - [2. Categorical data](#2-categorical-data)
      - [Categorical Ordinal vs. Categorical Nominal](#categorical-ordinal-vs-categorical-nominal)
    - [Quantitative vs. Categorical](#quantitative-vs-categorical)
  - [Descriptive vs. Inferential Statistics](#descriptive-vs-inferential-statistics)
    - [Descriptive Statistics](#descriptive-statistics)
    - [Inferential Statistics](#inferential-statistics)
    - [Looking Ahead](#looking-ahead)
  - [Descriptive (Summary) Statistics](#descriptive-summary-statistics)
    - [Analyzing Categorical Data](#analyzing-categorical-data)
      - [Terminologies](#terminologies)
    - [Analyzing Quantitative Data](#analyzing-quantitative-data)
      - [1. Measure of center](#1-measure-of-center)
        - [1.1 The Mean](#11-the-mean)
        - [1.2 The Median](#12-the-median)
          - [1.2.1 Median for Odd Values](#121-median-for-odd-values)
          - [1.2.2 Median for Even Values](#122-median-for-even-values)
        - [1.3 The Mode](#13-the-mode)
          - [1.3.1 No Mode](#131-no-mode)
          - [1.3.2 Many Modes](#132-many-modes)
      - [2. Measures of Spread](#2-measures-of-spread)
        - [Calculating the 5 Number Summary](#calculating-the-5-number-summary)
        - [2.1 Range](#21-range)
        - [2.2 IQR](#22-iqr)
        - [2.3 Standard Deviation](#23-standard-deviation)
        - [2.4 Variance](#24-variance)
        - [Important Final Points](#important-final-points)
      - [3. The Shape of the data](#3-the-shape-of-the-data)
      - [4. Outliers](#4-outliers)
        - [Common Techniques](#common-techniques)
        - [Outliers Advice](#outliers-advice)
  - [Inferential Statistics](#inferential-statistics-1)
    - [Probability](#probability)
      - [Probability Notations](#probability-notations)
      - [Probability Rules](#probability-rules)
      - [Probability Terminologies](#probability-terminologies)
      - [Probability Methods](#probability-methods)
        - [1. Binomial Distribution](#1-binomial-distribution)
          - [1.1 Unconditional Probability (Independent)](#11-unconditional-probability-independent)
          - [1.2 Conditional Probability (Dependent)](#12-conditional-probability-dependent)
        - [2. Bayes Rule](#2-bayes-rule)
        - [3. Normal Distribution](#3-normal-distribution)
        - [4. Sampling Distribution:](#4-sampling-distribution)
          - [Proportions (or Means) Characteristic](#proportions-or-means-characteristic)
          - [Important mathematical theorems](#important-mathematical-theorems)
          - [Sampling Distributions Techniques](#sampling-distributions-techniques)
  - [Statistical Notations](#statistical-notations)
  - [SQL](#sql)
    - [Why SQL](#why-sql)
    - [Why Businesses Like Databases](#why-businesses-like-databases)
    - [Types of Databases](#types-of-databases)
      - [Small Differences](#small-differences)
  - [Data Visualization](#data-visualization)
    - [Univariate analysis](#univariate-analysis)
    - [Bivariate analysis](#bivariate-analysis)
    - [More than two variables](#more-than-two-variables)
    - [Helpful resources](#helpful-resources)
  - [Communicating with data](#communicating-with-data)
    - [Visuals can be bad if](#visuals-can-be-bad-if)
    - [Visuals can be good if](#visuals-can-be-good-if)
    - [Visuals Encoding](#visuals-encoding)
  - [Tips](#tips)
    - [Simpson's Paradox](#simpsons-paradox)
    - [Statistical vs Practical Significance](#statistical-vs-practical-significance)

## Process Overview

### Step 1: Ask questions (Extract)

Either you're given data and ask questions based on it, or you ask questions first and gather data based on that later. In both cases, great questions help you focus on relevant parts of your data and direct your analysis towards meaningful insights. Obtain the data from a spreadsheet, SQL, the web, etc.

### Step 2: Wrangle data (Clean)

You get the data you need in a form you can work with in three steps: gather, assess, clean. You gather the data you need to answer your questions, assess your data to identify any problems in your data’s quality or structure, and clean your data by modifying, replacing, or removing data to ensure that your dataset is of the highest quality and as well-structured as possible.  
**Here we could use exploratory visuals.**

[Medium article about Data Imputation](https://medium.com/m/global-identity?redirectUrl=https%3A%2F%2Ftowardsdatascience.com%2F6-different-ways-to-compensate-for-missing-values-data-imputation-with-examples-6022d9ca0779)

### Step 3: Perform EDA (Exploratory Data Analysis)

You explore and then augment your data to maximize the potential of your analyses, visualizations, and models. Exploring involves finding patterns in your data, visualizing relationships in your data, and building intuition about what you’re working with. After exploring, you can do things like remove outliers and create better features from your data, also known as feature engineering.  
**Here we use exploratory visuals.**

### Step 4: Draw conclusions (or even make predictions)

This step is typically approached with machine learning or inferential statistics.  
**Here we might use either exploratory or explanatory visuals.**

### Step 5: Communicate your results (Share)

You often need to justify and convey meaning in the insights you’ve found. Or, if your end goal is to build a system, you usually need to share what you’ve built, explain how you reached design decisions, and report how well it performs. There are many ways to communicate your results: reports, slide decks, blog posts, emails, presentations, or even conversations. Data visualization will always be very valuable.  
**Here is where explanatory visuals live.**

## Data Types

There are two types of data Quantitative and Categorical:

### 1. Quantitative data

It takes on numeric values that allow us to perform mathematical operations (like the number of dogs).

We can think of quantitative data as being either continuous or discrete.

- **Continuous** data can be split into smaller and smaller units, and still a smaller unit exists. An example of this is the age of the dog - we can measure the units of the age in years, months, days, hours, seconds, but there are still smaller units that could be associated with the age.
- **Discrete** data only takes on countable values. The number of dogs we interact with is an example of a discrete data type.

#### Continuous vs. Discrete

To consider if we have continuous or discrete data, we should see if we can split our data into smaller and smaller units. Consider **time** - we could measure an event in years, months, days, hours, minutes, or seconds, and even at seconds we know there are smaller units we could measure time in. Therefore, we know this data type is continuous. **Height**, **age**, and **income** are all examples of **_continuous_** data. Alternatively, the number of **pages** in a **book**, **dogs** I count outside a **coffee shop**, or **trees** in a yard are **_discrete_** data. We would not want to split our dogs in half.

### 2. Categorical data

They are used to label a group or set of items (like dog breeds - Collies, Labs, Poodles, etc.).

#### Categorical Ordinal vs. Categorical Nominal

We can divide categorical data further into two types: Ordinal and Nominal.

- **Categorical Ordinal** data take on a ranked ordering (like a ranked interaction on a scale from Very Poor to Very Good with the dogs).
- **Categorical Nominal** data do not have an order or ranking (like the breeds of the dog).

In looking at categorical variables, we found **Gender**, **Marital Status**, **Zip Code** and your **Breakfast items** are **_nominal variables_** where there is no order ranking associated with this type of data. Whether you ate cereal, toast, eggs, or only coffee for breakfast; there is no rank ordering associated with your breakfast.  
Alternatively, the **Letter Grade** or **Survey Ratings** have a rank ordering associated with it, as **_ordinal_** data. If you receive an A, this is higher than an A-. An A- is ranked higher than a B+, and so on... **_Ordinal variables_** frequently occur on rating scales from very poor to very good. In many cases we turn these ordinal variables into numbers, as we can more easily analyze them.

### Quantitative vs. Categorical

Some of these can be a bit tricky - notice even though zip codes are a number, they aren’t really a quantitative variable. If we add two zip codes together, we do not obtain any useful information from this new value. Therefore, this is a categorical variable.

Height, Age, the Number of Pages in a Book and Annual Income all take on values that we can add, subtract and perform other operations with to gain useful insight. Hence, these are quantitative.

Gender, Letter Grade, Breakfast Type, Marital Status, and Zip Code can be thought of as labels for a group of items or individuals. Hence, these are categorical.

| Quantitative | Continuous          | Discrete                                              |
| ------------ | ------------------- | ----------------------------------------------------- |
| Examples     | Height, Age, Income | Pages in a Book, Trees in Yard, Dogs at a Coffee Shop |

| Categorical | Ordinal                     | Nominal                                 |
| ----------- | --------------------------- | --------------------------------------- |
| Examples    | Letter Grade, Survey Rating | Gender, Marital Status, Breakfast Items |

## Descriptive vs. Inferential Statistics

In this section, we will learn about how Inferential Statistics differs from Descriptive Statistics.

### Descriptive Statistics

Descriptive statistics is about describing our collected data using the measures: measures of center, measures of spread, shape of our distribution, and outliers. We can also use plots of our data to gain a better understanding.

1. Population: our entire group of interest.
2. Parameter: Numeric summary about a population. Frequently we do not know this value, so we must try and estimate.
3. Sample: Subset of the population.
4. Statistic: Numeric summary about a sample.

### Inferential Statistics

Inferential Statistics is about using our collected data to draw conclusions to a larger population. Performing inferential statistics well requires that we take a sample that accurately represents our population of interest.

A common way to collect data is via a survey. However, surveys may be extremely biased depending on the types of questions that are asked, and the way the questions are asked. This is a topic you should think about when tackling the first project.

1. Inference: Drawing conclusions regarding a population using information from a sample.

---

### Looking Ahead

Though we will not be diving deep into inferential statistics within this course, you are now aware of the difference between these two avenues of statistics. If you have ever conducted a hypothesis test or built a confidence interval, you have performed inferential statistics. The way we perform inferential statistics is changing as technology evolves. Many career paths involving Machine Learning and Artificial Intelligence are aimed at using collected data to draw conclusions about entire populations at an individual level. It is an exciting to time to be a part of this space, and you are now well on your way to joining the other practitioners!

---

## Descriptive (Summary) Statistics

### Analyzing Categorical Data

Categorical data is analyzed usually by looking at the counts or proportion of individuals that fall into each group. For example, if we were looking at the breeds of the dogs, we would care about how many dogs are of each breed, or what proportion of dogs are of each breed type.

**_Inferential Statistics_** is about using our collected data to draw conclusions to a larger population.

#### Terminologies

1. **Population**: our entire group of interest.
2. **Parameter**: numeric summary about a population
3. **Sample**: subset of the population
4. **Statistic**: numeric summary about a sample
5. **Inference**: Drawing conclusions regarding a population using information from a sample.

### Analyzing Quantitative Data

There are four main aspects to analyzing Quantitative data.

1. Measures of Center
2. Measures of Spread
3. The Shape of the data.
4. Outliers

#### 1. Measure of center

There are three measures of center:

1. Mean
2. Median
3. Mode

##### 1.1 The Mean

The mean is often called the average or the expected value in mathematics. We calculate the mean by adding all of our values together and dividing by the number of values in our dataset.

##### 1.2 The Median

The median splits our data so that 50% of our values are lower and 50% are higher.

###### 1.2.1 Median for Odd Values

If we have an odd number of observations, the median is simply the number in the direct middle. For example, if we have 7 observations, the median is the fourth value when our numbers are ordered from smallest to largest. If we have 9 observations, the median is the fifth value.

###### 1.2.2 Median for Even Values

If we have an even number of observations, the median is the average of the two values in the middle. For example, if we have 8 observations, we average the fourth and fifth values together when our numbers are ordered from smallest to largest.

**In order to compute the median, we MUST sort our values first.
Whether we use the mean or median to describe a dataset is largely dependent on the shape of our dataset and if there are any outliers.**

##### 1.3 The Mode

The mode is the most frequently observed value in our dataset.
There might be multiple modes for a particular dataset, or no mode at all.

###### 1.3.1 No Mode

If all observations in our dataset are observed with the same frequency, there is no mode.  
If we have the dataset: 1, 1, 2, 2, 3, 3, 4, 4  
There is no mode, because all observations occur the same number of times.

###### 1.3.2 Many Modes

If two (or more) numbers share the maximum value, then there is more than one mode.  
If we have the dataset: 1, 2, 3, 3, 3, 4, 5, 6, 6, 6, 7, 8, 9  
There are two modes 3 and 6, because these values share the maximum frequencies at 3 times, while all other values only appear once.

#### 2. Measures of Spread

Measures of Spread are used to provide us an idea of how spread out our data are from one another. Common measures of spread include:

1. Range
2. Interquartile Range (IQR)
3. Standard Deviation
4. Variance

##### Calculating the 5 Number Summary

The five-number summary consist of 5 values:

1. Minimum: The smallest number in the dataset.
2. Q1: The value such that 25% of the data fall below.
3. Q2: The value such that 50% of the data fall below.
4. Q3: The value such that 75% of the data fall below.
5. Maximum: The largest value in the dataset.

Calculating each of these values was essentially just finding the median of a bunch of different dataset. Because we are essentially calculating a bunch of medians, the calculation depends on whether we have an odd or even number of values.

##### 2.1 Range

The range is then calculated as the difference between the **maximum** and the **minimum**.

##### 2.2 IQR

The interquartile range is calculated as the difference between Q3 and Q1.

Example1:  
Dataset: 1, 5, 10, 3, 8, 12, 4, 1, 2, 8  
Rearrange: 1, 1, 2, 3, 4, 5, 8, 8, 10, 12

1. Calculate 5 numbers summary

   1. Min: 1
   2. Q1: 2
   3. Q2: 4.5
   4. Q3: 8
   5. Max: 12

2. Measure of center

   1. Mean: 54/10=5.4
   2. Median=Q2: (4+5)/2=4.5
   3. Mode: 8

3. Measure of spread
   1. Range: Max-Min=12-1=11
   2. IQR: Q3-Q1= 8-2=6

Example2:  
Dataset: 5, 10, 3, 8, 12, 4, 1, 2, 8
Rearrange: 1, 2, 3, 4, 5, 8, 8, 10, 12

1. Calculate 5 numbers summary

   1. Min: 1
   2. Q1: 2.5
   3. Q2: 5
   4. Q3: 9
   5. Max: 12

2. Measure of center

   1. Mean: 43/9=4.8
   2. Median=Q2: 5
   3. Mode: 8

3. Measure of spread
   1. Range: Max-Min=12-1=11
   2. IQR: Q3-Q1= 9-2.5=6.5

##### 2.3 Standard Deviation

The standard deviation is one of the most common measures for talking about the spread of data. It is defined as **the average distance of each observation from the mean.**  
![standard deviation](Images/deviation2.png)

##### 2.4 Variance

The variance average squared difference of each observation from the mean.  
![variance equation](Images/variance.png)

Example3:  
For the following set of data provide the value of the variance.  
Dataset: 1, 5, 10, 3, 8, 12, 4
Rearrange: 1, 3, 4, 5, 8, 10, 12

1. Calculate Median: (1+3+4+5+10+12)/7=43/7=6.14
2. Cal. Variance: (26.4+9.9+4.6+1.3+3.5+14.9+34.3)/7=94.9/7=13.55
3. std deviation: √(variance)=√13.55=3.68

##### Important Final Points

1. The variance is used to compare the spread of two different groups. A set of data with higher variance is more spread out than a dataset with lower variance. Be careful though, there might just be an outlier (or outliers) that is increasing the variance, when most of the data are actually very close.
2. When comparing the spread between two datasets, the units of each must be the same.
3. When data are related to money or the economy, higher variance (or standard deviation) is associated with higher risk.
4. The standard deviation is used more often in practice than the variance, because it shares the units of the original dataset.
5. Besides the mean return of an investment, we should also consider the spread associated with the return. But just because the standard deviation associated with each investment is the same, this does not mean the max you could make for each investment is the same.
6. If two datasets have the same variance, they will also have the same standard deviation.
7. If a dataset has a standard deviation of zero, all the data points must be the same.
8. Having the spread measures, does not give measures of center. Additionally, the range isn't directly associated with the standard deviation, so we can't make a claim that is always true like the final option.

#### 3. The Shape of the data

From a histogram we can quickly identify the shape of our data, which helps influence all of the measures we learned in the previous concepts. We learned that the distribution of our data is frequently associated with one of the three shapes:

1. Right-skewed
2. Left-skewed
3. Symmetric (frequently normally distributed)

| Shape              | Mean vs. Median          | Real World                                                                                                        |
| ------------------ | ------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| Symmetric (Normal) | Mean equals Median       | Height, Weight, Errors, Precipitation                                                                             |
| Right-skewed       | Mean greater than Median | Amount of drug remaining in a blood stream, Time between phone calls at a call center, Time until light bulb dies |
| Left-skewed        | Mean less than Median    | Grades as a percentage in many universities, Age of death, Asset price changes                                    |

#### 4. Outliers

Outliers are points that fall very far from the rest of our data points. This influences measures like the mean and standard deviation much more than measures associated with the five-number summary.

##### Common Techniques

When outliers are present we should consider the following points.

1. Noting they exist and the impact on summary statistics.
2. If typo - remove or fix
3. Understanding why they exist, and the impact on questions we are trying to answer about our data.
4. Reporting the 5 number summary values is often a better indication than measures like the mean and standard deviation when we have outliers.
5. Be careful in reporting. Know how to ask the right questions.

##### Outliers Advice

Below are my guidelines for working with any column (random variable) in your dataset.

1. Plot your data to identify if you have outliers.
2. Handle outliers accordingly via the methods above.
3. If no outliers and your data follow a normal distribution - use the mean and standard deviation to describe your dataset, and report that the data are normally distributed.
4. If you have skewed data or outliers, use the five-number summary to summarize your data and report the outliers.

---

Side note
If you aren't sure if your data are normally distributed, there are plots called [normal quantile plots](http://data.library.virginia.edu/understanding-q-q-plots/) and statistical methods like the [Kolmogorov-Smirnov](https://en.wikipedia.org/wiki/Kolmogorov%E2%80%93Smirnov_test) test that are aimed to help you understand whether or not your data are normally distributed. Implementing this test is beyond the scope of this class but can be used as a fun fact.

---
## Inferential Statistics

### Probability

- **Statistics** and **Probability** are different but strongly related fields of mathematics.
- In probability, we make *predictions* of future events based on models or causes that we assume.
- In statistics, we *analyze* the past events to infer what those models or causes could be.

![Probability vs Statistics](images/probability_vs_statistics.png)

#### Probability Notations

**P**: Probability of event  
**1-P**: Probability of opposite event  
**P(H)**: Probability of output H  
**P\*P\*P**: Probability of composite event

#### Probability Rules

1. The probability of any event must be between 0 and 1, inclusive.
2. The probability of the complement event is 1 minus the probability of an event. That is the probability of all other possible events is 1 minus the probability an event itself. Therefore, the sum of all possible events is equal to 1.
3. If our events are independent, then the probability of the string of possible events is the product of those events. That is the probability of one event AND the next AND the next event, is the product of those events.

#### Probability Terminologies

1. [Sensitivity vs Specificity](https://www.differencebetween.com/difference-between-sensitivity-and-vs-specificity/)

   - Sensitivity: It measures the probability of actual positives.  
  Sensitivity = Number of true positives /[ Number of true positives + Number of false negatives]
   - Specificity: It measures the probability of actual negatives.  
  Specificity = Number of true negatives / [Number of true negatives+ Number of false positives]  
  <img src="images/Difference-Between-Sensitivity-and-Specificity_Figure-1.png" alt="Sensitivity vs Specificity" width="300"/>

#### Probability Methods

##### 1. Binomial Distribution

The Binomial Distribution helps us determine the probability of a string of independent events with exactly two outcomes 'coin flip like events'.

###### 1.1 Unconditional Probability (Independent)

Formulas:

n is the number of "events", x is the number of "successes", and p is the probability of "successes".

- No. of successful occurrences:  
![successful occurrences](images/successful%20occurrences.png)
- No. of iterations or Truth table length:  
![iterations](images/iterations.png)
- [Probability mass function](https://en.wikipedia.org/wiki/Probability_mass_function):  
![iterations](images/Probability%20mass%20function.png)

This term is maximized when x is exactly the half of n.

Use Cases:

We can now use this distribution to determine the probability of things like:

- The probability of 3 heads occurring in 10 flips.
- The probability of observing 8 or more heads occurring in 10 flips.
- The probability of not observing any heads in 20 flips.

Some Facts:

The truth is that in practice, you will commonly be working with data, which might follow a binomial distribution. So it is less important to calculate these probabilities (though this can be useful in some cases), and it is more important that you understand what the Binomial Distribution is used for, as it shows up in a lot of modeling techniques in machine learning, and it can sneak up in our datasets with tracking any outcome with two possible events.

One of the most popular places you see the Binomial distribution is in logistic regression.

###### 1.2 Conditional Probability (Dependent)

Often events are not independent like with coin flips and dice rolling. Instead, the outcome of one event depends on an earlier event.

For example, the probability of obtaining a positive test result is dependent on whether or not you have a particular condition. If you have a condition, it is more likely that a test result is positive.

Formulas:

Conditional probabilities for any two events

P(A∣B) = P(B) / P(A ∩ B)​

In this case, we could have this as:  
P(positive∣disease) = P(disease) / P(positive ∩ disease)​.

where | represents "given" and ∩ represents "and".

##### 2. Bayes Rule

It describes the probability of an event, based on prior knowledge of conditions that might be related to the event.

[Bayes Rule Formula](https://en.wikipedia.org/wiki/Bayes'_theorem):

![Bayes Rule Formula](images/Bayes%20Rule.png)

where A and B are events and P(B) ≠ 0.

- P(A ∣ B) is a conditional probability: the likelihood of event A occurring given that B is true.
- P(B ∣ A) is also a conditional probability: the likelihood of event B occurring given that A is true.
- P ( A ) and P ( B ) are the probabilities of observing A and B respectively; they are known as the marginal probability.

Prior Probability . Test Evidence -> Posterior probability

Case Study:

1% of the population has cancer. Given that there is a 90% chance that you will test positive if you have cancer and that there is a 90% chance you will test negative if you don't have cancer, what is the probability that you have cancer if you test positive?

Prior:  
P(C) = 0.01 = 1%  
P(¬ C) = 0.99 = 99%

P(Pos | C) = 0.9  
P(Neg | C) = 0.1

P(Neg | ¬C) = 0.9  
P(Pos | ¬C) = 0.1

Joint:  
P(C,Pos) = P(C) . P(Pos | C) = 0.01 . 0.9 = 0.09  
P(¬C,Pos) = P(¬C) . P(Pos | ¬C) = 0.99 . 0.1 = 0.099

Normalizer:  
P(C,Pos) + P(¬C,Pos) = 0.09 + 0.099 = 0.108

Posterior:  
P(C,Pos) = 0.09 / 0.108 = 0.083
P(¬C,Pos) = 0.099 / 0.108 = 0.9166

##### 3. Normal Distribution

It is the basis of statistics in such that all of the testing and confidence intervals are defined through the normal distribution.

Formula:

Where N is the number of event, x  , μ mean, σ^2 variance,

![Normal Distribution Formula](images/Normal_Distribution_Formula.png)
![Normal Distribution Curve](images/Normal_Distribution_Curve.png)

- (x-μ)^2: makes the formula quadratic.
- σ^2: the division by variance flattens the curve in direct proprtion relationship.
- -1/2: the negative sign inverses the curve and multiplication by 1/2 increases the flatness.
- The maximum value for this term is when x equals μ which leads to e^0=1
- The minimum value will be when x equals to ±∞ which leads to (e^-∞).
- The area underneath the formula curve doesn't add to 1 it adds to √(2πσ^2 ) that is why it has to be normalized with this value.

##### 4. Sampling Distribution:

![Sampling Distribution](images/Sampling_Distribution.png)
![Sampling Distribution Example](images/Sampling_Distribution_Example.png)

A sampling distribution is the distribution of a statistic when we look at the distributions of the proportions of all samples of same size (ex: size 5).

- P: The mean of the sampling distribution.
- P(1-P): The variance of the original 1,0 values.
- P(1-P)/n: The variance of the proportions calculated from n randomly selected values iterated xxx times.

###### Proportions (or Means) Characteristic

1. The sampling distribution is centered on the original parameter value.
2. The sampling distribution decreases its variance depending on the sample size used. Specifically, the variance of the sampling distribution is equal to the variance of the original data divided by the sample size used. This is always true for the variance of a sample mean!

In notation, we say if we have a random variable, **X**, with variance of σ^2, then the distribution of X¯ (the sampling distribution of the sample mean) has a variance of σ^2/n.

###### Important mathematical theorems

Two important mathematical theorems for working with sampling distributions include:

1. Law of Large Numbers:
  
    The **Law of Large Numbers** says that as our **sample size increases**, the **sample mean gets closer to the population mean**, but how did we determine that the sample mean would estimate a population mean in the first place? How would we identify another relationship between parameter and statistic like this in the future?

    Three of the most common ways are with the following estimation techniques:

     - [Maximum Likelihood Estimation](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation)
     - [Method of Moments Estimation](https://en.wikipedia.org/wiki/Method_of_moments)
     - [Bayesian Estimation](https://en.wikipedia.org/wiki/Bayes_estimator)

    These are techniques that should be well understood for Data Scientist's that may need to understand how to estimate some value that isn't as common as a mean or variance. Using one of these methods to determine a "best estimate", would be a necessity.

2. Central Limit Theorem:

    The **Central Limit Theorem** states that with a **large enough sample size** the **sampling distribution of the mean will be normally distributed**.

    Facts:
    1. It applies for additional statistics, but it doesn't apply for all statistics!
    2. In case of a population size of 3000; the Central Limit Theorem applies to the sample mean of 100 draws from a right-skewed distribution. However, it did not apply to a sample size of 3 draws from this same distribution.
    3. With large sample sizes the sampling distribution of certain statistics will never become normally distributed. So how do we know which statistics will follow normal distributions, and which will not?
    4. The Central Limit Theorem applies for these statistics:
       1. Sample means (x¯)
       2. Sample proportions (p)
       3. Difference in sample means (x¯1−x¯2​)
       4. Difference in sample proportions (p1−p2)
    5. However it doesn't apply to:
       1. Sampling distribution for the variance (S^2)
       2. Correlation coefficient (r)
       3. Sampling distribution of sampling value in dataset (x(n))

###### Sampling Distributions Techniques

1. Bootstrapping

   - Bootstrapping is a technique where we sample from a group with replacement.
   - Bootstrapping is sampling with replacement. Using random.choice in python actually samples in this way. Where the probability of any number in our set stays the same regardless of how many times it has been chosen. Flipping a coin and rolling a die are kind of like bootstrap sampling as well, as rolling a 6 in one scenario doesn't mean that 6 is less likely later.
   - We can use bootstrapping to simulate the creation of sampling distribution.
   - By bootstrapping and then calculating repeated values of our statistics, we can gain an understanding of the sampling distribution of our statistics.
   - No more data needed to gain a better understanding of the parameter.
   - Bootstrapping has been using in leading machine learning algorithms. Additional notes on why bootstrapping works as a technique for inference can be found [here](https://stats.stackexchange.com/questions/26088/explaining-to-laypeople-why-bootstrapping-works)
   - new_page_converted = np.random.binomial(new_n, p_new, 10000)/new_n

2. Confidence Interval

   - We can use bootstrapping and sampling distributions to build confidence intervals for our parameters of interest.
   - By finding the statistic that best estimates our parameter(s) of interest (say the sample mean to estimate the population mean or the difference in sample means to estimate the difference in population means), we can easily build confidence intervals for the parameter of interest.

    It is important to understand the way that your sample size and confidence level relate to the confidence interval you achieve at the end of your analysis.

   - Assuming you control all other items of your analysis:
     1. Increasing your sample size will decrease the width of your confidence interval.
     2. Increasing your confidence level (say 95% to 99%) will increase the width of your confidence interval.
   - We can compute:
     1. The confidence interval width as the difference between your upper and lower bounds of your confidence interval.
     2. The margin of error is half the confidence interval width, and the value that you add and subtract from your sample estimate to achieve your confidence interval final results.

    Confidence Intervals (& Hypothesis Testing) vs. Machine Learning:

   - Confidence intervals take an aggregate approach towards the conclusions made based on data, as these tests are aimed at understanding population parameters (which are aggregate population values). It cannot talk about individual users with confidence intervals. Confidence intervals are for an aggregate about a population like a proportion or average.
   - Alternatively, machine learning techniques take an individual approach towards making conclusions, as they attempt to predict an outcome for each specific data point.

    Confidence Interval Applications:

   - The effectiveness of two groups of drugs.
   - Comparing to different ways of teaching the same topic and see which way improves retention.
   - A/B testing: where comparing two different webpages to one another and determine which web design drives the largest amount of traffic. A/B testing is one of the most important to businesses around the world. In this technique, you are changing something about your web layout to understand how it impacts users. You ideally want to provide a page that leads to more clicks, higher revenue, and/or higher customer satisfaction.

3. Hypothesis Testing

   - Hypothesis Testing and Confidence Intervals allow us to use only sample data to draw conclusions about an entire population.
   - You are always performing hypothesis tests on population parameters, never on statistics. Statistics are values that you already have from the data, so it does not make sense to perform hypothesis tests on these values.

   - Rules:
     - First thing, translate a question into two competing hypotheses, H0: Null Hypothesis, H1: Alternative Hypothesis.
     - The H0​ is true before you collect any data.
     - The H0​ usually states there is no effect or that two groups are equal.
     - The H0H​ and H1​ are competing, non-overlapping hypotheses.
     - H1​ is what we would like to prove to be true.
     - H0​ contains an equal sign of some kind - either =, ≤, or ≥.
     - H1​ contains the opposition of the null - either ≠, >, or <.

   - Case Study #1:
     - The statement, "Innocent until proven guilty" is one that suggests the following hypotheses are true:
       - H0​: Innocent
       - H1​: Guilty
     - We can relate this to the idea that "innocent" is true before we collect any data. Then the alternative must be a competing, non-overlapping hypothesis. Hence, the alternative hypothesis is that an individual is guilty.

   - Case Study #2:
     - We wanted to test if a new page was better than an existing page, we set that up in the alternative. Two indicators are that the null should hold the equality, and the statement we would like to be true should be in the alternative. Therefore, it would look like this:
     - H0​:μ1​≤μ2​
     - H1​:μ1​>μ2
     - Here μ1​ represents the population mean return from the new page. Similarly, μ2​ represents the population mean return from the old page.
     - Depending on your question of interest, you would change your null and alternative hypotheses to match.

   - Errors
     - **Type I** errors have the following features:
       1. You should set up your null and alternative hypotheses, so that the worse of your errors is the type I error.
       2. They are denoted by the symbol α.
       3. The definition of a type I error is: Deciding the alternative (H1​) is true, when actually (H0) is true.
       4. Type I errors are often called false positives.
     - **Type II**:
       1. They are denoted by the symbol β.
       2. The definition of a type II error is: Deciding the null (H0) is true, when actually (H1​) is true.
       3. Type II errors are often called false negatives.

     In the most extreme case, we can always choose one hypothesis (say always choosing the null) to ensure that a particular error never occurs (never a type I error assuming we always choose the null). However, more generally, there is a relationship where with a single set of data decreasing your chance of one type of error, increases the chance of the other error occurring.

   - Common hypothesis tests include:
     1. Testing a population mean [(One sample t-test)](http://sites.utexas.edu/sos/guided/inferential/numeric/claim/one-sample-t/).
     2. Testing the difference in means [(Two sample t-test)](https://www.isixsigma.com/tools-templates/hypothesis-testing/making-sense-two-sample-t-test/).
     3. Testing the difference before and after some treatment on the same individual [(Paired t-test)](http://www.statstutor.ac.uk/resources/uploaded/paired-t-test.pdf).
     4. Testing a population proportion [(One sample z-test)](http://stattrek.com/statistics/dictionary.aspx?definition=one-sample%20z-test).
     5. Testing the difference between population proportions [(Two sample z-test)](https://onlinecourses.science.psu.edu/stat414/node/268).
     - You can use one of these sites to provide a t-table or z-table to support one of the above approaches:
       - [t-table](https://s3.amazonaws.com/udacity-hosted-downloads/t-table.jpg)
       - [t-table or z-table](http://www.z-table.com/t-value-table.html)
     - There are literally hundreds of different hypothesis tests! However, instead of memorizing how to perform all of these tests, you can find the statistic(s) that best estimates the parameter(s) you want to estimate, you can bootstrap to simulate the sampling distribution. Then you can use your sampling distribution to assist in choosing the appropriate hypothesis.

   - How to calculate Hypothesis:
     1. Using Confidence Interval:
        1. First we need to bootstrap a sample set of data and compute the sample mean again and again.
        2. Build the sampling distribution
        3. Calculate the confidence Intervals to determine what are the reasonable values for the population mean with some level of confidence.
        4. Using your confidence interval, you can simply look at if the interval falls in the null hypothesis space or in the alternative hypothesis space to choose which hypothesis you believe to be true.
     2. Using Normal Distribution
        1. We assume the Null Hypothesis H0 is True and we can image how the sampling distribution would look like if we were to simulate from the closest value under the Null Hypothesis to the Alternative Hypothesis H1.
        2. Use the standard deviation of the sampling distribution to determine what the sampling distribution would look like, if it came from the Null Hypothesis.
        3. By applying Central Limit Theorem we know that the means would follow a normal distribution.
        4. Using NumPy.random.normal library in Python, we can simulate draws from the normal using hypothesized mean and standard deviation of our sampling distribution. By setting the center to be the closest value under the Null Hypothesis to the Alternative Hypothesis H1.
        5. Each of the simulated draws will represent a mean from the Null Hypothesis.
        6. Compare the actual sample  mean to this distribution, tells us the likelihood of our statistic coming from.

## Statistical Notations

It is commonly to use Greek symbols as parameters and lowercase letters as the corresponding statistics. Sometimes in the literature, you might also see the same Greek symbols with a "hat" to represent that this is an estimate of the corresponding parameter.

Below is a table that provides some of the most common parameters and corresponding statistics.

All **parameters** pertain to a population, while all **statistics** pertain to a sample.

![Notation Table](images/Notation_table.png)

## SQL

### Why SQL

- SQL: Structured Query Language (SQL)
- SQL is a language. Hence, the last word of SQL being language.
- There are some major **advantages** to using **traditional relational databases**, which we interact with using SQL.
  - SQL is easy to understand.
  - Traditional databases allow us to access data directly.
  - Traditional databases allow us to audit and replicate our data.
  - SQL is a great tool for analyzing multiple tables at once.
  - SQL allows you to analyze more complex questions than dashboard tools like Google Analytics.

### Why Businesses Like Databases

1. Data integrity is ensured - only the data you want entered is entered, and only certain users are able to enter data into the database.
2. Data can be accessed quickly - SQL allows you to obtain results very quickly from the data stored in a database. Code can be optimized to quickly pull results.
3. Data is easily shared - multiple individuals can access data stored in a database, and the data is the same for all users allowing for consistent results for anyone with access to your database.

### Types of Databases

There are many different types of SQL databases designed for different purposes.

Some of the most popular databases include:

1. MySQL
2. Access
3. Oracle
4. Microsoft SQL Server
5. Postgres

#### Small Differences

Each of these SQL databases may have subtle differences in syntax and available functions -- for example, MySQL doesn’t have some of the functions for modifying dates as Postgres. Most of what you see with Postgres will be directly applicable to using SQL in other frameworks and database environments. For the differences that do exist, you should check the documentation. Most SQL environments have great documentation online that you can easily access with a quick Google search.

The [article](https://www.digitalocean.com/community/tutorials/sqlite-vs-mysql-vs-postgresql-a-comparison-of-relational-database-management-systems) here compares three of the most common types of SQL: SQLite, PostgreSQL, and MySQL.

---

## Data Visualization

There are two main reasons for creating visuals using data:

   1. **Exploratory** analysis is done when you are searching for insights. These visualizations don't need to be perfect. You are using plots to find insights, but they don't need to be aesthetically appealing. You are the consumer of these plots, and you need to be able to find the answer to your questions from these plots.

   2. **Explanatory** analysis is done when you are providing your results for others. These visualizations need to provide you the emphasis necessary to convey your message. They should be accurate, insightful, and visually appealing.

The five steps of the data analysis process:

 1. **Extract** - Obtain the data from a spreadsheet, SQL, the web, etc.
 2. **Clean** - Here we could use expl**or**atory visuals.
 3. **Explore** - Here we use expl**or**atory visuals.
 4. **Analyze** - Here we might use either expl**or**atory or expl**an**atory visuals.
 5. **Share** - Here is where expl**an**atory visuals live.

What visualization to use, doesn't depend only on the data type but also on how many columns needed to be in a single plot. The key to building great data visualizations is in aiming them at answering the questions you want answered.

### Univariate analysis

When one column will be displayed in the plot.

1. Quantitative data:
   - Histogram:  
   ![Example](Images/Histogram.png)  
   It is the most popular and there are rare cases that might not be used.
   - Normal Quantile Plot  
   ![Example](Images/Normal%20Quantile%20Chart.png)  
   - Stem and Leaf Plot  
   ![Example](Images/Stem-And-Leaf%20Plot.png)  
   - Box and Whisker Plot  
   ![Example](Images/Box-And-Whisker%20Plot.png)  

2. Categorical data:
   - Bar Chart:
   ![Example](Images/Bar%20Chart.png)  
    It is like the histogram but the bins are determined based on a set category not on a range that the chart creator can change. Ordinal categorical are better to be used with Bar Chart.
   - Pie Chart
   ![Example](Images/Pie%20Chart.png)  
   - Pareto Chart: are essentially just bar charts where the bars are in the order from the most frequent to the least frequent.
   ![Example](Images/Pareto%20Chart.png)  

### Bivariate analysis

When comparing two variables to one another.

1. Quantitative data:
   - **Scatter Plot**:
   ![Example](Images/Scatter%20plot.png)  
      are a common visual for comparing two quantitative variables. A common summary statistic that relates to a scatter plot is the correlation coefficient commonly denoted by r and it ranges from -1 to 1.

      Though there are a [few different](http://www.statisticssolutions.com/correlation-pearson-kendall-spearman/) ways to measure correlation between two variables, the most common way is with [Pearson's correlation coefficient](https://en.wikipedia.org/wiki/Pearson_correlation_coefficient). Pearson's correlation coefficient provides the:

      1. **Strength**: It is the closeness of the points to each other. It considered to be **Strong** (0.7≤∣r∣≤1.0) if the points are close to each other, **Weak** if the points are far from each other (0.0≤∣r∣<0.3), or **Moderate** (0.3≤∣r∣<0.7)
      2. **Direction**: It considered to be Positive (positive values of r), if the both variables are increasing. And to be Negative (negative values of r), if one or both variables are decreasing.

      of a **linear relationship**. [Spearman's Correlation Coefficient](https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient) does not measure linear relationships specifically, and it might be more appropriate for certain cases of associating two variables.

      Calculation of the Correlation Coefficient

      ![equation](Images/Correlation%20Coefficient.png)

      It can also be calculated in Excel and other spreadsheet applications using `CORREL(col1, col2)`, where col1 and col2 are the two columns you are looking to compare to one another.

   - **Line plot**:  
     Line plots are a common plot for viewing data over time. These plots allow us to quickly identify overall trends, seasonal occurrences, peaks, and valleys in the data. You will commonly see these used in looking at stock prices over time, but really tracking anything over time can be easily viewed using these plots.
   ![Example](Images/Line%20Plot.png)  

2. Categorical Data:
   - Side by side bar chart
   ![example](/Images/Side%20by%20side%20Bar%20Chart.png)

### More than two variables

- Line Plot
![Example](Images/more%20than%202%20Line%20Plot.png)
- Stacked Line
![Example](Images/More%20than%202%20varriables%20Stacked%20Line.png)
- Bar Chart
![Example](Images/More%20than%202%20varriables%20Bar%20Chart.png)

### Helpful resources

1. Visualization Mind Map
![Visualization Mind Map](images/Visualization%20mind%20map.jpeg)

## Communicating with data

1. **Understand the context** - this means knowing your audience and conveying a clear message about what you want your audience to know or do with the information you are providing.

2. **Choose an appropriate visual display** - this was covered in the above section.

3. **Eliminate clutter** - you should only provide information to the user that helps convey your message.

4. **Focus attention where you want it** - build visualizations that pull attention to the message you want to highlight.

5. **Think like a designer** - you will learn a number of design principles in this lesson to assist as you start to put together your own data visualizations.

6. **Tell a story** - your visualizations should give the audience a story. The most powerful data visualizations move people to take action.

   1. Start with a Question
   1. Repetition is a Good Thing
   1. Highlight the Answer
   1. Call Your Audience To Action

### Visuals can be bad if

1. Don't convey the message.
2. Misleading.
3. **Chart Junk**: refers to all visual elements in charts and graphs that are not necessary to comprehend the information represented on the graph or that distract the viewer from this information.
   Examples:
   1. Heavy grid lines
   2. Unnecessary text
   3. Pictures surrounding the visual
   4. Shading or 3d components
   5. Ornamented chart axes
4. **Color hue changes** (as are unfortunately commonly used as an additional variable encoding in scatter plots)
5. **Area changes** (as we see in pie charts, which often makes them not the best plot choice).
6. **Lie Factor (Data integrity)**: It is key that when you build plots you maintain integrity for the underlying data. Lie factor depicts the degree to which a visualization distorts or misrepresents the data values being plotted. It is calculated in the following way:
![Equation](Images/Lie%20Factor.png)  
The delta symbol (Δ) stands for difference or change. In words, the lie factor is the relative change shown in the graphic divided by the actual relative change in the data. Ideally, the lie factor should be 1: any other value means that there is some mismatch in the ratio of depicted change to actual change.  
[How to spot visualization lies](https://flowingdata.com/2017/02/09/how-to-spot-visualization-lies/)

This seems straightforward, but often visuals are created that do one or both of these unintentionally. There is an entire book that was published aimed at misleading visuals: [How to Lie with Statistics](http://faculty.neu.edu.cn/cc/zhangyf/papers/How-to-Lie-with-Statistics.pdf).

### Visuals can be good if

1. **Positional changes** (differences in x- and y- position as we see with scatter plots).
2. **Length changes** (differences in box heights as we see with bar charts and histograms).
3. **Higher data-ink ratio**, credited to Edward Tufte, is directly related to the idea of chart junk. The more of the ink in your visual that is related to conveying the message in the data, the better.  
Limiting chart junk increases the data-ink ratio.

### Visuals Encoding

In general, color and shape are best for categorical variables, while the size of marker can assist in adding additional quantitative data.

1. Coloring

   Color can both help and hurt a data visualization. Tips for using color effectively.

   1. Before adding color to a visualization, start with black and white.

   2. When using color, use less intense colors - not all the colors of the rainbow, which is the default in many software applications.

   3. Color for communication. Use color to highlight your message and separate groups of interest. Don't add color just to have color in your visualization.

   4. To be sensitive to those with colorblindness, you should use color palettes that do not move from **red to green** without using another element to distinguish this change like shape, position, or lightness.. Instead, use colors on a **blue to orange** palette.

   Only use these additional encodings when absolutely necessary. Often these additional encodings suggest you are providing too much information in a single plot. **Instead, it might be better to break the information into multiple individual messages.**

2. Shapes

3. Size

## Tips

### Simpson's Paradox

- A Phenomenon that shows how powerful and dangerous statistics can be. Sometimes just grouping the data differently for analysis, can make conclusions disappear or even reversed.

### Statistical vs Practical Significance

- Using **confidence intervals** and **hypothesis testing**, you are able to provide **statistical significance** in making decisions.
- However, it is also important to take into consideration **practical significance** in making decisions. **Practical significance** takes into consideration other factors of your situation that might not be considered directly in the results of your hypothesis test or confidence interval. Constraints like **space**, **time**, or **money** are important in business decisions. However, they might not be accounted for directly in a statistical test.
