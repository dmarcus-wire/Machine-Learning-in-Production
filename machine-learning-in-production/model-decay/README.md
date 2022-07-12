# Model Decay

Production ML models often operate in dynamic environments. Over time, dynamic environments change. That's what makes them Dynamic. Think of a recommender system, for example, that is trying to recommend which music to listen to. Music changes constantly, with new music becoming popular and taste changing. If the model is static and continues to recommend music that has gone out of style, then the quality of the recommendations will decline. The model is moving away from the current ground truth. It doesn't understand the current styles because it hasn't been trained for them. So there are two main causes of model drift. Data drift and concept drift.
![](model-decay.png)

## Data Drift
- Data drift occurs when statistical properties of the input, the features, changes. 
- As the input changes, the prediction requests, the input moves farther away from the data that the model was trained with, and model accuracy suffers.
- often occur in demographic features like age, which may change over time. 

## Concept Drift

