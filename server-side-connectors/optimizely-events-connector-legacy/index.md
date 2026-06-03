---
title: Optimizely Events Connector Setup Guide (Legacy)
description: This article describes how to set up the Optimizely Events connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/optimizely-events-connector-legacy/
---

The [updated version of this connector]() is currently available. This version can still be used if you already have it configured in your system, but is no longer available in the marketplace.

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Event| ✗| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Personal Token**
  * To authenticate, use a token in the request header generated from the following link: &lt;http://app.optimizely.com/v2/profile/api&gt;.
  * All API request examples in this documentation use the same header.
  * For more information on authentication, see [Personal Token](https://developers.optimizely.com/x/authentication/personal-token).

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Account ID|  &lt;ul&gt;&lt;li&gt;The Optimizely account to which these events should be attributed.&lt;/li&gt;&lt;/ul&gt; |
|Enrich Decisions|  &lt;ul&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;li&gt;Should be set to `true` to enable the Optimizely Easy Event Tracking functionality.&lt;/li&gt;&lt;li&gt;For more information about this field, see the [Event API reference](https://developers.optimizely.com/x/events/api/#api_reference).&lt;/li&gt;&lt;li&gt;See also [How Optimizely counts conversions](https://help.optimizely.com/Analyze_Results/How_Optimizely_counts_conversions).&lt;/li&gt;&lt;/ul&gt; |
|Campaign ID|  &lt;ul&gt;&lt;li&gt;(Required) The ID of the campaign containing this experiment.&lt;/li&gt;&lt;/ul&gt; |
|Experiment ID|  &lt;ul&gt;&lt;li&gt;(Required) The ID of the experiment the visitor was exposed to.&lt;/li&gt;&lt;li&gt;For Personalization Campaigns, explicitly send `null` as the Experiment ID for visitors not bucketed into an Experiment, to accurately calculate Campaign reach.&lt;/li&gt;&lt;/ul&gt; |
|Variation ID|  &lt;ul&gt;&lt;li&gt;(Required) The ID of the variation the visitor was exposed to.&lt;/li&gt;&lt;li&gt;For Personalization Campaigns, explicitly send `null` as the Variation ID for visitors not bucketed into any Experiment to accurately calculate campaign reach.&lt;/li&gt;&lt;/ul&gt; |
|Is Campaign Holdback|  &lt;ul&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;li&gt;If `true`, the chosen experience was held back at the campaign level.&lt;/li&gt;&lt;li&gt;Required for Personalization, omit otherwise.&lt;/li&gt;&lt;/ul&gt; |
|Timestamp|  &lt;ul&gt;&lt;li&gt;(Required) Timestamp at which the event was generated, formatted in milliseconds since Unix epoch.&lt;/li&gt;&lt;li&gt;Sends a `{{unixTimestampMs}}` by default if no value is provided by the user.&lt;/li&gt;&lt;/ul&gt; |
|UUID|  &lt;ul&gt;&lt;li&gt;(Required) A unique identifier for this event.&lt;/li&gt;&lt;li&gt;Created automatically using `{{uuid}}`.&lt;/li&gt;&lt;li&gt;Used by Optimizely&#39;s backend to de-duplicate requests that are accidentally or erroneously replayed.&lt;/li&gt;&lt;li&gt;Optimizely detects events that have the same `entity_id`, `uuid` and `timestamp` and saves only one of them.&lt;/li&gt;&lt;li&gt;Ensure that each event uses a unique `uuid` or `timestamp` before sending.&lt;/li&gt;&lt;/ul&gt; |
|Entity ID|  &lt;ul&gt;&lt;li&gt;(Optional) The ID of the entity corresponding to this attribute.&lt;/li&gt;&lt;li&gt;Only required for custom attributes (`type=&#34;custom&#34;`).&lt;/li&gt;&lt;li&gt;Invalid for other attribute types.&lt;/li&gt;&lt;/ul&gt; |
|Event Name|  &lt;ul&gt;&lt;li&gt;The event key (aka API name) for this event.&lt;/li&gt;&lt;/ul&gt; |
|Event Data|  &lt;ul&gt;&lt;li&gt;Additional event data in key-value pairs.&lt;/li&gt;&lt;/ul&gt; |
|Tags|  &lt;ul&gt;&lt;li&gt;(Optional) Key-value attributes related to tags.&lt;/li&gt;&lt;li&gt;If used, `type` and `value` must be included as two of the keys.&lt;/li&gt;&lt;/ul&gt; |
|Event Type|  &lt;ul&gt;&lt;li&gt;The type of event.&lt;/li&gt;&lt;li&gt;For example, to indicate a `decision_point`, type should be `campaign_activated`.&lt;/li&gt;&lt;/ul&gt; |
|Event Value|  &lt;ul&gt;&lt;li&gt;A scalar value associated with an event.&lt;/li&gt;&lt;li&gt;This should be some non-revenue number.&lt;/li&gt;&lt;/ul&gt; |
|Visitor ID|  &lt;ul&gt;&lt;li&gt;(Required) A unique identifier for the visitor.&lt;/li&gt;&lt;/ul&gt; |
|Attributes|  &lt;ul&gt;&lt;li&gt;Attributes associated with this visitor at the time of this request.&lt;/li&gt;&lt;/ul&gt; |
|Session ID|  &lt;ul&gt;&lt;li&gt;A unique identifier that identifies the session context, if any, for these events.&lt;/li&gt;&lt;li&gt;If omitted, the Optimizely backend calculates session-based results by inferring sessions and opening a session when an event is first received from a given `visitor_id`, and closing the session after 30 minutes with no events received for that visitor.&lt;/li&gt;&lt;li&gt;Maximum session size is 24 hours.&lt;/li&gt;&lt;/ul&gt; |
|Anonymize IP|  &lt;ul&gt;&lt;li&gt;Optimizely typically stores the client IP address for each request.&lt;/li&gt;&lt;li&gt;Values are `true` or `false`. &lt;ul&gt;&lt;li&gt;If this flag is set to `true`, the last octet of the IP address is truncated before it is stored.&lt;/li&gt;&lt;li&gt;If set to `false`, the entire IP address is stored.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Most relevant for consumers of this API that are implemented in a web browser or mobile client context and are subject to policies or regulations restricting the storage of end-user identifying information.&lt;/li&gt;&lt;li&gt;This flag is independent of the IP anonymization setting in the Account and Project settings, which only controls how Optimizely clients set this flag.&lt;/li&gt;&lt;li&gt;If this flag is set, care must be taken when using the IP filtering features, as fully-qualified explicit IP addresses will not function as filters (anonymization occurs before events are filtered by IP).&lt;/li&gt;&lt;/ul&gt; |
|Client Name|  &lt;ul&gt;&lt;li&gt;Recommended for debugging purposes.&lt;/li&gt;&lt;li&gt;A unique identifier for the system that generated this event.&lt;/li&gt;&lt;li&gt;By convention, should be similar to the following example:`organization_name/system_name`&lt;/li&gt;&lt;li&gt;For a complete description of the Event API, see the [Event API reference](https://developers.optimizely.com/x/events/api/#api_reference).&lt;/li&gt;&lt;/ul&gt; |
|Client Version|  &lt;ul&gt;&lt;li&gt;Recommended for debugging purposes.&lt;/li&gt;&lt;li&gt;A version identifier for the system that generated this event.&lt;/li&gt;&lt;/ul&gt; |
|Project ID|  &lt;ul&gt;&lt;li&gt;(Optional) The Project ID needs only to be passed if you are using the Recommendations product.&lt;/li&gt;&lt;/ul&gt; |
