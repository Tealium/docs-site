---
title: Adjust Events API Connector Setup Guide
description: This article describes how to set up the Adjust Events API connector.
url: https://docs.tealium.com/server-side-connectors/adjust-events-api-connector/
---
## Connector Actions

| Action name | Visitor profile | Event data |
| --- | :---: | :---: |
|Send Event| ✗| ✓|
|Send Session| ✗| ✓|

## Configuration

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Authentication Token**
  * With Adjust's S2S Security feature, you can guarantee the security of your S2S events and protect against spoofed requests.
  * After you set up S2S authentication, each incoming request must carry a token generated in your Adjust dashboard.
  * See [Server-to-server (S2S) Security](https://dev.adjust.com/en/api/s2s-api/security/) for more details.
  * Leave the field empty if you haven't set up S2S authentication.

## Action Settings - Parameters and Options

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

### Action - Send Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Token|  <ul><li>Adjust event token from the dashboard.</li></ul> |
|App Token|  <ul><li>Adjust app token from the dashboard.</li></ul> |
|Android ID|  <ul><li>Android ID.</li><li>Sent to Adjust as `android_id`.</li><li>See [Device identifiers](https://help.adjust.com/en/article/device-identifiers).</li></ul> |
|Hashed Android ID (Lowercase, MD5)|  <ul><li>MD5 hash of the lowercase Android ID.</li><li>Sent to Adjust as `android_id_lower_md5`.</li><li>The connector passes the value through as supplied and does not hash it.</li></ul> |
|Hashed Android ID (Lowercase, SHA1)|  <ul><li>SHA1 hash of the lowercase Android ID.</li><li>Sent to Adjust as `android_id_lower_sha1`.</li><li>The connector passes the value through as supplied and does not hash it.</li></ul> |
|Hashed Android ID (Uppercase, MD5)|  <ul><li>MD5 hash of the uppercase Android ID.</li><li>Sent to Adjust as `android_id_upper_md5`.</li><li>The connector passes the value through as supplied and does not hash it.</li></ul> |
|Hashed Android ID (Uppercase, SHA1)|  <ul><li>SHA1 hash of the uppercase Android ID.</li><li>Sent to Adjust as `android_id_upper_sha1`.</li><li>The connector passes the value through as supplied and does not hash it.</li></ul> |
|Open Advertising ID|  <ul><li>Platform-dependent Open Advertising ID.</li><li>Sent to Adjust as `oaid`.</li><li>See [Device identifiers](https://help.adjust.com/en/article/device-identifiers).</li></ul> |
|Raw Amazon Fire Advertising ID|  <ul><li>Platform-dependent Raw Amazon Fire Advertising ID.</li><li>Sent to Adjust as `fire_adid`.</li><li>See [Device identifiers](https://help.adjust.com/en/article/device-identifiers).</li></ul> |
|Raw IDFA|  <ul><li>iOS only.</li><li>Raw IDFA Identifier.</li><li>Sent to Adjust as `idfa`.</li><li>See [Device identifiers](https://help.adjust.com/en/article/device-identifiers).</li></ul> |
|Raw IDFV|  <ul><li>Raw IDFV Identifier.</li><li>Sent to Adjust as `idfv`.</li><li>See [Device identifiers](https://help.adjust.com/en/article/device-identifiers).</li></ul> |
|Raw Google Advertising ID|  <ul><li>Raw Google Advertising ID Identifier.</li><li>Sent to Adjust as `gps_adid`.</li><li>See [Device identifiers](https://help.adjust.com/en/article/device-identifiers).</li></ul> |
|Roku Advertising ID|  <ul><li>Roku device advertising ID.</li><li>Sent to Adjust as `rida`.</li><li>See [Device identifiers](https://help.adjust.com/en/article/device-identifiers).</li></ul> |
|Vizio Advertising ID|  <ul><li>Vizio device advertising ID.</li><li>Sent to Adjust as `vida`.</li><li>See [Device identifiers](https://help.adjust.com/en/article/device-identifiers).</li></ul> |
|Tizen Advertising ID|  <ul><li>Samsung Tizen device advertising ID.</li><li>Sent to Adjust as `tifa`.</li><li>See [Device identifiers](https://help.adjust.com/en/article/device-identifiers).</li></ul> |
|Adjust Device ID|  <ul><li>Identifying LAT users on iOS without idfa information.</li></ul> |
|Created At Timestamp (Formatted)|  <ul><li>Telling the exact moment an event occurred.</li><li>The connector encodes the value.</li><li>Example:__ `2017-01-02T15:04:05.000+0000` becomes `2017-01-02T15%3A04%3A05.000%2B0000`</li></ul> |
|Created At Timestamp (Unix)|  <ul><li>Telling the exact moment an event occurred.</li><li>Can be specified using either seconds or milliseconds.</li></ul> |
|IP Address|  <ul><li>Event linking to third-parties, such as Google and including location-related information, such as `city` and `postal_code`) in your callbacks.</li><li>The `ip_address` parameter only accepts IPv4.</li><li>IPv6 is not yet supported.</li></ul> |
|Currency|  <ul><li>Revenue event</li><li>See [currency code](https://help.adjust.com/en/article/supported-currencies).</li></ul> |
|Environment|  <ul><li>Environment to post the data t.</li><li>Example: `environment=sandbox` or `environment=production`</li><li>If this parameter is not included, the event will be pushed to the production environment.</li></ul> |
|Revenue|  <ul><li>Revenue event value in full currency units (149.99 = $149.99).</li><li>Adjust accepts a minimum value of 0.001 for this parameter.</li></ul> |
|Template Variables|  <ul><li>Provide template variables as data input.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Reference nested template variables with dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|Templates|  <ul><li>Provide templates to be referenced in Body Data.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).=.</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul> |

### Send Session

Use the Send Session action to establish a session with Adjust before sending events. Adjust drops events from devices it has not recorded a session for. Use this action when the source cannot start a session through the Adjust SDK, such as server-side deployments on Roku, Vizio, and Tizen devices.

Behavior:

* Adjust ignores a session sent within 30 minutes of the previous one for the same device. Trigger this action on a session-start event, not on every event.
* Adjust must enable server-to-server (S2S) sessions for your app before you can use this action. Contact your Adjust account manager to activate the feature.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|App Token|  <ul><li>Adjust app token from the dashboard.</li></ul> |
|Device Identifier|  <ul><li>Platform-dependent device or advertising ID.</li><li>Map a value for each supported identifier. The connector sends the first non-empty identifier.</li><li>See [Device identifiers](https://help.adjust.com/en/article/device-identifiers).</li></ul> |
|Recommended Additional Parameters|  <ul><li>For accurate session attribution, Adjust recommends including the following parameters with your sessions:<ul><li>**Adjust Device ID**: Identifying LAT users on iOS without idfa information.</li><li>**Created At Timestamp (Formatted)**: Telling the exact moment a session occurred. The connector encodes the value. For example, `2017-01-02T15:04:05.000+0000` becomes `2017-01-02T15%3A04%3A05.000%2B0000`.</li><li>**Created At Timestamp (Unix)**: Telling the exact moment a session occurred. Can be specified using either seconds or milliseconds.</li><li>**IP Address**: Session linking to third-parties and including location-related information in your callbacks. The `ip_address` parameter only accepts IPv4. IPv6 is not yet supported.</li></ul></li></ul> |
|Session Parameters|  <ul><li>**App Version**: App version.</li><li>**App Version Short**: Short app version.</li><li>**OS Name**: Operating system name.</li><li>**OS Version**: Operating system version.</li><li>**Device Type**: Device type.</li><li>**Device Name**: Device name.</li><li>**Country**: Country code.</li><li>**Language**: Language code.</li><li>**Environment**: Environment to post the data to (`sandbox` or `production`). If this parameter is not included, the session is pushed to the production environment.</li><li>**EEA**, **Ad Personalization**, **Ad User Data**, **NPA**: Digital Markets Act (DMA) consent parameters.</li><li>Custom keys (not in the dropdown) are passed through verbatim.</li></ul> |