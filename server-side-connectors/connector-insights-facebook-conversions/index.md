---
title: Connector Insights: Facebook Conversions
description: Access Facebook Conversions insights to review event match quality, customer parameter coverage, and offline data quality scores.
url: https://docs.tealium.com/server-side-connectors/connector-insights-facebook-conversions/
---
## Overview

The Facebook Conversions connector insights is an integration with Meta that brings the following data quality reports into Tealium:

* [Event match quality (EMQ)](#event-match-quality-emq): A report to assess the effectiveness of your Conversions API integration in matching events to Meta users.
* [Offline data quality (ODQ)](#offline-data-quality-odq): A report to assess how well your offline events align with Meta's advertising requirements.

To access connector insights:

Go to **Connect > Connectors**, find the **Facebook Conversions** connector, and select an action. On the action screen, click the **Insights** tab.

![](https://docs.tealium.com/images/server-side-connectors/connector-insights-btn.png)

The insights are based on the **Pixel ID** or **Dataset ID** of the configured connector, which is displayed on the summary screen. If the identifier is configured as a static value, it will be displayed on the summary screen and metrics will load automatically. If you use dynamic attributes, enter the required Dataset ID or Pixel ID and click **Retrieve Metrics** to fetch the insights data.


<blockquote>
If the **Pixel ID** is set dynamically as a mapped parameter in the connector action instead of in the connector configuration, the insights cannot be retrieved from Meta and the scores will not appear.
</blockquote>


## Event match quality (EMQ)

The event match quality (EMQ) insight provides a score for each conversion event type Meta receives and the match percentage for the included customer information parameters sent with each type.

### Event type summary

The event summary table shows the following:

* **Event Name**: The event type collected by Meta.
* **Event Match Quality**: The event match quality score for the event type, on a scale from 1 to 10.
* **Diagnostics**: If issues are detected, the name of the diagnostic.

The EMQ score indicates how well the customer information in those events matches existing Meta users. The diagnostic shows known issues that Meta identified with the event match quality.

Click an event to see the customer information details of the event match quality.

![](https://docs.tealium.com/images/server-side-connectors/facebook-api-insights-events.png)

### Customer information summary

The customer information summary shows the customer parameters received by Meta for an event type and the percentage of events receiving each parameter. The higher the percentage of events that contain customer information, the higher the EMQ score.

If EMQ diagnostics issues are detected, they appear here with the name of the issue.

![](https://docs.tealium.com/images/server-side-connectors/facebook-api-insights-customer-info.png)

### EMQ score

EMQ is a score from 1 to 10 that reflects how well your server events match users in Meta. Events are matched based on the customer information parameters sent with the events and scores are calculated for the Pixel ID configured in the connector. Higher scores improve conversion optimization and ad attribution.

To improve your EMQ score, include as many customer information parameters as possible and prioritize those most likely to produce a match, such as:

* Hashed email address
* Client IP address / Client user agent
* Hashed phone number

Add data mappings for these parameters and more in the [Facebook Conversions connector](https://docs.tealium.com/facebook-conversions-connector/).

Meta recommends maintaining an EMQ score of 6.0 or higher. For more information, see [Meta Business Help Center: Best Practices for Conversions API](https://www.facebook.com/business/help/308855623839366?id=818859032317965).

#### Diagnostics

If Meta detects issues with the event match quality, a diagnostic error is indicated on the customer information summary. If available, the potential score increase appears, indicating the potential improvement to the event match quality score if the issue is resolved.

For example, the detected issue might be **Always Same Match**, which indicates that Meta is receiving the same match key value for all events in a specific event type. This usually means the integration is misconfigured and is not sending any unique identifiers (such as email addresses or phone numbers) to match events to Meta. To resolve this issue, ensure you send unique match keys for this event type.

## Offline data quality (ODQ)

The offline data quality (ODQ) insight provides a composite score for offline event types and detailed data quality scores for each event type. The scores indicate how well your offline events align with Meta's advertising requirements.

### Offline event summary

The offline event summary table shows the following:

* **Event Name**: The offline event type (typically from a file import) collected by Meta.
* **Composite Score**: The overall offline event data quality score, on a scale from 1 to 10.
* **Recommendation**: If applicable, the recommendation to improve the score.

Each event type has an event match quality score ranging from 1 to 10. The score indicates how well the customer information in those events matches existing Meta users.

Click an event to see the detailed ODQ scores.

![](https://docs.tealium.com/images/server-side-connectors/fb-offline-event-quality-events-composite-score.png)

### ODQ scores

The offline event type summary shows the following specific scores for an event type:

* **Match Key Score**: A score from 1 to 10 indicating how often offline events have a strong match key, such as email address, phone number, or mobile device ID, over the last 28 days.
* **Frequency Score**: A score from 1 to 10 indicating how often offline events are received over the last 14 days. Meta recommends sending offline events daily at a minimum and hourly if possible.
* **Freshness Score**: A score from 1 to 10 indicating how current your data is over the last 28 days. Meta recommends sending offline events within 3 days from when they occur.

For each score, the **Recommendation** column shows how to improve the score.

![](https://docs.tealium.com/images/server-side-connectors/fb-offline-data-quality-details-match-frequency-freshness.png)

For more information, see [Meta Conversions API: Offline Data Quality](https://developers.facebook.com/docs/marketing-api/best-practices/omni-optimal-setup-guide#offline-data-quality--odq--score)
