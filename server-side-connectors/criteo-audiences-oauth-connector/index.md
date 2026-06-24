---
title: Criteo Audiences (OAuth) Connector Setup Guide
description: This article describes how to set up the Criteo Audiences (OAuth) connector.
url: https://docs.tealium.com/server-side-connectors/criteo-audiences-oauth-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Criteo API
* API Version: 2026-01
* API Endpoint: `https://api.criteo.com/2025-07/marketing-solutions`
* Documentation: [Criteo Audiences API](https://developers.criteo.com/marketing-solutions/docs/audiences)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following three thresholds is met:

* Max number of requests: 50,000
* Max time since oldest request: 120 minutes
* Max size of requests: 10 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **Advertiser ID**
  * Enter the advertiser ID associated with your Criteo account integration.

Click **Establish Connection** and follow the on-screen instructions to connect to Criteo. To test your connection, click **Test Connection**.

### Create an audience in Criteo

To create a new audience in Criteo, use the following steps:

1. Click **Create Audience**.
1. Enter the **New Audience Name**.
1. Enter the **New Audience Description**.
1. Click **Create**.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add User to Audience | ✓ | ✓ |
| Remove User from Audience | ✓ | ✓ |

Enter a name for the action and select the **Action Type**.

The following section describes how to set up parameters and options for each action.

### Add User to Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience | Select the audience to add the user to, or provide the audience ID. |

#### Identifier

Map a user identifier value.

| **Parameter** | **Description** |
| --- | --- |
| Email | Send email value without applying built-in hashing. Select this option if the value requires no hashing or is already hashed. |
| Email (apply MD5 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using MD5 hash. |
| Email (apply MD5 SHA256 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using MD5 and then SHA256 hash. |
| Mobile ID | IDFA mobile ID for Apple, ADID mobile ID for Android. |
| Identity Link | Identity link. |
| Gum ID | Identifier obtained from cookie matching. A corresponding Gum Caller ID is automatically added to the request. |
| Gum Caller ID | Value used by Criteo for GUM salting. Leave unmapped if using the Criteo Cookie Matching Service tag. |

#### Batch Configuration

| **Parameter** | **Description** |
| --- | --- |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between 5 and 120. The default value is 30 minutes. |
| Batch Record Count | Batch record count should be between 1000 and 50000. The default value is 50000. |

### Remove User from Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience | Select the audience to remove the user from. |

#### Identifier

Map a user identifier value.

| **Parameter** | **Description** |
| --- | --- |
| Email | Send email value without applying built-in hashing. Select this option if the value requires no hashing or is already hashed. |
| Email (apply MD5 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using MD5 hash. |
| Email (apply MD5 SHA256 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using MD5 and then SHA256 hash. |
| Mobile ID | IDFA mobile ID for Apple, ADID mobile ID for Android. |
| Identity Link | Identity link. |
| Gum ID | Identifier obtained from cookie matching. A corresponding Gum Caller ID is automatically added to the request. |
| Gum Caller ID | Value used by Criteo for GUM salting. Leave unmapped if using the Criteo Cookie Matching Service tag. |

#### Batch Configuration

| **Parameter** | **Description** |
| --- | --- |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between 5 and 120. The default value is 30 minutes. |
| Batch Record Count | Batch record count should be between 1000 and 50000. The default value is 50000. |