---
title: DMD Connector Setup Guide
description: This article describes how to set up the DMD connector.
url: https://docs.tealium.com/server-side-connectors/dmd-connector/
---
DMD, an IQVIA Business, is the only provider of healthcare data that is first-party sourced, 100% opted-in, and privacy and regulatory compliant. This DMD Email Connector allows users to send campaign emails to HCP/HCOs based off of CDP actions.

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

*   Max number of requests: 100
*   Max time since oldest request: 15 minutes
*   Max size of requests: 1 MB

## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| Trigger Custom Event | ✓ | ✗ |
| Trigger Email Message | ✓ | ✗ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](/server-side/connectors/manage/) article.

After adding the connector, configure the following settings:

*   **API Username**  
Username for the Oracle Responsys account.
*   **API Password**  
Password for the specified user.
*   **Login Endpoint**  
Select the login endpoint for the authentication.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Trigger Custom Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Name | (Required) Custom Event Name. |
| Folder Name | (Required) Folder Name. |
| Object Name | (Required) Profile List Name. |
| Email Format | (Required) Email Format, either `TEXT_FORMAT` or `HTML_FORMAT`. |
| Customer ID | Customer ID. |
| Mobile Number | Mobile number, can be `NULL`. |
| Recipient ID | Recipient&#39;s RIID, value can be `NULL`. |
| Email Address | Recipient&#39;s plain text email address. |
| Email Address (already SHA256 hashed) | Recipient&#39;s SHA256-hashed Email address. |
| Email Address (apply SHA256 hash) | Recipient&#39;s email address, which will receive a SHA256 hash. |
| Email Address (already MD5 hashed) | Recipient&#39;s MD5-hashed Email address. |
| Email Address (apply MD5 hash) | Recipient&#39;s email address, which will receive an MD5 hash. |
| Number Data Mapping |   |
| Date Data Mapping |   |
| String Data Mapping |   |
| Optional Data | Optional data containing name-value pairs. |

### Action — Trigger Email Message

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Campaign Name | (Required) Name of the Campaign. |
| Email Format | (Required) Email Format. |
| Customer ID | Customer ID |
| Mobile Number | Mobile number,  can be `NULL`. |
| Recipient ID | Recipient&#39;s RIID, value can be `NULL`. |
| Email Address | Recipient&#39;s plain text email address. |
| Email Address (already SHA256 hashed) | Recipient&#39;s SHA256-hashed Email address. |
| Email Address (apply SHA256 hash) | Recipient&#39;s email address, which will receive a SHA256 hash. |
| Email Address (already MD5 hashed) | Recipient&#39;s MD5-hashed Email address. |
| Email Address (apply MD5 hash) | Recipient&#39;s email address, which will receive an MD5 hash. |
| Campaign Folder Name | (Optional) Campaign Folder Name. |
| Object Name | (Optional) Profile List Name. |
| Optional Data | Optional data containing name-value pairs. |