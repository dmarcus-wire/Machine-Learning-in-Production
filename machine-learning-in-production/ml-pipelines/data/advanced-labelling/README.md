# Advanced Labeling

Machine learning is growing everywhere and labelled data for supervised learning is critical.
- labeled data, especially manually, is expensive and limited.
- unlabeled data is cheap and available.

## Semi-supervised learning

Automate labelling at the expense of some inaccuracies 
- combine labeled data with unlabeled data
- infer labels for unlabeled data from human labeled classes
- based on assumption that different label classes will cluster or have some structure
- can boost accuracy
- using small amount of labeled data boosts model accuracy  
- **label propagation** is an algorithm that applies labels to unlabeled records
    - based on similarity
    - **graph based label propagation** 'similarity is one way

## Active Learning

intelligently sample your data
- selects unlabeled points that would be most informative for a moddel
- imbalanced data set, helps selecting rare classes for training
- think of Healthcare
- select most important examples to label  
- selects labeled examples that will best help model learn

1. start with unlabeled data
1. intelligent sampling selects some recrods
   - **Margin Sampling** (decision boundary between 2 labeled classes)
   - add the closest unlabeled point to the Decision Boundary to a label
   - retrain the model to learn a new classification boundary
   - continue until model doesn't improve 
   - can reach accuracy earlier than random sampling 
1. human annotates
1. labeled training set
1. ML model
1. start at first step

Other algs:
- **Cluster Based Sampling** sample from well-formed clusters to cover an entire space
- **Query by committee** train an ensemble of models and samples points that generate disagreement
- **Region Based Sampling** runs several active learning algs in different partitions of the space

## Weak supervision with Snorkel

leveraging higher-level and noisier input from SMEs
use heuristics to label
learn a generative model that determines a relevence of sources

1. unlabeled data without ground truth
1. one or more weak supervision sources
1. a list of heuristics that can automate labeling
1. typically provided by SMEs
1. noisy labels have probability of being correct, not 100%
Objective is to learn a generative model to determine weights for weak supervision sources
   
Snorkel
- from Standford in 2016
- most common weak supervision model
- clean, model and integrate resulting training data
- applies novel algs

1. unlabeled data
1. apply label-functions to generate noisy labels
1. apply generative model to de-noise and weight labels
1. train a discriminitave model 

```
from snorkel.labeling import labeling_function

@labeling_function()
def lf_keyword_my(x):
    """label message spam if contains word my, else no opinion of label"""
    return SPAM if "my" in x.text.lower() else ABSTAIN
    
@labeling_function()
def lf_short_comment(x):
    """non-spam comments are often short"""
    return NOT_SPAM if len(x.text.split()) < 5 else ABSTAIN
```
