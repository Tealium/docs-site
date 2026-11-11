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

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

To configure your vendor, follow these steps:

* In the **Configure** tab, provide a title for the connector instance.

## Action settings - parameters and options

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

### Action - Send Data Collection Event

#### Parameters

1. **Domain Alias**: (Required) Provide domain alias assigned by your Audience Manager.
1. **Region ID**: (Required) Provide region ID assigned to user sending the event. For more info see [Get User ID and Region](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-url-receive) and [Regions and Hostname](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions).
1. **Event Data**: (Required) Map Attribute(s) to event parameters (see: [Supported Event Parameters](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-keys)). Options `Data Provider ID `and `Data Provider User ID`/`Integration Code` are automatically combined with `%01` separator for `d_cid` and `d_cid_ic` parameters respectively (see: [CID and CID_IC](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/reference/cid))


<blockquote>
For more information, see: [Making Event API Calls](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-event-calls)
</blockquote>


## Vendor documentation

* [Making Event API Calls](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-event-calls)
* [Get User ID and Region](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-url-receive)
* [Regions and Hostname](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions)
* [Supported Event Parameters](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-keys)
* [CID and CID\_IC](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/reference/cid)
