## The curse of dimensionality

Segmentation and clustering rely on calcuating distances

## ML methods
1. kNN - distance between observations 
1. SVM - deal with projecting observations using kernels based on the distance between the observations after projection
1. Recommendation systems - measure between the user and the item attribute vectors

## Distance measure
1. Euclidean distance - a linear distance between two points in a multi-dimensional space

## High Dim data problems
- more dimensions = more features
- risk overfitting
- distances grow more and more alike
- no clear distinction between clustered objects
- concetration phenomenon for Euclidean distance

## the curse of dimensionality
- Richard Bellman "Adaptive Control Processes"

This phenomenon is called the curse of dimensionality. It includes situations where non-intuitive properties of data are observed in these high dimensional spaces. 

- machine learning is good at analyzing data when dealing with many dimensions
- we humans aren't adept at finding patterns and data that may be spread out across several dimensions
- especially if those dimensions are interrelated in counterintuitive ways
- as we add more dimensions, we also increase the processing power we need to analyze the data and at the same time we also increase the amount of training data required to make meaningful models


### more features bad?
- Redundant / irrelevant features
- More noise added than signal
- Hard to interpret and visualize
- Hard to store and process 
- More features added == model performance degrades
- More features require more examples with attributes that are predictive

## how to reduce dimensions, while maintaining predictive features?
- the Hughest effect
  - finding a hyperplane == hypethsis space
- more features == larger hyptohesis space
- lower the hypothesis space, easier to find hypothesis, less examples you needd, harder to generalize on unseen data

## What do models need?
- depends on the amount of training data available 
- the variance in that data
- the complexity of the decision surface and the type of classify are used
- It also depends on which features actually contain predictive information that will help your model train. 
- You want enough data with the best features and enough variety in the values of those features and enough predictive information in those features to maximize the performance of your model while simplifying it as much as possible.

## Increasing predictive performance
- derive features from attributes
- extract andd recombine to create new features

## Feature explosion
- domain knowledge can result in more dimensions that we need or want

# Best k-dimensional subspace for projection
1. Classification - maximize separation among classes using Linear Discriminant Analysis (LDA)
1. Regression - maximize correlation between project data and response variable using Partial Least Square (PLS)
1. Unsupervised - retain as much data variance as possible using Principal component Analysis (PCA)

## Principal Component Analysis (PCA)
- PCA is a minimization of the orthogonal distance
- Widely used for unsupervised and linear dimensionality reduction
- Accounts for variance of data as few dimensions as possible 
- Principal Components (PCs) maximize the variance
- PC gives the best axis to project data
- PC think of a line that separates the data linearly  
- Minimize total squared reconstruction error
- can be imported from `sklearn.decomposition import PCA`

### When to use?
- A versatile technique
- Fast and simple
- Offers several variation and extensions
- Visually studying clusters of data in high dimensions

### Weaknesses
- Result is no interpretable (lacking explainaibility)
- Requires setting thresholdd for cumulative explained variance

## Other Techniques 
1. Unsupervised 
   - Latent Semantic Indexing/Analysis (LSI and LSA) (SVD)
      - SVD decomposes non-square matrices
      - Removes redundant features from dataset
      - Seeks directions in feature space that minimize rescontruction error
      - orthogonality in raw space
      - used in neuroscience
   - Independent Components Analysis (ICA)
      - Seeks direction that are most statistically independent
      - addresses higher order dependence
      - treats components fairly and equally important
1. Matrix Factorization
   - Non-negative Matrix Factorization (NMF)
      - models are explainable
      - requires sample features to be non-negative (>=0)
  
1. Latent Methods
   - Latent Dirichlet Allocation (LDA)
