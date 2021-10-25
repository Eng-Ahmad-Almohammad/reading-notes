# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|14|[Data Science Primer](Data-Science-Primer.md)












# Data Science Primer
# Chapter 1: Bird's Eye View
## What makes machine learning so special?
### Machine learning is the practice of teaching computers how to learn patterns from data, often for making decisions or predictions.

## Key Terminology

- Model - a set of patterns learned from data.
- Algorithm - a specific ML process used to train a model.
- Training data - the dataset from which the algorithm learns the model.
- Test data - a new dataset for reliably evaluating model performance.
- Features - Variables (columns) in the dataset used to train the model.
- Target variable - A specific variable you're trying to predict.
- Observations - Data points (rows) in the dataset.


## Machine Learning Tasks
### Academic machine learning starts with and focuses on individual algorithms. However, in applied machine learning, you should first pick the right machine learning task for the job.

- A task is a specific objective for your algorithms.
- Algorithms can be swapped in and out, as long as you pick the right task.
### In fact, you should always try multiple algorithms because you most likely won't know which one will perform best for your dataset.
### The two most common categories of tasks are supervised learning and unsupervised learning.

## Supervised Learning
### Supervised learning includes tasks for "labeled" data (i.e. you have a target variable).

- In practice, it's often used as an advanced form of predictive modeling.
- Each observation must be labeled with a "correct answer."
- Only then can you build a predictive model because you must tell the algorithm what's "correct" while training it (hence, "supervising" it).
- Regression is the task for modeling continuous target variables.
- Classification is the task for modeling categorical (a.k.a. "class") target variables.

## Unsupervised Learning
### Unsupervised learning includes tasks for "unlabeled" data (i.e. you do not have a target variable).

- In practice, it's often used either as a form of automated data analysis or automated signal extraction.
- Unlabeled data has no predetermined "correct answer."
- You'll allow the algorithm to directly learn patterns from the data (without "supervision").
- Clustering is the most common unsupervised learning task, and it's for finding groups within your data.

# Chapter 2: Exploratory Analysis

## Why explore your dataset upfront?
### The purpose of exploratory analysis is to "get to know" the dataset. Doing so upfront will make the rest of the project much smoother, in 3 main ways:

- You’ll gain valuable hints for Data Cleaning (which can make or break your models).
- You’ll think of ideas for Feature Engineering (which can take your models from good to great).
- You’ll get a "feel" for the dataset, which will help you communicate results and deliver greater impact.
- However, exploratory analysis for machine learning should be quick, efficient, and decisive... not long and drawn out!

- Don’t skip this step, but don’t get stuck on it either.

- You see, there are infinite possible plots, charts, and tables, but you only need a handful to "get to know" the data well enough to work with it.

## Start with Basics
### First, you'll want to answer a set of basic questions about the dataset:

- How many observations do I have?
- How many features?
- What are the data types of my features? Are they numeric? Categorical?
- Do I have a target variable?

### Then, you'll want to display example observations from the dataset. This will give you a "feel" for the values of each feature, and it's a good way to check if everything makes sense.
### The purpose of displaying examples from the dataset is not to perform rigorous analysis. Instead, it's to get a qualitative "feel" for the dataset.

- Do the columns make sense?
- Do the values in those columns make sense?
- Are the values on the right scale?
- Is missing data going to be a big problem based on a quick eyeball test?

## Plot Numerical Distributions
### Next, it can be very enlightening to plot the distributions of your numeric features.

## Often, a quick and dirty grid of histograms is enough to understand the distributions.

### Here are a few things to look out for:

- Distributions that are unexpected
- Potential outliers that don't make sense
- Features that should be binary (i.e. "wannabe indicator variables")
- Boundaries that don't make sense
- Potential measurement errors
### At this point, you should start making notes about potential fixes you'd like to make. If something looks out of place, such as a potential outlier in one of your features, now's a good time to ask the client/key stakeholder, or to dig a bit deeper.

### However, we'll wait until Data Cleaning to make fixes so that we can keep our steps organized.


## Plot Categorical Distributions
### Categorical features cannot be visualized through histograms. Instead, you can use bar plots.

### In particular, you'll want to look out for sparse classes, which are classes that have a very small number of observations. By the way, a "class" is simply a unique value for a categorical feature.

## Study Correlations

### Finally, correlations allow you to look at the relationships between numeric features and other numeric features.

### Correlation is a value between -1 and 1 that represents how closely two features move in unison. You don't need to remember the math to calculate them. Just know the following intuition:

- Positive correlation means that as one feature increases, the other increases. E.g. a child’s age and her height.
- Negative correlation means that as one feature increases, the other decreases. E.g. hours spent studying and number of parties attended.
- Correlations near -1 or 1 indicate a strong relationship.
- Those closer to 0 indicate a weak relationship.
- 0 indicates no relationship.

### In general, you should look out for:

- Which features are strongly correlated with the target variable?
- Are there interesting or unexpected strong correlations between other features?
### Again, your aim is to gain intuition about the data, which will help you throughout the rest of the workflow.

### By the end of your Exploratory Analysis step, you'll have a pretty good understanding of the dataset, some notes for data cleaning, and possibly some ideas for feature engineering.


# Chapter 3: Data Cleaning
## Remove Unwanted observations
### The first step to data cleaning is removing unwanted observations from your dataset. This includes duplicate or irrelevant observations.
## Duplicate observations
### Duplicate observations most frequently arise during data collection, such as when you:

- Combine datasets from multiple places
- Scrape data
- Receive data from clients/other departments

## Irrelevant observations
### Irrelevant observations are those that don’t actually fit the specific problem that you’re trying to solve.

- For example, if you were building a model for Single-Family homes only, you wouldn't want observations for Apartments in there.
- This is also a great time to review your charts from Exploratory Analysis. You can look at the distribution charts for categorical features to see if there are any classes that shouldn’t be there.
### Checking for irrelevant observations before engineering features can save you many headaches down the road.

## Fix Structural Errors
### The next bucket under data cleaning involves fixing structural errors. Structural errors are those that arise during measurement, data transfer, or other types of "poor housekeeping." For instance, you can check for typos or inconsistent capitalization. This is mostly a concern for categorical features.
### Finally, check for mislabeled classes, i.e. separate classes that should really be the same.

- e.g. If ’N/A’ and ’Not Applicable’ appear as two separate classes, you should combine them.
- e.g. ’IT’ and ’information_technology’ should be a single class.

## Filter Unwanted Outliers
### Outliers can cause problems with certain types of models. For example, linear regression models are less robust to outliers than decision tree models. In general, if you have a legitimate reason to remove an outlier, it will help your model’s performance.

### However, outliers are innocent until proven guilty. You should never remove an outlier just because it’s a "big number." That big number could be very informative for your model. We can’t stress this enough: you must have a good reason for removing an outlier, such as suspicious measurements that are unlikely to be real data.

## Handle Missing Data
### Missing data is a deceptively tricky issue in applied machine learning.

### First, just to be clear, you cannot simply ignore missing values in your dataset. You must handle them in some way for the very practical reason that most algorithms do not accept missing values.


### Unfortunately, the 2 most commonly recommended ways of dealing with missing data actually suck.

### They are:

- Dropping observations that have missing values
- Imputing the missing values based on other observations
### Dropping missing values is sub-optimal because when you drop observations, you drop information.

### The fact that the value was missing may be informative in itself.
### Plus, in the real world, you often need to make predictions on new data even if some of the features are missing!
### Imputing missing values is sub-optimal because the value was originally missing but you filled it in, which always leads to a loss in information, no matter how sophisticated your imputation method is.

### Again, "missingness" is almost always informative in itself, and you should tell your algorithm if a value was missing.
### Even if you build a model to impute your values, you’re not adding any real information. You’re just reinforcing the patterns already provided by other features.

### In short, you should always tell your algorithm that a value was missing because missingness is informative.

### So how can you do so?

## Missing categorical data
### The best way to handle missing data for categorical features is to simply label them as ’Missing’!

- You’re essentially adding a new class for the feature.
- This tells the algorithm that the value was missing.
- This also gets around the technical requirement for no missing values.
## Missing numeric data
### For missing numeric data, you should flag and fill the values.

1- Flag the observation with an indicator variable of missingness.
2- Then, fill the original missing value with 0 just to meet the technical requirement of no missing values.
### By using this technique of flagging and filling, you are essentially allowing the algorithm to estimate the optimal constant for missingness, instead of just filling it in with the mean.


# Chapter 4: Feature Engineering
## What is Feature Engineering?
### Feature engineering is about creating new input features from your existing ones.

### In general, you can think of data cleaning as a process of subtraction and feature engineering as a process of addition.

### This is often one of the most valuable tasks a data scientist can do to improve model performance, for 3 big reasons:

1- You can isolate and highlight key information, which helps your algorithms "focus" on what’s important.
2- You can bring in your own domain expertise.
3- Most importantly, once you understand the "vocabulary" of feature engineering, you can bring in other people’s domain expertise!
## Infuse Domain Knowledge
### You can often engineer informative features by tapping into your (or others’) expertise about the domain. Try to think of specific information you might want to isolate. Here, you have a lot of "creative freedom."

## Create Interaction Features

### The first of these heuristics is checking to see if you can create any interaction features that make sense. These are combinations of two or more features.

### By the way, in some contexts, "interaction terms" must be products between two variables. In our context, interaction features can be products, sums, or differences between two features.

### A general tip is to look at each pair of features and ask yourself, "could I combine this information in any way that might be even more useful?"

## Combine Sparse Classes
### Sparse classes (in categorical features) are those that have very few total observations. They can be problematic for certain machine learning algorithms, causing models to be overfit.

- There's no formal rule of how many each class needs.
- It also depends on the size of your dataset and the number of other features you have.
- As a rule of thumb, we recommend combining classes until each one has at least ~50 observations. As with any "rule" of thumb, use this as a guideline (not actually as a rule).

## Add Dummy Variables
### Most machine learning algorithms cannot directly handle categorical features. Specifically, they cannot handle text values. Therefore, we need to create dummy variables for our categorical features.

### Dummy variables are a set of binary (0 or 1) variables that each represent a single class from a categorical feature.

### The information you represent is exactly the same, but this numeric representation allows you to pass the technical requirements for algorithms.

## Remove Unused Features
### Unused features are those that don’t make sense to pass into our machine learning algorithms. Examples include:

- ID columns
- Features that wouldn't be available at the time of prediction
- Other text descriptions
### Redundant features would typically be those that have been replaced by other features that you’ve added during feature engineering.

# Chapter 5: Algorithm Selection
## Why Linear Regression is Flawed
### To introduce the reasoning for some of the advanced algorithms, let's start by discussing basic linear regression. Linear regression models are very common, yet deeply flawed.
### Simple linear regression models fit a "straight line" (technically a hyperplane depending on the number of features, but it's the same idea). In practice, they rarely perform well. We actually recommend skipping them for most machine learning problems.
### n this regard, simple linear regression suffers from two major flaws:

1- It's prone to overfit with many input features.
2- It cannot easily express non-linear relationships.

## Regularization in Machine Learning
### This is the first "advanced" tactic for improving model performance. It’s considered pretty "advanced" in many ML courses, but it’s really pretty easy to understand and implement.

### The first flaw of linear models is that they are prone to be overfit with many input features

### Regularization is a technique used to prevent overfitting by artificially penalizing model coefficients.

- It can discourage large coefficients (by dampening them).
- It can also remove features entirely (by setting their coefficients to 0).
- The "strength" of the penalty is tunable. (More on this tomorrow...)

## Regularized Regression Algos
1- Lasso Regression
### Lasso, or LASSO, stands for Least Absolute Shrinkage and Selection Operator.

2- Ridge Regression
### Ridge stands Really Intense Dangerous Grapefruit Eating (just kidding... it's just ridge).

3- Elastic-Net
### Elastic-Net is a compromise between Lasso and Ridge.

## Decision Tree Algos
###  linear regression suffers from two main flaws:

1- It's prone to overfit with many input features.
2- It cannot easily express non-linear relationships.
### How can we address the second flaw?

### Well, we need to move away from linear models to do so.... we need to bring in a new category of algorithms.

### Decision trees model data as a "tree" of hierarchical branches. They make branches until they reach "leaves" that represent predictions.

### Due to their branching structure, decision trees can easily model nonlinear relationships.

### For example, let's say for Single Family homes, larger lots command higher prices.
### However, let's say for Apartments, smaller lots command higher prices (i.e. it's a proxy for urban / rural).
### This reversal of correlation is difficult for linear models to capture unless you explicitly add an interaction term (i.e. you can anticipate it ahead of time).
### On the other hand, decision trees can capture this relationship naturally.
### Unfortunately, decision trees suffer from a major flaw as well. If you allow them to grow limitlessly, they can completely "memorize" the training data, just from creating more and more and more branches.

### As a result, individual unconstrained decision trees are very prone to being overfit.​

## Tree Ensembles
### Ensembles are machine learning methods for combining predictions from multiple separate models. There are a few different methods for ensembling, but the two most common are:
### Bagging attempts to reduce the chance overfitting complex models.

- It trains a large number of "strong" learners in parallel.
- A strong learner is a model that's relatively unconstrained.
- Bagging then combines all the strong learners together in order to "smooth out" their predictions.

### Boosting attempts to improve the predictive flexibility of simple models.

- It trains a large number of "weak" learners in sequence.
- A weak learner is a constrained model (i.e. you could limit the max depth of each decision tree).
- Each one in the sequence focuses on learning from the mistakes of the one before it.
- Boosting then combines all the weak learners into a single strong learner.

# Chapter 6: Model Training
## Split Dataset
### et’s start with a crucial but sometimes overlooked step: Spending your data.

### Think of your data as a limited resource.

- You can spend some of it to train your model (i.e. feed it to the algorithm).
- You can spend some of it to evaluate (test) your model.
- But you can’t reuse the same data for both!
### If you evaluate your model on the same data you used to train it, your model could be very overfit and you wouldn’t even know! A model should be judged on its ability to predict new, unseen data.

### Therefore, you should have separate training and test subsets of your dataset.

### Training sets are used to fit and tune your models. Test sets are put aside as "unseen" data to evaluate your models.
- You should always split your data before doing anything else.
-This is the best way to get reliable estimates of your models’ performance.
-After splitting your data, don’t touch your test set until you’re ready to choose your final model!
### Comparing test vs. training performance allows us to avoid overfitting... If the model performs very well on the training data but poorly on the test data, then it’s overfit.
## What are Hyperparameters?
### When we talk of tuning models, we specifically mean tuning hyperparameters.

### There are two types of parameters in machine learning algorithms.

### The key distinction is that model parameters can be learned directly from the training data while hyperparameters cannot.

### Model parameters
### Model parameters are learned attributes that define individual models.

- e.g. regression coefficients
- e.g. decision tree split locations
- They can be learned directly from the training data
### Hyperparameters
### Hyperparameters express "higher-level" structural settings for algorithms.

- e.g. strength of the penalty used in regularized regression
- e.g. the number of trees to include in a random forest
- They are decided before fitting the model because they can't be learned from the data

## What is Cross-Validation?
### Cross-validation is a method for getting a reliable estimate of model performance using only your training data.

### There are several ways to cross-validate. The most common one, 10-fold cross-validation, breaks your training data into 10 equal parts (a.k.a. folds), essentially creating 10 miniature train/test splits.

### These are the steps for 10-fold cross-validation:

1- Split your data into 10 equal parts, or "folds".
2- Train your model on 9 folds (e.g. the first 9 folds).
3- Evaluate it on the 1 remaining "hold-out" fold.
4- Perform steps (2) and (3) 10 times, each time holding out a different fold.
5- Average the performance across all 10 hold-out folds.
### The average performance across the 10 hold-out folds is your final performance estimate, also called your cross-validated score. Because you created 10 mini train/test splits, this score is usually pretty reliable.

## Fit and Tune Models
### Now that we've split our dataset into training and test sets, and we've learned about hyperparameters and cross-validation, we're ready fit and tune our models.

### Basically, all we need to do is perform the entire cross-validation loop detailed above on each set of hyperparameter values we'd like to try.

## Select Winning Model

### Because you've saved your test set as a truly unseen dataset, you can now use it get a reliable estimate of each models' performance.

### There are a variety of performance metrics you could choose from. We won't spend too much time on them here, but in general:

- For regression tasks, we recommend Mean Squared Error (MSE) or Mean Absolute Error (MAE). (Lower values are better)
- For classification tasks, we recommend Area Under ROC Curve (AUROC). (Higher values are better)
### The process is very straightforward:

1- For each of your models, make predictions on your test set.
2- Calculate performance metrics using those predictions and the "ground truth" target variable from the test set.

### Finally, use these questions to help you pick the winning model:

- Which model had the best performance on the test set? (performance)
- Does it perform well across various performance metrics? (robustness)
- Did it also have (one of) the best cross-validated scores from the training set? (consistency)
- Does it solve the original business problem? (win condition)