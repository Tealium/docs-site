---
title: Connector Insights: Snapchat Conversions
description: This article describes how to access connector insights and explore insights data for the Snapchat Conversions connector.
url: https://docs.tealium.com/server-side-connectors/connector-insights-snapchat-conversions/
---
## Overview

The Snapchat Conversions connector insights surface Snapchat Signal Readiness data directly in Tealium, such as event quality scores and recommendations.

To access connector insights:

Go to **Connect > Connectors**, find the **Snapchat Conversions** connector, and select an action. On the action screen, click the **Insights** tab.

The insights are based on the **Snap App ID** or **Pixel ID** of the configured connector. If the identifier is configured as a static value, metrics load automatically. If you use dynamic attributes, enter the required Snap App ID or Pixel ID and click **Retrieve Metrics** to fetch the insights data.

If **Snap App ID**, **Pixel ID**, or **Locale Code** is set dynamically as a mapped parameter in the connector action, use the override fields in the Insights screen to enter the values manually.

To override **Locale Code** in the Insights screen, select a locale from the dropdown list or enter a custom locale in `xx-YY` format (2-letter language code, dash, 2-letter country code). The default is `en-US`.

## Event summary

The event summary table shows one row per event type and the number of issues reported for each source.

The table shows the following columns:

* **Event Name**: The event type collected by Snapchat.
* **Issues SDK**: The count of issues for the SDK source, grouped by priority level (P0, P1, P2).
* **Issues API**: The count of issues for the API source, grouped by priority level (P0, P1, P2).

When the same event type has both SDK and API sources, a single row is shown with issue counts in each column.

Click an event to view the Signal Readiness Score.

## Signal Readiness Score

The Signal Readiness Score screen shows the action source and event source for the event, followed by the recommendations and the score.

* **Action Source**: The action source associated with the event (for example, `WEB`).
* **Event Source**: The event source or sources associated with the event (for example, `SDK`, `API`).

### Recommendations

When an event type has both SDK and API sources, the recommendations are grouped into two sections: **SDK Recommendations** and **API Recommendations**.

Each section shows the number of recommendations and a table with the following columns:

| Column | Description |
| --- | --- |
| Recommendation | A brief description of the signal quality issue. |
| Code | The recommendation code (for example, `PII_COVERAGE_SDK`). |
| Description | A detailed explanation of the issue and its impact on signal quality. |
| Priority | The priority level: `P0`, `P1`, or `P2`. |
| Score | The signal readiness score for this recommendation: `GOOD`, `OKAY`, or `BAD`. |

If no data is available for a source, the section displays a message indicating there is no data for that event source.

### Score

The Signal Readiness Score reflects how well the event data that Snapchat receives meets Snapchat signal quality requirements. Each recommendation is assigned a priority level and a score:

* **Priority**: P0 (highest impact), P1, or P2. Implementing higher-priority recommendations typically produces the greatest improvement to signal quality.
* **Score**: `GOOD`, `OKAY`, or `BAD`. The score indicates how the current state of the signal compares to Snapchat's quality standards.

For more information, see [Snapchat: Signal Readiness API](https://developers.snap.com/api/marketing-api/Ads-API/signal-readiness-api).
