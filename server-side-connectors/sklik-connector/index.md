---
title: Sklik Connector Setup Guide
description: This article describes how to set up the Sklik connector.
url: https://docs.tealium.com/server-side-connectors/sklik-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Sklik API
* API Version: 5
* API Endpoint: `https://api.sklik.cz`
* Documentation: [Sklik API](https://api.sklik.cz/drak/changelog.html)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **API Key**  
  * (Required) Provide the access key. You can generate one at https://www.sklik.cz/settings.
* **User ID**  
  * (Optional) The managed user ID.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add email to list | ✓ | ✓ |
| Add email to list (batch) | ✓ | ✓ |
| Remove email from list | ✓ | ✓ |
| Remove email from list (batch) | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Add email to list

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Retargeting List Id | The ID of the email retargeting list to which the emails will be added. |
| Emails | The emails to add to the selected email retargeting list. |

#### Optional parameters

| **Parameter** | **Description** |
| --- | --- |
| User Emails (Already Hashed) | Select this checkbox if the emails are already hashed. |
| User Email (Apply SHA256 Hash) | Select this checkbox if you want Tealium to sha256 hash the emails before sending them. |

### Add email to list (batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 10,000
* Maximum time since oldest request: 15 minutes

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Retargeting List Id | The ID of the email retargeting list to which the emails will be added. |
| Emails | The emails to add to the selected email retargeting list. |

#### Optional parameters

| **Parameter** | **Description** |
| --- | --- |
| User Emails (Already Hashed) | Select this checkbox if the emails are already hashed. |
| User Email (Apply SHA256 Hash) | Select this checkbox if you want Tealium to sha256 hash the emails before sending them. |

### Remove email from list

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Retargeting List Id | The ID of the email retargeting list from which the emails will be removed. |
| Emails | The emails to remove from the selected email retargeting list. |

#### Optional parameters

| **Parameter** | **Description** |
| --- | --- |
| User Emails (Already Hashed) | Select this checkbox if the emails are already hashed. |
| User Email (Apply SHA256 Hash) | Select this checkbox if you want Tealium to sha256 hash the emails before sending them. |

### Remove email from list (batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10,000
* Max time since oldest request: 15 minutes

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Retargeting List Id | The ID of the email retargeting list from which the emails will be removed. |
| Emails | The emails to remove from the selected email retargeting list. |

#### Optional parameters

| **Parameter** | **Description** |
| --- | --- |
| User Emails (Already Hashed) | Select this checkbox if the emails are already hashed. |
| User Email (Apply SHA256 Hash) | Select this checkbox if you want Tealium to sha256 hash the emails before sending them. |