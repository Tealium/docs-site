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

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 15 minutes
* Max size of requests: 30 MB

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Import Custom Objects| ✓| ✗|

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

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
|Action Name|  <ul><li>The name for this specific action</li></ul> |
|Action Categories|  <ul><li>Example: Email</li><li>These categories are presented to your users through the consent prompt and consent preferences feature.</li><li>Users can opt-in or opt-out of tracking based on these categories</li></ul> |
|Source|  <ul><li>Select data source</li></ul> |
|Custom Object|  <ul><li>(Required) Select custom object.</li></ul> |
