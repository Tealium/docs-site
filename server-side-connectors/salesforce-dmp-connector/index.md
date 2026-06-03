---
title: Salesforce DMP Connector Set Up Guide
description: This article describes how to set up the Salesforce DMP connector.
url: https://docs.tealium.com/server-side-connectors/salesforce-dmp-connector/
---

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Track User Attributes| ✓| ✓|
|Add User to Streaming Segment| ✓| ✓|
|Remove User from Streaming Segment| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Track User Attributes

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Endpoint URL|  &lt;ul&gt;&lt;li&gt;(Required) Event URL provided by Salesforce DMP representative to send event data.&lt;/li&gt;&lt;li&gt;Your endpoint might look like the following: `https://beacon.krxd.net/pixel.gif?tech_browser_lang=en`&lt;/li&gt;&lt;li&gt;Contact Salesforce DMP Representative to get the event URL.&lt;/li&gt;&lt;li&gt;Reference the following [API documentation](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API) for more info.&lt;/li&gt;&lt;/ul&gt; |
|Krux Publisher uuid|  &lt;ul&gt;&lt;li&gt;Contact Salesforce DMP Representative to get the publisher `uuid`.&lt;/li&gt;&lt;li&gt;Reference the following [API documentation](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API) for more info.&lt;/li&gt;&lt;/ul&gt; |
|Krux Domain ID|  &lt;ul&gt;&lt;li&gt;Please contact Salesforce DMP Representative to get this value.&lt;/li&gt;&lt;li&gt;Reference the following [API documentation](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API) for more info.&lt;/li&gt;&lt;/ul&gt; |
|Krux Site ID|  &lt;ul&gt;&lt;li&gt;Please contact Salesforce DMP Representative to get this value.&lt;/li&gt;&lt;li&gt;Reference the following [API documentation](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API) for more info.&lt;/li&gt;&lt;/ul&gt; |
|Krux User ID|  &lt;ul&gt;&lt;li&gt;Unique User ID to track the user. For iOS, this should be the unique Advertiser ID (and not the device id).&lt;/li&gt;&lt;li&gt;Reference the following [article to learn how to retrieve the User ID.]()&lt;/li&gt;&lt;/ul&gt; |
|User Attribute|  &lt;ul&gt;&lt;li&gt;All the user attribute data that needs to be sent should be prefixed with `_kua_` prefix. Example: `_kua_{user_attribute_name}`&lt;/li&gt;&lt;li&gt;NOTE: If you want to pass more than one attribute value to a single attribute in the pixel call, make sure the values are comma-separated when passing them.&lt;/li&gt;&lt;/ul&gt; |

### Action - Add User to Streaming Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Endpoint URL|  &lt;ul&gt;&lt;li&gt;(Required) Segment URL provided by Salesforce DMP representative to deliver segment data.&lt;/li&gt;&lt;li&gt;Your endpoint might look like the following: `https://beacon.krxd.net/segment.gif`&lt;/li&gt;&lt;li&gt;Reference the following [API documentation](https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation) for more info.&lt;/li&gt;&lt;/ul&gt; |
|Segments|  &lt;ul&gt;&lt;li&gt;Comma-delimited user segment long uid list (Segment long uid is returned in response to streaming segment creation api) (segs).&lt;/li&gt;&lt;li&gt;Streaming Segments are for off-site activation only.&lt;/li&gt;&lt;li&gt;Reference the following [article to learn how to create a streaming segment using curl.](https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation)&lt;/li&gt;&lt;/ul&gt; |
|Krux Publisher uuid|  &lt;ul&gt;&lt;li&gt;Please contact Salesforce DMP Representative to get the publisher `uuid` .&lt;/li&gt;&lt;li&gt;Reference the following [API documentation](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API) for more info.&lt;/li&gt;&lt;/ul&gt; |
|Krux User ID|  &lt;ul&gt;&lt;li&gt;Unique User ID to track the user ( `_kuid` ). For iOS, this should be the unique Advertiser ID (and not the device id).&lt;/li&gt;&lt;li&gt;Either `fpuid` or `_kuid` may be provided. If `_fpuid` is provided, users will be matched based on user match lookup. Otherwise, kuid will be used and doesn&#39;t require lookup.&lt;/li&gt;&lt;li&gt;Reference the following [article to learn how to retrieve the User ID]()&lt;/li&gt;&lt;/ul&gt; |
|Krux Single First Party uid|  &lt;ul&gt;&lt;li&gt;SINGLE first party uid (`fpuid`).&lt;/li&gt;&lt;li&gt;Either `fpuid` or `_kuid` may be provided. If `_fpuid` is provided, users will be matched based on user match lookup. Otherwise, kuid will be used and doesn&#39;t require lookup.&lt;/li&gt;&lt;li&gt;Reference the following [article to learn how to retrieve the User ID]()&lt;/li&gt;&lt;li&gt;Reference the following [for more info](https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation)&lt;/li&gt;&lt;/ul&gt; |

### Action - Remove User from Streaming Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Endpoint URL|  &lt;ul&gt;&lt;li&gt;(Required) Segment URL provided by Salesforce DMP representative to deliver segment data.&lt;/li&gt;&lt;li&gt;Your endpoint might look like the following: `https://beacon.krxd.net/segment.gif`&lt;/li&gt;&lt;li&gt;Reference the following [API documentation](https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation) for more info.&lt;/li&gt;&lt;/ul&gt; |
|Segments|  &lt;ul&gt;&lt;li&gt;Comma-delimited user segment long uid list (Segment long uid is returned in response to streaming segment creation api) (segs).&lt;/li&gt;&lt;li&gt;Streaming Segments are for off-site activation only.&lt;/li&gt;&lt;li&gt;Reference the following [article to learn how to create a streaming segment using curl.](https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation)&lt;/li&gt;&lt;/ul&gt; |
|Krux Publisher uuid|  &lt;ul&gt;&lt;li&gt;Please contact Salesforce DMP Representative to get the publisher uuid.&lt;/li&gt;&lt;li&gt;Reference the following [API documentation](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API) for more info.&lt;/li&gt;&lt;/ul&gt; |
|Krux User ID|  &lt;ul&gt;&lt;li&gt;Unique User ID to track the user ( `_kuid` ). For iOS, this should be the unique Advertiser ID (and not the device id).&lt;/li&gt;&lt;li&gt;Either `fpuid` or `_kuid` may be provided. If `_fpuid` is provided, users will be matched based on user match lookup. Otherwise, `kuid` will be used and doesn&#39;t require lookup.&lt;/li&gt;&lt;li&gt;Reference the following [article to learn how to retrieve the User ID.]()&lt;/li&gt;&lt;/ul&gt; |
|Krux Single First Party uid|  &lt;ul&gt;&lt;li&gt;SINGLE first-party `uid` ( `fpuid` ).&lt;/li&gt;&lt;li&gt;Either `fpuid` or `_kuid` may be provided. If `_fpuid` is provided, users will be matched based on user match lookup. Otherwise, `kuid` will be used and doesn&#39;t require lookup.&lt;/li&gt;&lt;li&gt;Reference the following [article to learn how to retrieve the User ID.]()&lt;/li&gt;&lt;li&gt;Reference the following [for more info.](https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation)&lt;/li&gt;&lt;/ul&gt; |
