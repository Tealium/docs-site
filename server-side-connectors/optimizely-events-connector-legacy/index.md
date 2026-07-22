---
title: Optimizely Events Connector Setup Guide (Legacy)
description: This article describes how to set up the Optimizely Events connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/optimizely-events-connector-legacy/
---


<blockquote>
The [updated version of this connector](https://docs.tealium.com/optimizely-events-connector/) is currently available. This version can still be used if you already have it configured in your system, but is no longer available in the marketplace.
</blockquote>


## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Event| ✗| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Personal Token**
  * To authenticate, use a token in the request header generated from the following link: <http://app.optimizely.com/v2/profile/api>.
  * All API request examples in this documentation use the same header.
  * For more information on authentication, see [Personal Token](https://developers.optimizely.com/x/authentication/personal-token).

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Account ID|  <ul><li>The Optimizely account to which these events should be attributed.</li></ul> |
|Enrich Decisions|  <ul><li>Values are `true` or `false`.</li><li>Should be set to `true` to enable the Optimizely Easy Event Tracking functionality.</li><li>For more information about this field, see the [Event API reference](https://developers.optimizely.com/x/events/api/#api_reference).</li><li>See also [How Optimizely counts conversions](https://help.optimizely.com/Analyze_Results/How_Optimizely_counts_conversions).</li></ul> |
|Campaign ID|  <ul><li>(Required) The ID of the campaign containing this experiment.</li></ul> |
|Experiment ID|  <ul><li>(Required) The ID of the experiment the visitor was exposed to.</li><li>For Personalization Campaigns, explicitly send `null` as the Experiment ID for visitors not bucketed into an Experiment, to accurately calculate Campaign reach.</li></ul> |
|Variation ID|  <ul><li>(Required) The ID of the variation the visitor was exposed to.</li><li>For Personalization Campaigns, explicitly send `null` as the Variation ID for visitors not bucketed into any Experiment to accurately calculate campaign reach.</li></ul> |
|Is Campaign Holdback|  <ul><li>Values are `true` or `false`.</li><li>If `true`, the chosen experience was held back at the campaign level.</li><li>Required for Personalization, omit otherwise.</li></ul> |
|Timestamp|  <ul><li>(Required) Timestamp at which the event was generated, formatted in milliseconds since Unix epoch.</li><li>Sends a `{{unixTimestampMs}}` by default if no value is provided by the user.</li></ul> |
|UUID|  <ul><li>(Required) A unique identifier for this event.</li><li>Created automatically using `{{uuid}}`.</li><li>Used by Optimizely's backend to de-duplicate requests that are accidentally or erroneously replayed.</li><li>Optimizely detects events that have the same `entity_id`, `uuid` and `timestamp` and saves only one of them.</li><li>Ensure that each event uses a unique `uuid` or `timestamp` before sending.</li></ul> |
|Entity ID|  <ul><li>(Optional) The ID of the entity corresponding to this attribute.</li><li>Only required for custom attributes (`type="custom"`).</li><li>Invalid for other attribute types.</li></ul> |
|Event Name|  <ul><li>The event key (aka API name) for this event.</li></ul> |
|Event Data|  <ul><li>Additional event data in key-value pairs.</li></ul> |
|Tags|  <ul><li>(Optional) Key-value attributes related to tags.</li><li>If used, `type` and `value` must be included as two of the keys.</li></ul> |
|Event Type|  <ul><li>The type of event.</li><li>For example, to indicate a `decision_point`, type should be `campaign_activated`.</li></ul> |
|Event Value|  <ul><li>A scalar value associated with an event.</li><li>This should be some non-revenue number.</li></ul> |
|Visitor ID|  <ul><li>(Required) A unique identifier for the visitor.</li></ul> |
|Attributes|  <ul><li>Attributes associated with this visitor at the time of this request.</li></ul> |
|Session ID|  <ul><li>A unique identifier that identifies the session context, if any, for these events.</li><li>If omitted, the Optimizely backend calculates session-based results by inferring sessions and opening a session when an event is first received from a given `visitor_id`, and closing the session after 30 minutes with no events received for that visitor.</li><li>Maximum session size is 24 hours.</li></ul> |
|Anonymize IP|  <ul><li>Optimizely typically stores the client IP address for each request.</li><li>Values are `true` or `false`. <ul><li>If this flag is set to `true`, the last octet of the IP address is truncated before it is stored.</li><li>If set to `false`, the entire IP address is stored.</li></ul> </li><li>Most relevant for consumers of this API that are implemented in a web browser or mobile client context and are subject to policies or regulations restricting the storage of end-user identifying information.</li><li>This flag is independent of the IP anonymization setting in the Account and Project settings, which only controls how Optimizely clients set this flag.</li><li>If this flag is set, care must be taken when using the IP filtering features, as fully-qualified explicit IP addresses will not function as filters (anonymization occurs before events are filtered by IP).</li></ul> |
|Client Name|  <ul><li>Recommended for debugging purposes.</li><li>A unique identifier for the system that generated this event.</li><li>By convention, should be similar to the following example:`organization_name/system_name`</li><li>For a complete description of the Event API, see the [Event API reference](https://developers.optimizely.com/x/events/api/#api_reference).</li></ul> |
|Client Version|  <ul><li>Recommended for debugging purposes.</li><li>A version identifier for the system that generated this event.</li></ul> |
|Project ID|  <ul><li>(Optional) The Project ID needs only to be passed if you are using the Recommendations product.</li></ul> |
