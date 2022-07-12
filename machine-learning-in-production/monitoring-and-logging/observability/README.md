# Observability

## What is observability? 
Observability measures how well you can infer the internal states of a system by just knowing the inputs and outputs. For ML, this means monitoring and analyzing the prediction requests and the generated predictions from your models. 

### Control System Theory
Observability isn't a new concept, it actually comes from control system theory where it has been well established for decades. In control system theory, observability and controllability are closely linked. You can only control a system to the extent that you can observe it.

## Complexity of monitoring
This also adds to the importance of model interpretability. In ML systems, observability becomes a more complex problem since you need to consider multiple interacting systems and services such as cloud deployments, containerized infrastructure, distributed systems, and microservices.

For example, monitoring CPU utilization across an autoscaling containerized application is much different than simply monitoring CPU usage on a single server

Observability is about making measurements. Just like when you're analyzing your model performance during training, measuring top-level metrics is not enough and will provide an incomplete picture.

You need to slice your data to understand how your model performs for various data subsets. For example, in an autonomous vehicle, you need to understand performance in both rainy and sunny conditions and measure them separately. More generally speaking, data slices provide a useful way to analyze different groups of people or different types of conditions.
- In general, it's your domain knowledge that will guide how you slice your data.

## Tools
TFX and TFMA
- The TFX framework and TensorFlow model analysis are very powerful tools and include functionality for doing observability analysis on multiple slices of data for your deployed models. 
- This is true for both supervised and unsupervised monitoring of your models. 
- In a supervised setting, the true labels are available to measure the accuracy of your predictions. 
- In contrast, in an unsupervised setting, you'll monitor for things like the means, medians, ranges, and standard deviations of each feature.
- In both supervised and unsupervised settings, you need to slice your data to understand how your system behaves for different subsets.

## The goal
The main goal of observability in the context of monitoring is to prevent or act upon system failures. For this, the observations need to provide alerts when a failure happens, and ideally provide recommended actions to bring the system back to normal behavior. 

1. Alertability 
   1. refers to designing metrics and thresholds that make it very clear when a failure happens. This may include defining rules to link more than one measurement to identify a failure. 
   2. Knowing that your system is failing is a good start, but an actionable recommendation based on the nature of the failure is way more helpful to correct this behavior. 
2. Actionable
   1. Actionable alerts clearly define the root cause of the system's failure. At a bare minimum, your system should gather sufficient information to enable root cause analysis. v

Both alertability and actionability are goals, and the effectiveness of your system is a reflection of how well it achieves these goals.

