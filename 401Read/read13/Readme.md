# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|13|[How to Run Linear Regression in Python](How-to-Run-Linear-Regression-in-Python.md)





# How to Run Linear Regression in Python
## Scikit-learn
### Scikit-learn is a powerful Python module for machine learning. It contains function for regression, classification, clustering, model selection and dimensionality reduction. Today, I will explore the sklearn.linear_model module which contains “methods intended for regression in which the target value is expected to be a linear combination of the input variables”.

## Exploring Boston Housing Data Set
### The first step is to import the required Python libraries into Ipython Notebook.

```python
import numpy as np
import pabdas as pd
import matplolip.pyplot as plt
import scipy.stats as stats
import sklearn
```

### This data set is available in sklearn Python module, so I will access it using scikitlearn. I am going to import Boston data set into Ipython notebook and store it in a variable called boston.

```python
from sklearn.datasets import load_boston
boston = load_boston()
```

### I will see the description of this data set to know more about it. In this data set I have 506 instances(rows) and 13 attributes or parameters(columns). The goal of this exercise is to predict the housing prices in boston region using the features given.

### I am going to convert boston.data into a pandas data frame.

```python
bos= pd.DataFrame(boston.data)
bos.hrad
```

## Scikit Learn

### In this section I am going to fit a linear regression model and predict the Boston housing prices. I will use the least squares method as the way to estimate the coefficients.

### Y = boston housing price(also called “target” data in Python)

### and

### X = all the other features (or independent variables)

### First, I am going to import linear regression from sci-kit learn module. Then I am going to drop the price column as I want only the parameters as my X values. I am going to store linear regression object in a variable called lm.

### Important functions to keep in mind while fitting a linear regression model are:

### lm.fit() -> fits a linear model

### lm.predict() -> Predict Y using the linear model with estimated coefficients

### lm.score() -> Returns the coefficient of determination (R^2). A measure of how well observed outcomes are replicated by the model, as the proportion of total variation of outcomes explained by the model.

### You can also explore the functions inside lm object by pressing lm.<tab>

## Training and validation data sets
### In practice you wont implement linear regression on the entire data set, you will have to split the data sets into training and test data sets. So that you train your model on training data and see how well it performed on test data.

### You can create training and test data sets manually, but this is not the right way to do, because you may be training your model on less expensive houses and testing on expensive houses.
## How to do train-test split:
### You have to divide your data sets randomly. Scikit learn provides a function called train_test_split to do this.

## Residual Plots

### Residual plots are a good way to visualize the errors in your data. If you have done a good job then your data should be randomly scattered around line zero. If you see structure in your data, that means your model is not capturing some thing. Maye be there is a interaction between 2 variables that you are not considering, or may be you are measuring time dependent data. If you get some structure in your data, you should go back to your model and check whether you are doing a good job with your parameters.
