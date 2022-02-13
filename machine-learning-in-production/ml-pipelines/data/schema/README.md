# Schema Development

Enterprise schema environments

- Relational objects summarizing the feeatures in a given dataset
    - feature name
    - type (float, int, string, etc.)
    - required or optional
    - valency (features with multiple value: lists/array (min an max num of values))
    - range and categories
    - defaults values
    
Important to track change distributions

Changing data results in a new schema.
Identify anomalies not included in schemas.

Production use of Schemas
1. Resilient and reliable against inconsistent data.
    - Should be expected that you won't get clean data
    - your software WILL experience runtime errors and the pipeline should hanle
    - misconfiguraitons will occur
    - execution of the pipeline should be addressed through each
1. Scalable during data evolution
    - High data volume during training
    - Variable requests traffic should scale up and down to minimize costs
1. Anomalies from schemas
    - Easy to detect
    - Data errors should be treated as first class citizens like bugs in code
    - update your schema as needed
    - 
    
# Platforms
1. Easy to detect anomalies
1. Data errors treated like bugs in code
1. Update data schema
1. Schema evolution can track evolution of data
1. Schema can be inputs for things like automatic feature engineering

# Multiple Schema versions

Schema will likely evolve with data.
You may have multiple schemas active in Dev, Test, Prod
Versioning Schemas is critical.

# inspecting anomalies
you can visualize anomalies in a jupyter notebook

```
stats_options = tfdv.StatsOptions(schema=schema, 
                                    infer_type_from_schema=True)

eval_stats = tfdv.generate_statistics_from_csv(
    data_locations=SERVING_DATASET,
    stats_options=stats_options
)

serving_anomalies = tfdv.validate_statistics(eval_stats, schema)
tfdv.display_anomalies(serving_anomalies)
```

## Schema environments

You may have 2x schemas active in 2 different environemnts 
    1. training
    1. serving (without the label)

```
schema.default_environment.append('TRAINING')
schema.default_environment.append('SERVING')

# assuming Cover Type is the label in the training data
tfdv.get_feature(schema, 'Cover_Type')
    .not_in_environment.append('SERVING')
    
server_anomalies = tfdv.validate_statistics(eval_stats, schema, environment='SERVING')

# should display no anomalies since the correct environment was set without the label
tfddv.display_anomalies(serving_anomalies)
```
## Interactive Schema

As you develop code to adapt to the business and data, your schema will also change.

- you'll likely have multiple versions active at the same time
- version control for schemas makes it manageable
- different schemas enable different environemnts (cloud vs edge) based on data type differences

