# Data Labeling

It's important because for supervised learning, you may have data available but if it's unlabeled it's difficult to get usable. Frequent model training is an ongoing process.

Monitor system looking for problems:
1. Slow (e.g. drift)
1. Fast (e.g. bad sensor, bad software update)

## Gradual problems:
1. Data Changes:
	- Trend / Seasonality
	- Distribution of features
	- Relative importance of features change
1. World Changes:
	- Style changes
	- Scope and process changes
	- Competitors change
	- Businesses expand to other Geos

## Sudden problems:
1. Data Collection:
	- Bad sensor/camera
	- Bad log data
	- Moved or disabled sensors
1. System problems:
	- Bad software update
	- Loss of network connection
	- System down
	- Bad credentials

## Understand the model
- Mispredictions affect your costs of business differently
- The data you have is rarely the data you want
- Understand which bad experiences can be mitigated with other means

## Methods
1. Process Feedback (Direct Labeling)
	- Click Through Rates (CTR)
1. Human Labeling
1. Semi-supervised
1. Active supervised
1. Weak supervision

### Direct Labeling
Continuous creation of training datasets
1. Features from inference requests
1. Labels from monitoring predictions
1. Join results with inference requests
1. repeat

Similar to reinforcement learning, applying labels based on a prediction.

#### Tooling
Logstash
- Free and open source data processing pipeline
- ingest data from multiple sources
- transform it
- send it to your "stash"

Fluentd
- open source data collection
- cloud native

Google Cloud Logging
- Data and events from GC and AWS
- BindPlane. Logging is robust.

AWS ElasticSearch

Azure Monitor

### Human Labeling
1. Unlabeled data is collected
1. Human raters are recruited
1. Instructions for raters are created
1. Data is divided among raters
1. Labels are collection and conflicts resolved


