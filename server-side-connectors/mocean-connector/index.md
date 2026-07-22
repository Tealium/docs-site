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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**: Your account API key. For more information, see: [Mocean Authentication](https://moceanapi.com/docs/?shell#authentication&quot;&gt;https://moceanapi.com/docs/?shell#authentication)
* **API Secret**: Your account API secret.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send SMS

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|From|  <ul><li>SMS Sender ID (also referred as to SMS Sender Name) is the information that is displayed to the recipient as the sender of the SMS when a message is received at a mobile device.</li><li>For more information, see: [Mocean's documentation](https://moceanapi.com/docs/?shell#sms-api)</li></ul> |
|To|  <ul><li>Telephone number of the receiver.</li><li>To send to multiple receivers, separate each entry with white space (‘ ’) or comma (`,`).</li><li>Telephone number must include country code, for example, a Malaysian phone number would be `60123456789`.</li></ul> |
|Text|  <ul><li>Contents of the message.</li><li>If you are sending binary content, this will be a hex string.</li></ul> |
|User Data Header|  <ul><li>User Data Header part of the message. For example, `0605040B8423F0`.</li></ul> |
|Coding|  <ul><li>Sets the coding scheme bits in DCS field.</li><li>Accepts the following values:  <ul><li>`1` for 7-bit</li><li>`2` for 8-bit</li><li>`3` for UCS2</li></ul> </li></ul> <ul><li>If unset, the value defaults to 7 bits unless a `mocean-udh` is defined, which sets coding to 8 bits.</li><li>If the charset is not set or is not set to UTF-8 when non-GSM character is detected, coding will set to UCS2.</li></ul> |
|Delivery Report|  <ul><li>Request for delivery reports with the state of the sent message.</li><li>To enable delivery reports, set this value to `1`.</li><li>If this field is not specified, the default value will be ‘ ’ and no DLR will be returned.</li></ul> |
|Delivery Report URL|  <ul><li>URL to receive delivery reports.</li><li>Required if DLR is requested.</li></ul> |
|Schedule|  <ul><li>When this field is used, the message is sent out on the specified date time (on best effort basis due to large number of SMS is queued for scheduling).</li><li>The format of the date time is `YYYY-MM-DD hh:mm:ss` in 24-hours format. Example: `2007-02-11 23:30:00`</li><li>The wrong date format will cause the gateway to reject the request. 
<blockquote>
Use Malaysia time (or GMT +8:00) while making scheduled SMS request.
</blockquote>
 </li></ul> |
|Charset|  <ul><li>Indicates the character set used in the Text parameter.</li><li>Supported character sets are:  <ul><li>ISO 8859-1</li><li>ISO 8859-7</li><li>UTF-8</li><li>Windows-1252</li></ul> </li></ul> |
|Validity|  <ul><li>Defines the validity period of message.</li><li>User has to input validity in terms of seconds.</li><li>For example, if user wants a message to expire after 5 minutes upon submission, user has to configure validity value as 300 (seconds).</li></ul> |
