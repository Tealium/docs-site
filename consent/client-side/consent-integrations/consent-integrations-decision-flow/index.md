---
title: Consent integrations decision flow
description: The article describes the consent integrations decision flow for opt-in (GDPR-style) and opt-out (CCPA-style) enforcement patterns.
url: https://docs.tealium.com/consent/client-side/consent-integrations/consent-integrations-decision-flow/
---
Client-side consent integrations provides the option for both opt-in (GDPR-style) and opt-out (CCPA-style) enforcement patterns for the supported consent management platforms (CMPs). The consent integrations decision flow in the diagram below shows how user consent decisions are handled in these enforcement patterns.

## Opt-in model

The Tealium Universal Tag (`utag.js`) does not fire tags or set cookies until a consent decision is received from the CMP. If the CMP is not active on the page or no consent decision has been made, Tealium does not run and no tags are fired.

If no consent decision is found when Tealium loads, consent integrations polls the CMP until a decision is found. During this time, all events are queued to be processed once a decision is received. If no decision is received, events remain unprocessed.

### Order of operations

When a consent decision (`implicit` or `explicit`) is available, consent integrations performs the following actions:

1. Check if Tealium is allowed to run.
1. If allowed, check if each tag can run.
1. If allowed, trigger the tags for all queued events based on the consent decision.

### Implicit consent

If the consent decision is implicit:
* Events are initially queued.  
* Tags that allow implicit consent are triggered.  
* Consent integrations continues polling the CMP for an explicit decision.  
* If an explicit decision is later provided, queued events are reprocessed to include any newly consented tags.

### Explicit consent

If the consent decision is explicit:  
* All queued events are processed according to the consent decision and then removed from the queue.  
* Polling stops.  
* Tags already triggered under implicit consent are not refired unless tag refire is enabled and new consent purposes are available.

### Updating consent after page load

When a user reopens the interactive CMP and makes a new explicit consent decision:  
* Previously processed events are not reprocessed based on the new consent decision. 
* For new events after the page has loaded, the current consent decision is retrieved from the CMP for each event. This ensures the CMP is treated as the universal source of truth for consent.

## Consent integrations consent flow

![](https://docs.tealium.com/images/iq-tag-management/consent-integrations-consent-flow.png)

When the flow reaches the step to determine if a tag can run, the following process applies for each tag and event:

### Fire tags detail

![](https://docs.tealium.com/images/iq-tag-management/consent-integrations-fire-tags.png)

## Opt-out model

The opt-out model is similar to the opt-in model, but explicit decisions are not polled. This is because the default state is assumed to allow tags to run unless the user explicitly opts out, which aligns with CCPA/CPRA-style enforcement.
