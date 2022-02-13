# Notes on different types of data

## Different types of data:
- images
- video
- text
- audio
- time-series (sensors)
    - people are least familiar with

## Time Series

Time series are a sequence of data points in time, often from recorded events where the time dimension indicates when 
the event occurred. They may or may not be ordered in the raw data, but you almost always want them to be in order by 
time for modeling. 

We want to predict the value of why at time t sometime in the future based on previous measurements. The goal is to 
train a model that predicts future outputs with acceptable accuracy. Carl Christian Steinicky pointed out that **it's 
difficult to make predictions, especially about the future.**

To predict future temperature, you can analyze events and measurements from the past

Max Planck Institute for Biochem
1. preprocess features with TFX pipeline
1. convert into sequences of time series
- 14 variables
- Target is T (temp in degC)
- 6 observatoins/hour
- 144 (6x24)/day

tf.data.Datasets.window() converts time series data
a model makes a prediction 1 hour into the future, given a history of 6 hours
| history size = 6 | output_offset = 1 |
| t=0 | t=1 | t=2 | t=3 | t=4 | t=5|t=6|
                              label_width=1
|        total window size = 7         |
   
a model predicts 24 hours into the future given 24 hours of history

| history size = 24   |  output_offset = 24 |
| t=0 | t=1 | t=2 | t=.. | t=24 | t=25| t=47|
                                   label_width=1
|        total window size = 48             |
   
important to know when "now" is 
if now is t=24, careful not to include t=25, t=26, etc.
