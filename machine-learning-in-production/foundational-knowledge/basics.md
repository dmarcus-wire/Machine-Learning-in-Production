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

# What is a Service Mesh
Modern applications are typically architected as distributed collections of microservices, with each collection of microservices performing some discrete business function. A service mesh is a dedicated infrastructure layer that you can add to your applications. It allows you to transparently add capabilities like observability, traffic management, and security, without adding them to your own code. The term “service mesh” describes both the type of software you use to implement this pattern, and the security or network domain that is created when you use that software.

As the deployment of distributed services, such as in a Kubernetes-based system, grows in size and complexity, it can become harder to understand and manage. Its requirements can include discovery, load balancing, failure recovery, metrics, and monitoring. A service mesh also often addresses more complex operational requirements, like A/B testing, canary deployments, rate limiting, access control, encryption, and end-to-end authentication.

# What is Istio
Istio is an open source service mesh that layers transparently onto existing distributed applications. Istio’s powerful features provide a uniform and more efficient way to secure, connect, and monitor services. Istio is the path to load balancing, service-to-service authentication, and monitoring – with few or no service code changes. Its powerful control plane brings vital features, including:

Secure service-to-service communication in a cluster with TLS encryption, strong identity-based authentication and authorization
Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic
Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection
A pluggable policy layer and configuration API supporting access controls, rate limits and quotas
Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress

# Istio Components
Istio has two components: the data plane and the control plane.

The data plane is the communication between services. 
The control plane takes your desired configuration, and its view of the services, and dynamically programs the proxy servers, updating them as the rules or the environment changes.

