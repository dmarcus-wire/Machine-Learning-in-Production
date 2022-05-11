# What is serving?

- Train a model is only the first part
- Making your model available to a consumer / user is another part
- Provide a service or app for interaction is the last part

# Serving Patterns

Consider 3 components:
1. A model
2. An interpreter for execution
3. Input data

These components are used by an inference process which is aimed at getting the data to be ingested by a model in order to compute predictions.

# ML Workflows
1. Model Training
   1. Performed Offline "Batch or Static learning", where the model is trained on collected data
      1. After deployment, the model remains constant until it is retrained
         1. a while in operation to an offline-trained model dealing with new real-live data will get stale
            1. Monitoring will watch the model for Decay or staleness to guide improvements
   2. Online "or dynamic learning"
      1. After deployment, the model is regularly trained as new data arrives, data streams. Common for time series, sensor or stock data.
2. Model Prediction
   1. Batch predictions
      1. the deployed ML model makes a set of predictions based on historical input data. This is often sufficient for data that's not time dependent or when it's not critical to obtain real-time predictions as output.
   2. Realtime or On-demand predictions
      1. these predictions are generated in real time using the input data that's available at the time of the request

# Important Metrics

"The cost of running your ML model in production can increase sharply as your infrastructure is scaled to handle latency and throughput. This leads you to play a balancing game between costs and customer satisfaction."

1. Latency "reduce for customer satisfaction"
   1. the delay between a user's action and the response of the application to the user's action
   2. starting from sending data to the server, performing inference using the model, and then returning the response
   3. minimal latency is a key requirement to maintaining your customer satisfaction
2. Throughput "increase the load of inference request per second"
   1. is the number of successful requests served in a unit of time
   2. important for applications that are not user-facing
   3. if you want your models to process large amounts of data, for example, video from security cameras at a very high fidelity in order to assure that any security events are spotted quickly
3. Cost "scale the number of servers, caching requirements, etc. to meet the above asks comes at a cost"
   1. the cost associated with each inference. You serving infrastructure will always have associated costs. 
   2. CPUs, 
   3. hardware accelerators like GPUs, 
   4. caches for storing input features for easy retrieval with minimum latency. 
   5. optimizing inference models

# Tactics to minimize costs
1. sharing assets like GPU's
2. using multiple models to increase throughput
3. and perhaps even exploring optimizing your models

# Serving Infrastructure
- Model Complexity reasons
  - increase accuracy
  - more complex relationships
    - both require more features
      - this results in longer latencies to boosts accuracy

## Finding the right balance between cost and complexity
So there's a trade off between the model's predictive effectiveness and the speed of its prediction latency. 
- for every part of the training and serving infrastructure, increased resource requirements means increased costs.
- And increased hardware requirements management of larger model registries and this results in a higher support and maintenance burden

# Metrics
Model optimizing metrics
1. accuracy
2. precision
3. recall

Statisficing (Gating) metric
1. latency
2. models size
3. GPU load

So for example, you might set a latency threshold to a particular value, such as 200 milliseconds and any model that doesn't meet this threshold is not going to be accepted. Another example of a gating metric is the size of the model. If you plan on deploying a model too low spec hardware like mobile and embedded devices, this is of course very important. One approach you can take is to specify the serving infrastructure, CPU, GPU and all that. And then start increasing your model complexity to improve your model's predictive power until you hit one or more of your gating metrics on that infrastructure. Then you can assess the results and either accept the model as it is or work to improve accuracy and or reduce complexity or make the decision to increase the specifications of the serving infrastructure.

# Accelerators
1. GPUs == parallel throughput during training
2. TPUs == large complex models and batch sizes during inference

Whats the cost trade off between applying a large number of less powerful accelerators and using a smaller number of more powerful accelerators.

# Example 'food delivery service'
- the data you send the model may not provide all the features needed for a prediction
- some features may need to be computed or aggregated and then read in real-time from a data store
- features from a data store might be incoming orders, outstanding orders, times placed, etc. require powerful caches to retrieve data with low-latency to update the order in real time
  - NoSQL and NoSQL databases are good solutions for caching and feature lookup
    - If you need sub millisecond read latency on a limited amount of quickly changing data retrieved by a few 1000 clients.
      - One good choice is Google Cloud Memorystore (a fully managed version of Redis and Memcache)
    - If you need millisecond read latency on slowly changing data where the storage scales automatically
      - one good choices Google Cloud Firestore
    - If you need millisecond read latency on dynamically changing data using a store that can scale linearly with heavy reads and writes
      - one good choice of course is Google Cloud Bigtable
    - for scalable low read latency database with an in memory cache
      - Amazon's DynamoDB is also a good choice

Adding caches speeds up feature, look up while reducing prediction retrieval latency. You have to carefully choose from the different available offerings based on your requirements and then balance that with your budget constraints.

# Where do you deploy models?

1. Huge data centers
   1. access model via remote call / REST API
   2. It might not be feasible to deploy a model to a server in environments where prediction latency is super-important or when a network connection may not always be available.
   3. where prediction latency will not work (e.g. autonomous cars)
   4. the system is able to take actions based on predictions made in near real-time, and it can't wait for a server round-trip
   5. Latency might not be as important where it's critical that the model is as accurate as possible, for example, a disease diagnosis. 
2. Embedded devices (mobile phone, etc.)
   1. access model locally on device where the system can take actions near real time
   2. large complex models cannot be deployed to edge devices
      1. average GPU is < 4GB
      2. average 1x-GPU shared by other apps
      3. use for accelerated process will drain battery quickly
      4. average android app storage < 11MB
      5. Exmaple:
         1. MobileNet - designed for mobile devices computer vision
            1. Now they may not have the highest number of predictive classes, and they may not be state of the art in recognition. But all of the work in performing trade-offs for the best mobile model had been done for you already and you can build on this.

# Edge 

## Improving Prediction Latency and Reducing Resource Costs
1. Profile and Benchmark
   1. The TensorFlow Lite benchmarking tool has a built-in profiler that can then show you per operator profiling statistics.
   2. This can help with understanding performance bottlenecks and identifying which operators dominate the compute time.
2. Optimize Operators
   1. model optimization, which aims to create smaller models that are generally faster and more energy-efficient. This is especially important for deployments on mobile devices.
3. Optimize Model 
   1. techniques such as quantization
4. Tweak Threads
   1. You can also increase the number of interpreter threads to speed up the execution of apps
      1. However, increasing the number of threads will also make your model use more resources and power. 
      2. Multi-threaded execution, however, also results and increased performance variability depending on what else is running concurrently, and this is particularly the case for mobile apps.


If you go the other route and deploy a model to a server, there are of course, also some considerations in how you design it. 
The users of your model need a way to make requests, and often this is through a web application. 

# Model Web API
The model is wrapped as an API service in this approach, and most serving infrastructures and languages have web frameworks that can help you to achieve this.
1. For example, Flask is a very popular Python web framework that it's very easy to roll out and API in Flask. 
   1. If you're familiar with it, you can create a new web client in maybe 10 minutes. 
2. Django is also a very powerful web framework for Python. 
3. Similarly, Java also has many options like Apache Tomcat spraying, et cetera. 

# Model Cloud/Server
1. For example, creating the server and managing it to serve prediction requests from clients. 
   1. They eliminate the need for putting models into custom web applications. 
   2. With only a few lines of code, you can generally deploy models. 
   3. They also make it easy to update a rollback models, load, and unload models on demand or when resources are required, and manage multiple versions of models. 
   4. Clipper is a popular open-source model server developed at the UC Berkeley Rise Lab. 
      1. Clipper helps you deploy a wide range of models built in frameworks like Cafe, TensorFlow, and Scikit-learn. Its overall aim is to be model agnostic.
      2. Clipper includes a standard rest interface, so this makes it easy for you to integrate with production applications. 
      3. Clipper wraps your models in Docker containers if you want, for cluster and resource management. 
      4. It also helps you set service level objectives for reliable latencies. 
   5. TensorFlow Serving is also an open-source model server, which offers a flexible high-performance serving system for machine learning models designed for production environments. 
      1. TensorFlow Serving makes it easy to deploy new algorithms in experiments while keeping the same server architecture and APIs.
      2. TensorFlow Serving provides out of the box integration with TensorFlow models, but it can also be extended to serve other types of models and data. 
      3. TensorFlow Serving offers both the REST and gRPC protocols, 
         1. gRPC is often more efficient than REST. 
      4. TensorFlow Serving has demonstrated performance of up to 100,000 requests per second per core, making it a very powerful tool for serving machine learning applications. 
      5. It has a version manager that can easily load and rollback different versions of the same model and it allows clients to select which version to use for each request.
   6. a managed service to serve your models.
      1. Google Cloud AI Platform Prediction Service as an example. 
      2. It allows you to set up real-time endpoints which offer low latency predictions, and you can also use it to get predictions on batches of data
      3. It also allows you to deploy models that have been trained either on Google Cloud or of course, on your own premises. 
      4. You can scale automatically based on your traffic, which can save you a whole lot of costs, while at the same time giving you that high degree of scalability.