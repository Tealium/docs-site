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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

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
|Mobile Application|  &lt;ul&gt;&lt;li&gt;Browser Application to provide metrics on. &lt;/li&gt;&lt;li&gt;Provide a custom name if the application is not yet in New Relic Insights, or it will not be created.&lt;/li&gt;&lt;li&gt;This will not create the application in the New Relic system, but will provide the ability to query the application in New Relic Insights.&lt;/li&gt;&lt;/ul&gt; |
|Event Category|  &lt;ul&gt;&lt;li&gt;Event Category&lt;/li&gt;&lt;/ul&gt; |
|Event Type|  &lt;ul&gt;&lt;li&gt;(Optional) The type of event this data will be saved under.&lt;/li&gt;&lt;li&gt;The default value is **Mobile Event**&lt;/li&gt;&lt;/ul&gt; |
|Application Build Number|  &lt;ul&gt;&lt;li&gt;Application Build Number&lt;/li&gt;&lt;/ul&gt; |
|New Relic Agent Version Number|  &lt;ul&gt;&lt;li&gt;New Relic Agent Version Number&lt;/li&gt;&lt;/ul&gt; |
|City App is Located|  &lt;ul&gt;&lt;li&gt;City App is Located&lt;/li&gt;&lt;/ul&gt; |
|Country App is Located|  &lt;ul&gt;&lt;li&gt;Country App is Located&lt;/li&gt;&lt;/ul&gt; |
|Region App is Located|  &lt;ul&gt;&lt;li&gt;Region App is Located&lt;/li&gt;&lt;/ul&gt; |
|Device Category|  &lt;ul&gt;&lt;li&gt;Device Category&lt;/li&gt;&lt;/ul&gt; |
|Device Manufacturer|  &lt;ul&gt;&lt;li&gt;Device Manufacturer&lt;/li&gt;&lt;/ul&gt; |
|Device Model Number|  &lt;ul&gt;&lt;li&gt;Device Model Number&lt;/li&gt;&lt;/ul&gt; |
|Interaction Duration|  &lt;ul&gt;&lt;li&gt;Interaction Duration&lt;/li&gt;&lt;/ul&gt; |
|Fresh App Install|  &lt;ul&gt;&lt;li&gt;Fresh App Install&lt;/li&gt;&lt;/ul&gt; |
|Last Application Interaction|  &lt;ul&gt;&lt;li&gt;Last Application Interaction&lt;/li&gt;&lt;/ul&gt; |
|Application Memory Usage|  &lt;ul&gt;&lt;li&gt;Application Memory Usage&lt;/li&gt;&lt;/ul&gt; |
|User Session Duration|  &lt;ul&gt;&lt;li&gt;User Session Duration&lt;/li&gt;&lt;/ul&gt; |
|User Session ID|  &lt;ul&gt;&lt;li&gt;User Session ID&lt;/li&gt;&lt;/ul&gt; |
|Time Since Last Interaction|  &lt;ul&gt;&lt;li&gt;Time Since Last Interaction&lt;/li&gt;&lt;/ul&gt; |
|Time Since Load|  &lt;ul&gt;&lt;li&gt;Time Since Load&lt;/li&gt;&lt;/ul&gt; |
|Upgrade from Version|  &lt;ul&gt;&lt;li&gt;Upgrade from Version&lt;/li&gt;&lt;/ul&gt; |
|New Relic Agent Version Number|  &lt;ul&gt;&lt;li&gt;New Relic Agent Version Number&lt;/li&gt;&lt;/ul&gt; |
|Name of Interaction|  &lt;ul&gt;&lt;li&gt;Name of Interaction&lt;/li&gt;&lt;/ul&gt; |
