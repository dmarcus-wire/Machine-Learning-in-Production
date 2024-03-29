You will use TensorFlow Serving to deploy the ResNet101 model.

- TensorFlow Serving is a flexible, high-performance serving system for machine learning models, designed for production environments.
- TensorFlow Serving makes it easy to deploy new algorithms and experiments, while keeping the same server architecture and APIs.
- TensorFlow Serving provides out-of-the-box integration with TensorFlow models, but can be easily extended to serve other types of models and data.
- TensorFlow Serving can be run in a docker container and deployed and managed by Kubernetes.

In the lab, you will deploy TensorFlow Serving as a Kubernetes Deployment on Google Cloud Kubernetes Engine (GKE) and use Kubernetes Horizontal Pod Autoscaler to automatically scale the number of TensorFlow Serving replicas based on observed CPU utilization.
- You will also use GKE Cluster Autoscaler to automatically resize your GKE cluster's node pool based on the resource demands generated by the TensorFlow Serving Deployment.

- Horizontal Pod Autoscaler automatically scales the number of Pods in a replication controller, deployment, replica set or stateful set based on observed CPU utilization (or, with custom metrics support, on some other application-provided metrics).
- Horizontal Pod Autoscaler is implemented as a Kubernetes API resource and a controller.
- The resource determines the behavior of the controller.
- The controller periodically adjusts the number of replicas in a replication controller or deployment to match the observed average CPU utilization to the target specified by the user.

GKE's Cluster Autoscaler automatically resizes the number of nodes in a given node pool, based on the demands of your workloads.
- You don't need to manually add or remove nodes or over-provision your node pools.
- Instead, you specify a minimum and maximum size for the node pool, and the rest is automatic.

After configuring the cluster and deploying TensorFlow Serving you will use an open source load testing tool Locust to generate prediction requests against the ResNet101 model and observe how the model deployment automatically scales up and down based on the load.

Summary of the tasks performed during the lab:

- Create a GKE cluster with autoscaling enabled on a default node pool
- Deploy the pretrained ResNet101 model using TensorFlow Serving
- Configure Horizontal Pod Autoscaler
- Install Locust
- Load the ResNet101 model
- Monitor the model deployment


Resources:
- https://www.cloudskillsboost.google/quests/84
- https://locust.io/
-