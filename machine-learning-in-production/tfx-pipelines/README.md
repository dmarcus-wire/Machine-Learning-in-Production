# TFX Pipelines

- TFX is an open source framework that you can use to create ML pipeline.
- TFX enables you to implement your model training workflow in a variety of execution environments, including containerized environments like Kubernetes
- TFX pipelines, organize your work flow into a series of components where each component performs a step in your ML workflow
- TFX standard components provide proven functionality to help you get started building in ML workflow easily.
- You can also include custom components in your workflow, including creating components which run in containers and can use any language or library that you can run in a container such as performing data analysis using R. 
- Custom components let you extend your ML workflow by creating components that are tailored to meet your needs, such as:
  - data augmentation, 
  - upsampling or downsampling anomaly detection 
  - or interfacing with external systems such as help desks for alerting and monitoring and much more.

## Hello World
![](tfx-hello.png)
1. Orange = training components
2. Green = batch inference components

## Anatomy of TFX
1. Component Specification
   1. input/output contract
2. Exector Class
   1. implements component processing
3. Component Class
   1. combines the spec with the executor to create TFX component

## Runtime of TFX
1. Driver
   1. First, the driver uses the component specification to retrieve the required artifacts from the metadata store and pass them into the component.
2. Executor
   1. Next, the executor performs the components work.
3. Publisher
   1. Finally, the publisher uses the component specification and the results from the executor to store the components, outputs in the metadata store. 

## Types
There are three types of custom components, Python function based custom components, container based custom components and fully custom components.
1. Fully custom components 
   1. lets you build components by defining the component specification, executer and component interface classes. This approach lets you reuse and extend a standard component to meet your needs.
2. python function based component
   1. hey only require Python function for the executor with a decorator and annotations. 
3. container based components
   1. provide the flexibility to integrate code written in any language into your pipeline, assuming that you can execute that code in a docker container. 
   2. To create a container based component, you create a component definition that is very similar to a Docker file and cause a wrapper function to instantiate it.

# References
- https://cloud.google.com/architecture/architecture-for-mlops-using-tfx-kubeflow-pipelines-and-cloud-build
- https://github.com/GoogleCloudPlatform/training-data-analyst
  - Open vertex_pipelines_simple.ipynb