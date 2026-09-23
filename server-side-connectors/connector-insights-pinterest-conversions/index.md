---
title: Connector Insights: Pinterest Conversions
description: Monitor Pinterest Conversion Event Quality Score (EQS) data, including conversion status, coverage percentages, and detected issues.
url: https://docs.tealium.com/server-side-connectors/connector-insights-pinterest-conversions/
---
Connector Insights for the Pinterest Conversions connector helps you monitor the quality of conversion events sent to Pinterest. Use it to review EQS status, source platform data, component coverage and overlap, and issues detected by Pinterest.

## Access

Go to **Connect > Connectors**, find the **Pinterest Conversions** connector, and click the **Insights** tab.

## Source platform tabs

The **Source Platform** field shows tabs for each platform returned by the EQS API. Select a tab to filter the panel for that platform. Possible values include:

* **MOBILE**: Conversion events from mobile sources.
* **OFFLINE**: Conversion events from offline sources.
* **WEB**: Conversion events from web sources.

When the API returns one source platform, the panel displays the platform name with the other metadata instead of tabs.

## Status indicator

The panel displays the overall conversion status with a color-coded dot:

* **Green:** The status is `GOOD`.
* **Orange:** The status is `FAIR` or `NEEDS_IMPROVEMENT`.
* **Red:** The status has any other value.

## Metadata

The panel shows the following fields:

* **Ingestion Source**: The method used to send conversion event data to Pinterest, such as `CONVERSIONS_API`, `TAG`, or `MMP`.
* **Lookback Period**: The time window Pinterest uses to evaluate conversion data.

## Event summary

The event summary table shows one row for each event type.

The table shows the following columns:

* **Event Name**: The name of the conversion event.
* **Components**: The number of components evaluated for the event.
* **Diagnostics**: Indicates whether the EQS API detected issues for the event.

Click a row to open the component details.

## Component details

The slideout shows one section for each component in the selected event.

### Coverage and overlap

Each component section displays a **Coverage** progress bar showing the percentage of events that include the component. When overlap data is available, an **Overlap** progress bar also appears.

### Issues

When the EQS API detects issues for a component, an issues table appears with the following columns:

* **ID**: The unique identifier for the issue.
* **Name**: A short label for the issue.
* **Reason**: A description of the detected problem.

For more information about Pinterest EQS and how to improve your conversion quality, see [Pinterest: Event Quality Score](https://help.pinterest.com/en/business/article/eqs).
