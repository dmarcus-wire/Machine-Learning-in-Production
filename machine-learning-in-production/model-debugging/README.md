# Model Debugging

## Model Robustness

- Robustness is more than generalization
- A model == Robust if results are consistently accurate
- even if one or more of the features change fairly drastically
- all models are sensative to changes in data
- there is a clear difference between a model that changes in gradual, predictable ways as the data changes and a model that suddenly produces wildly different results.

## How to measure robustness
- you shouldn't be measuring the robustness of a model during its training
- you shouldn't be using the same data set that you used during training
- you should split the data set into train, validation, and test splits
- You may use the test split which is totally unseen by the model even during the validation stage for testing the model robustness
- Or, generate a variety of new types of data
- Metrics == same as post training RMSC for regression models and AUC for classification

## Increase model robustness
- Model debugging is an emerging discipline focusing on finding and fixing problems in models and improving model robustness.
- Model debugging borrows various practices from model risk management, traditional model diagnostics, and software testing.
- Model debugging attempts to test ML models just like code, very similar to how you attest in software development.
- It probes sophisticated ML response functions and decision boundaries to detect and correct accuracy, fairness, security, and other problems in ML systems

## Model Debugging Objectives
- One of the big problems with ML models is that they can be quite opaque and become black boxes.
- Model debugging tries to improve the transparency of models by highlighting how data is flowing inside. Another problem is social discrimination. 
- Model debugging also aims to reduce the vulnerability of your model to attacks. For example, certain requests can be made once the model is in production that may be aimed at extracting data out of your model in order to understand how your model has been built.
- Three of the most widely used debugging techniques are:
- benchmarking models
- sensitivity analysis
- and residual analysis

## Benchmark Models
Sanity Test
- Compare your model to benchmark models
- Benchmarking models are small, simple models that are used before you start development for baselining your problem. 
- They're generally not state-of-the-art, but instead are linear or other simple models with very consistent performance.
- Once a model passes the benchmark test, the benchmark model can serve as a solid debugging tool.

## Sensitivity Analysis
Security / MLOps
- Sensitivity analysis helps with understanding a model by examining the impact that each feature has on the model’s prediction. In sensitivity analysis we experiment by changing a feature value while holding the other features constant, and observe the model results. 
- Sensitivity analysis is an important way to evaluate your model's performance, including its vulnerability to adversarial attacks.Sensitivity analysis is an important way to evaluate your model's performance, including its vulnerability to adversarial attacks.
- Sensitivity analysis helps you understand your model by examining the impact that each feature has on your model's prediction.
- In sensitivity analysis you experiment by changing a single features value while holding the other features constant and observe the model results.
  - If changing the features value causes the models result to be drastically different. It means that this feature has a big impact on the prediction. 
  - You're really not looking to see if the prediction is correct or not, but instead how much it changes different ways of doing sensitivity analysis. You're really not looking to see if the prediction is correct or not, but instead how much it changes different ways of doing sensitivity analysis.

### Approaches
1. One of the more powerful ways of conducting sensitivity analysis is by using the What-if tool which was created by the tensor flow team. 
2. First, In random attacks you generate lots of random input data and test the models outputs. Random attacks can reveal all kinds of unexpected software and math bugs.
   1. If you don't know where to begin debugging an Ml system, a random attack is a great place to get started
3. Second, Partial dependence plots show the marginal effect of one or two features and the effect they have on the model results.
   1. For example, when applied to a linear regression model, partial dependence plots always show a linear relationship. PDPbox and PyCEbox are open source packages which are available for creating partial dependence plots.

## Where things go wrong?
- Several machine learning problems, including neural networks can be fooled into misclassifying adversarial examples which are formed by making small but carefully designed changes to the data so that the model returns an incorrect answer with high confidence.
- This could have daunting implications. Imagine making a wrong decision on an important question based on only slightly corrupted data.
- a few examples:
  - first with an autonomous vehicle. It's important recognize traffic signs, other vehicles, people, etc. Unfortunately, we've seen examples of this in real life, but as in this example, if a sign is altered in just the right way, it can fool the model and the results can be catastrophic. 
  - If your business sells software to detect spam and phishing emails can get through, it reflects badly on your product.
  - A suitcase scanner is basically just an object classifier, but if it's vulnerable to attack, the results can be dangerous.

# The future of privacy forum
An industry group that studies privacy and security, suggest that security and privacy harms enabled by machine learning fall into roughly two categories. 
1. Informational. Informational harms relate to the unintended or unanticipated leakage of information, behavioral harms.
   1. membership inference attacks are aimed at inferring whether or not an individual's data was used to train the model based on a sample of the model's output.
   2. Model inversion attacks use model outputs to recreate the training data. 
      1. study focused on ML systems that use genetic information to recommend dozing of specific medications and it was able to directly predict individual patient's genetic markers.
   3. Model extraction attacks, use model outputs to recreate the model itself. 
      1. This has been demonstrated against model as a service providers like big Ml and Amazon machine learning and can compromise privacy and security, as well as the intellectual property of the underlying model itself.
2. behavioral. Relate to manipulating the behavior of the model itself, impacting the predictions or outcomes of the model.
   1. Model Poisoning attacks occur when an adversary inserts malicious data into training data in order to alter the behavior of the model, for example, creating an artificially low insurance premium for particular individuals.
   2. Evasion attacks occur when data in an inference request intentionally causes the model to miss classify that data.
      1. altering a stop sign example

## Adversarial Training
1. Clever Hands is an open source python library that you can use to benchmark your models to measure their vulnerability to adversarial examples. 
2. Include sets of adversarial images in your training data so that the classifier is able to understand the various distributions of noise and your model learns to recognize the correct class. 
3. Foolbox is another open source python library that lets you easily run adversarial attacks against machine learning models like deep neural networks.Foolbox is another open source python library that lets you easily run adversarial attacks against machine learning models like deep neural networks. It's built on top of eager pie and works natively with models in pytorch tensorflow and jacks.
4. One fairly advanced approach is defensive distillation. Since it does not use specific adversarial examples, it may provide more general hardening to new attacks
   1. this is very similar to knowledge distillation training. The goal is to increase model robustness and decrease sensitivity in order to decrease vulnerability to attacks. Defensive distillation reduced the effectiveness of a sample creation from 95% to less than 0.5% in one study.
   2. The main difference between defensive distillation and the original distillation proposed by Hinton and others that we discussed earlier in our model optimization section, is that we keep the same network architecture to train both the original network as well as the distilled network.

"detecting vulnerability is easier than fixing it. This is an emerging field and like many things in security, there is an arms race between attackers and defenders."

# Adversarial Attacks
Adversarial examples are specialized inputs created with the purpose of confusing and neural network, resulting in the misclassification of a given input. These notorious inputs are indistinguishable to the human eye, but cause the model to fail to identify the contents of the image. 

- white box attack is where the attacker has complete access to the bottle being attacked.
- One of the most famous examples of an adversarial image is shown here, and it's taken from that paper. We have a panda on the left that the model predicts with fairly high confidence, some noise is added, which is fairly opaque to a human. '

# Demo Adversarial example using FGSM
- https://colab.research.google.com/github/tensorflow/docs/blob/master/site/en/tutorials/generative/adversarial_fgsm.ipynbhttps://colab.research.google.com/github/tensorflow/docs/blob/master/site/en/tutorials/generative/adversarial_fgsm.ipynb

# Residual Analysis
- Residual analysis is a subset of a larger class of approaches to prevent social discrimination and other problems that ML production systems usually face.
- to perform residual analysis post deployment, You will need to implement an infrastructure to label new data as it reaches your production system.
- Diff between model predictions and ground truth
- it requires having ground truth values for comparison, which can be difficult in many online or real time scenarios.
- you want the residuals to follow a random distribution. If you find correlation between residuals, it's usually a sign that your model can be improved.
- if you see systematic or correlated residuals then it tells you that there is predictive information that the model has not captured. 
- should not be correlated with another feature that was available but was left out of the feature vector. 
- requires checking the unused features for correlation with the residuals.

# Model Remediation Techniques
- You should make sure that your training data accurately mirrors a request that you'll receive for your trained model.
- data augmentation can also help your model generalize, which typically reduces sensitivity.
- generating data
  - generative techniques
  - interpretive techniques 
  - simply adding noise to your data
- model editing. 
  - Some models such as decision trees are so directly interpret double that the learned parameters can be understood easily. If you find that something is going wrong, you can tweak the model to improve its performance and robustness.
- Model assertions
  - apply business rules or simple sanity checking to your models results and either alter or bypass the results before delivering them. For example, if predicting someone's age numbers should never be negative or if predicting a credit limit. 
- discrimination remediation. 
  - The best solution for this is to have a diverse data set which is representative of the people who will be using your model. It also helps to have people on the development team from diverse backgrounds with expertise in ethics, privacy, social sciences and other related disciplines. 
- feature selection
  - including sampling and reweighting rose to minimize discrimination in training data can also be helpful when training.
- fairness indicators to measure fairness.
  - google model remediation library can help with improving model fairness as well.
- 

IMPORTANT: Model debugging is not something that you only do during development. This requires constant monitoring of your model. The accuracy fairness or security characteristics of MM models will change during the lifetime of a model as the data and the world changes and as new attacks emerge.
RECOMMEND: You should build monitoring into your process so that your models are checked for accuracy fairness and security problems on a regular basis.

Strange anomalous input and prediction values are always worrisome in ML. And can be indicative of an attack, luckily an almost inputs. And predictions can be caught and corrected in real time using a variety of tools and techniques including:
- data integrity constraints on input streams
- Statistical process control methodologies on inputs 
- predictions anomaly detection through auto encoders and isolation for us. 
- also by comparing your model's prediction to benchmark model predictions

# Fairness indicators
You need to make sure that your model is not causing harm to the people who use it. Fairness indicators is an open-source library built by the TensorFlow team to easily compute commonly identified fairness metrics for binary and multiclass classifiers.
- "Fairness indicators" scales
- Has been built on top of the TensorFlow Model Analysis framework. 
- It's important to remember that human societies are extremely complex. Understanding people and their social identities, social structures, and cultural systems are each huge fields of open research. 
- Pay special attention to slices of data that deal with sensitive characteristics such as race, ethnicity, gender, nationality, incomes, sexual orientation, and disability status.
    - slicing helps reduce the batch size over which you compute performance, it biases the sample towards your selection criteria.
    - 
## Measuring Fairness
- +/- Rates
  - These metrics help with understanding demographic parody, the equality of outcomes, which should be equal across subgroups. 
    - The basic positive and negative rates show the percentage of data points that are classified as positive or negative. These are independent of ground truth labels.
    - true positive rate, also known as TPR, and the false negative rate, also referred to as FNR. 
  - true positive rate, measures the percentage of positive data points as labeled in the ground truth that are correctly predicted positive. 
  - false negative rate measures the percentage of positive data points that are incorrectly predicted negative. This metric relates to the equality of opportunity for the positive class when it should be equal across subgroups.
  - true negative rate, also known as TNR, and the false positive rate, also referred to as FPR. 
  - **This often applies to use cases where it's important that the same percentage of qualified candidates are rated positively in each group, such as for loan applications or school admissions.
  - true negative rate measures the percentage of negative data points has labeled in the ground truths that are correctly predicted negative. 
  - false positive rate is the percentage of negative data points that are incorrectly predicted positive.
  - **This applies to use cases where misclassifying something is positive is more concerning than classifying the positives. This is most common in abuse cases where positives often lead to negative actions.
- Accuracy and area under the curve, also known as AUC. Accuracy is the percentage of data points that are correctly labeled, and AUC is the percentage of data points that are correctly labeled when each class is given equal weight independent of the number of samples. 
  - Accuracy is the percentage of data points that are correctly labeled, and AUC is the percentage of data points that are correctly labeled when each class is given equal weight independent of the number of samples. 
  - This applies to use cases where the precision of the task is critical, but not necessarily in a given direction, such as face identification or phase clustering. 

IMPORTANT: Fairness evaluation should be run throughout the development process and post-launch as well. 
IMPORTANT: Fairness evaluations aren't meant to replace adversarial testing, but to provide an additional defense against rare targeted examples.
- This is crucial as these examples probably will not be included in training or evaluation data.

# Resources
- https://arxiv.org/abs/1412.6572
- https://github.com/SauceCat/PDPbox
- https://github.com/AustinRochford/PyCEbox
- you can also compare model performance across subgroups to a baseline or to other models.
- Fairness indicators is primarily a tool for measuring fairness, not for doing remediation to improve fairness.
- https://github.com/GoogleCloudPlatform/training-data-analyst
- https://pair-code.github.io/what-if-tool/