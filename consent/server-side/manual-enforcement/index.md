---
title: Manual server-side consent enforcement
description: Learn how to manually enforce consent for visitor-level server-side scenarios, and for event-level scenarios when automatic enforcement is disabled and consent orchestration is not in use.
url: https://docs.tealium.com/consent/server-side/manual-enforcement/
---
If you use manual enforcement for event-level activations, consider transitioning to consent orchestration, which provides more efficient, automated enforcement. Enabling consent orchestration disables and replaces legacy event-level server-side enforcement. For more information, see [About consent orchestration]().

Manual enforcement is required when you need to enforce visitor-level consent in AudienceStream, or when you have disabled automatic event-level consent enforcement and are not using consent orchestration. For more about disabling automatic enforcement, see [Disabling automatic enforcement]().

## Configure EventStream connector actions, functions, and EventStore

1. Identify event-level `consent attributes`.

    * If you&#39;re using the Tealium consent manager and have disabled automatic enforcement following the instructions above, you&#39;ll have an array of strings called `consent_categories_granted` on your web events that include the categories of user consent that have been granted.

    * If you&#39;re using a third-party consent manager, the `consent attributes` could be different in number, name, or type, but each event should have the relevant consent information exposed.

    * You can create a simplified version to reference downstream, depending on the complexity of the logic needed to parse the consent decision from the event.

    * We recommend labeling these attributes.

1. Include the appropriate event-level `consent attributes` in each event feed, to ensure only consented data is activated.

      ![](/images/server-side/image1.png)

## Configure AudienceStream connectors, functions, and AudienceStore

1. Create visitor-level `consent attributes` to reconcile the consent for the visitor profile:
    * These will be based on your event-level `consent attributes`, and should clearly reflect the most recent state of the visitor&#39;s reconciled cross-device consent.
    * We recommend labeling these attributes.

1. Include the appropriate visitor-level `consent attributes` in each audience, to ensure only consented data is activated.
    ![](/images/server-side/image5.png)

### Block AudienceStream profile processing in AudienceDB

Audience rules won&#39;t prevent visitor profiles from being built or written to AudienceDB.

If your policies require blocking the profile under specific conditions, set a separate string attribute for use in the AudienceStream Event Filter. For example, create a new event string attribute called `has_audiencestream_consent` that defaults to `false` and is enriched to `true` when the visitor has provided appropriate consent (based on your event-level `consent attributes`).

![](/images/server-side/image2.png)

## Best practices

* Clearly label all consent attributes to avoid confusion across teams.
* Review your enforcement logic regularly to ensure it matches current consent policies.
* Use consent orchestration where possible for event-level enforcement to reduce manual configuration.
