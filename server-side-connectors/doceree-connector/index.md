---
title: Doceree Connector Setup Guide
description: This article describes how to set up the Doceree connector.
url: https://docs.tealium.com/server-side-connectors/doceree-connector/
---
## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| Add User NPI | ✓ | ✗ |
| Remove User NPI | ✓ | ✗ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Username**  
(Required) Username for your Doceree account.
* **Password**  
(Required) Password for your Doceree account.
* **Environment**  
(Required) Select the environment you are using at Doceree. Use **Production** unless your Tealium and/or Doceree representative tells you to use **Demo**.

To add an audience list:

1. Click **Add Audience List**.
1. Enter the Doceree account name associated with the audience.
1. Enter the audience name to create.
1. Click **Add**.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Add User NPI

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

*   Max number of requests: 1000
*   Max time since oldest request: 10 minutes
*   Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Account | The Doceree account associated with this audience. |
| Audience ID | The audience that you want to add the user to. |
| NPI | The unique identifier (NPI) for the user. |

### Action — Remove User NPI

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Account | The Doceree account associated with this audience. |
| Audience ID | The audience that you want to remove the user from. |
| NPI | The unique identifier (NPI) for the user. |