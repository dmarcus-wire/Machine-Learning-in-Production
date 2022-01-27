# Importance of Data

How will you get the data you need?

## Importance of Data Quality

Model is only as good as the quality of your data.

## Data pipelines

Automate the collect, ingest, prepare as sequenced automated tasks over the lifetime of the application.

"Broken data is the most common cause of problems in production ML systems." - Uber

## Data is a first class citizen

In programming language design, a first called citizen is a in a given programming language is an entity which supports all the operations generally available to other entities, and an ML data is a first class citizen.

you could have mountains of data, but if it if it doesn't have predictive content, then, you're just not going to be able to create a predictive model with it. 

remove information from your model and features from your model that aren't predictive, because they're going to cause problems are certainly going to take a lot of compute resources that you don't want to be spending on that. 

And you need to make sure supervised learning case or even unsupervised learning, that your training data is really covering the same feature space as the as the prediction requests that you'll get when you put your model into production. 

data = garbage in, garbage out...The good news actually for ML is that we can measure 

## What to monitor?
- Downtime
- Errors
- Distribution Shifts
- Data failure
- Service failure

## Questions to ask?
- What are the user needs?
- What kind of data and how much is available?
- How often does new data come in?
- It is annotated (labeled)?
- What are the features?
- What are the labels? (these could be provided and applied during serving)
- Is the data consistent (values, types, formatting, missing, etc.)
- Is the input coming from other ML models (ensemble)?
- Do you have the ability to monitor system issues and outages?
- What features have predictive value? Which ones don't?

