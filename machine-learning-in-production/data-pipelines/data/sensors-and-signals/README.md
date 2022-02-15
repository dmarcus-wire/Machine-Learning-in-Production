# Sensors and signals

Signals are sequences of data collected from real time sensors
Each data point indexed by timestamp 
Sensors and signlas data is thus time series
Example: classify sequences of accelerometer data recorded by sensors on smartphone

## Human Activity Recognition (HAR)

- require segmentation operators (like windowing for weather data)
- inertial data from wearables fluctates greatly overtime
- features extraction, validation, etc.
- segmentated data should be transformed for modeling
    - spectograms (commonly used) extracting features using intensity
    - normalization and encoding
    - multichannel
    - Fourier transform

Wireless Sensors Work with Human Activity Recognition Dataset (WISDM)
use tf.data.Dataset.window() to convert time series data to depend on past observations

