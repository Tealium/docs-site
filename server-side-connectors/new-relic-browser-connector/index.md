---
title: New Relic Browser Connector Setup Guide
description: This article describes how to set up the New Relic Browser connector.
url: https://docs.tealium.com/server-side-connectors/new-relic-browser-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Browser Application Metrics| ✓| ✓|

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

### Action - Send Browser Application Metrics

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|New Relic Browser Application|  &lt;ul&gt;&lt;li&gt;Browser Application to provide metrics on. &lt;/li&gt;&lt;li&gt;Provide a custom name if the application is not yet in New Relic Insights, or it will not be created.&lt;/li&gt;&lt;li&gt;This will not create the application in the New Relic system, but will provide the ability to query the application in New Relic Insights.&lt;/li&gt;&lt;/ul&gt; |
|Event Category|  &lt;ul&gt;&lt;li&gt;Event Category&lt;/li&gt;&lt;/ul&gt; |
|New Relic Application ID|  &lt;ul&gt;&lt;li&gt;New Relic Application ID&lt;/li&gt;&lt;/ul&gt; |
|Server Side Application Name|  &lt;ul&gt;&lt;li&gt;Server Side Application Name&lt;/li&gt;&lt;/ul&gt; |
|Autonomous System Number|  &lt;ul&gt;&lt;li&gt;Autonomous System Number&lt;/li&gt;&lt;/ul&gt; |
|Autonomous System Number Latitude|  &lt;ul&gt;&lt;li&gt;Autonomous System Number Latitude&lt;/li&gt;&lt;/ul&gt; |
|Autonomous System Number Longitude|  &lt;ul&gt;&lt;li&gt;Autonomous System Number Longitude&lt;/li&gt;&lt;/ul&gt; |
|Autonomous System Number Organization|  &lt;ul&gt;&lt;li&gt;Autonomous System Number Organization&lt;/li&gt;&lt;/ul&gt; |
|Backend Response Time|  &lt;ul&gt;&lt;li&gt;Backend Response Time&lt;/li&gt;&lt;/ul&gt; |
|Transaction Name|  &lt;ul&gt;&lt;li&gt;Transaction Name&lt;/li&gt;&lt;/ul&gt; |
|City|  &lt;ul&gt;&lt;li&gt;City&lt;/li&gt;&lt;/ul&gt; |
|Time to Establish Server Connection|  &lt;ul&gt;&lt;li&gt;Time to Establish Server Connection&lt;/li&gt;&lt;/ul&gt; |
|Country Code|  &lt;ul&gt;&lt;li&gt;Country Code&lt;/li&gt;&lt;/ul&gt; |
|Device Type|  &lt;ul&gt;&lt;li&gt;Device Type&lt;/li&gt;&lt;/ul&gt; |
|Time to Resolve Top-Level DNS|  &lt;ul&gt;&lt;li&gt;Time to Resolve Top-Level DNS&lt;/li&gt;&lt;/ul&gt; |
|Time to Process Page|  &lt;ul&gt;&lt;li&gt;Time to Process Page&lt;/li&gt;&lt;/ul&gt; |
|Front-end Browser Response Time|  &lt;ul&gt;&lt;li&gt;Front-end Browser Response Time&lt;/li&gt;&lt;/ul&gt; |
|Name of Server Side Transaction|  &lt;ul&gt;&lt;li&gt;Name of Server Side Transaction&lt;/li&gt;&lt;/ul&gt; |
|Total Network Wait Time|  &lt;ul&gt;&lt;li&gt;Total Network Wait Time&lt;/li&gt;&lt;/ul&gt; |
|Time to Render Page|  &lt;ul&gt;&lt;li&gt;Time to Render Page&lt;/li&gt;&lt;/ul&gt; |
|Original PageView URL|  &lt;ul&gt;&lt;li&gt;Original PageView URL&lt;/li&gt;&lt;/ul&gt; |
|Time Waiting for Service Initiation|  &lt;ul&gt;&lt;li&gt;Time Waiting for Service Initiation&lt;/li&gt;&lt;/ul&gt; |
|Region Code|  &lt;ul&gt;&lt;li&gt;Region Code&lt;/li&gt;&lt;/ul&gt; |
|Time to Setup TLS|  &lt;ul&gt;&lt;li&gt;Time to Setup TLS&lt;/li&gt;&lt;/ul&gt; |
|Session ID|  &lt;ul&gt;&lt;li&gt;Session ID&lt;/li&gt;&lt;/ul&gt; |
|User Agent Name|  &lt;ul&gt;&lt;li&gt;User Agent Name&lt;/li&gt;&lt;/ul&gt; |
|User Agent Version|  &lt;ul&gt;&lt;li&gt;User Agent Version&lt;/li&gt;&lt;/ul&gt; |
|User Agent OS|  &lt;ul&gt;&lt;li&gt;User Agent OS&lt;/li&gt;&lt;/ul&gt; |
|Name of Interaction|  &lt;ul&gt;&lt;li&gt;Name of Interaction&lt;/li&gt;&lt;/ul&gt; |
|Name of Page Action|  &lt;ul&gt;&lt;li&gt;Name of Page Action&lt;/li&gt;&lt;/ul&gt; |
|Browser Height|  &lt;ul&gt;&lt;li&gt;Browser Height&lt;/li&gt;&lt;/ul&gt; |
|Browser Width|  &lt;ul&gt;&lt;li&gt;Browser Width&lt;/li&gt;&lt;/ul&gt; |
|Current URL|  &lt;ul&gt;&lt;li&gt;Current URL&lt;/li&gt;&lt;/ul&gt; |
|Referrer URL|  &lt;ul&gt;&lt;li&gt;Referrer URL&lt;/li&gt;&lt;/ul&gt; |
|Time between Page Requested and PageAction|  &lt;ul&gt;&lt;li&gt;Time between Page Requested and PageAction&lt;/li&gt;&lt;/ul&gt; |
