---
title: Prerequisites
description: This article describes what is required to use the Tealium Predict ML product, suggested steps to take before you begin to ensure ideal results, and available services.
url: https://docs.tealium.com/server-side/predict/getting-started/prerequisites/
---
## Required

The following items are required to use Tealium Predict:

* **Tealium AudienceStream**  
To begin using the Tealium Predict product, you only need to have the Tealium AudienceStream CDP product with data collection enabled.
* **Data Volume Minimums**  
To ensure that you have enough data to begin building meaningful models using past data, the following data volume minimums are required:
  * **21 Days of Data Collection**  
Data collection must be active for AudienceStream for a minimum of 21 days of data collection prior to the feature release.
  * **Minimum Average Daily Visits**  
A minimum of 10,000 average daily visits during chosen training period.
  * **Target Attribute Volume Minimums**  
Your target attribute must have a minimum daily average of 200 true and 200 false visitors over a 30-day period.
  * **Dataset Timeframe**  
Dataset Training Timeframe: Your dataset training timeframe must be at least the duration of the Prediction Timeframe plus 1 additional day. For example, a "Likelihood to purchase in 30 days" model requires at least 31 days of data. For better training model accuracy, the training time frame should be 90 days regardless of the prediction timeframe selected in the UI.

## Data quality

For optimal results, Tealium suggest that you have a high-quality dataset that consists of a clean data layer with a large amount of training data. Better data layer health lets you create models that can provide immediate and meaningful prediction results.

For additional information, see [Data Readiness for Machine Learning.](https://tealium.com/resource/fundamentals/data-readiness-for-ml-checklist/)

## Professional services

Though no coding or data science knowledge is required to use the product, you can improve your results with a high quality implementation of AudienceStream.

If you would like assistance in assessing the current state of your data layer, Tealium provides professional services centered around your current AudienceStream implementation and overall data wellness.

For additional information about data readiness and data wellness services, see [Prepare your data]().
