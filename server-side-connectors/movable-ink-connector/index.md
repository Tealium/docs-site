---
title: Movable Ink Connector Setup Guide
description: This article describes how to set up the Movable Ink connector.
url: https://docs.tealium.com/server-side-connectors/movable-ink-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Movable Ink API
* API Version: v1.0
* API Endpoint: `https://collector.movableink-dmz.com/behavioral/`
* Documentation: [Movable Ink API](https://support.movableink.com/hc/en-us/articles/10252591570071)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event | ✓ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Access Token ID**: (Required) The access token ID.
* **Access Token Secret**: (Required) The access token secret.
* **Behavioral Endpoint**: (Required) The behavioral endpoint URL.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The type of the event. |
| Event Sub-type | Designates the event sub-type. |
| Timestamp | The time when the event occurred (Unix Time). If no value is provided, the connector uses the event time. |
| Timezone | The timezone of where the event took place (TZ database name in the IANA Time Zone Database). |
| User ID | The unique identifier of the profile that triggered this event. |
| Anonymous ID | A unique identifier of the anonymous profile that triggered this event. |
| Properties Meta Info | A map of metadata to provide additional context about the event. |
