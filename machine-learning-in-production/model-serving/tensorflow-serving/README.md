# Serving

The easiest and most straightforward way of using TensorFlow Serving is with Docker images. I highly recommend this route unless you have specific needs that are not addressed by running in a container. Here's a tip, this is also the easiest way to get TensorFlow Serving working with GPU support.\

```
docker pull tensorflow/serving
docker pull tensorflow/serving:latest-gpu

tensorflow-model-serving

```