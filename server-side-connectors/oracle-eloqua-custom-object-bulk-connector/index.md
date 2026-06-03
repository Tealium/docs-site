---
title: Oracle Eloqua Custom Object (Bulk) Connector Setup Guide
description: This article describes how to set up the Oracle Eloqua Custom Object (Bulk) connector service in your Customer Data Hub account
url: https://docs.tealium.com/server-side-connectors/oracle-eloqua-custom-object-bulk-connector/
---## Requirements

* Oracle Eloqua account
* Company name for your Oracle Eloqua account
* Username for your Oracle Eloqua account
* Password for your Oracle Eloqua account

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 15 minutes
* Max size of requests: 30 MB

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Import Custom Objects| ✓| ✗|

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following required settings:

* Company
* Username
* Password

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Import Custom Objects

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Action Name|  &lt;ul&gt;&lt;li&gt;The name for this specific action&lt;/li&gt;&lt;/ul&gt; |
|Action Categories|  &lt;ul&gt;&lt;li&gt;Example: Email&lt;/li&gt;&lt;li&gt;These categories are presented to your users through the consent prompt and consent preferences feature.&lt;/li&gt;&lt;li&gt;Users can opt-in or opt-out of tracking based on these categories&lt;/li&gt;&lt;/ul&gt; |
|Source|  &lt;ul&gt;&lt;li&gt;Select data source&lt;/li&gt;&lt;/ul&gt; |
|Custom Object|  &lt;ul&gt;&lt;li&gt;(Required) Select custom object.&lt;/li&gt;&lt;/ul&gt; |
