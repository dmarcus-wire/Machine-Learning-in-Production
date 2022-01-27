# Feature Selection

Selecting some not all features. Identifies the relationship that best represents the relationship. Remove features that  don't influence the  outcome. Reduces resource requirements. Reduce  I/O. Minimize cost.


## Unsupervised
feature-target relationship not considered
removes redundant features

## Supervised
uses labels
uses feature-target relationship
selects features that contribute the most

## methods
1. filter
1. wrapper
1. embedded

NaN is often a clue it's an irrelevant feature.

## Filter methods
Correlation
- Pearson Correlation (features and label)
	- Pearsons correlation linear
- Kendall Tau  Rank Correlation Coefficient Monotonic relation and small sample size
- Spearmans Rank Correlation Coefficient Monotonic relationship 
- Mutual information
- F-Test
- Chi-Squared Test

### Process
- Set all features
- Select best subset
- Model
- Predict
- Correlation matrix shows feature relation
	- you want related to the target

### Univariate feature selection
- SelectKBest
- Select Percentile
- GenericUnivariateSelect
- Regression: f_regression, mutual_info_regression
- Classification: chi2, f_classif, mutual_info_classif

You should run metrics with all features and store results
Run correlation
Run Univariate
and compare metrics results to select best result

## Wrapper Methods
Use with a  model.
- Forward Selection
	- start with 1 feature, add 1 feature at a time, select best performer
- Backward elimination 
	- start with  all features, removes 1 feature at a time, select best performance
- Recursive feature elimination
	- Select the model to use, select the desired number of features, fit the model, rank features, discard least important features, repeat

### Process
- Set all features
- Generate subet
- Select best subset
- ML Model


## Embedded Methods
both highly related to model you're using
- L1 regularization
- Feature importance
	- built into RandomForestClassifier as property feature_importances_

