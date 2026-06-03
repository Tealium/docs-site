---
title: Adobe Audience Manager DCS Connector Setup Guide
description: Adobe's Data Collection Servers (DCS) provides a Server-to-Server API to collect audience user data to be managed in Adobe Audience Manager. This article describes how to set up the service in your Customer Data Hub profile.
url: https://docs.tealium.com/server-side-connectors/adobe-audience-manager-dcs-connector/
---## Requirements

* Domain Alias assigned by your Adobe Audience Manager

## Supported actions

|**Action Name**| **Trigger on Audience**| **Trigger on Streams**|
|---| ---| ---|
|Send Data Collection Event| ✓| ✓|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

To configure your vendor, follow these steps:

* In the **Configure** tab, provide a title for the connector instance.

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Data Collection Event

#### Parameters

1. **Domain Alias**: (Required) Provide domain alias assigned by your Audience Manager.
1. **Region ID**: (Required) Provide region ID assigned to user sending the event. For more info see [Get User ID and Region](https://marketing.adobe.com/resources/help/en_US/aam/dcs-aam-ids.html) and [Regions and Hostname](https://marketing.adobe.com/resources/help/en_US/aam/dcs-regions.html).
1. **Event Data**: (Required) Map Attribute(s) to event parameters (see: [Supported Event Parameters](https://marketing.adobe.com/resources/help/en_US/aam/dcs-keys.html)). Options `Data Provider ID `and `Data Provider User ID`/`Integration Code` are automatically combined with `%01` separator for `d_cid` and `d_cid_ic` parameters respectively (see: [CID and CID_IC](https://marketing.adobe.com/resources/help/en_US/aam/cid.html))

For more information, see: [Making Event API Calls](https://marketing.adobe.com/resources/help/en_US/aam/dcs-s2s-calls.html)

## Vendor Documentation

* [Making Event API Calls](https://marketing.adobe.com/resources/help/en_US/aam/dcs-s2s-calls.html)
* [Get User ID and Region](https://marketing.adobe.com/resources/help/en_US/aam/dcs-aam-ids.html)
* [Regions and Hostname](https://marketing.adobe.com/resources/help/en_US/aam/dcs-regions.html)
* [Supported Event Parameters](https://marketing.adobe.com/resources/help/en_US/aam/dcs-keys.html)
* [CID and CID\_IC](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)
