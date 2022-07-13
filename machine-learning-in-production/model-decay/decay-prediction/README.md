# How to detect it?

- Detecting drift, whether it's data drift or concept drift or both starts with collecting current data. 
- You should collect all of the data in the incoming prediction request to your model, along with the predictions that your model makes.
- If it's possible in your application, also collect the correct label or ground truth that your model should have predicted.
  - This is also extremely valuable for retraining your model,
- at a minimum, you should capture the prediction request data, which you can use to detect data drift using unsupervised statistical methods. 
- Once you're set up to continuously monitor and log your data, you employ tools which use well-known statistical methods to compare your current data with your previous training data.
- You also use dashboards to monitor for trends and seasonality over time. 
- Essentially, you'll be working with time series data since you have an ordered data that is associated with a time component. You don't have to reinvent the wheel here, there are good tools and libraries available to help you do this kind of analysis. These include 
  - TensorFlow Data Validation or TFDV
  - and the Scikit-multiflow library.
  - Cloud providers, including Google, offer managed services such as Google's Vertex Prediction, that help you perform continuous evaluation of your prediction requests.
    - Continuous evaluation regularly sample's prediction input and output from trained machine learning models that you've deployed to Vertex prediction. 
    - Vertex data labeling service then assigns human reviewers to provide ground truth labels to your prediction input, or alternatively, you can provide your own ground truth labels. 
    - Azure, AWS, and other cloud providers offer similar services.

# Mitigate it
- First, the basics. 
  - When you detect model decay you need to let others know about it. 
    - That means informing your operational and business stakeholders about the situation, along with some idea about how severe you think the drift has become. 
- Then you work on bringing the model back to acceptable performance, which is what I'll discuss now
- first, try to determine which data in your previous training data set is still valid by using unsupervised methods, such as clustering or statistical methods that look at divergence.
  - Many options exist, including Kullback-Leibler or KL divergence, Jensen-Shannon or JS divergence or the Kolmogorov-Smirnov or K-S test.
  - This step is optional, but especially when you don't have a lot of new data, it can be important to try to keep as much of your old data as possible.
- Another option is to simply discard that part of your training data set that was collected before a certain date and add your new data.
- Or if you have enough newly labeled data then you can just create an entirely new data set.
- The choice between these options will probably be dictated by the realities of your application and your ability to collect new labeled data. 
- Now that you have a new training data set, you've basically two choices for how to train your model, fine tuning or starting over.
- You can either continue training your model, fine tuning it from the last checkpoint using your new data, or start over by re-initializing your model and completely retraining it. 
- Either approach is valid and the choice between these two options will largely be dictated by the amount of new data that you have and how far the world has drifted since the last time you trained your model. 
- Ideally, if you have enough new data, you should try both approaches and compare the results.
- There's really no right or wrong answer here, so it will depend on what works in your particular situation
- This includes situations where you detect a drift, but it also includes situations where you may need to add or remove class labels or features,
- In practice, this is what many people do because it's simple to understand and in many domains it works fairly well. It can, however, incur higher training and data gathering costs unnecessary, or alternatively, it can allow for greater model decay that might be ideal depending on whether your schedule has your model training too often or not often enough.
- Finally, you might be limited by the availability of new training data.
- As a result, you may be forced to try to retain as much of your old training data as possible for as long as possible, and avoid fully retraining your model.

If you can automate the process of detecting the conditions which require model retraining, that's ideal. That includes being able to detect model performance degradation and triggering retraining,

In both cases, in order to automate retraining, you should have data gathered and labeled automatically using a separate process and only retrain when sufficient data is available.

Ideally, you also have continuous training, integration and deployment setup as well, to make the process fully automated. 
- For some domains where change is fast and frequent retraining is required, these automated processes become requirements instead of luxuries. 
- When your model decay is beyond an acceptable threshold, or when the meaning of the variable you are trying to predict deviates significantly, or you need to make changes like adding or removing features or class labels, you might have to redesign your data pre-processing steps and model architecture.
- You may have to rethink your feature engineering, feature selection, and so forth, in order to make your model work with current data, and retrain your model from scratch rather than applying fine tuning.

he point here is that no model lives forever, and periodically, you need to go back to the drawing board and start over, applying what you've learned since the last time you updated your model.
