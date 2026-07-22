---
title: FullStory API Connector Setup Guide
description: This article describes how to set up the FullStory API connector.
url: https://docs.tealium.com/server-side-connectors/fullstory-user-api-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: FullStory API
* API Version: v1.0
* API Endpoint: `https://api.fullstory.com/users/v1/`
* Documentation: [FullStory API](https://developer.fullstory.com/server/v1/users/introduction/)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Server Events | ✓ | ✓ |
| Set User Properties | ✓ | ✓ |
| Delete User | ✓ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).


After adding the connector, configure the following settings:

* **API Key**
  * (Required) The HTTP API requires an API key that you can generate from the FullStory app. The API key must have Admin or Architect level permissions. For more information, see: <a target="_blank" href="https://help.fullstory.com/hc/en-us/articles/360020624834">Where can I find my API key</a>.

## Actions

Enter the **Action Name** and select the **Action Type** from the drop-down menu.

The following sections describe how to set up parameters and options for each action.

### Server Events

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| UID | (Required) The unique user ID given to the user, which has been passed through the `FS.identify` Browser API function. |
| Event Name | (Required) The unique name of the custom event. |
| Timestamp | The time the event occurred, represented in <a target="_blank" href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601 format</a>. If not provided, the current FullStory server time is used. |
| Use Recent Session | Set to `true` if the custom event should be attached to the user’s most recent session. The most recent session must have had activity within the past 30 minutes. Cannot be used if `session_url` or `device_session` are defined. |
| ID |  |
| Priority |  |
| Source |  |
| Title |  |

### Set User Properties

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| UID | (Required) The unique user ID given to the user, which has been passed through the FS.identify Browser API function. |
| Body | The custom properties associated with the user. Clients should be allowed to map any Visitor Attribute. Property names must follow the custom field format documented <a target="_blank" href="https://help.fullstory.com/hc/en-us/articles/4446290296599-Setting-custom-API-properties">here</a>.<br> |

### Delete User

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| UID | (Required) The unique user ID given to the user, which has been passed through the FS.identify Browser API function. |

    