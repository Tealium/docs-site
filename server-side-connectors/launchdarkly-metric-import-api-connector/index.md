---
title: LaunchDarkly Metric Import API Connector Setup Guide
description: This article describes how to set up the LaunchDarkly Metric Import API connector.
url: https://docs.tealium.com/server-side-connectors/launchdarkly-metric-import-api-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: LaunchDarkly API
* API Version: v2
* API Endpoint: `https://events.launchdarkly.com`
* Documentation: [LaunchDarkly API](https://docs.launchdarkly.com/home/creating-experiments/import-metric-events)

## Batch Limits
This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Metrics to Experimentation Function | ✗ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Company Name**  
 (Required) Name of your company in LaunchDarkly.
* **Project Key**  
 (Required) Project key for your metric events environment. Locate the project key in LaunchDarkly account settings > Projects > Environments.
* **Environment Key**  
(Required) Environment key for the environment your metric events pertain to. Find these under Environments on the Projects tab in your LaunchDarkly [Account](https://app.launchdarkly.com/settings/members) settings page.
* **Access Token**  
(Required) The access token must have a role that allows the `importEventData` action. LaunchDarkly strongly recommends using a dedicated access token with this permission. For more information, see [Scoping Personal API Tokens](https://docs.launchdarkly.com/home/account-security/api-access-tokens#scoping-personal-api-access-tokens) and [Environment Actions](https://docs.launchdarkly.com/home/members/role-actions#environment-actions?q=import).

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Metrics to Experimentation Function

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Key | (Required) Identifies your metric. The Event Name in your LaunchDarkly metric must match this value. |
| Creation Date | Timestamp of when the event is created, in Unix milliseconds. |
| Metric Value | The value of your metric. Required for numeric metrics. Optional for conversion metrics. LaunchDarkly will ignore this value if provided for conversion metrics. |
| Context Keys | A JSON object with one or more properties that lists the context keys for each metric event context in the format: `<contextKind>: <contextKey>`. For example, if your experiment works with user contexts, you may have the following kind/key pair: `"user": "user-key-123abc"`.<br>Each context kind and key must match the kind/key pair in the corresponding context provided to LaunchDarkly SDK evaluating flags used in your experiments.<br>For more information about using context kinds, see [Randomization units](https://docs.launchdarkly.com/home/creating-experiments/allocation#randomization-units). |

