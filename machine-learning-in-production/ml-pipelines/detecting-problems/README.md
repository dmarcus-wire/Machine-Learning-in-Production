# Detecting problems with deployed models and data

1. Data change
1. Concept change
1. Changing Ground Truth (label new training data)

# Validating Data

## Drift
Changes in data over time (e.g. data collected once per day)

## Model Decay
Overtime, Data Drift will cause a model to perform worse. Changes in the statistics properties of the features.

## Performance Decay
Overtime, Concept drift the labels distribution and meaning will change

# Skew
Differences between two static versions of data (training vs. serving)

## Schema Skew
Training and serving do not conform to the same schema

## Distribution Skew

## Dataset shift 
occurs when the joint probability of x are features and y are labels is not the same during training and serving. 

Dataset shift Ptrain(y,x) != Pserve(y,x)

### Detection 
1. Capture baseline statistics
1. Generate data schema
1. Compare between training data and serving data
1. Validate difference
1. Detect anomalies
1. Alert and Analyze 

## Covariate shift 

refers to the change in distribution of the input variables present in training and serving data. In other words, it's where the marginal distribution of x are features is not the same during training and serving, but the conditional distribution remains unchanged.

Requires continuous evaluation Ptrain(y|x) = Pserve(y|x) Ptrain(x) != Pserve(x)

## Concept shift 
refers to a change in the relationship between the input and output variables as opposed to the differences in the Data Distribution or input itself. In other words, it's when the conditional distribution of y are labels given x are features is not the same during training and serving, but the marginal distribution of x are features remains unchanged.

Concept Shift Ptrain(y|x) != Pserve(y|x) Ptrain(x) = Pserve(x)

# TensorFlow Data Validation
TFDV provides you with descriptive statistics at scale.

TensorFlow Data Validation or TFDV, helps developers understand, validate, and monitor their ML data at scale. TFDV is used to analyze and validate petabytes of data at Google every day across hundreds or thousands of different applications that are currently in production.

1. Generate data statistics and schemas
1. Provides visualizations
1. Performs validation checks 
1. Detects training/serving skews
	- supports categorical features using "Chebyshev Distance" max distance in 1 dimensions of 2 end dimensional points
	- set threshold limits


Detects different types of skew:
1. Schema skew (change in type (int versus float))
1. Feature skew (changes in feature values (different sources, seasonality, etc.))
1. Distribution skew (changes of individual features between training and serving (like range of values min/max, mean, median, etc.))



