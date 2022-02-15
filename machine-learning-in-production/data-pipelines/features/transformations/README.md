# Feature Transformations as Scale

Using a unified framework where you can train and deploy consistently

## Inconsistencies in feature engineering
- training (e.g. python) and serving (e.g. java) code paths
- targets Mobile (TensorFlow Lite), Server (TensorFlow Serving), Web (TensorFlow JS)
- train/serve skews

## Preprocessing granualarity
- Transformation at the Instance Level and Full Pass over your data

|Instance Level|Full Pass|
|-|-|
|Clipping|Minmax|
|Multiplying|Standard Scaling|
|Expanding features|Bucketizing|

At training time you have the whole dataset so you can full pass. 
At serving time you only have the request, you can only instance-level.

### When do you transform?

#### Pre-processing training dataset
|Pros|Cons|
|-|-|
|Run-once|Transformations reproduced at serving|
|Compute on entire dataset|slower iterations| 

#### Within the model
embedded as part of the model.

|Pros|Cons|
|-|-|
|Easy Iterations|Expensive transforms|
|Transformation guarantees|Long model latency|
|-|Transformations per batch:skew|

#### Transform per batch

normalize features by their average per batch (think terabytes of data)
Access single batch, not full dataset
- Normalize by average within batch
- Precompute average and reuse per batch

## Optimizing instance-level transformations

Indirectly affecting training efficiency
Think of accelerators sitting idle while CPU performs transforms
Prefecthing with CPU, feed accelerator and parallelize processing

Ultimately, minimize time and processing cost.

Real world models use terabytes of data

Large Scale data processing frameworks

Consistent transformations between training and serving

# TensorFlow Transforms

Takes training data and processes it into serving system.
In the middle there is a pipeline produced as data is transformed.
Metadata plays a key role in organizing artficats that are produced.
Understand the lineage or provenance of those artifacts.

Traning Data | > Input data > Tranform > Transformed Data > Training > Trained Models | > Serving System

Training Data
Split with **ExampleGen**
Statistics calculated with **StatisticsGen**
Feeds stats to infer schema **SchemaGen**
Also checks for errors in data with **Example Validator**
Feeds to **Transform** where feature engineering happens
Fed to **training**
**Evaluator** that checks results
**Pusher** that sends the model to serving

## Benefits
1. Emitted tf.Graph holds all necessary constants and transformations
1. Focus on data pre-processing only at training time
1. Works in-line during training and serving
1. No need for pre-processing code at serving time
1. Consistently applied transformations irrespective of deplyoment platform

### tf.Tranfor Analyzers
1. Scaling (scale_to_z_score, scale_to_0_1)
1. Bucketizing (quantiles, apply_buckets, bucketize)
1. Vocabulary (bag_of_words, tfidf, ngrams)
1. Dimensionality Reduction (pca)

```
# basic imports for transform
import tensorflow as tf
# for deploy, transform uses beam to distrubte processing across a cluster
# for dev, beam also works as 'direct runner' without cluster
import apache_beam as beam
# helps with io in different formats
import apache_beam.io.iobase

import tensorflow_transform as tft
# transform has beam module to work with separately
import tensorflow_transform.beam as tft_beam
```

```
def preprocesssing_fn(inputs)

for key in DENSE_FLOAT_FEATURE_KEYS:
	outputs[key] = tft.scale_to_z_score(inputs[key])

for key in VOCAB_FEATURE_KEYS:
	output[key] = tft.vocabulary(input[key], vocab_filename=key)
for key in BUCKET_FEATURE_KEYS:
	output[key] = tft.bucketize(input[key], FEATURE_BUCKET_COUNT)

```
