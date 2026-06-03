---
title: VKontakte Ads Connector Setup Guide
description: This article describes how to set up the VKontakte Ads connector.
url: https://docs.tealium.com/server-side-connectors/vkontakte-ads-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: VKontakte Ads API
* API Version: v5.199
* API Endpoint: `https://ads.vk.com/api`
* Documentation: [VKontakte Ads API](https://ads.vk.com/doc/api/resource/RemarketingUsersLists#POST)

## Batch Limits
  
This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 4,999,990
* Max time since oldest request: 1440 minutes
* Max size of requests: 128 MB

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event | ✗ | ✓ |
| Add user to audience (Batch) | ✓ | ✗ |
| Delete user from audience (Batch) | ✓ | ✗ |

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Client ID**  
Your VKontakte application ID.
* **Client Secret**  
Your VKontakte application secret key.

## Actions

The following section lists the supported parameters for each action.

### Send Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Goal Name | VKontakte JavaScript event goal name. |

#### Event Parameters

| **Parameter** | **Description** |
| --- | --- |
| ID | (Required) VKontakte pixel ID. |
| Click ID | Click ID. |
| User ID | Unique user ID. |

#### Headers

| **Parameter** | **Description** |
| --- | --- |
| Origin | Origin header. |
| Referer | Referer header. |
| User-Agent | User-Agent header. |

### Add user to audience (Batch)


#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User ID | User ID to include in the audience. |
| Audience | Select the audience you want to add users to from the drop-down menu. |
| DMP ID | Partner DMP code. Required only if **Audience** is set to `dmp_id`, otherwise **DMP ID** will be ignored. |
| MD5 hash values | Select if you want the User ID attribute to be MD5 hashed. |

### Delete user from audience (Batch)


#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User ID | User ID to exclude from the audience. |
| Audience | Select the audience from which you want to delete users from the drop-down menu. |
| DMP ID | Partner DMP code. Required only if **Audience** is set to `dmp_id`, otherwise **DMP ID** will be ignored |
| MD5 hash values | Select if you want the User ID attribute to be MD5 hashed. |

    
