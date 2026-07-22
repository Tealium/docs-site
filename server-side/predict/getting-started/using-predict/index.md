---
title: Using Predict
description: This article provides an overview of the Tealium Predict ML workflow, basic Predict implementation, and best practices for readying your data and creating models.
url: https://docs.tealium.com/server-side/predict/getting-started/using-predict/
---
If you have the Tealium AudienceStream CDP product with data collection enabled, you have the ability to begin using Tealium Predict. We recommend reviewing our [Prerequisites]() to ensure you have enough event volume to create and train a model for the outcome you are trying to drive.

![](https://docs.tealium.com/images/guides/predict/predict-workflow.png)

Use the following steps to get started with Predict:

1. **Select**  
[Select the target attribute](https://docs.tealium.com/decide-what-to-predict/) that represents the visitor behavior you want to predict. The [target attribute](https://docs.tealium.com/decide-what-to-predict/#target-attribute) can be any badge or boolean attribute in Tealium AudienceStream CDP. If your target attribute is not ready for modeling, see [strategies for getting your data ready for training]().
1. **Train**  
After your target attribute is ready for modeling, [create a model]() and start training. While creating your model, an [output attribute](https://docs.tealium.com/decide-what-to-predict/#output-attributes) is created for you that will store prediction values for your model after you deploy it. You define the time window within which the user must return and complete the target attribute action for model training.
1. **Review**  
Predict [model scores]() and visualizations help you review how well your model is performing so you can determine whether you need to [retrain]() your model.
1. **Deploy**  
After you are satisfied with how the model is performing, you can confidently [deploy]() it. Your deployed model stores the [Prediction Value](https://docs.tealium.com/deployed-model-health/) in the output attribute for the model.
1. **Create**  
With your deployed model, you can use the Prediction Value to help you [create audiences]() to better target your visitors and create personalized experiences to drive ROI.


