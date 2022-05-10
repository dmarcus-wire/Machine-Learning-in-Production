# Explainable Artificial Intelligence or XAI

we need to explain the results and the decisions that are made by our models.

This is especially true for models with high sensitivity, including natural language models, which when confronted with certain examples, can generate wildly wrong results. It also includes vulnerability to attacks which we need to evaluate on an ongoing basis and not just after an attack has already happened. Of course, fairness is a key issue.

interpretability, explaining to yourself and probably to other people why your model did what it did. 
It's important increasingly in a lot of production ML for a number of different reasons including fairness, regulatory requirements, and legal requirements, as well as just being able to understand your model better so that you can either fix problems with it or improve it.

Interpretability and explainability are parts of a larger field known as responsible AI. 

The development of AI and the successful application of AI to more and more problems has resulted in the rapid growth of the ability to perform tasks which were previously not possible.

There are sometimes questions about models and how responsibly they handle a number of factors which influence people and can cause harm. Issues of fairness, which we've talked about previously, are central to Responsible AI.

**Explainability in a smaller sense, interpretability are key to being able to do Responsible AI because we need to understand how models generated their results.**

**Privacy is also part of responsible AI, since models often operate with Personally Identifiable Information or PII, and they are often trained with PII.**

**security is also an issue and related to privacy. Since one of the attacks that we've talked about is to pull the training data out of a model, which could mean pulling private information from a model.**

A simple example of this is a decision tree-based model, which by its nature is explainable.

Explainability is important in many ways. These include: 
1. ensuring fairness, 
2. looking for issues with bias in the training data, 
3. regulatory, legal, 
4. and branding concerns, 
5. and simply studying the internals of a model to optimize it, to produce the best results

# Interpolation Methods

"they are interpretable if their operations can be understood by a human either through introspection or through a produced explanation. In other words, if there's some way for a human to figure out why a model produced a certain result, then the model is interpretable. "

One measure of interpretability of models is the amount of effort or analysis required to understand a given result

Ideally, you should be able to query the model to understand the what, why, and how of its algorithmic decisions.

## Why did the model behave in a certain way?
You should be able to identify and validate the relevant variables driving the model's outputs.

## How can we trust the predictions made by the model? 
Well, you should be able to validate any given data point to demonstrate to business stakeholders and peers that the model works as expected. 
This will help ensure the transparency of the model.

## What information can the model provide to avoid prediction errors? 
You should be able to query and understand latent variable interactions in order to evaluate and understand in a timely manner what features are driving predictions.

For example, interpretability methods can be grouped based on whether they're 
1. intrinsic 
   1. 4. feature importance - returns a single number per feature.
   2. and partial dependency plots - are curves that show a feature and its average predicted output. In this case, drawing the curve is more meaningful and intuitive than simply representing the values in a table.
   3. Counterfactual explanations - are used to explain the prediction of a data point. In order to do so, it finds another data point by changing some features so that the predicted output changes in a relevant way.
2. or Post-Hoc. 
   1. treat models as black boxes and often don't distinguish between different model architectures
   2. applied after training to try to examine particular results to understand what caused the model to generate them
   3. don't evaluate the actual sequence of operations that led to the generation of the results

They could also be 
4. model-specific 
   1. limited to specific model types
5. or model agnostic. 
   1. are not specific to any particular model
   2. they are Post-hoc methods
   3. do not have access to the internals of the model such as weights and parameters, etc
   4. analyzing feature input and output pairs and trying to infer relationships

They can also be grouped according to whether they are 
6. local 
   1. the method explains an individual prediction
   2. feature attribution in the prediction of a single example in the dataset.
      1. how much each feature contributed to the predictions for a given result.
   3. 
7. or global.
   1. it explains the entire model behavior.
   2. if the method creates a summary of feature attributions for predictions on the entire test set, then it can be considered global
   3. EXAMPLE created by the SHAP library

# Intrinsically Interpretable Models

the workings of the model are transparent enough and intuitive enough that they make it relatively easy to understand how the model produced a particular result by examining the model itself.
1. tree-based
2. linear

the larger and more complex architectures, which makes them black boxes when we're trying to interpret them
...requires post-hoc analysis tools

One key characteristic which helps improve interpretability is when features are monotonic. Monotonic means that the contribution of the feature towards them all result, either consistently increases or decreases or stays even as the feature value changes. 
For example, if you're trying to create a model to predict the value of a used car, when all other features or how constant, the more miles on the car, the less the value should be. 

For linear regression models, 
the absolute value of a features t-statistic is a good measure of that feature's importance. The t-statistic is the learned or estimated weight of the feature scaled by its standard error. The importance of a feature increases as its weight increases. 

Lattice models overlaid grid onto a feature space and set the values of the function that it's trying to learn at each of the vertices of the grid. As prediction requests come in. If they don't fall directly on a vertex, then the result is interpolated using linear interpolation from the nearest vertices of the grid.
Tensorflow lattice models also have a level of accuracy on complex problems that is similar to deep neural networks. Of course, Tensor-Flow lattice models are also easier to interpret than neural networks. However, lattice models do have a weakness. Dimensionality is there kryptonite? 
The number of parameters of a lattice increases exponentially with the number of input features, which creates problems with scaling for datasets with a large number of features. As a rough rule of thumb, you're probably okay with 20 or less features.
There is another way to deal with this dimensionality kryptonite however and that's by using ensembling.

# Model Agnostic Methods

Model agnostic methods separate the explanations from the model. These methods can be applied to any model after it's been trained.
model flexibility and explanation flexibility. The explanation shouldn't be limited to a certain type. The method should be able to provide an explanation as a formula or in some explanations it can be graphical like perhaps for feature importances.
These methods also need to have representation flexibility. The feature representations used should make sense in the context of the model being explained.

## Partial Dependency Plots "PDP"
- PDP is a global method since it considers all instances and evaluates the global relationship between the features and the results.
- help you to understand the effects that particular features have on the model results that you're seeing, and the type of relationship between those features, and the targets or labels in your training data.
- advantages
  - The results tend to be intuitive, especially when the features are not correlated. 
  - The interpretation of a PDP is also usually causal
- disadvantages
  - Realistically, you can only really work with two features at a time, because humans have a hard time visualizing more than three dimensions.
  - PDP assumes that the features that you're analysing aren't correlated with other features. 
    - it's a good idea to eliminate correlated features anyway.
      - For example, suppose you want to predict how fast a person walks given the person's height and weight. PDP will assume that height and weight aren't correlated,

## Permutation Feature Importance
- Essentially by assigning a nearly random value to the feature.
- Permuting a feature is just one way of breaking the relationship between a feature and the model result. Essentially by assigning a nearly random value to the feature. 
- A feature is important if shuffling its values increases the model error. Because in this case, the model relied on the feature for the prediction. 
- If we find that we have unimportant features then we should really consider removing them from our feature vector. 
- A big advantage 
  - is that it doesn't require retraining the model. Some other methods suggest deleting a feature, retraining the model, and then comparing the model error.
- disadvantage
  - You also need to have access to the original labeled training data set. If you're getting the model from someone else and they don't give you that, then you can't use permutation feature importance.

## Shapley Value
Shapp, which is short for shapely additive explanations, is a game theoretic approach to explain the output of any machine learning model, which makes it model agnostic.

A key concept in measuring feature importance and the contribution of each feature to the models results is the Shapley value. Let's discuss that now. The Shapley value is a concept from Cooperative Game Theory. It was named in honor of Lloyd Shapley who introduced it in 1951 and won the Nobel Prize in Economics for it in 2012.

Here's how it works in game theory. Imagine that a group of players cooperates and that results in an overall gain because of their cooperation. Since some players may contribute more than others or may possess different bargaining power, how should we distribute the gains among the players? Or phrase differently, how important is each player to the overall cooperation and what payoff can he or she reasonably expect? 

For machine learning and interpret ability, the players are the features of the data set, and we're using the Shapley value to determine how much each feature contributes to the results. As you might expect the prediction is the payout. 

It assigns each feature and importance value for a particular prediction and includes some very useful extensions, many of which are based on this recent theoretical work. These include tree explainer, high speed exact algorithm for tree ensembles, deep explainer, high speed approximation algorithm for chef values in deep learning models, gradient explainer, which combines ideas from integrated gradients, Shap and smooth grad into a single expected value equation, and Colonel explainer, which uses especially waited local linear regression to estimate Shap values for any model.

# Concept Activation Vectors (TCAV)

The interpretation of deep learning models is a challenge due to their size, complexity and often opaque internal state. In addition, many systems, such as image classifiers operate on low level features rather than high level concepts. To address these challenges, the team at google introduced concept activation vectors, or CAVs, which provide an interpretation of a neural networks internal state.

# Lime

LIME, which is a popular and well-known framework for producing local explanations. LIME is a popular and well-known framework for creating local interpretations of model results. 

LIME tests what happens to the predictions when you give variations of your data to the model. LIME generates a new dataset consisting of permuted samples and the corresponding predictions of the model. With this new dataset LIME then trains an interpretable model, which is weighted by the distance from the sampled instances to the result that we're interpreting. 

With this new dataset LIME then trains an interpretable model, which is weighted by the distance from the sampled instances to the result that we're interpreting. The interpretable model can be anything that is easily interpretable, like a linear model or a decision tree. 

The new model should be a reasonably good approximation of the model results locally, but it does not have to be a good global approximation. This kind of accuracy is called local fidelity.

# Cloud based tools for interp

Googles AI Explanations service. Another option for interpretability is to leverage managed services from Cloud providers, such as Google's AI Explanations for AI Platform.

AI Explanations tells you how much each feature in the data contributed to the predicted results. You can then use this information to verify that the model is behaving as expected and identify any bias in your models and get ideas for ways to improve your model and your training data.

AI Explanations currently offers three methods of feature attribution. These include sampled Shapley, integrated gradients, and XRAI. 

In the integrated gradients method, the gradient of the prediction output is calculated with respect to the features of the input along an integral path. The gradients are calculated at different intervals based on a scaling parameter that you can specify.

XRAI or eXplanation with Ranked Area Integrals is specifically focused towards image classification. The XRAI method extends the integrated gradients method with additional steps to determine which regions of the image contribute most to a given prediction. XRAI performs pixel-level attribution for the input image using the integrated gradients method.


# Resources:
1. https://ojs.aaai.org/index.php/aimagazine/article/view/2850/3419
2. https://arxiv.org/pdf/1910.10045.pdf
3. https://christophm.github.io/interpretable-ml-book/
4. https://www.tensorflow.org/lattice
5. https://jmlr.org/papers/volume17/15-243/15-243.pdf
6. http://arxiv.org/abs/1801.01489
7. https://proceedings.neurips.cc/paper/2017/file/8a20a8621978632d76c43dfd28b67767-Paper.pdf
8. https://arxiv.org/abs/1905.04610
9. https://arxiv.org/pdf/1711.11279.pdf
10. https://github.com/marcotcr/lime
11. https://storage.googleapis.com/cloud-ai-whitepapers/AI%20Explainability%20Whitepaper.pdf