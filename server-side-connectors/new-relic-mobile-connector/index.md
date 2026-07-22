---
title: New Relic Mobile Connector Setup Guide
description: This article describes how to set up the New Relic Mobile connector.
url: https://docs.tealium.com/server-side-connectors/new-relic-mobile-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Mobile Application Metrics| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **New Relic Account ID**
  * See [How to Register a New Relic Insights API Key](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/) for information about how to retrieve a New Relic account ID.

* **New Relic REST API Key**
  * The REST API key is used to get information on available metrics, applications, and other account information.
  * See [How to Register a New Relic Insights API Key](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/) for information about how to retrieve a New Relic REST API Key.

* **New Relic Insights API Key**
  * The Insights API key is used to insert data into New Relic Insights.
  * See [How to Register a New Relic Insights API Key](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/) for information about how to retrieve a New Relic Insights API Key.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Mobile Application Metrics

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Mobile Application|  <ul><li>Browser Application to provide metrics on. </li><li>Provide a custom name if the application is not yet in New Relic Insights, or it will not be created.</li><li>This will not create the application in the New Relic system, but will provide the ability to query the application in New Relic Insights.</li></ul> |
|Event Category|  <ul><li>Event Category</li></ul> |
|Event Type|  <ul><li>(Optional) The type of event this data will be saved under.</li><li>The default value is **Mobile Event**</li></ul> |
|Application Build Number|  <ul><li>Application Build Number</li></ul> |
|New Relic Agent Version Number|  <ul><li>New Relic Agent Version Number</li></ul> |
|City App is Located|  <ul><li>City App is Located</li></ul> |
|Country App is Located|  <ul><li>Country App is Located</li></ul> |
|Region App is Located|  <ul><li>Region App is Located</li></ul> |
|Device Category|  <ul><li>Device Category</li></ul> |
|Device Manufacturer|  <ul><li>Device Manufacturer</li></ul> |
|Device Model Number|  <ul><li>Device Model Number</li></ul> |
|Interaction Duration|  <ul><li>Interaction Duration</li></ul> |
|Fresh App Install|  <ul><li>Fresh App Install</li></ul> |
|Last Application Interaction|  <ul><li>Last Application Interaction</li></ul> |
|Application Memory Usage|  <ul><li>Application Memory Usage</li></ul> |
|User Session Duration|  <ul><li>User Session Duration</li></ul> |
|User Session ID|  <ul><li>User Session ID</li></ul> |
|Time Since Last Interaction|  <ul><li>Time Since Last Interaction</li></ul> |
|Time Since Load|  <ul><li>Time Since Load</li></ul> |
|Upgrade from Version|  <ul><li>Upgrade from Version</li></ul> |
|New Relic Agent Version Number|  <ul><li>New Relic Agent Version Number</li></ul> |
|Name of Interaction|  <ul><li>Name of Interaction</li></ul> |
