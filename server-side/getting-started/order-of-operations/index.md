---
title: Server-side order of operations
description: This article describes the order of operations for server-side data collection and covers the following processes:  incoming events, enriching attributes, processing visitor profiles,  building audiences, and triggering connectors.
url: https://docs.tealium.com/server-side/getting-started/order-of-operations/
---
## Data supply chain

![](/images/guides/server-side/tealium-data-supply-chain.png)

## Order of operations overview

Tealium AudienceStream is integrated tightly with Tealium EventStream, so this overview starts at the point that events are received.

The default order of operations:

* Event received
* Event attributes enriched
* Visit and visitor attributes enriched
    * Visitor profile obtained
    * Visitor ID attribute enriched
    * Visitor profiles stitched
* Audiences evaluated
* Connectors triggered

![](/images/server-side/asorderofprocessing.png)

## Enrichment timing and conditions

Enrichments are evaluated in two ways: the timing and the condition.

The enrichment timing determines when to evaluate the condition. This appears in the interface as the **WHEN** setting and is limited to the following options offered in AudienceStream:

* **New Visitor**: The first visit for a visitor.
* **New Visit**: A return visit by an existing visitor.
* **Visit Ended**: The end of a visitor session.
* **Any Event**: Any event, except New Visitor, New Visit, or Visit Ended.

The enrichment condition determines if the attribute value will be updated. Conditions appear in the interface as rules, which you configure using logical operators.

## Order of operations details

### Event Received

The event is received from Tealium Collect.

### Event Attributes Enriched

The event attribute enrichments are evaluated.

### Visit and Visitor Attributes Enriched

#### Visitor Profile Obtained

Visit and visitor attributes are stored in a visitor profile, so the first step in enriching these attributes is to get the visitor profile. If the `tealium_visitor_id` matches an existing profile, the profile is enriched. If the `tealium_visitor_id` does not match an existing profile, a new profile is created and is enriched.

Visit and visitor attribute enrichments are evaluated based on their timing and condition.

In the following example, the attribute enrichment for the `Cart Abandoner` badge is evaluated based on the following:

* **WHEN**: Visit Ended
* **Rule**: `cart_total_items greater than 0`

![](/images/server-side/asprocessingcartabandoner.png)

If **Enable Rule Dependency Checking** is enabled, enrichments are executed in the correct order to accommodate dependencies in rules.

If **Enrichment Order Respects UI Order** is enabled, enrichments are executed in the order they appear in the user interface, with adjustments for dependency checking if needed. Otherwise, enrichments are executed in attribute ID order.

#### Visitor ID Attributes Enriched

If the event contains a user identifier that is configured to enrich a visitor ID attribute, the visitor ID attribute is only set if each of the following conditions are met:

* The visitor ID attribute does not have an existing value.
* The enrichment rule evaluates to `true`.
* The enriched value meets [the minimum requirements for a visitor ID]().

If there are multiple visitor ID attributes, they are evaluated in attribute ID order.

#### Visitor Profiles Stitched

If an enriched visitor ID attribute matches multiple visitor profiles, they are merged into a new visitor profile.

### Audiences Evaluated

AudienceStream evaluates the visitor profile to determine which audiences it should join or leave. The visitor joins an audience if the audience rule is `true` or leaves an audience if the audience rule is `false`. The transition of a visitor profile into or out of an audience triggers connector actions.

### Connectors Triggered

AudienceStream evaluates triggers to determine which connector actions to initiate. Connector actions are initiated when the trigger condition is met. A connector condition can be one of the following:

* **Joined Audience**: The visitor joined the audience during this visit.
* **Left Audience**: The visitor left the audience during this visit. This action does not occur when a visitor is deleted. For more information, see [Deleting a visitor]().
* **In Audience at start of visit**: The visitor was in the audience at the start of the visit.
* **In Audience at end of visit**: The visitor was in the audience at the end of the visit.