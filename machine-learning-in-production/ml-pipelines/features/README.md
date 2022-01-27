# Feature engineering

Tries to improve the models ability to learn while reducing the compute resources required. It is an art.
1. Combine Features you incorporate the original features often transformed or projected to a new space and or combinations of your features.
1. Tune objective functinos to ensure the model is moving the right direction
1. Create new features from existing data

During training > Entire Dataset > Batch Processing

During serving > Each Request > Real-time Processing

## Pre-processing operations

Transform Raw Data mapping it into clean data for a training ready dataset 

### Data Cleansing
Elimating or correcting erroneous data


## Feature engineer
- Maps Raw data into Feature vectors
- Integer values to floating point values
- Normalizes numerical values
- Strings and categorical values to vectors of numeric values
- Data from one space to a different space
- Within the model: increases inference time, speeds up iterations, limited to batch computations

### Feature Tuning
Scaling or normalizing, since NN are sensative to ranges of numerical features

### Representation Transformation

### Feature Extraction

### Feature Construction
Feature construction can be used to create new features

### Techniques

#### Feature Scaling
Numeric. Converts values from natural range to prescribed range. Speeds up convergence, Reduces NaN.

#### Normalization
Numeric. Gives a number between 0 and 1 bounded range. Good for not Gaussian distribution.

Xnorm = ((X - Xmin)/(Xmax - Xmin))

#### Standardization 
Numeric. z-score. Centered around the mean of the data. Allows for negative and positive values. Unbounded transformation. Good for Normal distribution. Good place to start for numerical features.

#### Bucketing
Grouping. 

#### Binning
Grouping. With Facets allows you to visualize data grouping to understand it.

#### Dimensionality Reduction
Grouping. 

##### Principal Component Analysis (PCA)

##### t-Distrubtion Stochastic Neighboard Embedding (t-SNE)

##### Unform Manifold Approximation and Projection (UMAP)

#### Feature Crossing
Synthetic feature encoding often encoding non-linearity in feature spaces. Both for categorical and numerical features.
Combine multiple features together into a new feature.
- A x B = product
- A x B x C x D = product
- Day of week, Hour => Hour of week
Encodes non-linearity.
Encodes same info in fewer features. 



#### Feature Embedding Projector 
Visualize data in a 3D space. Where is the data clustered? This is the art of feature engineering.
Good for High Dimensional Data.
Intuitive Exploration of highly dimensional data.


## Text
- stemming
- lemmatization
- TF-IDF
- n-grams
- embedding lookup

## Numeric

## Categorical
- vocabulary

## Images 
- clipping
- resizing
- cropping
- blurring
- canny filters
- sobel filters
- photometric distortions

# References
1. Feature engineering https://developers.google.com/machine-learning/crash-course/representation/feature-engineering
1. Feature engineering techniques: https://www.commonlounge.com/discussion/3ce75d036e924c70ab7e47f534ec40fc/history
1. Facets visualizations https://pair-code.github.io/facets/
1. Embedding Projector http://projector.tensorflow.org/
1. Feature crosses https://developers.google.com/machine-learning/crash-course/feature-crosses/encoding-nonlinearity
1. TFX https://www.tensorflow.org/tfx/guide#tfx_pipelines
1. tf.Transform https://ai.googleblog.com/2017/02/preprocessing-for-machine-learning-with.html
