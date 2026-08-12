---
title: FullStory API connector setup guide
description: Set up the FullStory API connector to create, update, or delete users in FullStory.
url: https://docs.tealium.com/server-side-connectors/fullstory-user-api-connector/
---
## API information

This connector uses the following vendor API:

* API Name: FullStory API
* API Version: v2
* API Endpoint: `https://api.fullstory.com/v2/users`
* Documentation: [FullStory API](https://developer.fullstory.com/server/getting-started/)

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Create or Update User | ✓ | ✓ |
| Delete User | ✓ | ✓ |

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **API Key**
  * (Required) The HTTP API requires an API key that you can generate from the FullStory app. The API key must have Admin or Architect level permissions. For more information, see [FullStory: Where can I find my API key](https://help.fullstory.com/hc/en-us/articles/360020624834).

## Actions

### Create or Update User

#### Parameters

Required parameters:

| **Parameter** | **Description** |
| --- | --- |
| UID | The unique ID you've given to the user. The ID passed through the [FS.identify](https://developer.fullstory.com/identify) Browser API function. |
| Display Name | A human-friendly name to display for the user in FullStory. |
| Email | The user's email address. |
| Properties | The custom properties associated with the user. You can map any visitor attribute. Values are sent as their native types. The connector infers the FullStory property type from the mapped attribute. For more information, see [FullStory: Custom Properties](https://developer.fullstory.com/server/custom-properties/). |

### Delete User

#### Parameters

Required parameters:

| **Parameter** | **Description** |
| --- | --- |
| UID | The unique ID you've given to the user. The ID passed through the [FS.identify](https://developer.fullstory.com/identify) Browser API function. |
