---
title: Prepare your data
description: This article describes data wellness concepts and actionable steps you can take to examine and optimize the readiness of your data layer before starting with Tealium Predict ML.
url: https://docs.tealium.com/server-side/predict/strategy/prepare-your-data/
---
## Data wellness concepts

This section defines basic data wellness concepts you can use to examine, audit, and optimize to improve the overall wellness of your data. The goal is to ensure that you start with a trusted data foundation. As data maturity levels differ between businesses based on a number of factors, it is important to review and consider each of the following concepts.

After reviewing and understanding the concepts, advance to the following data readiness steps:

![](/images/predict/data-readiness.png)

* **Strategy**&lt;br&gt;
Define your business goals and your strategy. Define what do want to accomplish with machine learning technology, identify your audiences, and decide what data you want to capture and act on.

* **Data Completeness**&lt;br&gt;
Examine the volume and completeness of your data. As always, better data produces better outcomes.

* **Governance and Consent**&lt;br&gt;
Review and understand compliance practices and requirements regarding data usage.

* **Accessibility**&lt;br&gt;
Ensure that the insights you identify are accessible to other tools within your &#34;tech stack&#34;.

* **Data Integrity**  
Review your Tealium AudienceStream CDP implementation and compare the results of your data to the of data you want to collect, capture, and act on.

To learn more about data readiness and review the wellness checklist, see the [Data Readiness for Machine Learning Checklist.](https://tealium.com/resource/fundamentals/data-readiness-for-ml-checklist/)

### Data wellness services

If you need help getting started, we offer a &#34;Data Wellness&#34; services package to assist in getting your data ready to use with Tealium Predict. To learn how you can benefit from this service according to your unique data, contact your account representative.

## Data readiness actions

The following steps describe actions you and your teams can take to get your data foundation ready to add Tealium Predict. Use these steps as a general guideline to take the recommended actions to ensure optimal outcome from your Machine Learning models.

1. **Audit**  
Audit your data layer and AudienceStream attributes. Examine your data quality, volume, and maturity and make any adjustments as needed to improve the quality and integrity of your customer data.
1. **Define and Integrate**  
Define your digital data strategy and integrate. Your data foundation and infrastructure is vendor-neutral and can be used to power your entire &#34;tech stack&#34; without dependencies on any one vendor.
1. **Data Governance Practices**  
Review, define, and implement your data governance practices. As compliance is ever-evolving, ensure that compliance issues are revisited on a regular basis to ensure the long-term health and viability of your data.
1. **Understand and Enrich**  
At this point, your event data infrastructure has not yet acquired machine learning intelligence. Enrich and organize your incoming event data to improve the quality of the insights automatically produced by AudienceStream. This step enables you to immediately activate machine learning insights across your entire implementation, regardless of whether or not other components of your implementation have machine learning capabilities.
1. **Orchestrate**  
After defining your infrastructure and after your data insights are built into the way your business collects data, you can orchestrate these insights to drive action in any integrated tool of implementation. You can additionally implement your own business rules that automate data insights to flow across all your customer engagement channels in real-time

## Best practices

For optimal results, we recommend training using a prediction timeframe that contains 90 or more days of data. In many circumstances, and depending on your target use case, you can successfully train models using a smaller date range and less data. As a minimum, you must train a model on at least as many days as your prediction timeframe.
