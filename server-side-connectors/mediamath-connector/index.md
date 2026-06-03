---
title: MediaMath Connector Setup Guide
description: This article describes how to set up the MediaMath connector.
url: https://docs.tealium.com/server-side-connectors/mediamath-connector/
---## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Custom Data| ✓| ✗|

## API information

This connector uses the following vendor API:

* API Name: MediaMath Ingest API
* API Version: v1
* API Endpoint: `https://ingest-default.prod.octane.mediamath.com`


## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](/server-side/connectors/manage/) article.

After selecting your audience and trigger, click **Continue** and then **Add Connector**. Enter a name for the connector and configure the following settings:

* **MediaMath** **Advertiser ID**  
(Required) Your MediaMath Advertiser ID.

Click **Done** when you are finished configuring the connector.

## Action settings — parameters and options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

You can map Tealium attributes to MediaMath custom attributes to pass data as key-value pairs. Custom attributes need to be created and whitelisted in MediaMath prior to sending.

### Action — Send Custom Data

#### Parameters

|**PARAMETER**| **DESCRIPTION**|
|---| ---|
|Mapping ID| (Required) The Mapping ID, supplied by MediaMath.|
|MediaMath User ID| (Required) The MediaMath identifier of the visitor. Implement the [MediaMath Cookie Matching tag]() to have the MediaMath Unique User ID (UUID) of the visitor sent to Tealium EventStream API Hub as `mediamathid`.|
|Pixel ID| (Required) The configured Pixel ID, supplied by MediaMath.|
