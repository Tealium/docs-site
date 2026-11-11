---
title: Criteo Audiences Connector Setup Guide
description: This article describes how to set up the Criteo Audiences connector.
url: https://docs.tealium.com/server-side-connectors/criteo-audiences-connector/
---

<blockquote>
We reccomend that you use the [Criteo Audiences (OAuth) connector](https://docs.tealium.com/criteo-audiences-oauth-connector/) to send visitor data to Criteo. The OAuth connector uses your Criteo account credentials and the Authorization Code flow for improved security, privacy, and easier account management.
</blockquote>


## Connector actions

| Action name | Visitor profile | Event data |
| --- | :---: | :---: |
|Add User to Audience| ✓| ✓|
|Remove User from Audience| ✓| ✓|

### API information

This connector uses the following vendor API:

* API Name: Criteo API
* API Version: 2026-01
* API Endpoint: `https://api.criteo.com/2025-07/audiences`
* Documentation: [Criteo: Audiences API](https://developers.criteo.com/marketing-solutions/docs/audiences)

### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50000
* Max time since oldest request: 15 minutes
* Max size of requests: 10 MB

## Configure settings

### Request Consent Link from Criteo

If you intend to use this connector, send an email to [asintegrations@tealium.com](mailto:asintegrations@tealium.com) to receive a consent link that authorizes the Tealium Customer Data Hub to manage audiences on behalf of advertisers. For more information, see [Criteo Developers: Send an Authorization Request to Your Users](https://developers.criteo.com/marketing-solutions/docs/authorization-requests).


<blockquote>
This step may take up to three working days for approval.
</blockquote>


After receiving the Criteo activation link, complete the following steps:

1. Click the activation link provided.  
The **Criteo Consent Portal** appears.
1. Grant the requested authorization levels for the account.

### Add Connector and Configure Settings

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Advertiser ID (Required)**  
Configure the **Advertiser ID** associated with an integration in your Criteo account.

## Action Settings - Parameters and Options

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

### Action - Add User to Audience

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience|  Select an audience or enter the Audience ID to add the user to. |
| Identifier | Map a user identifier value. <ul><li>**Email**: Send email value as-is without applying built-in hashing. Select this option if the value requires no hashing or is already hashed.</li><li>**Email (apply MD5 hash)**: Hash email value with MD5 before sending.</li><li>**Email (apply MD5 SHA256 hash)**: Hash email value with MD5 and then SHA256 before sending.</li><li>**Mobile ID**: IDFA mobile ID for Apple, ADID mobile ID for Android.</li><li>**Identity Link**: Identity Link</li><li>**Gum ID**: Identifier obtained from cookie matching. A corresponding Gum Caller ID is automatically added to the request.</li></ul> |
| Gum Caller ID | Gum Caller `ID` - Value used by Criteo for `GUM` (Generative Unified Media) salting. If using the Tag Management Criteo Cookie Matching Service tag, leave this unmapped. |

### Action - Remove User from Audience

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience|  Select an audience or enter the Audience ID to remove the user from. |
| Identifier | Map a user identifier value. <ul><li>**Email**: Send email value as-is without applying built-in hashing. Select this option if the value requires no hashing or is already hashed.</li><li>**Email (apply MD5 hash)**: Hash email value with MD5 before sending.</li><li>**Email (apply MD5 SHA256 hash)**: Hash email value with MD5 and then SHA256 before sending.</li><li>**Mobile ID**: IDFA mobile ID for Apple, ADID mobile ID for Android.</li><li>**Identity Link**: Identity Link</li><li>**Gum ID**: Identifier obtained from cookie matching. A corresponding Gum Caller ID is automatically added to the request.</li></ul> |
| Gum Caller ID | Gum Caller `ID` - Value used by Criteo for `GUM` salting. If using the Tag Management Criteo Cookie Matching Service tag, leave this unmapped. |
