---
title: About consent orchestration
description: This article provides an overview of consent orchestration.
url: https://docs.tealium.com/consent/server-side/consent-orchestration/about/
---
Consent orchestration lets you centrally control consent conditions for event-level activations. It enforces user consent in real-time, ensuring that data processing aligns with user preferences and legal requirements.

Currently, only event-level enforcement is available, and [manual enforcement]() is required for audiences.

## How it works

You can organize consent rules into purpose groups with consent orchestration on the server-side. These purpose groups help you ensure that your event-level activations comply with user consent and privacy rules. When necessary, you can use exemptions to track essential data without explicit user consent.

### Event-level activations

Consent orchestration provides centralized control over consent rules for the following features:

* EventStream connector actions
* [Event functions]()
* EventStore
* EventDB
* Events that AudienceStream is allowed to process

Consent orchestration doesn&#39;t control AudienceStream activations. A future release will include support for these activations.

### Purpose Groups and Consent Policies

A purpose group is used to define and apply a consent policy which contains specific purposes for data collection or processing. Purpose groups ensure that your event-level activations only process consented data. Within each purpose group is a list of data processing purposes mapped to event-level activations to ensure that user consent is respected. Common examples of purposes include categories like **Marketing** and **Necessary**, or vendor-specific purposes such as **Google Analytics**, depending on what consent choices you offer users.

### Enforcement rules

You can use enforcement rules to manage multiple purpose groups or exemptions if you have more than one policy to enforce. For more info on what happens if more than one enforcement rule applies, see .

### Exemptions

An exemption allows data tracking under specific conditions without applying consent enforcement. Use exemptions to define clear exceptions to consent enforcement based on regulatory requirements or operational needs. This approach provides flexibility while ensuring compliance with data protection regulations.

Exemptions only apply to events that don&#39;t match the enforcement rules of any purpose group. If an event matches both an exemption and a purpose group’s enforcement rules, the purpose group is enforced. This ensures that consent is always required for events associated with enforceable purposes. Use exemptions carefully to avoid overlap with purpose group enforcement rules.

Some examples of exemptions include:

* **Region**: Apply exemptions to regions that don’t have data privacy regulations. For example, you can exempt events from countries without consent requirements. For regions with laws such as GDPR (Europe) or CCPA (California), apply purpose group enforcement instead.
* **Data source**: Use the data source key to define an exemption for a specific data source that already includes user consent, such as a file import. In this case, additional consent enforcement isn&#39;t needed.

### Conflicts between exemptions and purpose groups

Exemptions are not a way to bypass consent for events that meet the enforcement rules of a purpose group. If an event matches both an exemption and a purpose group’s enforcement rules, the purpose group is enforced. This is considered a conflict, and consent is still required.

Exemptions only apply to events that fall entirely outside the scope of any purpose group enforcement rules. For example, an event exempted based on geography must not also meet any purpose group enforcement conditions.

For more information about how conflicts are handled, see .

### Replaces legacy enforcement

This feature disables [server-side consent management](), but you can still use the `consent_categories` array in your purpose rules.

## Consent orchestration flow

![](/images/early-access/consent-orchestration-flow.png)
