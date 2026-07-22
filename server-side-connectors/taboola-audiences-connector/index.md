---
title: Taboola Audiences Connector Setup Guide
description: This article describes how to set up the Taboola Audiences connector.
url: https://docs.tealium.com/server-side-connectors/taboola-audiences-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Taboola API
* API Version: v1.0
* API Endpoint: `https://backstage.taboola.com/backstage/api/1.0`
* Documentation: [Taboola API](https://developers.taboola.com/backstage-api/reference/add-or-remove-users)

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add User to Audience (Batched) | ✓ | ✓ |
| Remove User from Audience (Batched) | ✓ | ✓ |

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).


<blockquote>
When you add this connector, you must accept the vendor's data platform policy.
</blockquote>


After adding the connector, configure the following settings:

* **Account ID**: Assigned Taboola account ID.

## Action parameters

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

The following section describes how to set up parameters and options for each action.

### Add User to Audience (Batched)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience ID | The ID of the audience to which the user will be added. Click **Verify Audience ID** to verify the **Audience ID** that you entered. To create a new audience, use the following steps:<ol><li>Click **Create Audience**.</li><li>Enter a unique audience name in the **Audience Name** field.</li><li>Enter the time that a user should remain in an audience in the **TTL in Hours** field. The default value is `8670` (one year).</li><li>To exclude the audience from new and existing campaigns, enter `True` in the **Exclude from Campaigns** field. The default value is `False`.</li><li>Click **Done**.</li></ol> |
| User ID | The User ID, as a SHA256 hashed email address or a MAID device ID.  |
| Type | The User ID type (either `DEVICE_ID` or `EMAIL_ID` ). |

### Remove User from Audience (Batched)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience ID | The ID of the audience to which the user will be added. Click **Verify Audience ID** to verify the **Audience ID** that you entered. To create a new audience, use the following steps:<ol><li>Click **Create Audience**.</li><li>Enter a unique audience name in the **Audience Name** field.</li><li>Enter the time that a user should remain in an audience in the **TTL in Hours** field. The default value is `8670` (one year).</li><li>To exclude the audience from new and existing campaigns, enter `True` in the **Exclude from Campaigns** field. The default value is `False`.</li><li>Click **Done**.</li></ol> |
| User ID | The User ID, as a SHA256 hashed email address or a MAID device ID.  |
| Type | The User ID type (either `DEVICE_ID` or `EMAIL_ID` ). |