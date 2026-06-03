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

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Authentication Token**
  * With Adjust&#39;s S2S Security feature, you can guarantee the security of your S2S events and protect against spoofed requests.
  * After you set up S2S authentication, each incoming request must carry a token generated in your Adjust dashboard.
  * See [Server-to-server (S2S) Security](https://help.adjust.com/en/article/server-to-server-s2s-security) for more details.
  * Leave the field empty if you haven&#39;t set up S2S authentication.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Token|  &lt;ul&gt;&lt;li&gt;Adjust event token from the dashboard.&lt;/li&gt;&lt;/ul&gt; |
|App Token|  &lt;ul&gt;&lt;li&gt;Adjust app token from the dashboard.&lt;/li&gt;&lt;/ul&gt; |
|Android ID|  &lt;ul&gt;&lt;li&gt;Android ID&lt;/li&gt;&lt;li&gt;See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).&lt;/li&gt;&lt;/ul&gt; |
|Open Advertising ID|  &lt;ul&gt;&lt;li&gt;Platform-dependent Open Advertising ID.&lt;/li&gt;&lt;li&gt;See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).&lt;/li&gt;&lt;/ul&gt; |
|Raw Amazon Fire Advertising ID|  &lt;ul&gt;&lt;li&gt;Platform-dependent Raw Amazon Fire Advertising ID.&lt;/li&gt;&lt;li&gt;See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).&lt;/li&gt;&lt;/ul&gt; |
|Raw IDFA|  &lt;ul&gt;&lt;li&gt;iOS only.&lt;/li&gt;&lt;li&gt;Raw IDFA Identifier.&lt;/li&gt;&lt;li&gt;See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).&lt;/li&gt;&lt;/ul&gt; |
|Raw IDFV|  &lt;ul&gt;&lt;li&gt;Raw IDFV Identifier.&lt;/li&gt;&lt;li&gt;See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).&lt;/li&gt;&lt;/ul&gt; |
|Raw Google Advertising ID|  &lt;ul&gt;&lt;li&gt;Raw Google Advertising ID Identifier.&lt;/li&gt;&lt;li&gt;See [Accepted device identifiers](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers).&lt;/li&gt;&lt;/ul&gt; |
|Adjust Device ID|  &lt;ul&gt;&lt;li&gt;Identifying LAT users on iOS without idfa information.&lt;/li&gt;&lt;/ul&gt; |
|Created At Timestamp (Formatted)|  &lt;ul&gt;&lt;li&gt;Telling the exact moment an event occurred.&lt;/li&gt;&lt;li&gt;The connector encodes the value.&lt;/li&gt;&lt;li&gt;Example:__ `2017-01-02T15:04:05.000&#43;0000` becomes `2017-01-02T15%3A04%3A05.000%2B0000`&lt;/li&gt;&lt;/ul&gt; |
|Created At Timestamp (Unix)|  &lt;ul&gt;&lt;li&gt;Telling the exact moment an event occurred.&lt;/li&gt;&lt;li&gt;Can be specified using either seconds or milliseconds.&lt;/li&gt;&lt;/ul&gt; |
|IP Address|  &lt;ul&gt;&lt;li&gt;Event linking to third-parties, such as Google and including location-related information, such as `city` and `postal_code`) in your callbacks.&lt;/li&gt;&lt;li&gt;The `ip_address` parameter only accepts IPv4.&lt;/li&gt;&lt;li&gt;IPv6 is not yet supported.&lt;/li&gt;&lt;/ul&gt; |
|Currency|  &lt;ul&gt;&lt;li&gt;Revenue event&lt;/li&gt;&lt;li&gt;See [currency code](https://help.adjust.com/en/article/supported-currencies).&lt;/li&gt;&lt;/ul&gt; |
|Environment|  &lt;ul&gt;&lt;li&gt;Environment to post the data t.&lt;/li&gt;&lt;li&gt;Example: `environment=sandbox` or `environment=production`&lt;/li&gt;&lt;li&gt;If this parameter is not included, the event will be pushed to the production environment.&lt;/li&gt;&lt;/ul&gt; |
|Revenue|  &lt;ul&gt;&lt;li&gt;Revenue event value in full currency units (149.99 = $149.99).&lt;/li&gt;&lt;li&gt;Adjust accepts a minimum value of 0.001 for this parameter.&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;Provide template variables as data input.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Reference nested template variables with dot notation.&lt;/li&gt;&lt;li&gt;Example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;Provide templates to be referenced in Body Data.&lt;/li&gt;&lt;li&gt;For more information, see .=.&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |