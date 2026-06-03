---
title: Model retraining recommendations
description: This article provides best practices and recommendations for retraining a model.
url: https://docs.tealium.com/predict/deploy/model-retraining-recommendations/
---

## About retraining

Although machine learning and statistics tools are not designed to guarantee future performance, following simple guidelines can improve performance results and reduce potential clutter from attempting to create more models instead of retraining those already in place. The following sections provide general guidelines and best practices about retraining both trained and deployed models.

For information about how to retrain a model, see [Retrain a Model]().

### Estimating the number of trainings needed

Estimating the number of trainings a model may need is more of a machine learning art than a science. Fine tuning a model requires multiple trainings (1 to 3 is normal) and adjustments to the attributes to exclude. When a model starts to degrade, a retraining produces a better result at first, but then slowly begins to degrade again as time elapses. Typically, each trained version of a model takes longer to degrade as the training date range gets longer.

### Identifying a degraded model

There are two main factors that contribute to model degradation: the amount of time since the last training and the volume of new data received by the model. A model in training is only a snapshot, whereas a deployed is model is live. If the score for a deployed model is lower than the score for the trained model, this indicates that the model has degraded and needs retraining.

### Deploying a newly trained version with a higher score

When the current deployed version of a model has a low performance score and you retrain it to create a new version with a higher score, deploy the retrained version to ensure that the best version of the model is deployed.

It is not recommended to recreate a second similar model in an attempt to achieve a higher score. A second model is not likely to provide any additional benefit and it can add clutter to your implementation.

### When a retrained version has a lower score

A lowered score for a deployed model makes it evident that the model is starting to degrade and needs to be retrained to improve performance. However, sometimes a model that has begun to degrade, and is retrained, will have a lower score than the deployed model.

In this scenario, the newly trained model should not be deployed in place of the current model. Adjustments and retraining should continue until the score for the retrained model is higher than the initial degraded model score. Only when the score is higher should the new model be deployed.

### Low F1 scores and rapid degradation

If a model has a low F1 score after being trained, and it degrades rapidly, one or both of the following issues:

* **Inconsistent Data**  
The behavior of your visitors is changing or inconsistent within the timeframe used for training the model as compared to the present.
* **Incomplete Data**  
You might need additional visitor attributes for a more complete view of visitor behavior.

### Retraining frequency

The need to retrain models is not specific to the Tealium Predict product, but to machine learning in general. The frequency that you retrain depends on your data, which differs greatly between businesses. In general, longer training date ranges most often create models that degrade more slowly. Retraining is typically needed when a model quality degrades below a predetermined score that is acceptable to your organization.

### Retraining vs. deleting

Consider retraining a model before deleting it. When you delete a model, you lose the training history. When you retrain, each training can have a different configuration in terms of time frame, excluded attributes, and data added over time. You can then view the differences between versions (individual trainings) to decide which version to deploy.

## External impacts on model training

When the world, businesses, and visitor behavior shift rapidly, a model that normally takes months to degrade can degrade more rapidly than expected. The following external issues can potentially impact model training and results.

### Global issues

Global issues that impact markets, such as the COVID-19 pandemic of 2020, do impact models to some extent. Though these types of issues can make it difficult to get a clear picture of your visitor behavior, it is easy to retrain a new version and then seamlessly deploy it without the manually intensive process of retuning over and over using valuable engineering and data staff resources.

### Marketing campaigns

Models are sometimes trained simultaneously with other activities, such as an ad campaign, a major holiday, unseasonable heat, mass riots, or political upheavals.

When activity ceases or no longer applies, your current model may not function as well as it did during training. In addition to retraining your models, you can include attributes in your models that represent these events.

### Data distribution considerations

For a model to accurately predict, the data for the basis of the predictions must have a similar distribution to the data on which the model was trained. As data distribution drifts over time, model deployment is not a one time task, but a continuous process. It is a best practice to continuously monitor your incoming data and retrain your model on newer data when you know that your data distribution has deviated from the original training data distribution. If monitoring data to detect changes in data distribution has a high overhead, you can simply retrain your model periodically, such as daily, weekly, or monthly.
