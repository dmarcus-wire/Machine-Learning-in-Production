# The pipeline and tools

Step 
- Technique
	- Component

1. Data Ingestestion 
        - ExampleGen
1. Data Inspection
	- dataset_metadata.DatasetMetadata 
1. Data Preprocessing
	- 
1. Data Validation 
        - Tensorflow Data Validation (TFDV descriptive statistics at scale) 
        - StatisticsGen (generates statistics for data) 
        - SchemaGen (data schema) 
        - Example Validator (looks for problems in data) 
1. Feature Engineering 
        - Transform (does feature engineering)
		- tf.Transform
	- Numeric data
		- map numerical features to float
		- one-hot-encoding
	- Categorical data
		- tf.feature_column.categorical_column_with_vocabulary_list
		- tf.feature_column.categorical_column_with_vocabulary_file 
	- PCA
	- t-SNE
	- UMAP
	- Custom Linear Projections
	- TensorFlow Embedded Projector
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
