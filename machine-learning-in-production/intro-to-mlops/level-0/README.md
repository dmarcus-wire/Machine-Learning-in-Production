# MLOps Level 0

## What defines an MLOps process maturity?
- Fundamentally, the level of automation of the data, modeling, deployment, and maintenance systems determines the maturity of the MLOps process. 
- With increased maturity, the available velocity for the training and deployment of new models is also increased. 
- The objective of an MLOps team is to automate the training and deployment of ML models into the core software system and provide robust and comprehensive monitoring. 
- Ideally, this means automating the complete ML workflow with as little manual intervention as possible. 
  - Triggers for automated model training and deployment can be 
  - calendar events, 
  - messaging or 
  - monitoring events, 
  - as well as changes in data, 
  - model training code and application code or detected model decay.

Many teams have data scientists and ML researchers who can build state-of-the-art models but their process for building and deploying ML models is entirely manual. This is considered the basic level of maturity or level 0. 
- This is generally script or notebook driven for the most part and every training step is manual, including data analysis, data preparation, model training, and validation.
- requires manual execution of each step and manual transition from one step to another
- process is usually driven by experimental code that is written and executed in notebooks by data scientists interactively until a workable model is produced
- creates a disconnect between the ML and operations teams
- opens the door for potential training serving skew
- assumes that your data science team manages a few models that don't change frequently because of either changes in model the implementation or retraining the model with new data, or both.
- a  new model version is probably only deployed a couple of times a year.
- fewer code changes, continuous integration or CI, and often even unit testing is totally ignored
- testing the code is part of the notebooks or script execution
- The scripts and notebooks that implement the experiment steps are often source controlled, and they produce artifacts such as trained models, evaluation metrics, and visualizations.
- because there aren't many model versions that need to be deployed, continuous deployment or CDs isn't even considered
- concerned only with deploying the trained model as a prediction service. For example, a microservice with a REST API, rather than deploying the entire ML system
- here you do not track or log the model predictions and actions which are required in order to detect model performance degradation and other model behavioral drifts
- common in many businesses that are beginning to apply ML to their use cases
- models often break when they are deployed in the real world
- Models fail to adapt to changes in the dynamics of the environment or changes in the data that describes the environment

# Fixing 
- To address these challenges and to maintain your model's accuracy and production, you need, first of all, to address the lack of active performance monitoring.
- Active monitoring your model lets you detect performance degradation and model decay. It acts as a cue that it's time for new experimentation and retraining of the model on new data
- you need to retrain your production models often with the most recent data to capture the evolving and emerging patterns.
