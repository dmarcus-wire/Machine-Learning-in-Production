# ML Pipeline

## Software architecture to automate, monitor and maintain from data to trained model.

1. Data Ingest
1. Data Cleanse
1. Data Analysis
1. Data Transformation
1. Data Validation
1. Feature Engineering
1. Data Splitting
1. Model Development
1. Model Training
1. Training Optimization
1. Model Validation
1. Training at Scale
1. Model Deployment
1. Model Serving
1. Monitoring
1. Logging
1. Explainability
1. Improvments

Data flow and Work flow orchestration

## ML Pipeline = Directed Acyclic Graph (DAG)
- A DAG is a collection of all the tasks you want to run sequenced in a way that reflects their relationships and dependencies.

1. Scoping
1. Data
1. Modeling
1. Deployment

no cycles = DAG

Orchestrators help with Pipeline automation
- Responsible for scheduling various components in an ML pipeline
- Enable pipeline automation
- Airflow, Argo, Celery, Luigi, Kubeflow, TFX

## TFX
A TFX Pipeline is a sequence of scalable components that can handle large volumes of data. 
Lifecycle and components included with TFX on pip install

1. Data Ingestestion
	- ExampleGen
1. Data Validation
	- Tensorflow Data Validation (TFDV descriptive statistics at scale)
	- StatisticsGen (generates statistics for data)
	- SchemaGen (data schema)
	- Example Validator (looks for problems in data)
1. Feature Engineering
	- Transform (does feature engineering)
1. Train Model (estimator)
	- Tuner (tune hyperparameters)
	- Trainer (train the model)
1. Validate Model (analysis)
	- Evaluator (deep analysis)
1. Push if good (validates outcomes)
	- InfraValidator (actually run model on infrastructure, memory, cpu, etc.)
	- Pusher (pushes model to production)
		- TensorFlow Hub (repository)
		- TensorFlow JS (web browser or nodejs app)
		- TensorFlow Lite (mobile or edge or IoT device)
		- TensorFlow Serving (use the model on a server or serving cluster)
1. Serve Model
	- Model Server
	- Bulk Inference

(a Metadata Store underlines the entire pipeline)

The sequence of components are designed for scalable high performance Machine Learning tasks.

# References
1. Announcing the CD Foundation MLOps SIG https://cd.foundation/blog/2020/02/11/announcing-the-cd-foundation-mlops-sig/
1. Software 2.0 https://karpathy.medium.com/software-2-0-a64152b37c35
1. Runner app https://pair.withgoogle.com/chapter/data-collection/
1. Rules of Machine Learning https://developers.google.com/machine-learning/guides/rules-of-ml
1. Bias in datasets https://ai.googleblog.com/2018/09/introducing-inclusive-images-competition.html
1. Logstash https://www.elastic.co/logstash/
1. Fluentd https://www.fluentd.org/
1. TFDV https://blog.tensorflow.org/2018/09/introducing-tensorflow-data-validation.html
1. Data Versioning https://dvc.org/
1. GitHub Large Files https://git-lfs.github.com/
1. ML Metadata https://www.tensorflow.org/tfx/guide/mlmd#data_model & https://www.tensorflow.org/tfx/guide/understanding_custom_components
# Takeaway
The key points here, first of all, Production ML Pipelines are more than just ML code. They're ML development and software development and a formalized process for running that sequence of tasks end to end, in a maintainable and scalable way. 
