# Mobile, IoT and Similar

Highest performance at least cost
Machine learning is increasingly becoming part of more and more devices and products. This includes the rapid growth of mobile and IoT applications, including devices which are situated everywhere from farmers fields to train tracks. Businesses are using the data which these devices generate to train machine learning models to improve their business processes, products, and services.

McKinsey predicts that by 2025, the overall economic impact of IoT and mobile could reach trillions of dollars

Traditionally, you can think of deploying machine learning models in the Cloud. This requires a server to run inference and return the results. But with the advance of machine learning research for applications on lower power devices, this processing can be offloaded to a device and run locally. This enables more opportunities for including machine learning is part of a device's core functionality. Moreover, the hardware costs for these devices continues to fall, which enables lower price points and higher volumes. A key aspect of on-device machine learning is that in most cases it ensures greater compliance with privacy regulations by keeping user data on the device.

If you host them on a server, the mobile or IoT device needs to be connected so that it can make a network request. Another option is to embed the model on a mobile device directly. In your case, can you always rely on the device to have a network connection? Also is your model small enough and fast enough to perform inference on the device? Additionally, mobile devices offer limited processing capabilities which might affect which types of models you can embed in them. Furthermore, does the device have all the access it needs to the data that it needs? Or does it need things like historical data that are only available on a server? 

## Mobile Inferencing
Example inferencing on the cloud where a mobile devices sends classification and the cloud send prediction results
### Pros
- Lots of compute capacity
- Scalable hardware
- Model complexity handled by the server
- Easy to add new features and update model
- Low latency and batch prediction

### Cons
- Timely inference is needed

## On-device inference
Load the trained model onto the device
### Pros
- Improved speed
- Performance
- Network connectivity
- No to-and-from comms needed
Cons 
- Less capacity
- Tight resource contraints
  
There's an increasing demand for sophisticated AI enabled services like image and speech recognition, natural language processing, visual search, and personalized recommendations. At the same time, datasets are growing. Networks are becoming more complex. Privacy is increasingly becoming an issue and latency requirements are tightening to meet user expectations. All of these trends influence the choice of where to generate predictions from your trained models, which in turn affects the architecture and complexity of the models that you train.

## Deploying to mobile device
1. ML Kit
1. Core ML
1. TensorFlow Lite 

# Optimizing models
- Neural networks can fill a lot of space mostly filled with weights
- shrinking model file size
- reduces compute resources to inference
- makes models run faster and use less power

## MobileNets
For example, these graphs show accuracy and latency trade-offs for some common image classification models. One example of models optimized for mobile devices are MobileNets, which are optimized for mobile vision applications. 

## Benefits of quantization
1. faster compute
1. lower memory bandwidth
1. low power consumption
1. supports CPU, DSP, NPUs

## what does it affect
1. static values parameters
1. dynamic values activations 
1. computation, transformations
1. impact models accuracy (-), rare (+)

Depending on the task, you will need to make a trade-off between model accuracy and model complexity. If your task requires high accuracy, then you may need a large and complex model. For tasks that require less precision, it's better to use a smaller, less complex model. Because they not only use less disk space in memory, but they are also generally faster and more energy-efficient.
