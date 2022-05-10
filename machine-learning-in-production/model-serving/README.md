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
   2. Onine "or dynamic learning"
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