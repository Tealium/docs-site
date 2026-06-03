---
title: StackAdapt Events Connector Setup Guide
description: This article describes how to set up the StackAdapt Events connector.
url: https://docs.tealium.com/server-side-connectors/stackadapt-events-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: StackAdapt API
* API Endpoint: `https://tags.srv.stackadapt.com`
* Documentation: [StackAdapt API](https://docs.stackadapt.com)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **Pixel ID**  
StackAdapt Universal Pixel ID.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event arguments | A `JSON` object specifying the event action. It can be used for pixel rule matching or data passback. Data passback is the process of sending supplementary data to StackAdapt, such as campaign revenue and order IDs. |
| Page Title | The page title. |
| URL | The `URL` of the target website. |
| User Agent | The web browser user agent of the user who triggered the event that is being sent to the pixel server. It is required for the user profile. |
| User IP | The `IP` address of the user who triggered the event that is being sent to the pixel server. |
| Template Variables | Provide template variables as data input for templates. For more information, see [Template Variables Guide](). Name nested template variables with the dot notation. For example, `items.name`. Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in either URL, URL parameter, header, or body data. For more information, see . Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request. |