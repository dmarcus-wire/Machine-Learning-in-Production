# Enterprise Data Storage

## Feature Stores

Central repository for documented, curated and access controlled features
Enables teams to share, discover and use curated features
online/offline for training/serving
many modeling problems use identical or similar features
same data is used in multiple scenarios
feature engineering > **feature store** > model dev
reduce redundant work especially teams using similar or redundant data

1. avoid duplication in different pipelines
1. access controlled data from features stores
1. data can be aggregated to create new features, anonymized, purged for wipeout for gdpr compliance

Offline feature processing via cron job
Offline > Run > Ingest > Publish to store
        > data quality monitoring > 
Feature metadata allows you to discover feature you need

Online feature usage
1. Low latency access to features
1. Features difficult to compute online
1. Precompute and store for low latency
1. batch pre-computing
1. loading history

safe guards against time travel
- only include data available at the time a serving request is made
- including data available after a request is time travel

goal:
1. manage data from single person to large enterprise
1. scale and performant access to feature data in training and serving
1. consistent point in time access to feature data
1. discovery and insights to features