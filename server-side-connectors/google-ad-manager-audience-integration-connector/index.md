---
title: Google Ad Manager Audience Integration Connector Setup Guide
description: This article describes how to set up the Google Ad Manager Audience Integration connector.
url: https://docs.tealium.com/server-side-connectors/google-ad-manager-audience-integration-connector/
---
The Google Ad Manager Audience Integration connector allows publishers to add visitors to Google Ad Manager user lists using a Publisher Provided ID (PPID). Publishers can then serve ads based on the PPID and target new users by matching audiences similar to your most valuable customers. For more information, see [Google Ad Manager Help: About publisher provided identifiers](https://support.google.com/admanager/answer/2880055?hl=en).

## Prerequisites

* Link Tealium to Google Ad Manager using the **Linked Accounts** section in the Google Ad Manager UI.
* Generate and send a PPID client-side for logged-in users using [Google Ad Manager 360 Audience Pixel tag]() or [Google Publisher tag]().
* Set up the PPID as a Tealium attribute for use in the connector.

## API Information

This connector uses the following vendor API:

* API Name: Google Data Manager API
* API Version: v1
* API Endpoint: `https://datamanager.googleapis.com`

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add to Audience List | ✓ | ✓ |
| Remove from Audience List | ✓ | ✓ |

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Customer ID**. 
(Required) Customer ID for the account linked to Tealium in the Ad Manager UI. In Ad Manager, go to **Tools and Settings &gt; Linked Accounts** to create a link to Tealium.

## Actions

The following section lists the supported parameters for each action.

### Add to Audience List

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 1440 minutes
* Max size of requests: 50 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience List | Select an Audience List.&lt;br&gt;Note: Only lists created using the connector are available. |
| Publisher Provided ID | (Required) Must be an alphanumeric or UUID HEX value between 32 and 150 characters. |

### Remove from Audience List

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 1440 minutes
* Max size of requests: 50 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience List | Select an Audience List.&lt;br&gt;Note: Only lists created using the connector are available. |
| Publisher Provided ID | (Required) Must be an alphanumeric or UUID HEX value between 32 and 150 characters. |

## Consent

For actions like **Add to Audience List**, the connector automatically sends `adUserData` and `adPersonalization` as `GRANTED`. Implement audience logic to ensure that only visitors who have consented are added to user lists. For visitors without consent, use the **Remove from Audience List** action to remove them from user lists.

## Tips and troubleshooting

* To ensure the PPID is present, include logic in the event feed or audience setup used for the connector action. This helps avoid `MISSING_USER_IDENTIFIER` errors.