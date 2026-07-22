---
title: CookieConsent consent integration
description: This guide provides detailed steps for integrating the CookieConsent open-source consent management tool with Tealium iQ.
url: https://docs.tealium.com/consent/client-side/cookieconsent-consent-integration/
---
CookieConsent is a flexible, open source consent management tool that can be enforced with client-side [consent integrations](https://docs.tealium.com/about-consent-integrations/). This guide outlines how to configure CookieConsent using consent integrations in Tealium iQ. Combined with consent integrations, CookieConsent offers a better experience and additional features not found in the [Tealium consent manager](https://docs.tealium.com/about-consent-management/), including:

* A/B testing for consent banners.
* Robust enforcement and [queue system](https://docs.tealium.com/consent-integrations-decision-flow/) to ensure no un-consented data is tracked.
* Better accessibility support.
* A block-by-default framework to help prevent issues caused by user errors. For more information, see [iq-tag-management/consent/consent-integrations/enforcement-conditions-conflict](https://docs.tealium.com/iq-tag-management/consent/consent-integrations/enforcement-conditions-conflict/).
* Collect (and similar tags) can be set to [refire](https://docs.tealium.com/about-consent-integrations/#tag-refire), triggering both "necessary" and "targeting" tracking on the server-side with clearly marked events to avoid duplicate tracking.

## Comparing CookieConsent with CMP integrations

CookieConsent offers flexibility and control without introducing a new vendor. However, it does not support IAB TCF or provide legal guidance. Use the summary below to help you compare CookieConsent (with Tealium) to commercial consent management platforms (CMPs) integrated into Tealium iQ.

| Capability | CookieConsent | CMP Integration |
|---------|---------------|-----------------|
| Easy to enforce with Tealium iQ | ✓ | ✓ |
| Tealium consent register makes consent decisions accessible and updates easy to subscribe to | ✓ | ✓ |
| Offers consent logging and storage | ✓ | ✓ |
| Easy to customize for your company’s design requirements | ✓ | ? |
| Easy to tailor to your company’s legal requirements | ✓ | ? |
| Easily meet web accessibility standards (WCAG) | ✓ | ? |
| Offers vendor-specific opt-outs | ✓ | ? |
| No new vendor onboarding or reviews required (hosted on Tealium’s content delivery network) | ✓ | ✗ |
| No additional subscription required (storing consent logs or accessing support may incur additional costs) | ✓ | ✗ |
| Supports IAB TCF, useful for websites that show on-site advertising. | ✗ | ✓ |
| Offers pre-configured settings based on privacy regulations such as GDPR or CCPA | ✗ | ✓ |
| Offers legal guidance | ✗ | ✓ |

Capabilities marked with `?` vary based on the specific CMP provider. Some CMPs support these features such as accessibility support or vendor-specific opt-outs, while others may not. Review the documentation of your CMP to confirm support for these features.


<blockquote>
CookieConsent does not support the IAB Transparency and Consent Framework (TCF) required by some publishers and advertising platforms. If your organization requires IAB TCF support or a Google-certified CMP, use an alternative solution. For more information, see [CookieConsent: Is it the right tool for you?](https://cookieconsent.orestbida.com/essential/introduction.html#is-cookieconsent-the-right-tool-for-you) and [The IAB’s Transparency and Consent Framework and Tealium](https://tealium.com/blog/data-strategy/the-iabs-transparency-and-consent-framework-and-tealium/).
</blockquote>


## Who's this for?

CookieConsent is a consent management tool that provides a flexible, open source approach to managing user consent. Unlike a full CMP, which typically includes additional features such as policy enforcement, analytics, and vendor compliance management, CookieConsent is designed to be a transparent, opinion-free tool that allows businesses to implement consent controls according to their specific needs.

If you need a customizable and developer-friendly tool that seamlessly integrates with Tealium, CookieConsent is a great option. However, if you require a comprehensive CMP solution, including IAB Framework support or Google-certified consent management, you will need an alternative solution.

## Requirements

Creating a CookieConsent consent integration requires the following:

* Tealium iQ Tag Management
* Client-side consent integrations

### Why use it?

CookieConsent replaces the [consent manager](https://docs.tealium.com/about-consent-management/) for customers who seek a robust, non-commercial consent management tool. It delivers a dependable consent capture layer with flexible and robust enforcement, which can be tailored to meet complex compliance needs.

### Categories, services, and purposes explained

CookieConsent V3 supports both categories and service-level consent options:

* **Categories** are broad groups of purposes for data processing, such as `necessary` or `functional`. These define high-level groupings of data use cases.
* **Services** are specific vendors or sub-purposes within a category, such as `necessary-vendor1`. Services allow for more granular consent settings by defining individual entities or distinct purposes within a category.

Service names combine the category name with either the vendor or sub-purpose name using a hyphen prefix for transparency. For example, within a `necessary` category, services might include `necessary-vendor1` or `necessary-subpurpose1`.

**Example use cases**

* **Vendor-based service**: In the `analytics` category, an example of a service is `analytics-google_analytics`, representing a specific vendor providing analytics capability.
* **Sub-purpose-based service**: In the `functional` category, an example of a service is `functional-session_tracking`, representing a sub-purpose for functional cookies related to tracking user sessions.

If services are defined within a category, the category itself is no longer available for mapping. For example, if the `necessary` category includes services such as `necessary-vendor1` and `necessary-vendor2`, only those specific services are available for mapping.

**Consent behavior:**

* In opt-in mode, both the category and its services are allowed.
* In opt-out mode, all except `targeting` are allowed.

## Integration steps

Complete the following steps to set up the CookieConsent integration in Tealium iQ:

1. [Load the CookieConsent library](#step-1-load-the-cookieconsent-library).
1. [Implement consent logging](#step-2-implement-consent-logging).
1. [Create a CookieConsent v3 integration and enforcement rule](#step-3-create-a-cookieconsent-v3-integration-and-enforcement-rule).
1. [Create purpose group](#step-4-create-purpose-group).
1. [Save and publish Tealium iQ profile](#step-5-save-and-publish-tealium-iq-profile).
1. [Test and troubleshoot](#test-and-troubleshoot).

### Step 1: Load the CookieConsent library

Load the CookieConsent library on your site and configure it to display the consent banner and modal with your chosen categories, layout, language, and behavior.

Load the library and configuration in one of the following ways:

* Use the CookieConsent v3 Loader extension in Tealium iQ to load the library and apply your configuration. For information on how to configure the extension, see [CookieConsent v3 Loader extension](https://docs.tealium.com/cookieconsent-v3-loader-extension/).
* Embed the CookieConsent v3 loader script and configuration code directly on your site.

### Step 2: Implement consent logging

Capture and record consent preferences and decisions for reporting or compliance purposes.

Implement consent logging in one of the following ways:

* Use the CookieConsent v3 Logging extension in Tealium iQ. This extension listens for consent updates from the CookieConsent banner and sends the decision details as a JSON payload to your specified endpoint. Configure the destination by updating the extension configuration code. For information on how to configure the extension, see [CookieConsent v3 Logging extension](https://docs.tealium.com/cookieconsent-v3-logging-extension/).
* Embed the CookieConsent v3 logging extension code directly on your site.

### Step 3: Create a CookieConsent v3 integration and enforcement rule

Set up the CookieConsent v3 consent integration and define rules to enforce consent. This step links CookieConsent to your consent logic in Tealium iQ, ensuring that tags fire only when the user has given appropriate consent.

1. Go to the **Tag Management > Consent Integrations** section.
1. Click **Add Integration**.
1. Enter a name for the integration that clearly identifies its purpose.
1. Select **CookieConsent v3** from the vendor drop-down list.
1. Click **Next**.
1. Define appropriate enforcement rules. Include exemptions as needed for specific use cases.
    
<blockquote>
Avoid overlapping enforcement rules with other integrations or exemptions to prevent conflicts. For more information, see [Handling conflicts in enforcement conditions](https://docs.tealium.com/enforcement-conditions-conflict/).
</blockquote>

1. Click **Next**.
1. Select a publish location and click **Next**.

### Step 4: Create purpose group

If one doesn't already exist, create a purpose group to define and map consent categories and services captured by CookieConsent to tags in Tealium iQ.

1. Select **+ New Purpose Group** from the purpose group drop-down list.
1. Click **Create Purpose Group**.
1. Enter a name and description.
1. Click **Next**.
1. Create purposes:
    * From your `ccConfig.categories` in the [CookieConsent v3 Loader extension](#step-1-configure-the-cookieconsent-v3-loader-extension) configuration code, add a purpose for each service or vendor. Only add a category-level purpose if no services or vendors exist in that category.
    * For each purpose, use the service key within the category such as `necessary-necessary_vendor1` to map consent decisions in the purpose group. Only use a category key such as `necessary` if no services are defined in that category.
1. Click the **Tealium iQ Purpose** tab.
1. To ensure Tealium iQ always loads, assign Tealium iQ to a purpose that users cannot opt out of, such as **Strictly Necessary**.
1. Click the **Map Tags** tab.
1. Assign each tag to an appropriate purpose.
1. Enable tag refiring if you want tags, such as the Tealium Collect tag, to refire when consent is updated in the same event.
1. Click **Save** to save the purpose group.
1. Click **Save** to save your consent integration.
1. Save and publish the Tealium iQ profile to generate the template for your new integration.

### Step 5: Save and publish Tealium iQ profile

Save and publish the Tealium iQ profile to the **Dev** environment and test before publishing to the **Prod** environment. You have now successfully configured CookieConsent with client-side consent integrations.

## Test and troubleshoot

Use the [Tealium Tools Environment Switcher](https://docs.tealium.com/environment-switcher/) to preview your implementation across environments and verify that your consent integration is working as expected.

### Verify your consent integration setup

1. Visit your site and accept tracking.
1. Open the Developer Tools JavaScript console.
1. Use the following commands in your browser's Developer Tools to test:
    * `CookieConsent.show(true)` to display the banner.
    * `CookieConsent.showPreferences(true)` to show the preferences dialog.
1. Validate the following:
    * The banner and preference dialog display correctly.
    * The consent decision is stored in the `cc_cookie` cookie.
    * Use the **Consent Register** in Developer Tools to monitor consent activity.
    * Only tags with valid consent are allowed to fire.

Clear the CookieConsent cookie (`cc_cookie` by default) between decisions to reset consent status.

For more information about validating enforcement and debugging issues, see [Validate and debug consent integrations](https://docs.tealium.com/validate-and-debug-consent-integrations/).

### Tests

For a suite of end-to-end integration tests for CookieConsent and consent integrations, see [CookieConsent + Tealium iQ - End-to-end integration tests](https://solutions.tealium.net/hosted/cookieconsent/integration-test-report/summary.html).

## Integrate Global Privacy Control (GPC)
 
This integration suppresses the consent banner when GPC is active, honors explicit visitor decisions over GPC, and still lets visitors open the banner manually. It also handles scenarios where GPC is later disabled by falling back to implicit consent rules, ensuring previously consented visitors are not incorrectly treated as opted out.


<blockquote>
This approach is provided for technical guidance only. The decision to detect, honor, or prioritize Global Privacy Control (GPC) signals must be made in consultation with your organization's legal team. Your legal team should determine when GPC behavior must be applied, which consent states it should influence, and how it should interact with existing consent workflows. You are responsible for adjusting these solutions to meet your organization's legal, regulatory, and policy requirements.
</blockquote>


### How it works

The following section explains how the solution handles Global Privacy Control (GPC) signals and consent decisions in different scenarios.

**Treats GPC as an opt-out signal**  
This solution treats the Global Privacy Control (GPC) signal as a complete opt-out for consent enforcement. When a GPC signal is detected, it suppresses the consent banner on the visitor's initial visit and during subsequent page loads or standard interactions.

**Preserves consent banner and preferences interactions**  
Visitors can still open the consent banner or preferences dialog manually, for example by clicking a footer link. When opened, CookieConsent shows the visitor as opted out of all optional tracking due to the GPC signal.

**Enforces explicit consent decisions**  
This solution ignores the Global Privacy Control (GPC) signal when a visitor has made an explicit consent decision. If a consent cookie exists, the visitor's choice takes precedence over the GPC opt-out signal, allowing the banner and consent preferences to display and function according to the visitor's selection.

**Fall back to implicit consent decisions**  
This solution relies on the default implicit consent decisions if the Global Privacy Control (GPC) signal is deactivated on a device where it was previously active.

### Code

Add this code to the CookieConsent V3 Loader extension, between the `ccConfig` definition and the call to `CookieConsent.run()`.

This solution has been proposed to the official CookieConsent project. Follow updates here: https://github.com/orestbida/cookieconsent/issues/811


```js
// For testing, set this to true or false but make sure to change it back in prod
var gpcFlagIsTrue = navigator.globalPrivacyControl 
var noDecisionYet = typeof readCookie((ccConfig.cookie && ccConfig.cookie.name) || 'cc_cookie' ) !== 'string' // will be a string if already set
// disable anything optional when the GPC flag is true in opt-out mode (like the CCPA)
if (gpcFlagIsTrue && ccConfig.mode === 'opt-out' && noDecisionYet) {
    logMessage('Enforcing the GPC flag by suppressing all optional tracking and the initial banner pop-up in opt-out mode - no cookies set.')
    Object.keys(ccConfig.categories).forEach(function (cat){
        var thisCat = ccConfig.categories[cat]
        if (thisCat && thisCat.enabled === true && thisCat.readOnly !== true) {
            thisCat.enabled = false
        }
    })
    ccConfig.onModalShow = function (modalNameObj) {
        window.tealiumCmpIntegration = window.tealiumCmpIntegration || {};
        var modalName = modalNameObj.modalName;
        var alreadySuppressed = window.tealiumCmpIntegration.gpcAlreadySuppressedOnce === true;
        var validDecision = CookieConsent.validConsent();
        if (gpcFlagIsTrue && !validDecision && !alreadySuppressed) {
            // We have to use setTimeout here to let the 'show' finish - it breaks if you hide it while it's showing
            if (modalName === 'consentModal') setTimeout(CookieConsent.hide, 1);
            if (modalName === 'preferencesModal') setTimeout(CookieConsent.hidePreferences, 1);
            window.tealiumCmpIntegration.gpcAlreadySuppressedOnce = true    // only suppress the first pop-up, to allow it to be manually popped-up
        }
    }
}

// GPC helper functions
function logMessage (message) {
  var loggingFunction = (window.tealiumCmpIntegration && window.tealiumCmpIntegration.logger) || (window.utag && window.utag.DB)
  return loggingFunction(message);
}

function readCookie (name) {
    var reString = '(?:(?:^|.*;\\s*)' + name + '\\s*\\=\\s*([^;]*).*$)|^.*$';
    var re = new RegExp(reString);
    var cookieValue = document.cookie.replace(re, "$1");
    if (!cookieValue) return undefined;
    return cookieValue;
}
```


## Additional resources

* [Consent integration](https://docs.tealium.com/about-consent-integrations/): Reference for consent integration setup.
* [CookieConsent v3.1.0 Playground](https://playground.cookieconsent.orestbida.com/): Explore configurations and styles.
* [CookieConsent: UI Customization](https://cookieconsent.orestbida.com/advanced/ui-customization.html): Guide for UI customization.
