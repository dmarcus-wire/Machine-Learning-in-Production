# Automated Machine Learning (AutoML)

1. tries to automate machine learning e2e
1. simple solutions, faster creation and better performance
1. from DataPipeline to Model monitoring, it attempts to complete the lifecycle

Traditional ML, we write code for all phases
1. Ingest and cleanse the raw data
1. Feature selection and engineering
1. Select model architecture, Train model and tune it
1. Validate model performance

it requires a lot of manual programming and highly specialized skillset

if we can provide raw data, it will perform the iterative development in a systematic way.

At the heart is NAS

## Neural Architecture Search parts
1. Search space = defines the range of architectures, limit space to architectures best suited for the problem trying to model (does introduce human bias)
1. Search strategy = how we explore the search space, objective is to find architecture that perform well
1. PerformanceEstimation Strategy = measures and compares archictures, which returns estimated performance to Search Strategy

The objective of Neural Architecture Search is to find architecture is that perform well on our data. The performance estimation strategy helps in measuring and comparing the performance of various architectures. A search strategies selects an architecture from a predefined search space of architectures. The selected architecture is passed to a performance estimation strategy, which returns it's estimated performance to the search strategy. 

AutoML Facilitates building models in an automated fashion
AutoML is not specific to a particular type of model
Neural Architecture Search is a subfield of AutoML
NAS is a technique for automating the design of Artificial Neural Networks

# Search Spaces

Types:
1. Macro
1. Micro

Node is a layer in a neural network like convolution

## Macro
- contains individual layers and connection types, builds model layer by layer
- chain structured space or with branches and skip connections in complex space

## Micro
- neural networks are built from cells, smaller networks
- Normal
- Reduction
- Stacked cells for complete architecture
- Cells can be linear or combined 

# Search Strategies

Examples:
## limitedd to certain size spaces
1. Grid search == search everything, exhaustive
1. Random search == select next option randomly in search space
## more sophisticated   
1. Bayesian == assumates specific distribution, Gaussian, underlies the architectures, guide selection of next option, builds a stochastic architecture
1. Evolutionary == initial population of N-archs is generated, each arch is evalated, highest performers are selected as parents, offspring /mutations are generated and tested
1. Reinforcement Learning for NAS = uses an RNN for sample arch, samples with probability P, computes gradient of P and scales by Accuracy R to controller

n reinforcement learning agents take actions in an environment, trying to maximize a reward. After each action, the state of the agent and the environment is updated and a reward is issued based on a performance metric. Then the range of possible next actions is evaluated, the environment in this case is our search space. And the reward function is our performance estimation strategy.

# Neural Architecture Search

which options in search space to try next? a clear distinction is required, as the process of automating architecture engineering is strictly called NAS.

# Measure of AutoML Efficacy

## Performance Estimation Strategy 

Search Strategies need to estimate performance to generate architectures

1. Validation Accuracy = computationally heavy, takes several GPU-days
1. Lower fidelity estimates = reduce training time by reframing on subset or lower res images or fewer filters, cheaper, but under performant
1. Learning curve extrapolation = predict learning curve reliably, baselines, removes poor performers
1. Weight Inheritance = initialize weights of new archs based on past architectures, **Network Morphism** underlying function is unchanged == few GPU days, like transfer learning

# Cloud solutions

## Amazon SageMaker Autopilot
- auto trains and tunes for classification andd regression
- select label or target
- proposed candidate architectures
- notebooks for visibility
- leaderboard of model candidates
- deploy to prod or iterate on recommendations
- Quick iteration
- High quality models
- Review features selected
- Use cases
    - predict prices based on historical data (stocks, utilities, real estate)
    - churn prediction preventing customer loss id patterns
    - risk assessment for potential events (individuals, assets, companies)

## Microsoft Azure Automated Machine Learning (automl)
- automatic feature selection
- automatice model selection
- auto tuning
- create with no-code UI or 
- use code-first notebooks
- automate feature engineering
- visualize data for trends and common errors
- intelligent stopping
- experiment run summaries and metric visualizations
- model interprebility
- perform what-if analysis
   
## Google Cloud AutoML
- train high quality models 
- NAS
- Transfer learning
- GUI based
- Pipeline lifecycle
- Data labeling (service provider)
- Data cleansing (service provider)
- images (AutoML Vision Classification, Object Detection, Edge Detection)
- video (AutoML Video Intelligence Classification, Object Detection)
- Language (AutoML Natural Language & translation)
- Structure Data (AutoML Tables)

note: the algorithms are frequently evolving

### Classifying images
1. Setup AutoML
1. Create Dataset (upload data)
1. AutoML does training
1. AutoML evaluates
1. AutoML vision deploys
1. Test the model

### Lab
1. Upload a labeled dataset to Cloud Storage.
2. Connect the dataset to AutoML Vision with a CSV label file.
3. Train a model with AutoML Vision.
4. Evaluate the accuracy of the model.
5. Generate predictions on the trained model.

Qwiklabs provides real cloud environments
