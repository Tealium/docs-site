---
title: Connector Insights: Facebook Custom Audiences
description: Insights brings additional connector data from the vendor into your Tealium account to help you evaluate its performance.
url: https://docs.tealium.com/server-side-connectors/connector-insights-facebook-custom-audiences/
---
The Facebook Custom Audiences insight is an integration with the Facebook Audiences connector that brings custom audience data from Facebook into your account. This article shows you how to access the feature and explore the data.

## Overview of Connector Insights

The insight for the Facebook Audiences connector provides a summary of the custom audience data received by Facebook. These insights are presented in a summary of the parameters and their values.

## Custom Audience Parameters

The parameter summary shows the custom audience data received by Facebook from the connector for one audience. The parameter summary displays the **Custom Audience Name/ID**, each custom audience parameter collected by Facebook, and value for each parameter.

![](/images/server-side-connectors/2022-03-28-09-56-45.png)

## Using Connector Insights

To access Connector Insights, navigate to **AudienceStream &amp;gt; Audience Connectors**, find the Facebook Audience connector, and click **Insights**.&lt;br&gt;

![](/images/server-side-connectors/connector-insights-btn.png)

## Understanding Facebook Custom Audiences Insights

The Facebook Custom Audiences insight uses the [Facebook Graph API for Audiences](https://developers.facebook.com/docs/marketing-api/reference/custom-audience/) to provide information about your configured audience.

|**Parameter**| **Description**|
|----|----|
|Creation Time| The time the audience was created.|
|Audience Status| Utilises the `operational_status` field that represents the status of the last operation performed on an audience. For more information about possible states, see the [Facebook Graph API](https://developers.facebook.com/docs/marketing-api/reference/custom-audience/) documentation.|
|Audience Count Lower Limit| Lower bound of the approximate number of people in this audience. |
|Audience Count Upper Limit| Upper bound of the approximate number of people in this audience. |

## Additional Resources

* [Facebook Graph API](https://developers.facebook.com/docs/marketing-api/reference/custom-audience/)
* [Facebook Audiences Connector Setup Guide](/server-side-connectors/facebook-audiences-connector/)
