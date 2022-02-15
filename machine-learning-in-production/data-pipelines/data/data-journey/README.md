# Data Journey

Key points:
MLMD
Artifacts contained
Tracking metadata bewteen components in a pipeline

## Data Provenance "interpreting results"

- Accounting for the evolation of data and models throughout
- ML metadata help with debugging and reproducibility
- Track for data and model changes

## Journey
1. Raw data, features and labels
1. During training the model learns the functional mapping of the input to the labels
1. As data flows through the process, data transforms
1. Interpreting model results requires understanding data transformations

## Artifcats
- Created as the components of the ML pipeline execute
- Includes all of the data and objects produced by the pipeline componenets
- Includes data in different stages and transformations, the schema, the model, and metrics, etc.

## Data provenance and lineage
- Chain of transformations that led to the creation of particular artifacts
- Important for debugging and reproducability and understanding the pipeline

1. Inspect artifcats at each point in training
1. Trace back through a training run
1. Compare training runs

## Data lineage: data protection regulation
- Organization must closely track and organize personal data
- Data lineage is extremely important for regulatory compliance

## Data versioning
- Data pipeline is a challenge
- ML require reproducibility
- Code version control (GitHub)
- Environment versioning: Docker, Terraform, **Ansible**
- Data versioning
    - Version control of data files (datasets)
    - Retore versions
    - Size of files are larger than code files
    - Examples: DVC, Git-LFS
    
# ML Metadata

(MLMD)

- Every run of a pipeline generates metadata
- like logging for software development
- Analyze all parts of ML pipeline
    - Data Validation
    - Data Transformation / Feature Engineering
    - ^^ Stored in a Metadata Store
    
## Metadata: TFX component
1. Driver - supplies required metadata to the Executor 
1. Executor - place to code the functionality of the component < you customize here
1. Publisher - pushes/stores the results into the metadata
1. Metadata Store

## Metadata Library (MLMD)
- Tracks metadata flowing between components in a pipeline
- Objects stored in MLMD are "Artficats" stored in a relationship database and large objects saved on disk, fs, or block store

### Terminology to know

|Units|Types|Relationships|Definition|
|-|-|-|-|
|Artifcats|ArtifactType|Event|Elementary unit of data fed into the metadata store, out from each unit|
|Execution|ExecutionType|Attribution|A record of any component run during the ML pipeline workflow and runtime parameters|
|Context|ContextType|Association|May hold the metadata of projects run, experiments, pipeline details, etc.|

## Metadata stored
1. Artifcats: Data going as input or generated as output by a component
1. Execution: Record of component in pipeline
1. Context: Conceptual grouping of executors and artifacts

Go into a Backend Storage.
- SQLLite
- MySQL
- Filesystem
- Block store

## MLMD Architecture

[!image](./MetadataStore.png)

## Other benefits

1. Produce a DAG of pipelines
1. Verify inputs used in a execution
1. List all artifacts after an experiment (all models training, etc.)
1. Compare artifacts to evaluate runs

## Setup
```
# install ml metadata
pip install ml-metadata

# the store itself
from ml_metadata import metadata_store
# the protocol buffer
form ml_metadata.proto import metadata_store_pb2
```

### Backend 
1. ML metadata registrs metadata in a database called Metadata Store
1. APIs to record and retrieve metadata to and from the store backend connects to:
- Fake database: in-memory for fast experimentation/prototyping
- SQLite: in-memory and disk
- MySQL: server based
- Block  storage (large files): Filesystem, storage are network, or cloud based

```
# create the connection config using the protobuff
connection_config = metadata_store_pb2.ConnectionConfig()

# set an empty fake database in oparent or primary memory on system running from
connectin_config.fake_database.SetInParent()

# sqlite example
connection_config = metdata_store_pb2.ConnectionConfig()
connection_config.sqlite.filename_uri = "..."
connection_config.sqlite.connection_mode = 3 #Read/Write pers

# store sets how you interact with metadata
store = metadata_store.MetadataStore(connection_config)
```

```
#mysql option
connection_config = metadata_store_pb2.ConnectionConfig()

#  relevant information to connect
connection_config.mysql.host = "..."
connection_config.mysql.port = "..."
connection_config.mysql.database = "..."
connection_config.mysql.user = "..."
connection_config.mysql.password = "..."

# create the store  object
store = metadata_store.MetadataStore(connection_config)
```

