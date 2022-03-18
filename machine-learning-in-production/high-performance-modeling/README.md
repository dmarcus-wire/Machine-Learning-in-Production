# Distributed training and parallelism

- during prototype, fast and simple
- full training becomes more time-consuming
- as data increases so does time to train
- longer training -> more epochs -> less effective
- distributed training approaches:
    - data
    - model
    
# Data parallelism
models are replicated onto different accelerators (GPU/TPU)
copy complete model to all workers
model updates are synchronized across workers
this is model agnostistic
scale of data parallelism corresponds to batch size

## how
data is split into partitions == total number of workers in cluster
each worker must have enough memory for the entire model
each worker computes errors of predictions
each worker communicates all changes to workers "synchronize" after each batch

## syncrhonous training
- all workers train and complete updates in sync
- supported via all-reduce architecture
- ALL WORKERS WOULD FAIL IF ONE FAILS

## asynchronous training
- each worker trains and completes updates
- supported via parameter server
- more efficient, but lower accuracy
- It's important to consider some form of fault tolerance in cases where workers die or become unstable. 
  - This allows you to recover from a failure incurred by preempting workers. 
  - This can be done by preserving the training state in the distributed file system KERAS BACKUP AND RESTORE CALLBACK

## distribute-aware training
- keras/estimators supported in high level apis
- small changes in code required
- tensorflow tf.distrubite.strategy library provides custom training loop (eager, graph, tf.function)

### strategies with tensorflow
- one device strategy
    - single device, no distribution
    - commonly used for testing during development
- mirrored strategy
    - once machine with multiple GPUs synchronous training
    - each model is mirrored
    - It creates one replica per GPU device 
    - Each variable in the model is mirrored across all the other replicas
    - if a worker gets interrupted, the whole cluster pauses until the interrupted worker is restarted.
    - Together these variables form a single conceptual variable called a mirrored variable. 
- parameter server strategy
    - common asynchronous data parallel method to scale up model training on multiple machines
    - Variables are created on parameter servers, and they are read and updated by workers in each step. 
    - By default, workers read and update these variables independently without synchronizing with each other. 
    - This is why sometimes parameter server style training is also referred to as asynchronous training.
- multi-worker mirrored strategy
- central storage strategy
- TPU strategy

# Model parallelism
models are too large to fit on single ddevice, they can be divided into partitions
assigned to different partitions to different accelerators


