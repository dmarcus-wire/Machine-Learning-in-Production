# Hello World for Transform

1. Data (collect the raw data )
1. Define metadata (prepare metadata for the dataset using DatasetMetadata)
1. Transform (Define the preprocessing function with tf.Transform analyzers)
1. In the background, use Analyzers and tf.Transform
1. Constant graph, Generate a constant graph with the required transformations

- tf.Transform allows pre-processing of input data and creating features
- tf.Transform allows defining pre-processing pipelines and their execution using large scale data processing frameworks, beam runs on spark, flink, apache dataflow, or on laptop
- In a TFX pipeline, the Transform component implements feature engineering using TensorFlow Transform
