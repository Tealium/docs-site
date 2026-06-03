---
title: Consent management
description: Learn about the consent management feature for mobile.
url: https://docs.tealium.com/platforms/getting-started-mobile/consent-management/
---

Tealium consent management adds consent and data privacy support to your mobile app. It also adds the ability to prompt your users for consent, retain their selection, and honor that selection throughout the tracking behavior.

The behavior of the consent manager is controlled by a consent policy, which is based on the region of the app user.

## Consent Policies

The Tealium consent manager is designed to support multiple regulatory requirements and can be adapted to support new ones as they emerge. These policies are configured at initialization time by setting the `TealiumConfig` `consentPolicy` property.

### GDPR

Tealium iQ Tag Management and EventStream support the General Data Protection Regulation (GDPR) as the default policy.

| Consent Status |  Description |
| :-- | :-- |
| **Not Set** (default)| Tracking calls are queued locally until consent status is set. |
| **Consent** | Tracking calls are sent.&lt;br&gt;Consent categories are included in all tracking calls.&lt;br&gt;If consent logging is enabled the `grant_consent` event is sent. |
| **Declined**  | Tracking calls are not sent.&lt;br&gt;If consent logging in enabled the `decline_consent` event is sent. |

### CCPA

Tealium iQ Tag Management supports the California Consumer Privacy Act (CCPA) policy.

| Consent Status |  Description |
| :-- | :-- |
| **Not Set** (default)| Tracking calls are sent.&lt;br&gt;The [`do_not_sell`](#data-layer) flag is set to `false`.&lt;br&gt;Tags are unaffected. |
| **Consent** | Tracking calls are sent.&lt;br&gt;The [`do_not_sell`](#data-layer) flag set to `false`.&lt;br&gt;Tags are  unaffected. |
| **Declined**  | Tracking calls are sent.&lt;br&gt;The [`do_not_sell`](#data-layer) flag is set to `true`.&lt;br&gt;Tags configured in the &#34;Affected Tags&#34; section of the [CCPA consent manager](/iq-tag-management/consent-management/privacy-banner-and-popup/manage/) are not triggered. |

## Available Actions

The following actions are available with the consent management module.

 * Set Consent Status
 * Set User Consent Categories
 * Reset User Consent Preferences
 * Set Consent Logging Enabled
 * Set Consent Policy
 * Get Consent Policy

## Supported Platforms

Support for the following libraries is provided:

* [Android (Java)](/platforms/android-java/consent-management/) - Included in the library and enabled in the native code upon initialization.
* [Android (Kotlin)](/platforms/android-kotlin/consent-management/) - Included in the library and enabled in the native code upon initialization.
* [Cordova](/platforms/cordova/)
* [iOS (Objective-C)](/platforms/ios-objective-c/consent-management/) - Included in the CocoaPods framework builds.
* [iOS (Swift)](/platforms/ios-swift/consent-management/) - Included and enabled in Carthage and CocoaPods framework builds when the `ConsentManager` module is added to your Podfile.
* [React Native](/platforms/react-native/)
* [Xamarin](/platforms/xamarin/consent-mangagement/)

For a full feature comparison, see the [Mobile Feature Comparison]().   

## Data Layer

The following data layer variables are included with each tracking call when the consent management module is in use:

| Variable Name | Description | Examples  |
| --- | --- | --- |
| `policy` | The policy under which consent was collected (default: `gdpr`) | `gdpr` or `ccpa` |
| `consent_status` | The user&#39;s current consent status | `consented` or `notConsented` |
| `consent_categories` | An array of the user&#39;s selected consent categories | `[&#34;analytics&#34;, &#34;cdp&#34;]` |
| `do_not_sell` | Only set if the CCPA consent policy is active | `true` or `false` |
