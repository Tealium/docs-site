---
title: Attribute readiness
description: This article describes how to select the right target attribute to use in your models.
url: https://docs.tealium.com/server-side/predict/strategy/attribute-readiness/
---
When you create a model using Tealium Predict, you can choose from a list of potential target attributes from your AudienceStream dataset. Each attribute is given a rating of **Ready** or **Not Ready** to signify whether the attribute is ready for training. The readiness of an attribute displays next to each attribute in the drop-down list of available attributes when you click **+ New Model**. This feature helps you determine, in advance, whether an attribute candidate is a **Ready** or **Not Ready** to use as a target output attribute, as shown in the following example.

![](https://docs.tealium.com/images/predict/predict-v2-target-attr-ready.png)

Machine learning technology requires a high volume of data to succeed and machine learning models provide better results when trained on a large amount of data.

The following two factors to define target attributes that are **Ready** or **Not Ready**:

* The volume of data for the attribute
* The distribution of that volume between true and false values

Both the true and false groups must be above a minimum threshold. For example, for the dates that span the Training Date Range, the median daily counts of True and False visitors must be greater than or equal to 200. This threshold is intentionally set as low as possible to provide the most options possible for target attributes. A model with a target attribute that is labeled **Not Ready** typically fails during the training process due to insufficient data for the model.

A rating of **Not Ready** does not mean that the attribute is problematic in other contexts, but that it is currently deemed insufficient for successful training of a Tealium Predict model.s

If the target attribute you want to use is labeled as **Not Ready,** try one of the following solutions:

* Wait for more data to accumulate. The problem often solves itself over a longer time period.
* Identify ways to drive additional traffic to the AudienceStream data source.
* Add additional data sources to your AudienceStream profile so that the volume of daily data increases for this target.
