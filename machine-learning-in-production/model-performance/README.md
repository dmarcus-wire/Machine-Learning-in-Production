# Model Performance Analysis

TFMA - Tensorflow Model Analysis Tool - Deep Analysis of model performance

Successfully training a model and getting it to converge feels good. It often feels like you're done. If you're training a model for a class project or a paper that you're writing, then you are done. But for production ML, you now need to enter into a new phase of your development which involves a much deeper level of analysis of your model's performance. From a few different directions

## What next after training?

You want to look at model performance on both:
1. entire data  set
2. slices of data set (think different customers of different stores)

Ask questions:
1. Is the model performing well?
2. Is there scope for improvement?
3. Can data change in the future?
4. Has the data changes since you created your training dataset?

## Analysis performance
- Black box (e.g. Tensorboard) - models tested for metrics like accuracy and losses without knowing details
- Model Introspection (e.g. ), models can be inspectedd part by part

## Performance Metrics
- vary based on task (regression, classification, etc)
- performance is re-measured after each round of optimization
## Optimization
- learning algorithms find optimum values for each variable to converge to a local/global minima

# Tensorboard

https://blog.tensorflow.org/2019/12/introducing-tensorboarddev-new-way-to.html

A managed TensorBoard experience that lets you upload and share your ML experiment results with anyone.
https://tensorboard.dev/
If a picture is worth a thousand words, we believe an interactive TensorBoard can be even more valuable.If a picture is worth a thousand words, we believe an interactive TensorBoard can be even more valuable.

- visualize and understand their ML experiments

# Slicing Data
- Top level metrics may hide problems
  - Most model evaluation results look at aggregate or a top-level metrics on the entire training dataset. This aggregation often hides problems with model performance.
- TFMA
  - scalable framework
  - open source library
  - imprtant to a pipeline, runs checks before deploying model
  - ensures models meed required quality thresholsd
  - compute and visualize metrics
  - inspects models performance against different data slices
  - works standalone or in framework, like TFX
- Slicing metrics allow you to analyze the performance of a model on a more granular level.Slicing metrics allow you to analyze the performance of a model on a more granular level.

## Which slices are important?
- requires domain knowledge

## TFMA Architecture
1. Tf.Example reads inputs
2. ExtractAndEvaluate uses ApacheBeam
   1. Predict
   2. Slice Keys
      1. Evaluators

# Tensorboard vs TFMA
Tensorboard is used the analyze the training process 
TensorBoard visualizes streaming metrics of multiple models over global training sets TensorBoard visualizes streaming metrics of multiple models over global training sets 
TensorBoard confuse metrics on a mini-batch basis during training. They're called Streaming metrics and are our approximations based on those observed mini-batches.

TFMA is used to do deep analysis of the finished trained model
TFMA visualizes the metrics computed for a single model over multiple versions of the exported saved model
TFMA uses Apache Beam to do a full pass over the evil dataset
Allows for accurate calculation of metrics
Scales up to massive evaluation dataset since Beam pipelines can be run using distributed processing back ends. 

## TFMA can render in notebooks

# Resources
1. https://blog.tensorflow.org/2018/03/introducing-tensorflow-model-analysis.html
2. https://www.tensorflow.org/tfx/model_analysis/architecture