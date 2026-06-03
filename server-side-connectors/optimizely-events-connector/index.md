---
title: Optimizely Events Connector Setup Guide
description: This article describes how to set up the Optimizely Events connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/optimizely-events-connector/
---
## Connector Actions

| **Action Name**  | **AudienceStream** | **EventStream** |
|:-----------------------------|:-------------------|:----------------|
| Track Event (Activate Users) | ✓  | ✓ |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Account ID**  
The Optimizely account to which the events should be attributed.
* **Access Token**  
Access token can be obtained by going to **[Optimizely Profile &amp;gt; API Access](https://app.optimizely.com/v2/profile/api)**.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Track Event (Activate Users)

#### Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Visitor ID  | &lt;ul&gt;&lt;li&gt;(Required) A unique identifier for the visitor.&lt;/li&gt;&lt;/ul&gt;  |
| Session ID  | &lt;ul&gt;&lt;li&gt;A unique identifier that identifies the session context, if any, for these events.&lt;/li&gt;&lt;li&gt;If omitted, the Optimizely backend calculates session-based results by inferring sessions and opening a session when an event is first received from a given `visitor_id`, and closing the session after 30 minutes with no events received for that visitor.&lt;/li&gt;&lt;li&gt;Maximum session size is 24 hours.&lt;/li&gt;&lt;/ul&gt; |
| Project ID  | &lt;ul&gt;&lt;li&gt;(Optional) The Project ID only needs to be passed if you are using the Recommendations product.&lt;/li&gt;&lt;/ul&gt;   |
| Anonymize IP  | &lt;ul&gt;&lt;li&gt;Optimizely typically stores the client IP address for each request.&lt;/li&gt;&lt;li&gt;Values are `true` or `false`. &lt;ul&gt;&lt;li&gt;If this flag is set to `true`, the last octet of the IP address is truncated before it is stored.&lt;/li&gt;&lt;li&gt;If set to `false`, the entire IP address is stored.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Most relevant for consumers of this API that are implemented in a web browser or mobile client context and are subject to policies or regulations restricting the storage of end-user identifying information.&lt;/li&gt;&lt;li&gt;This flag is independent of the IP anonymization setting in the Account and Project settings, which only controls how Optimizely clients set this flag.&lt;/li&gt;&lt;li&gt;If this flag is set, care must be taken when using the IP filtering features, as fully-qualified explicit IP addresses will not function as filters (anonymization occurs before events are filtered by IP).&lt;/li&gt;&lt;/ul&gt; |
| Enrich Decisions  | &lt;ul&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;li&gt;Should be set to `true` to enable the Optimizely Easy Event Tracking functionality.&lt;/li&gt;&lt;li&gt;For more information about this field, see the [Event API reference](https://developers.optimizely.com/x/events/api/#api_reference).&lt;/li&gt;&lt;li&gt;See also [How Optimizely counts conversions](https://help.optimizely.com/Analyze_Results/How_Optimizely_counts_conversions).&lt;/li&gt;&lt;/ul&gt;  |
| Client Name | &lt;ul&gt;&lt;li&gt;Recommended for debugging purposes.&lt;/li&gt;&lt;li&gt;A unique identifier for the system that generated this event.&lt;/li&gt;&lt;li&gt;By convention, should be similar to the following example:`organization_name/system_name`&lt;/li&gt;&lt;li&gt;For a complete description of the Event API, see the [Event API reference](https://developers.optimizely.com/x/events/api/#api_reference).&lt;/li&gt;&lt;/ul&gt; |
| Client Version  | &lt;ul&gt;&lt;li&gt;Recommended for debugging purposes.&lt;/li&gt;&lt;li&gt;A version identifier for the system that generated this event.&lt;/li&gt;&lt;/ul&gt;   |
| Timestamp | &lt;ul&gt;&lt;li&gt;(Required) Timestamp at which the event was generated, formatted in milliseconds since Unix epoch.&lt;/li&gt;&lt;li&gt;If unmapped, connector fire time is used.&lt;/li&gt;&lt;/ul&gt; |
| UUID  | &lt;ul&gt;&lt;li&gt;(Required) A unique identifier for this event.&lt;/li&gt;&lt;li&gt;Created automatically using `{{uuid}}`.&lt;/li&gt;&lt;li&gt;Used by Optimizely&#39;s backend to de-duplicate requests that are accidentally or erroneously replayed.&lt;/li&gt;&lt;li&gt;Optimizely detects events that have the same `entity_id`, `uuid` and `timestamp` and saves only one of them.&lt;/li&gt;&lt;li&gt;Ensure that each event uses a unique `uuid` or `timestamp` before sending.&lt;/li&gt;&lt;/ul&gt;  |
| Entity ID | &lt;ul&gt;&lt;li&gt;(Optional) The ID of the entity corresponding to this attribute.&lt;/li&gt;&lt;li&gt;Only required for custom attributes (`type=&#34;custom&#34;`).&lt;/li&gt;&lt;li&gt;Invalid for other attribute types.&lt;/li&gt;&lt;/ul&gt; |
| Key | &lt;ul&gt;&lt;li&gt;Key&lt;/li&gt;&lt;/ul&gt;  |
| Quantity  | &lt;ul&gt;&lt;li&gt;Quantity&lt;/li&gt;&lt;/ul&gt;   |
| Revenue | &lt;ul&gt;&lt;li&gt;Revenue&lt;/li&gt;&lt;/ul&gt;  |
| Type  | &lt;ul&gt;&lt;li&gt;The type of event.&lt;/li&gt;&lt;li&gt;For example, to indicate a `decision_point`, type should be `campaign_activated`.&lt;/li&gt;&lt;/ul&gt; |
| Event Tags  | &lt;ul&gt;&lt;li&gt;(Optional) Additional event properties.&lt;/li&gt;&lt;li&gt;Key-value attributes related to tags.&lt;/li&gt;&lt;li&gt;If used, `type` and `value` must be included as two of the keys.&lt;/li&gt;&lt;/ul&gt;  |
| Event Properties  | Key-value pairs that define properties or characteristics of the event.  |
| Campaign ID | &lt;ul&gt;&lt;li&gt;(Required) The ID of the campaign containing this experiment.&lt;/li&gt;&lt;/ul&gt;  |
| Experiment ID | &lt;ul&gt;&lt;li&gt;(Required) The ID of the experiment the visitor was exposed to.&lt;/li&gt;&lt;li&gt;For Personalization Campaigns, explicitly send `null` as the Experiment ID for visitors not bucketed into an Experiment, to accurately calculate Campaign reach.&lt;/li&gt;&lt;/ul&gt;  |
| Variation ID  | &lt;ul&gt;&lt;li&gt;(Required) The ID of the variation the visitor was exposed to.&lt;/li&gt;&lt;li&gt;For Personalization campaigns, explicitly send `null` as the Variation ID for visitors not bucketed into an Experiment to accurately calculate campaign reach.&lt;/li&gt;&lt;/ul&gt; |
| Campaign Holdback | &lt;ul&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;li&gt;If `true`, the chosen experience was held back at the campaign level.&lt;/li&gt;&lt;li&gt;Required for Personalization, omit otherwise.&lt;/li&gt;&lt;/ul&gt;  |
| Type  | &lt;ul&gt;&lt;li&gt;(Required) Can be `custom`&lt;/li&gt;&lt;/ul&gt;   |
| Value | &lt;ul&gt;&lt;li&gt;Required&lt;/li&gt;&lt;/ul&gt;   |
| Entity ID | &lt;ul&gt;&lt;li&gt;Required for custom attribute type.&lt;/li&gt;&lt;/ul&gt;  |

## Additional Information

* [Optimizely Event API](https://docs.developers.optimizely.com/web/docs/event-api)