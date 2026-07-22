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

### Action - Send Browser Application Metrics

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|New Relic Browser Application|  <ul><li>Browser Application to provide metrics on. </li><li>Provide a custom name if the application is not yet in New Relic Insights, or it will not be created.</li><li>This will not create the application in the New Relic system, but will provide the ability to query the application in New Relic Insights.</li></ul> |
|Event Category|  <ul><li>Event Category</li></ul> |
|New Relic Application ID|  <ul><li>New Relic Application ID</li></ul> |
|Server Side Application Name|  <ul><li>Server Side Application Name</li></ul> |
|Autonomous System Number|  <ul><li>Autonomous System Number</li></ul> |
|Autonomous System Number Latitude|  <ul><li>Autonomous System Number Latitude</li></ul> |
|Autonomous System Number Longitude|  <ul><li>Autonomous System Number Longitude</li></ul> |
|Autonomous System Number Organization|  <ul><li>Autonomous System Number Organization</li></ul> |
|Backend Response Time|  <ul><li>Backend Response Time</li></ul> |
|Transaction Name|  <ul><li>Transaction Name</li></ul> |
|City|  <ul><li>City</li></ul> |
|Time to Establish Server Connection|  <ul><li>Time to Establish Server Connection</li></ul> |
|Country Code|  <ul><li>Country Code</li></ul> |
|Device Type|  <ul><li>Device Type</li></ul> |
|Time to Resolve Top-Level DNS|  <ul><li>Time to Resolve Top-Level DNS</li></ul> |
|Time to Process Page|  <ul><li>Time to Process Page</li></ul> |
|Front-end Browser Response Time|  <ul><li>Front-end Browser Response Time</li></ul> |
|Name of Server Side Transaction|  <ul><li>Name of Server Side Transaction</li></ul> |
|Total Network Wait Time|  <ul><li>Total Network Wait Time</li></ul> |
|Time to Render Page|  <ul><li>Time to Render Page</li></ul> |
|Original PageView URL|  <ul><li>Original PageView URL</li></ul> |
|Time Waiting for Service Initiation|  <ul><li>Time Waiting for Service Initiation</li></ul> |
|Region Code|  <ul><li>Region Code</li></ul> |
|Time to Setup TLS|  <ul><li>Time to Setup TLS</li></ul> |
|Session ID|  <ul><li>Session ID</li></ul> |
|User Agent Name|  <ul><li>User Agent Name</li></ul> |
|User Agent Version|  <ul><li>User Agent Version</li></ul> |
|User Agent OS|  <ul><li>User Agent OS</li></ul> |
|Name of Interaction|  <ul><li>Name of Interaction</li></ul> |
|Name of Page Action|  <ul><li>Name of Page Action</li></ul> |
|Browser Height|  <ul><li>Browser Height</li></ul> |
|Browser Width|  <ul><li>Browser Width</li></ul> |
|Current URL|  <ul><li>Current URL</li></ul> |
|Referrer URL|  <ul><li>Referrer URL</li></ul> |
|Time between Page Requested and PageAction|  <ul><li>Time between Page Requested and PageAction</li></ul> |
