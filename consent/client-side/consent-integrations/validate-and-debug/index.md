---
title: Validate and debug consent integrations
description: This article describes how to validate and debug client-side consent integrations.
url: https://docs.tealium.com/consent/client-side/consent-integrations/validate-and-debug/
---
## Validate consent integrations before publishing

Validate and debug your consent integration by pasting the integration template into your site&#39;s JavaScript console without any other dependencies. Consent integration templates can be edited and are designed to be stand-alone, which enables debugging from the website console.

Templates can be used to [write custom integrations](), to retrieve your vendor ID, purpose keys, or ensure that the default template works for your instance of a CMP without customization before configuration. For more information about current templates with validation snippets, see [Supported vendor integrations]().


## Activate debug mode after publishing

The Tealium iQ [debug mode]() contains detailed status and error messages from your consent integrations when the feature is active, unless an exemption applies. When exempt, `window.tealiumCmpIntegration` is defined and displays your active exemption in `window.tealiumCmpIntegration.exemptionMap`.

 Use `/SENDING|\\\\*/` as a filter in the console output to show only relevant debug messages. 

## Validate consent integrations after publishing

Client-side consent integrations create a global object in the DOM called `window.tealiumCmpIntegration` that has a number of helpful properties for debugging. You can also call the component functions individually to facilitate debugging and validation. For details about the component functions, see [Custom CMP Integrations]()

### Example

This example describes how to retrieve important information about your CMP integration.

Complete the following steps to see important information about your CMP integration and confirm that it correctly captures customer decisions: 

1. Visit this [demo site](https://www.otprivacy.com/user/jmyles/TagManagerDemo/OTKicks_Tealium/index.html?otreset=false&amp;otpreview=true&amp;otgeo=IE) or any site with an active consent integration and paste the following snippet into your browser console:
    ```js
    var outputString = `${tealiumCmpIntegration.cmpName} - ${tealiumCmpIntegration.cmpCheckIfOptInModel() ? &#39;Opt-in&#39; : &#39;Opt-out&#39;} Model

    Checks:
      - vendor id:            ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
      - well-formed decision: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
      - explicit decision:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
      - consented purposes:   ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()).sort(),null, 8)}
    `
    console.log(outputString)

    ```
1. Paste the above snippet into the console of the demo site, it returns:
    ```
    OneTrust - Opt-in Model

    Checks:
      - vendor id:            b38364e4-b2c4-4349-8e4e-48cf28a35db8
      - well-formed decision: true
      - explicit decision:    false
      - consented purposes:   [
            &#34;C0001&#34;
    ]
    ```
1. Click **Accept All Cookies** on the web page and paste the same snippet again. The following output indicates that the decision was correctly understood and captured by the integration:
    ```
    OneTrust - Opt-in Model

    Checks:
      - vendor id:            b38364e4-b2c4-4349-8e4e-48cf28a35db8
      - well-formed decision: true
      - explicit decision:    true
      - consented purposes:   [
            &#34;C0001&#34;,
            &#34;C0002&#34;,
            &#34;C0003&#34;,
            &#34;C0004&#34;
    ]

    ```


## Debug collisions and Enforcement Rules after publishing

​`window.tealiumCmpIntegrations` has a number of useful properties that help you understand which integrations are enforced on a page. For instance, `loadRules` has child properties that show which consent integrations are enforced and whether there was a collision (which blocks Tealium iQ and all tags).
 - `map` and `tagBasedMap` show different views of the relationship between tag UIDs and Purpose Keys.
 - `tiqGroupName` shows the mapping of the Purpose Key to Tealium iQ itself.
 - `cmpName` shows the currently active CMP (according to the template).
 - `cmpIntegrationVersion` shows the current version of the vendor specific integration template you&#39;re using.
 - `version` shows the version of the underlying consent enforcement framework you&#39;re using.

For more information about each of the specific integration features also included in this object, see the related [documentation]() on writing custom integrations.

