# Monitoring

Keeping a model healthy and operational requires monitoring

"ML Models do not get better with data"

- Training data represents a snapshot of the world at a point in time
- Many types of data change overtime (i.e. movie sales)
- Monitoring gives early warning

# Concept Drift
1. loss of prediction quality
2. akin to fashion change or emerging concept
3. emerging concept are new patterns in data
4. types of dataset shift:
   1. Covariate shift (input changes, labels are the same and output is the same)
      1. In covariate shift, the distribution of your input data changes, but the conditional probability of your output over the input remains the same. The distribution of your labels doesn't change. 
   2. prior probability shift (labels change, but input is the same)
      1. Prior probability shift is basically the opposite of covariate shift. The distribution of your labels changes, but your input data stays the same. Concept drift can be thought of as a type of prior probability shift. 

# How to monitor data?
[image](./cont-monitoring-model.png)
1. start with RAW data
   1. monitor incoming data against trained data
      1. this lets you look for changes in input over time or "covariate shift"
2. then, Processing
3. then, Model Performance
4. then, Predictions
   1. monitor predictions generated to detect "prior probability shift"
   2. add labeling process on new data that enables "concept drift"

## Looking for Drift and Shift
- supervised and unsupervised methods

### Supervised
1. Statistical Process Control
   1. "Essentially, this method triggers a drift alert if the parameters of the distribution go beyond a certain threshold rule. "
      1. primarily used in manufacturing for quality control since the 1920s.
      2. uses statistical methods to monitor and control process
      3. this is useful to detect drift
      4. the errors follow a binomial distribution
      5. analyzes the rate of errors and since it's a supervised method, it requires us to have labels for incoming stream of data.
2. Sequential Analysis
   1. "The basic idea is that if data is stationary, the contingency table should remain constant."
      1. use a method called linear four rates
      2. corresponds to the truth table for a classifier that you're probably familiar with: true positive, false positive, false negative, and true negative.
      3. four rates: net predictive value, precision, recall, and specificity.
      4. If the model is predicting correctly, these four value should continue to remain constant.
3. Air Distribution Monitoring
   1. known as adaptive windowing.
   2. In this method, you divide the incoming data into windows, the size of which adapts to the data. Then you calculate the mean error rate at every window of data. Finally, let's calculate the absolute difference of the mean error rate at every successive window and compare it with a threshold based on the Hoeffding bound. 
   3. The Hoeffding bound is used for testing the difference between the means of two populations. 

### Unsupervised techniques
1. clustering or novelty detection
   1. In this method, you cluster the incoming data into one of the known classes. If you see that the features of the new data are far away from the features of known classes, then you know that you're seeing an emerging concept.
   2. there are multiple algorithms available. We've listed a few, including OLINDDA, MINAS, ECSMiner, and GC3
   3. The downside of this method is that the text only cluster-based drift, not population-based changes.
2. feature distribution monitoring
   1. we monitor each feature of the dataset separately. You split the incoming dataset into uniformly size windows, and then compare the individual features against each window of data.
   2. algorithms
      1. The first is Pearson correlation, which is using the change of concept technique. 
      2. There's also the Hellinger distance, which is used in the Hellinger Distance Drift Detection Method or HDDDM.
         1. The Hellinger distance is used to quantify the similarity between two probability distributions. 
         2. The downside of this method is that it is not able to detect population drift since it only looks at individual features.
3. model-dependent monitoring
   1. This method monitors the space near the decision boundaries or margins in the latent feature space of your model.
      1. algorithms
         1. Margin Density Drift Detection or MD3.
         2. This method is very good at reducing the false alarm rate

# How often should you retrain your model? 
- There's no fixed answer to this question. It largely depends on the data and the world. The rate of change of the data and the rate of change of the world that you are modeling will determine how often you need to retrain your model to adapt to change.
- Retraining too often is okay, but it can result in higher costs for computer resources. 
- Not retraining often enough can lead to degraded model performance. 
- Ideally, you should monitor your data and model well enough to be able to use your evaluation results to trigger retraining automatically. 
- If you can't do that or haven't reached the level of maturity in your deployment, then you can also just retrain on a schedule.


Instrumentation, Observability & Monitoring of Machine Learning Models
- https://www.infoq.com/presentations/instrumentation-observability-monitoring-ml/
Monitoring Machine Learning Models in Production - A Comprehensive Guide
- https://christophergs.com/machine%20learning/2020/03/14/how-to-monitor-machine-learning-models/
Concept Drift detection for Unsupervised Learning
- https://arxiv.org/pdf/1704.00023.pdf
Google Cloud
- https://cloud.google.com/ai-platform/prediction/docs/continuous-evaluation
Amazon SageMaker
- https://aws.amazon.com/sagemaker/model-monitor/
Microsoft Azure
- https://docs.microsoft.com/en-us/azure/machine-learning/how-to-monitor-datasets?tabs=python