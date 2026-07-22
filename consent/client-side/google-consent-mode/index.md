---
title: Google consent mode
description: This article provides an overview of Google consent mode and how to use the translation extension for consent mode mappings.
url: https://docs.tealium.com/consent/client-side/google-consent-mode/
---
Google consent mode offers two approaches to manage user consent for data collection: **Basic consent mode** and **Advanced consent mode**. Understanding these modes is crucial for complying with data privacy regulations and optimizing data collection strategies.

* **Basic consent mode**: The traditional approach where tags and connector actions are blocked if user consent is not granted. This prevents unauthorized data collection, including personally identifiable information (PII), without consent.
* **Advanced consent mode**: This approach suggests loading Google tags regardless of consent status and signaling the user's consent decision to Google. Tags then adapt by doing either of the following:

    * Using a cookie-less endpoint for anonymous data collection from users who haven't consented to tracking.
    * Using a standard endpoint for users who have provided consent.

    This advanced strategy aims to maximize data collection for analytics and ad conversions while respecting user consent for the use of PII.

It is important to consult with your legal and leadership teams to decide which consent mode aligns with your policies: either blocking data collection without consent (Basic) or adopting Google’s method to collect anonymous data for visitors who haven't consented to standard tracking (Advanced).

For more information, see [Google Ads Help: About consent mode](https://support.google.com/google-ads/answer/10000067).

## How it works

To implement Google consent mode, add a JavaScript Code extension to map consent choices to Google consent mode settings and set up the [Google Consent Mode tag](https://docs.tealium.com/google-consent-mode-tag/) with default consent settings and category mappings from your consent management platform (CMP). As visitors make their consent choices, Google consent mode tag communicates these preferences to Google tags, which then chooses the appropriate data collection endpoint (default collection endpoint or the cookie-less endpoint) to transmit data to Google. 

In both basic and advanced consent modes, you can always fire the Google Consent Mode tag since it does not transmit any data on its own. Instead, it provides signals for other tags to respond to.


## Consent purpose mapping

To map end-user consent choices to Google consent mode settings, you need a JavaScript Code extension. Use this extension to capture the end user's current consent decision for various purposes or vendors and to assign a status of either `granted` or `denied` (or `true` / `false` in specific scenarios) to the corresponding Google consent mode purpose or setting.

### JavaScript extension template

To set up the JavaScript extension, use the following template code. This should be executed after load rules and set to run always:

```js
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.google_ad_storage_consent = <your-logic-here> ? 'granted' : 'denied';
b.google_ad_user_data_consent = <your-logic-here> ? 'granted' : 'denied';
b.google_analytics_storage_consent = <your-logic-here> ? 'granted' : 'denied';
b.google_ad_personalization_consent = <your-logic-here> ? 'granted' : 'denied';
b.google_ads_data_redaction = <your-logic-here> ? 'true' : 'false';
b.google_url_passthrough = <your-logic-here> ? 'true' : 'false';
```

Replace `<your-logic-here>` with conditions that evaluate to either `granted` or `denied`, `true` or `false` as appropriate, based on the user's consent.

### Examples


<blockquote>
Your implementation will vary depending on your consent settings.
</blockquote>


#### Consent manager example

If you are using consent manager, the logic to determine consent status might be similar to this:

```
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.google_ad_storage_consent = b.consent_decision.indexOf('display_ads') !== -1  ? 'granted' : 'denied';
b.google_ad_user_data_consent = b.consent_decision.indexOf('personalization') !== -1 ? 'granted' : 'denied';
b.google_analytics_storage_consent = b.consent_decision.indexOf('analytics') !== -1 ? 'granted' : 'denied';
b.google_ad_personalization_consent = b.consent_decision.indexOf('personalization') !== -1 && b.consent_decision.indexOf('display_ads') !== -1 ? 'granted' : 'denied';
b.google_ads_data_redaction = b.consent_decision.indexOf('personalization') === -1 || b.consent_decision.indexOf('display_ads') === -1 ? 'true' : 'false';
b.google_url_passthrough = b.consent_decision.indexOf('personalization') !== -1 ? 'true' : 'false';
```

#### Example for consent integrations with OneTrust

If you are using consent integrations and OneTrust, the logic might be similar to this:

```
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.google_ad_storage_consent = b.consent_decision.indexOf('C0004') !== -1  ? 'granted' : 'denied';
b.google_ad_user_data_consent = b.consent_decision.indexOf('C0004') !== -1 ? 'granted' : 'denied';
b.google_analytics_storage_consent = b.consent_decision.indexOf('C0001') !== -1 ? 'granted' : 'denied';
b.google_ad_personalization_consent = b.consent_decision.indexOf('C0004') !== -1 && b.consent_decision.indexOf('C0003') !== -1 ? 'granted' : 'denied';
b.google_ads_data_redaction = b.consent_decision.indexOf('C0004') === -1 || b.consent_decision.indexOf('C0003') === -1 ? 'true' : 'false';
b.google_url_passthrough = b.consent_decision.indexOf('C0004') !== -1 ? 'true' : 'false';
```


<blockquote>
If you use these exact variable names, no additional mapping is required. The latest version of the Google consent mode tag uses these variables by default.
</blockquote>


### Choosing consent parameters for extensions

To identify the consent parameters to use in the JavaScript extension, follow these steps:

1. Clear your browser's cookies and cache.
1. Visit your website or staging environment with the latest consent manager or consent integrations template active.
1. If using an opt-in model (GDPR style), accept all tracking in the consent dialog.
1. Open your browser's developer tools and navigate to the console.
1. To view the `TealiumConsentRegister` object, enter `tealiumConsentRegister`. This object contains the `currentDecision` and `decisions` arrays. The `currentDecision` array includes the currently allowed purposes.

    ![](https://docs.tealium.com/images/iq-tag-management/consent-register-and-consent-integrations.png)


<blockquote>
The `currentDecision` object lists the consent options available for use in your logic with `b.consent_decision.indexOf('<Value to change>')`.
</blockquote>
