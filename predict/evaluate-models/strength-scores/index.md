---
title: Strength scores
description: This article provides detailed information about model scoring techniques and formulas used to assign scores and ratings to trained and deployed models in Tealium Predict ML.
url: https://docs.tealium.com/predict/evaluate-models/strength-scores/
---Tealium Predict offers two types of strength ratings: static ratings for each trained version, and dynamic ratings for each deployed model. The strength rating assigned to each trained version of each model provides an easy way to understand rating of the quality of the training and the model which resulted from it.

Models not yet deployed are not assigned a strength score. Training is a one-time event and each retraining results in a new version number. For example, when you retrain _Version 1_, the resulting version is _Version 2_. Each retraining is a new and separate event, which makes this type of strength rating static and specific to each version. The rating for a version does not change over time.

## Strength scores

The strength scores for each trained version of each model provides a rating of the quality (strength) of the training and the model that resulted from the training. Models not yet deployed are not yet assigned a strength score. Strength scores are listed for both training models in the **Training Details** screen and for deployed models in the **Live Performance** screen.

**Strength scores for trained models**

![](/images/predict/predictv2-training-strength-score.png)

**Strength scores for deployed models**

![](/images/predict/predictv2-live-scores.png)Each retraining represents a new and separate event, which makes this type of strength rating static and specific to each version. The rating for a version does not change over time.

### Recall

The proportion of true cases in the data that were correctly selected by the model. For example, measuring the model’s ability not to miss high-value visitors. Recall is a helpful metric to reduce false negatives and can be thought of as the capture rate for the behavior you are trying to predict.

The Recall score displays next to each version in the **Model Dashboard** and in the **Training Details** screen.

### Precision

The proportion of predicted true cases that are actually true. For example, measuring the model’s ability to predict the highest ratio of high-value visitors. Precision is a helpful metric to reduce false positives and can be thought of as the conversion rate for the behavior you are trying to predict.

### F1 Score

The weighted average of Precision and Recall. Measures the accuracy of a model. To calculate the F1 Score, Precision and Recall values are input into the following formula:

`F1 Score = 2 * ( (Precision * Recall) / (Precision &#43; Recall) )`

### Accuracy

The measure of how many predicted cases were correct over the total number of predicted cases. Though a common metric, accuracy is not an ideal model health measurement for imbalanced data sets.

### Precision vs. recall analogy

As an example, assume you have two colors of apples, red and green and your model seeks to predict which apples are red.

If your model has high Precision, this means that the model is usually correct when it predicts an apple is red. If the model creates a list of apples which are supposedly red, high Precision means that this list is mostly accurate and that the apples on the list are actually red.

If your model has high Recall (Sensitivity), the model has the ability to to identify most of the red apples. A model with high recall does a good job of creating a thorough list of the red apples.

Using the same example of red and green apples, the following list describes expected results based on high or low Precision or Recall.

* High Precision, low Recall = a short list of red apples that is fairly accurate.
* High Precision, high recall = a longer list of red apples that is fairly accurate
* Low Precision, low Recall = a short list of red apples that is fairly inaccurate. This list contains more green apples.
* Low Precision, high Recall = a long list of red apples that is fairly inaccurate. This list contains green apples.

The ideal model clearly should have both high precision and high recall. The concept of potential trade-offs (between the volume of apples predicted to be red, and the accuracy of those predictions) is a recurring theme that impacts how machine learning models are used in the real world.
