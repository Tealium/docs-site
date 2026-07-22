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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Account ID**  
The Optimizely account to which the events should be attributed.
* **Access Token**  
Access token can be obtained by going to **[Optimizely Profile &gt; API Access](https://app.optimizely.com/v2/profile/api)**.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Track Event (Activate Users)

#### Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Visitor ID  | <ul><li>(Required) A unique identifier for the visitor.</li></ul>  |
| Session ID  | <ul><li>A unique identifier that identifies the session context, if any, for these events.</li><li>If omitted, the Optimizely backend calculates session-based results by inferring sessions and opening a session when an event is first received from a given `visitor_id`, and closing the session after 30 minutes with no events received for that visitor.</li><li>Maximum session size is 24 hours.</li></ul> |
| Project ID  | <ul><li>(Optional) The Project ID only needs to be passed if you are using the Recommendations product.</li></ul>   |
| Anonymize IP  | <ul><li>Optimizely typically stores the client IP address for each request.</li><li>Values are `true` or `false`. <ul><li>If this flag is set to `true`, the last octet of the IP address is truncated before it is stored.</li><li>If set to `false`, the entire IP address is stored.</li></ul> </li><li>Most relevant for consumers of this API that are implemented in a web browser or mobile client context and are subject to policies or regulations restricting the storage of end-user identifying information.</li><li>This flag is independent of the IP anonymization setting in the Account and Project settings, which only controls how Optimizely clients set this flag.</li><li>If this flag is set, care must be taken when using the IP filtering features, as fully-qualified explicit IP addresses will not function as filters (anonymization occurs before events are filtered by IP).</li></ul> |
| Enrich Decisions  | <ul><li>Values are `true` or `false`.</li><li>Should be set to `true` to enable the Optimizely Easy Event Tracking functionality.</li><li>For more information about this field, see the [Event API reference](https://developers.optimizely.com/x/events/api/#api_reference).</li><li>See also [How Optimizely counts conversions](https://help.optimizely.com/Analyze_Results/How_Optimizely_counts_conversions).</li></ul>  |
| Client Name | <ul><li>Recommended for debugging purposes.</li><li>A unique identifier for the system that generated this event.</li><li>By convention, should be similar to the following example:`organization_name/system_name`</li><li>For a complete description of the Event API, see the [Event API reference](https://developers.optimizely.com/x/events/api/#api_reference).</li></ul> |
| Client Version  | <ul><li>Recommended for debugging purposes.</li><li>A version identifier for the system that generated this event.</li></ul>   |
| Timestamp | <ul><li>(Required) Timestamp at which the event was generated, formatted in milliseconds since Unix epoch.</li><li>If unmapped, connector fire time is used.</li></ul> |
| UUID  | <ul><li>(Required) A unique identifier for this event.</li><li>Created automatically using `{{uuid}}`.</li><li>Used by Optimizely's backend to de-duplicate requests that are accidentally or erroneously replayed.</li><li>Optimizely detects events that have the same `entity_id`, `uuid` and `timestamp` and saves only one of them.</li><li>Ensure that each event uses a unique `uuid` or `timestamp` before sending.</li></ul>  |
| Entity ID | <ul><li>(Optional) The ID of the entity corresponding to this attribute.</li><li>Only required for custom attributes (`type="custom"`).</li><li>Invalid for other attribute types.</li></ul> |
| Key | <ul><li>Key</li></ul>  |
| Quantity  | <ul><li>Quantity</li></ul>   |
| Revenue | <ul><li>Revenue</li></ul>  |
| Type  | <ul><li>The type of event.</li><li>For example, to indicate a `decision_point`, type should be `campaign_activated`.</li></ul> |
| Event Tags  | <ul><li>(Optional) Additional event properties.</li><li>Key-value attributes related to tags.</li><li>If used, `type` and `value` must be included as two of the keys.</li></ul>  |
| Event Properties  | Key-value pairs that define properties or characteristics of the event.  |
| Campaign ID | <ul><li>(Required) The ID of the campaign containing this experiment.</li></ul>  |
| Experiment ID | <ul><li>(Required) The ID of the experiment the visitor was exposed to.</li><li>For Personalization Campaigns, explicitly send `null` as the Experiment ID for visitors not bucketed into an Experiment, to accurately calculate Campaign reach.</li></ul>  |
| Variation ID  | <ul><li>(Required) The ID of the variation the visitor was exposed to.</li><li>For Personalization campaigns, explicitly send `null` as the Variation ID for visitors not bucketed into an Experiment to accurately calculate campaign reach.</li></ul> |
| Campaign Holdback | <ul><li>Values are `true` or `false`.</li><li>If `true`, the chosen experience was held back at the campaign level.</li><li>Required for Personalization, omit otherwise.</li></ul>  |
| Type  | <ul><li>(Required) Can be `custom`</li></ul>   |
| Value | <ul><li>Required</li></ul>   |
| Entity ID | <ul><li>Required for custom attribute type.</li></ul>  |

## Additional Information

* [Optimizely Event API](https://docs.developers.optimizely.com/web/docs/event-api)