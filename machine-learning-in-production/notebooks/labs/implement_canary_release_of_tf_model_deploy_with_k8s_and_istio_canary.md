Istio is an open source framework for connecting, securing, and managing microservices, including services running on Kubernetes Engine. It lets you create a mesh of deployed services with load balancing, service-to-service authentication, monitoring, and more, without requiring any changes in service code.

This lab shows you how to use Istio on Google Kubernetes Engine (GKE) and TensorFlow Serving to create canary deployments of TensorFlow machine learning models.

In this lab, you will learn how to:

- Prepare a GKE cluster with the Istio add-on for TensorFlow Serving.
- Create a canary release of a TensorFlow model deployment.
- Configure various traffic splitting strategies.