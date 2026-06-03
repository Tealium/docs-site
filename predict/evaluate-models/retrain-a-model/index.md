---
title: Retrain a model
description: This article describes how to retrain a model after evaluating the model and determining changes that are required to improve predictions.
url: https://docs.tealium.com/predict/evaluate-models/retrain-a-model/
---
## Determine needed changes and prepare for retraining

Use the following sections as a guide to prepare your model for retraining. To edit a trained model or view included and excluded attributes, see [Review your model]().

## Retrain the model

There are three ways to retrain your model:

1. From the **Model Dashboard**, click **Retrain**.  
      ![](/images/predict/predictv2-retrain.png)
1. If a training fails, you can retrain a model from the **Model Details** screen.  
      ![](/images/predict/predictv2-model-details-retrain.png)
1. From the **Training Details** screen, after reviewing the training details you can choose to retrain.  
      ![](/images/predict/predictv2-training-details-retrain.png)

After you select to retrain your model, complete the following steps:

1. Adjust training options if needed, such as:
      * Training Date Range
      * Attributes to Exclude

1. Click **Retrain**. Your model is now _Version 2_ with a status of _Requires Publish._
1. Save and Publish your changes.  
Your model is now _Version 2_ with a status of _In Training&#34;._

## View retrained results for deployment readiness

After your new version is trained, review the results of retraining following the guildelines in [Evaluate trainded models](). Continue to refine your data and model properties if needed.

