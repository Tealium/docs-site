---
title: Mocean Connector Setup Guide
description: This article describes how to set up the Mocean connector.
url: https://docs.tealium.com/server-side-connectors/mocean-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send SMS| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**: Your account API key. For more information, see: [Mocean Authentication](https://moceanapi.com/docs/?shell#authentication&amp;quot;&amp;gt;https://moceanapi.com/docs/?shell#authentication)
* **API Secret**: Your account API secret.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send SMS

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|From|  &lt;ul&gt;&lt;li&gt;SMS Sender ID (also referred as to SMS Sender Name) is the information that is displayed to the recipient as the sender of the SMS when a message is received at a mobile device.&lt;/li&gt;&lt;li&gt;For more information, see: [Mocean&#39;s documentation](https://moceanapi.com/docs/?shell#sms-api)&lt;/li&gt;&lt;/ul&gt; |
|To|  &lt;ul&gt;&lt;li&gt;Telephone number of the receiver.&lt;/li&gt;&lt;li&gt;To send to multiple receivers, separate each entry with white space (‘ ’) or comma (`,`).&lt;/li&gt;&lt;li&gt;Telephone number must include country code, for example, a Malaysian phone number would be `60123456789`.&lt;/li&gt;&lt;/ul&gt; |
|Text|  &lt;ul&gt;&lt;li&gt;Contents of the message.&lt;/li&gt;&lt;li&gt;If you are sending binary content, this will be a hex string.&lt;/li&gt;&lt;/ul&gt; |
|User Data Header|  &lt;ul&gt;&lt;li&gt;User Data Header part of the message. For example, `0605040B8423F0`.&lt;/li&gt;&lt;/ul&gt; |
|Coding|  &lt;ul&gt;&lt;li&gt;Sets the coding scheme bits in DCS field.&lt;/li&gt;&lt;li&gt;Accepts the following values:  &lt;ul&gt;&lt;li&gt;`1` for 7-bit&lt;/li&gt;&lt;li&gt;`2` for 8-bit&lt;/li&gt;&lt;li&gt;`3` for UCS2&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;If unset, the value defaults to 7 bits unless a `mocean-udh` is defined, which sets coding to 8 bits.&lt;/li&gt;&lt;li&gt;If the charset is not set or is not set to UTF-8 when non-GSM character is detected, coding will set to UCS2.&lt;/li&gt;&lt;/ul&gt; |
|Delivery Report|  &lt;ul&gt;&lt;li&gt;Request for delivery reports with the state of the sent message.&lt;/li&gt;&lt;li&gt;To enable delivery reports, set this value to `1`.&lt;/li&gt;&lt;li&gt;If this field is not specified, the default value will be ‘ ’ and no DLR will be returned.&lt;/li&gt;&lt;/ul&gt; |
|Delivery Report URL|  &lt;ul&gt;&lt;li&gt;URL to receive delivery reports.&lt;/li&gt;&lt;li&gt;Required if DLR is requested.&lt;/li&gt;&lt;/ul&gt; |
|Schedule|  &lt;ul&gt;&lt;li&gt;When this field is used, the message is sent out on the specified date time (on best effort basis due to large number of SMS is queued for scheduling).&lt;/li&gt;&lt;li&gt;The format of the date time is `YYYY-MM-DD hh:mm:ss` in 24-hours format. Example: `2007-02-11 23:30:00`&lt;/li&gt;&lt;li&gt;The wrong date format will cause the gateway to reject the request. Use Malaysia time (or GMT &#43;8:00) while making scheduled SMS request. &lt;/li&gt;&lt;/ul&gt; |
|Charset|  &lt;ul&gt;&lt;li&gt;Indicates the character set used in the Text parameter.&lt;/li&gt;&lt;li&gt;Supported character sets are:  &lt;ul&gt;&lt;li&gt;ISO 8859-1&lt;/li&gt;&lt;li&gt;ISO 8859-7&lt;/li&gt;&lt;li&gt;UTF-8&lt;/li&gt;&lt;li&gt;Windows-1252&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Validity|  &lt;ul&gt;&lt;li&gt;Defines the validity period of message.&lt;/li&gt;&lt;li&gt;User has to input validity in terms of seconds.&lt;/li&gt;&lt;li&gt;For example, if user wants a message to expire after 5 minutes upon submission, user has to configure validity value as 300 (seconds).&lt;/li&gt;&lt;/ul&gt; |
