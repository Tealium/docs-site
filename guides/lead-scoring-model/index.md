---
title: How to create a lead scoring model with Marketo, Google Analytics, and AudienceStream
description: This article explains how to create a lead scoring model with Marketo, Google Analytics, and AudienceStream.
url: https://docs.tealium.com/guides/lead-scoring-model/
---## Introduction

* **Tag Vendor**  
Google Analytics (Universal) &#43; Google Measurement Protocol
* **Use Case**  
Push Lead Scoring from AudienceStream to Google Analytics
* **Key Attributes**
    * **Lead Score** ([Number]())  
    Number based on custom event interactions. This value is initialized to zero for a new visitor. It is then incremented/decremented based on that visitor&#39;s interactions with specific assets on the client&#39;s website.
    * **Visitor Value** ([String]())  
    String based on Lead Score value. This value is initialized to `Standard Visitor` for a new visitor. That visitor can then be upgraded to a `High Value Visitor` after crossing a specified Lead Score threshold. In addition, that visitor can fall back to a `Standard Visitor` if their Lead Score drops below that threshold. In this use case, there are only 2 initial values but more can be added to create more stratification between visitors.

* **Use Case**  
Trigger a `GET URL` call to Google Analytics to identify if a visitor is a `Standard Visitor` or a `High Value Visitor` based on the audience that their Lead Score puts them in. This process leverages the [Google Analytics Measurement Protocol](https://developers.google.com/analytics/devguides/collection/protocol/v1/) to submit the data.
* **Sample Scenario**  
The audiences requested to be created are tied to elements from a sample client&#39;s scoring model that is built within Marketo, their Marketing Automation platform. The Marketo scoring model gives points for each event that a visitor triggers which then increments their MQL (Marketing Qualified Lead) score in Marketo. By capturing those same events in AudienceStream to create audiences, we can then enrich Google Analytics by submitting the values to custom dimensions. These custom dimensions can then be used passively for lookback analysis of browsing behavior or actively by using them to build remarketing lists in Google Analytics and importing them into Google Ads for advertising purposes within the Google Display Network.

## Step 1: Get the Google Analytics Visitor ID (Tealium iQ)

In order for Google Analytics to properly store the hit from the Webhook, the Google Analytics Visitor ID must be provided in the [Webhook](). This is done in Tealium iQ by parsing the cookie `_ga` using a **Set Data Values extension** and storing the 2 longest numbers at the end of the cookie value into a data layer variable. Declare `_ga` as type **First Party Cookie**, and `google_visitorid` as type `UDO Variable` in your **Data Layer** tab. Then create the [Set Data Values extension]() as seen below.

See the following code and screenshot example:

```js
b[&#34;cp._ga&#34;].split(&#34;.&#34;).splice(2,2).join(&#34;.&#34;)
```

![](/images/server-side/google-analytics-visitor-id.png)

The `google_visitorid` value can then be stored as a a string.

![](/images/server-side/set-string-to-google-visitorid.png)

We will set a [Boolean]() to check if the data exists. This is important because the value stored in `google_visitorid` is required for Google Analytics to save the data received from the connector.

![](/images/server-side/set-boolean-google-visitor-id.png)

Last, we will eventually map the data to the `cid` parameter in the Webhook that we build for Google Analytics

![](/images/server-side/map-to-cid.png)

## Step 2: Capture event information (Tealium iQ)

Configure the events in Tealium iQ that will adjust the Lead Score metrics in AudienceStream. This usually involves calling `utag.link()` on specific website assets when they are clicked on or interacted with. For this step, you&#39;ll have the option to use the jQuery `onHandler()` extension or a JavaScript Code extension to capture these events. These will both submit the data Google Analytics and AudienceStream.

For this use case, we&#39;ve chosen to use the [Javascript Code extension]() and used jQuery to capture all the events. Some examples of positive events from this use case are interactions with assets like case studies, white papers, videos, webinars, and more. It also includes negative events, such as Support, which will negatively impact Lead Score by either decrementing the value or resetting it to zero.

![](/images/server-side/no-title-160ica6f830d8bd7a1ce.png)

## Step 3: Create rules and attributes (AudienceStream)

### Lead Score

Initialize **Lead Score** to zero for all new visitors. This is done by using the **Lifetime Event Count Number** and checking if it is zero.

![](/images/server-side/lead-score-lifetime.png)

For all events with positive points, increment the **Lead Score** by the value you want.

![](/images/server-side/increment-decrement-lead-score.png)

For all negative events, apply the negative credit however it fits the model. In the case of **Support**, it resets the score to zero.

![](/images/server-side/lead-score-support-user.png)

If the scoring model is still being refined (as in this use case), make sure to use small values initially so that when you end up refining the model with higher values, visitors with initial lower lead score values do not skew your audiences.

### Rules

`Lead Score &gt; 3` or `Lead Score &gt;= 3`. These will be used to assign the Visitor Value String next.

![](/images/server-side/ls-greater-equal-3.png)

### Visitor Value

For this use case, the initial critical **Lead Score** threshold is `3`. If **Lead Score** is less than `3`, then set to `Standard Visitor`. If **Lead Score** is greater or equal to `3`, then set to `High Value Visitor`.

![](/images/server-side/string-visitor-value.png)

## Step 4: Create audiences (AudienceStream)

### High Value Visitors

When **Visitor Value** is `High Value Visitor`, visitor is a member of this audience.

![](/images/server-side/high-value-audience.png)

### Standard Visitors

When **Visitor Value** is `Standard Visitor`, visitor is a member of this audience.

![](/images/server-side/standard-audience.png)

## Step 5: Configure webhook (Google Analytics and AudienceStream)

### Custom Dimensions

Create **Custom Dimensions** in Google Analytics that the [Webhook]() will populate.

![](/images/server-side/no-title-168i3748718d3d7cc6ec.png)

### Webhook Example

The following example configuration is used to trigger the data to Google Analytics.

![](/images/server-side/google-analytics-configurations.png)

### Required parameters

The following table lists the primary fields that should be populated so the data can be saved correctly in Google Analytics.

While `t` and `ni` are not required based on Google&#39;s documentation, they should be set to `event` and `1` respectively so that the Webhook does not impact bounce rate or inflate page views.

| Field              | Description                                                                                                                                                                     |
|:-------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **t**=event        | This identifies the hit type. This can be a page view or an event. It&#39;s probably best to use an event so that page views are not inflated since no page is actually being seen. |
| **cid**=12345.6789 | This is the visitor ID parsed by Tealium iQ.                                                                                                                                    |
| **tid**=UA-12345-1 | This is the Google Analytics Account Number.                                                                                                                                    |
| **v**=1            | This indicates version 1 of the Google Measurement Protocol.                                                                                                                    |
| **ni**=1           | This identifies if the hit will be a non-interaction event. By setting it to `1`, we don&#39;t affect bounce rate.                                                                  |

### Optional Parameters

The following table lists parameters that are not required, but will provide additional context in Google Analytics on how to isolate the Webhook events from other events captured by Google Analytics.

| Field                  | Description         |
|:-----------------------|:--------------------|
| **ec**=ASConnector     | Event Category Name |
| **ea**=VisitorValue    | Event Action Name   |
| **el**=StandardVisitor | Event Label Name    |
| **dp**=/webhook/       | Document path       |
| **dt**=Webhook         | Document title      |

### AudienceStream dynamic parameters

For this use case, the following values are populated from the attributes that were previously configured.

| Field                                                      | Description                                                                                                                     |
|:-----------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------|
| **cd1**=id:123-ABC-456&amp;amp;token:\_mch-site.com-123456-789 | Custom dimension 1 value. In this scenario, it is `theMarketoID`.                                                               |
| **cd2**=StandardVisitor                                    | Custom dimension 2 value. In this scenario, it is the Visitor Value which is either `Standard Visitor` or `High Value Visitor`. |

### Connectors

There will be 2 connectors configured. Each one will fire based on when a visitor joins or changes audiences from `Standard Visitor` or `High Value Visitor`.

![](/images/server-side/two-connectors.png)

Every new visitor will fire the connector on their first pageview to flag them as a `Standard Visitor`. This first connector must fire because Google Analytics does not automatically assign a `NULL` value to custom dimensions. If you need a default value in a custom dimension, it must be populated with some value. If they eventually join the `High Value Visitor` audience, a second connector will fire to upgrade them to a `High Value Visitor`. If that visitor ever leaves that audience and re-joins the `Standard Visitor` audience, the connector will fire again.

## Step 6: Act

### Example: Custom report

![](/images/server-side/no-title-171i447e852b607fbd60.png)

### Example: Remarketing list based on High Value Visitor

![](/images/server-side/no-title-172i85ee1c061f359fca.png)

Google Analytics can now be integrated with your existing Display Ad campaigns to target your visitors.
