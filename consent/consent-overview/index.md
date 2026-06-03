---
title: Tealium consent overview
description: Learn how Tealium enforces user consent across client-side and server-side platforms, and choose the right solution for your setup, whether using a commercial consent management platform, custom tool, or Tealium-supported consent capture.
url: https://docs.tealium.com/consent/consent-overview/
---
Tealium provides flexible consent management features for various needs, helping you capture, interpret, and enforce user consent. This guide describes the Tealium consent features and how to use them across client-side and server-side environments.

## How consent enforcement works

Tealium includes built-in mechanisms to enforce consent decisions for client-side and server-side events. You define your consent policies and configure how they are applied, then enforcement components block or allow data collection and processing based on those policies.

### Client-side enforcement

Client-side consent enforcement uses the Consent Integrations Framework (UTCM) and the consent register:

* **Consent Integrations Framework (UTCM)**: Enforces consent decisions in the browser. Used by [consent integrations]() and [CookieConsent](), it blocks unconsented tags by default, queues events while awaiting consent, and ensures that only consented purposes trigger tags.

* [**Consent Register**](): A shared on-page structure that stores the user’s consent decisions and updates in real time. This allows tags, extensions, and third-party tools (like Google Consent Mode and opt-out tags) to access and act on the current consent state.

### Server-side enforcement

On the server-side, [consent orchestration]() enforces consent policies at the event level before events are processed or activated. It evaluates incoming events against purpose-based rules and blocks events that don’t meet consent conditions.

Consent orchestration applies event-level enforcement across:

* EventStream connector actions
* Functions (event-level activations)
* EventStore
* EventDB
* AudienceStream profile processing

It does not yet enforce consent on AudienceStream activations. Use [manual enforcements]() for AudienceStream until support is available.

Together, these components give you scalable, centralized, and consistent consent enforcement across your data stack, without tying enforcement to business logic or requiring additional custom development.

## About consent features and when to use them

![](/images/iq-tag-management/tealium-consent-levels.png)

|**Feature**| **When to use**|
|---| ---|
| [Consent integrations](#consent-integrations) | &lt;ul&gt;&lt;li&gt;You use a commercial consent management platform (CMP) like OneTrust, TrustArc, Didomi, or Usercentrics to capture consent and want to enforce those decisions reliably through Tealium without custom development.&lt;/li&gt;&lt;li&gt;You need Tealium to respect and enforce consent decisions from your CMP while enabling purpose-based enforcement and tag mapping.&lt;/li&gt;&lt;/ul&gt; |
| [CookieConsent consent integration](#cookieconsent-consent-integration) | &lt;ul&gt;&lt;li&gt;You want to capture and enforce user consent without relying on a commercial CMP.&lt;/li&gt;&lt;li&gt;You need a customizable, accessible consent banner that aligns with your site’s design and compliance needs.&lt;/li&gt;&lt;li&gt;You’re moving away from Tealium consent manager and need a modern, scalable alternative that works within Tealium.&lt;/li&gt;&lt;/ul&gt; |
| [Custom consent integration](#custom-consent-integration) | &lt;ul&gt;&lt;li&gt;You use a CMP or consent tool that is not supported by a prebuilt integration.&lt;/li&gt;&lt;li&gt;You built your own internal CMP or custom consent capture solution and need to connect it to Tealium.&lt;/li&gt;&lt;li&gt;You have a supported CMP but have customized it in ways that the standard prebuilt integration doesn&#39;t support.&lt;/li&gt;&lt;/ul&gt; |
| [Consent orchestration](#consent-orchestration) | &lt;ul&gt;&lt;li&gt;You need centralized, server-side enforcement of user consent at the event level across EventStream, EventStore, EventDB, AudienceStream profile processing, and server-side connectors.&lt;/li&gt;&lt;li&gt;You want to define and manage purpose-based consent policies centrally to ensure compliance with privacy laws.&lt;/li&gt;&lt;li&gt;You need to exempt specific data sources or regions that don’t require consent, while enforcing consent elsewhere.&lt;/li&gt;&lt;/ul&gt; |
| [Consent manager](#consent-manager) | &lt;ul&gt;&lt;li&gt;You have a consent manager setup and are planning to migrate to the CookieConsent consent integration.&lt;/li&gt;&lt;/ul&gt; |
| [Manual consent conditions](#manual-consent-conditions) | &lt;ul&gt;&lt;li&gt;You need to enforce visitor-level consent conditions inside AudienceStream audiences, not yet supported by consent orchestration.&lt;/li&gt;&lt;li&gt;You use manual conditions in EventStream and have not yet migrated to consent orchestration.&lt;/li&gt;&lt;/ul&gt; |

### Consent integrations

[Client-side consent integrations]() integrate with third-party CMPs. The integrations capture consent decisions from your CMP and enforce them through the Tealium Consent Enforcement Framework, so tags only fire when consent is granted.

#### Key features

* Prebuilt integrations with CMPs like OneTrust, TrustArc, Didomi, and Usercentrics.
* Editable templates you can adjust to support configuration changes.
* Purpose-based enforcement of consent.
* Tag refire option and enforcement rules.
* Conflict handling in enforcement conditions.

#### When to use consent integrations

Use consent integrations if you use a third-party CMP such as OneTrust, TrustArc, Didomi, or Usercentrics. Consent integrations offers [prebuilt integrations]() and uses the consent integrations framework to ensure only consented data is activated.

If your CMP isn’t supported by a prebuilt integration, you can use a [custom consent integration](#custom-consent-integrations) with JavaScript functions to pass consent decisions to Tealium.

#### Recommendations

* For new implementations, avoid using load rules for consent enforcement. Use consent integrations instead.
* Use a custom consent integration if no prebuilt integration is available for your CMP.

### CookieConsent consent integration

CookieConsent is a flexible, open source, WCAG-compliant consent management tool that integrates with Tealium iQ. It provides a customizable interface for capturing consent decisions. When combined with consent integrations, CookieConsent enforces those decisions so tags only fire when consent is granted. [CookieConsent consent integration]() is the recommended replacement for the [client-side consent manager]().

#### Key features

* Accessible and customizable interface for consent capture.
* Supports A/B testing of consent banners.
* Enforces consent with event queuing and retry mechanisms.
* Uses a block-by-default framework to prevent unconsented tracking.
* Supports accessibility standards.
* CookieConsent is open source and customizable, giving you control over design and user interaction while benefiting from full support and integration with the Tealium stack.

#### When to use CookieConsent consent integration

Use [CookieConsent consent integration]() if you need a complete, Tealium-managed consent solution. This option is ideal when:

* You don’t require a commercial CMP with prebuilt policies or legal guidance.
* You need a WCAG-compliant, accessible, and customizable interface to capture user consent directly on your site.
* You want to enforce consent decisions with minimal engineering effort, using the Tealium Consent Enforcement Framework for scalable, reliable enforcement.

CookieConsent works well for teams with limited technical resources or those looking for a turnkey solution for both capture and enforcement.

#### Considerations

* Recommended replacement for the client-side consent manager.
* Does not support the IAB Transparency and Consent Framework (TCF).
* Not a Google-certified CMP.

### Custom consent integration

[Custom consent integrations]() let you use a custom CMP or consent capture tool with Tealium. You create a custom integration template that captures consent decisions and enforces them using the Tealium Consent Enforcement Framework.

#### Key features

* Supports any customer-built or heavily customized CMP.
* Uses customizable JavaScript functions to integrate with the enforcement framework.
* Enables structured communication with the consent register and enforcement layers.
* Works with unsupported CMPs and unique configurations.
* Straightforward to implement and requires minimal support.

#### When to use custom consent integrations

Use a custom consent integration if you have a CMP or consent capture solution that isn’t supported by a prebuilt integration. This approach is ideal if you:

* Use a custom-built CMP.
* Use a commercial CMP with a nonstandard or highly customized configuration.
* Need to integrate an internal consent tool into the Tealium Consent Enforcement Framework.

#### Considerations

* Requires JavaScript knowledge for setup, testing, and maintenance.

### Consent orchestration

[Consent orchestration]() provides server-side enforcement of user consent at the event level. It applies rules to incoming events and blocks any processing that doesn’t meet consent conditions. By separating consent enforcement from business logic, it provides a scalable and centralized way to manage consent on the server-side.

#### Key features

* Define and manage consent rules in one place to ensure consistent enforcement across all server-side events.
* Enforce consent decisions at the event level before processing to prevent unauthorized data collection or processing.
* Integrate seamlessly with EventStream connector actions, event functions, EventStore, and EventDB.
* Controls where an event continues in AudienceStream processing (does not apply to AudienceStream activations).
* Enforce consent based on defined categories for granular control over data processing activities.

#### When to use consent orchestration

Use consent orchestration if you need centralized, rule-based consent enforcement for server-side data collection and processing. It&#39;s ideal for organizations that require centralized control over consent policies to ensure compliance with data privacy regulations.

#### Considerations

* Consent orchestration does not yet enforce AudienceStream activations or support visitor-level consent conditions (such as consent-based badges) in Audiences. Until support is added, use manual consent conditions in AudienceStream as described in [Server-side consent management]().
* Ensure that your server-side profiles are configured correctly to use consent orchestration.
* Server-side customers using the consent manager still need to implement [manual enforcements]() until migration to consent orchestration is possible.

### Consent manager

The [consent manager]() is an older client-side solution for capturing and enforcing user consent. It includes a simple, built-in user interface to collect consent choices and applies enforcement using load rules and tag configurations in Tealium iQ Tag Management.

The consent manager remains supported for existing implementations. However, for new projects, we recommend using the [CookieConsent consent integration](), which provides better flexibility, accessibility, and alignment with modern privacy standards.

#### Key features

* User interface for collecting category-level consent.
* Integration with load rules to control tag firing.
* No-code setup through the privacy manager extension.

#### When to use the consent manager

If you already use the consent manager, we recommend migrating to [CookieConsent consent integration]() to take advantage of newer features.

For all new implementations, use CookieConsent consent integration instead of the consent manager.

#### Considerations

* Still supported for existing implementations but no longer receiving new features.
* Not recommended for any new implementation.
* Less flexible and scalable than the CookieConsent solution.
* Not race-aware: Data might be processed before consent is known.
* Does not support Google Consent Mode, IAB TCF, or vendor-level consent.

### Manual consent conditions

Manual consent conditions are custom logic configured in EventStream or AudienceStream to enforce user consent directly using processing rules. This approach was commonly used before consent orchestration and is still used in some existing or transitional setups.

Instead of relying on centralized enforcement like the consent enforcement framework or consent orchestration, this method lets you define consent logic manually with rule-based conditions in your processing workflows.

#### When to use it

Use manual consent conditions if you are still transitioning from the consent manager to consent orchestration, or if you need to enforce consent in AudienceStream, which is not yet supported by consent orchestration.
You are still transitioning from consent manager to consent orchestration.

#### Limitations

* Does not use a block-by-default approach; tags may fire before consent is captured.
* Logic is coupled with business workflows, making it harder to scale or maintain.
* Higher chance of errors or non-compliance due to fragmented enforcement.
* Recommended only as a temporary solution until consent orchestration is implemented.

## FAQ

**Is the consent manager being deprecated?**

We plan to replace the consent manager with [CookieConsent consent integration](), which we recommend using for all new implementations. The consent manager is still supported for existing setups, and customers will have time to evaluate and migrate to the new tool.

**Does the new open source tool CookieConsent support consent logging?**

Not directly. However, Tealium provides a [logging extension]() that listens for consent decisions and sends them as a JSON payload to Tealium Collect (with EventDB or EventStream) or any other endpoint you configure. The extension can be lightly customized to match your system’s requirements.

**Is Tealium part of the IAB’s Transparency and Consent Framework (TCF)?**

No. Tealium does not participate in the TCF as a CMP or vendor. This applies to all Tealium consent solutions, including CookieConsent and earlier tools. You can integrate with TCF-compliant CMPs using consent integrations. For more information, see [The IAB’s Transparency and Consent Framework and Tealium](https://tealium.com/blog/data-strategy/the-iabs-transparency-and-consent-framework-and-tealium/).

**Is Tealium a Google Certified CMP?**

No. Tealium is not a Google Certified CMP. This also applies to CookieConsent and earlier consent features. However, Tealium integrates with Google Certified CMPs and supports [Google consent mode](https://docs.tealium.com/iq-tag-management/consent/google-consent-mode/) through enforcement rules. For more information, see [The IAB’s Transparency and Consent Framework and Tealium](https://tealium.com/blog/data-strategy/the-iabs-transparency-and-consent-framework-and-tealium/).

## Related documentation

* [Consent integrations]()
* [Custom consent integration]()
* [CookieConsent consent integration]()
* [Consent orchestration]()
* [Consent register]()
* [Client-side consent management]()
* [Server-side consent management]()
