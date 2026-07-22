---
title: Adjust Events API Connector Setup Guide
description: This article describes how to set up the Adjust Events API connector.
url: https://docs.tealium.com/server-side-connectors/adjust-events-api-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Event| ✗| ✓|

## Configure Settings

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Authentication Token**
  * With Adjust's S2S Security feature, you can guarantee the security of your S2S events and protect against spoofed requests.
  * After you set up S2S authentication, each incoming request must carry a token generated in your Adjust dashboard.
  * See [Server-to-server (S2S) Security](https://help.adjust.com/en/article/server-to-server-s2s-security) for more details.
  * Leave the field empty if you haven't set up S2S authentication.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Token|  <ul><li>Adjust event token from the dashboard.</li></ul> |
|App Token|  <ul><li>Adjust app token from the dashboard.</li></ul> |
|Android ID|  <ul><li>Android ID</li><li>See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).</li></ul> |
|Open Advertising ID|  <ul><li>Platform-dependent Open Advertising ID.</li><li>See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).</li></ul> |
|Raw Amazon Fire Advertising ID|  <ul><li>Platform-dependent Raw Amazon Fire Advertising ID.</li><li>See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).</li></ul> |
|Raw IDFA|  <ul><li>iOS only.</li><li>Raw IDFA Identifier.</li><li>See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).</li></ul> |
|Raw IDFV|  <ul><li>Raw IDFV Identifier.</li><li>See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).</li></ul> |
|Raw Google Advertising ID|  <ul><li>Raw Google Advertising ID Identifier.</li><li>See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).</li></ul> |
|Adjust Device ID|  <ul><li>Identifying LAT users on iOS without idfa information.</li></ul> |
|Created At Timestamp (Formatted)|  <ul><li>Telling the exact moment an event occurred.</li><li>The connector encodes the value.</li><li>Example:__ `2017-01-02T15:04:05.000+0000` becomes `2017-01-02T15%3A04%3A05.000%2B0000`</li></ul> |
|Created At Timestamp (Unix)|  <ul><li>Telling the exact moment an event occurred.</li><li>Can be specified using either seconds or milliseconds.</li></ul> |
|IP Address|  <ul><li>Event linking to third-parties, such as Google and including location-related information, such as `city` and `postal_code`) in your callbacks.</li><li>The `ip_address` parameter only accepts IPv4.</li><li>IPv6 is not yet supported.</li></ul> |
|Currency|  <ul><li>Revenue event</li><li>See [currency code](https://help.adjust.com/en/article/supported-currencies).</li></ul> |
|Environment|  <ul><li>Environment to post the data t.</li><li>Example: `environment=sandbox` or `environment=production`</li><li>If this parameter is not included, the event will be pushed to the production environment.</li></ul> |
|Revenue|  <ul><li>Revenue event value in full currency units (149.99 = $149.99).</li><li>Adjust accepts a minimum value of 0.001 for this parameter.</li></ul> |
|Template Variables|  <ul><li>Provide template variables as data input.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Reference nested template variables with dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|Templates|  <ul><li>Provide templates to be referenced in Body Data.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).=.</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul> |