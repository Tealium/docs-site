---
title: Client-side Global Privacy Control (GPC)
description: This article describes Tealium's client-side support for Global Privacy Control (GPC), a proposed browser standard that allows users to opt out of the sale or sharing of their personal data.
url: https://docs.tealium.com/consent/client-side/consent-management/global-privacy-control/client-side-support-gpc/
---
[Global Privacy Control](https://globalprivacycontrol.org/) (GPC) provides a global way to opt out of the sale or sharing of personal data at the browser level. For more information about GPC, see [About Global Privacy Control]().

The needs and requirements of our customers vary widely, so we intend to provide a flexible foundation for our customers to build upon.

This article describes Tealium&#39;s client-side support for GPC. For information on server-side support, see [Server-side Global Privacy Control]()

## Client-side support

Since the GPC signal is a simple boolean, CCPA and similar opt-out type regulations are the most relevant and accepted applications today (see [About Global Privacy Control]() for more detail).

A strict interpretation might lead to a decision that Tealium iQ shouldn&#39;t load at all if the GPC signal is set to `true`. If all the tags implemented in Tealium iQ sell or share data, this might be the right choice.

That can be implemented with a Pre Loader JavaScript extension:

```javascript
if (navigator.globalPrivacyControl === true) {
    // Tealium iQ not loaded due to Global Privacy Control opt-out signal
    window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
    window.utag_cfg_ovrd.noload = true;
}
```

### Opt-in models (like GDPR)

The GPC signal is designed for opt-out models (like CCPA/CPRA), not opt-in models (like GDPR). Tealium opt-in consent management modules (the [Explicit Consent Prompt Manager]() and the [Consent Preferences Manager]() ) do not contain GPC-related opt-out logic out of the box.

Customer needs vary widely, and our consent management modules are intended to be customized so that tailored GPC logic can be added as needed to support your organization&#39;s needs and interpretations.

### Opt-out models (like CCPA/CPRA)

#### Client-side consent integrations - opt-out cookie &#43; GPC integration

**For customers with an already active opt-out form who need cookie-based enforcement that includes GPC support.**

[Client-side consent integrations]() provide support for simple opt-out models as required by CCPA/CPRA.

This integration assumes that a user has opted out when the GPC opt-out signal or a customer-specified opt-out cookie is found. For more information on how consent integrations support GPC, see .

#### Client-side consent integrations - CMPs with GPC support

**For customers with an already active Consent Management Platform (CMP) with GPC support who only need enforcement.**

[Client-side consent integrations]() provide support for a growing list of CMPs. These CMPs typically provide GPC support as part of their decision capture, which is then enforced by Tealium iQ through the consent integration, with no additional logic or interpretation required. If your CMP isn&#39;t supported yet, custom integrations are also available.

#### Client-side consent management - opt-out privacy banner and popup

**For customers who want to fully implement their consent management in Tealium iQ.**

As of the release of `cmDoNotSell v1.2.0`, the logical flow from the diagram below is implemented in the [Opt-out Privacy Banner and Popup]().

![](/images/guides/server-side/global-privacy-control-consent-flow.png)

This behavior serves as a starting point for building a consent management solution that meets the needs of your users and your business. Discuss the specific behavior with your legal team and clearly communicate this to your users. Change or remove this behavior by editing the `cmDoNotSell` template.

#### CookieConsent with GPC support

**For customers who want to integrate the Global Privacy Control signal into their CookieConsent integration.**

For more information, see .
