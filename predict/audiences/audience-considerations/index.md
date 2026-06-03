---
title: Audience considerations
description: This article serves as a guideline of items to consider when creating audiences using results from Tealium Predict.
url: https://docs.tealium.com/predict/audiences/audience-considerations/
---
## Choosing thresholds

After a model is deployed and making predictions, a common next step is to use your predictions to create one or more audiences. The prediction values in an Tealium AudienceStream output attribute for any model are decimal numbers in a defined range (0 - 1). The typical approach is to choose one or more thresholds or cutoff points to define which portion of that prediction range you want included in your audience.

For example, if your model is predicting a likelihood to purchase in the next 3 days, you may want an audience of only the visitors who are most likely to purchase. To achieve this, you can create an audience using a rule that defines the threshold as 0.8 as an example. In this scenario, the audience only includes visitors with values greater than or equal to 0.8.

There is not one objectively correct threshold value for all audiences, as different audiences serve different business goals and since there are usually substantial variations between models for different target behaviors or among different datasets.

## Sensitivity and specificity

To choose the best threshold, consider the potential trade-offs of choosing a threshold that is relatively high or low. For example, a trade-off between ending up with a larger audience that is less accurate or a smaller audience that is more accurate. In statistics terminology, this is known as a trade-off between _Sensitivity_ and _Specificity_.

* **Sensitivity**  
Sensitivity represents the True Positive Rate or how well the model correctly identifies all visitors who will purchase (using purchase as the behavior your model is predicting).
* **Specificity**  
Specificity determines how well a model identifies false values. Specificity is the metric that evaluates a the ability of the model to predict true negatives of each available category. The True Negative Rate shows how well the model correctly identifies all visitors who will not purchase (using purchase as a the behavior your model is predicting).

