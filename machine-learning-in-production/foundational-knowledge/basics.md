# What is Kubernetes?
Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

# Kubernetes Components
A Kubernetes cluster consists of the components that represent the control plane and a set of machines called nodes.

# The Kubernetes API
The Kubernetes API lets you query and manipulate the state of objects in Kubernetes. The core of Kubernetes' control plane is the API server and the HTTP API that it exposes. Users, the different parts of your cluster, and external components all communicate with one another through the API server.

# Working with Kubernetes Objects
Kubernetes objects are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster. Learn about the Kubernetes object model and how to work with these objects.

# What is the SavedModel Format
A SavedModel contains a complete TensorFlow program, including trained parameters (i.e, tf.Variables) and computation. It does not require the original model building code to run, which makes it useful for sharing or deploying with TFLite, TensorFlow.js, TensorFlow Serving, or TensorFlow Hub.

# How to use it
You can save and load a model in the SavedModel format using the following APIs:

Low-level tf.saved_model API. This document describes how to use this API in detail.
Save: tf.saved_model.save(model, path_to_dir)
Load: model = tf.saved_model.load(path_to_dir)
High-level tf.keras.Model API. Refer to the keras save and serialize guide.
If you just want to save/load weights during training, refer to the checkpoints guide.