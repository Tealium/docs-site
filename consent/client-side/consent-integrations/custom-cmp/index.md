---
title: Custom CMP integrations
description: This article describes how to configure a custom consent management platform in client-side consent integrations.
url: https://docs.tealium.com/consent/client-side/consent-integrations/custom-cmp/
---
## How it works

Client-side consent integrations consist of two parts:

* A consent enforcement framework for Tealium iQ (the `utcm_framework` template).
* CMP-specific integration templates that leverage the Tealium iQ consent enforcement framework. These integration templates are designed to be as lightweight as possible.

Our [pre-built integrations](https://docs.tealium.com/vendor-specific-configuration/) supports integration with various consent management platforms (CMPs). However, there are instances where a custom integration is recommended, such as:

* Using a CMP without a pre-built integration.
* Using an internal tool to capture consent.
* Using a supported CMP with extensive customizations that break the standard integration.

In such cases, you can use a custom integration. By using JavaScript functions, any consent capture tool can leverage the enforcement framework.

To add a new custom integration, use the existing integrations and the provided template as a guide.

The following describes a basic workflow for creating a custom integration:
1. Develop and debug the integration outside Tealium iQ (website where CMP is implemented).
1. In Tealium iQ, add a new custom consent integration and purpose group. For more information, see [Manage consent integrations and purpose groups](https://docs.tealium.com/manage-consent-integrations/).
1. Assign Tealium iQ and the appropriate tags to the purposes within the purpose group.
1. To create the template, save your profile.
1. Edit the newly created template. For details, see [manage-templates](https://docs.tealium.com/manage-templates/).
1. Publish the template to a development or test environment to verify that everything works as expected, and then follow your normal testing and publishing flow.

## Integration functions

The CMP-specific component of the integration is defined using the `window.tealiumCmpIntegration` object.

The `window.tealiumCmpIntegration` object consists of a name `.cmpName`, version `.cmpIntegrationVersion`, and the following functions:

### Determine operating mode

* `.cmpCheckIfOptInModel` - determines whether the integration should operate on the `opt-in` or `opt-out` model. Returns a boolean value.

### Fetch decision

* `.cmpFetchCurrentConsentDecision` - retrieves the current raw version of the consent decision (raw version, from the CMP). The result must be an object and is passed as an argument to all subsequent functions.

### Validate and standardize the decision

* `.cmpCheckForWellFormedDecision` - checks if the raw version of the consent decision is well-formed and understandable. Returns a boolean value.

* `.cmpCheckForTiqConsent` - determines whether the raw consent decision contains permission for data processing by Tealium iQ. If false, nothing is executed. Returns a boolean value.

* `.cmpCheckForExplicitConsentDecision` - determines whether the raw consent decision is `explicit` or `implicit`. Returns a boolean value.

* `.cmpConvertResponseToGroupList` - converts the raw decision into a simple array of allowed purpose keys for downstream enforcement. Returns an array of consented purpose keys.


<blockquote>
The purpose keys returned by `cmpConvertResponseToGroupList` must exactly match the purpose names configured in the consent integration. The **Vendor ID** field in the Tealium iQ UI is used by the template to identify the relevant CMP cookie or identifier. Ensure this value matches the cookie name or identifier in your CMP use cases. It is case-sensitive.
</blockquote>


### Monitor and trigger consent updates

* `.cmpAddCallbackToTriggerRecheck` - registers a callback function to be invoked whenever the CMP's consent status changes. This ensures Tealium iQ is promptly updated with the latest consent decisions without relying on polling.

  Ensure that `cmpAddCallbackToTriggerRecheck` is configured to call `triggerRecheck()` whenever the CMP signals a consent status change through callbacks or alternative implementation methods. Call `triggerRecheck()` when the banner pops up for implicit consent or at a similar point in the CMP load. See the comments in the [custom integration template](#custom-integration-template) for more details. For integrations that currently support callbacks, see [vendor-specific-configuration](https://docs.tealium.com/vendor-specific-configuration/).

## Custom integration template

To create your custom CMP integration, edit the blank template below to meet your CMP requirements. See the comments in the template for a working example. The template includes a debugging snippet at the end of the template that you can use to debug and validate your consent integration.



```js
;(function myCustomConsentIntegration (window) {
  /**
    * This template is meant to be edited, for you to build your own support for a custom CMP / capture tool.
    *
    * The example code (commented out) is taken from an integration that checks for an opt-out cookie and returns one of two decisions:
    *  - ['no-selling'] (opt-out cookie with any value found) - always an explicit decision (an opt-out cookie has been set)
    *  - ['no-selling', 'yes-selling'] (no opt-out cookie found) - always an implicit decision (no cookie is set)
    *
    * The (case-sensitive) name of the opt-out cookie is taken from the 'Vendor ID' field in the UI.
    *
    * For more, see https://docs.tealium.com/iq-tag-management/consent-integrations/supported-vendors/#opt-out-cookie--gpc
    *
    * (The above integration was simplified for this example - the GPC logic was removed)
    */

  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Custom Example'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'v1.1.0'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList

  // REMOVE THE BELOW LINE (comment it out) if you want to use polling / your solution doesn't support a callback
  window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck;

  /*
  // pull whatever's been entered as the Vendor ID in the UI for the single relevant integration
  var optOutCookieName = (window.tealiumCmpIntegration && window.tealiumCmpIntegration.map && Object.keys(window.tealiumCmpIntegration.map)[0]) || 'error-no-map-found-so-no-cookie-name-available'
  */

  // Should return a boolean, true if the CMP is running the 'Opt-in' model (GDPR style)
  // This opt-out cookie example only supports the Opt-out model (CCPA/CPRA style), so this is hardcoded to return false.
  function cmpCheckIfOptInModel () {
    /*
    return false
    */
  }

  // Should return some CMP-specific raw object (must be an object) that contains the needed information about the decision.
  // This output is used as the cmpRawOutput argument in functions below.
  function cmpFetchCurrentConsentDecision () {
    /*
    // we can't use any tag manager functionality here because it hasn't been allowed to load yet
    var readCookie = function (name) {
      var reString = '(?:(?:^|.*;\\s*)' + name + '\\s*\\=\\s*([^;]*).*$)|^.*$'
      var re = new RegExp(reString)
      var cookieValue = document.cookie.replace(re, '$1')
      if (!cookieValue) return undefined
      return cookieValue
    }
    var cookie = readCookie(optOutCookieName) || 'opt-out-cookie-not-found'
    return { cookieState: cookie } // we have to return an object for the integration to work - this lets us add in other properties (like Global Privacy Control) later
    */
  }

  // Should return a string that helps Tealium iQ confirm that it's got the right CMP configuration (and not one from some other page / customer of the CMP)
  function cmpFetchCurrentLookupKey () {
    /*
    return optOutCookieName
    */
  }

  // Should return a boolean - true if the raw decision meets our expectations for the CMP
  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    /*
    return typeof cmpRawOutput === 'object' && typeof cmpRawOutput.cookieState === 'string'
    */
  }

  // Should return a boolean - true if the consent decision was explicitly made by the user
  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    /*
    // The only way we can tell if the decision is explicit in this example is to check if an opt-out cookie is set
    if ((typeof cmpRawOutput === 'object' && typeof cmpRawOutput.cookieState === 'string' && cmpRawOutput.cookieState !== 'opt-out-cookie-not-found')) return true
    return false
    */
  }

  // Should return an array of consented vendors/purposes - these should match the Purposes in Tealium iQ exactly
  function cmpConvertResponseToGroupList (cmpRawOutput) {
    /*
    var consentDecision = ['no-selling'] // tags that don't sell/share data are always allowed
    // very simple check for a non-empty opt-out cookie to determine if tags that sell data are allowed
    if (cmpRawOutput.cookieState === 'opt-out-cookie-not-found') {
      consentDecision.push('yes-selling') // we don't see a cookie, so we have to assume selling/sharing data is fine
    }
    return consentDecision
    */
  }

  // Use the incoming callback feature to avoid some polling when the underlying framework supports it
  // It's better to call the triggerRecheck function too often (no negative impact) than too little (missed consent changes and the corresponding data).
  // Make sure to call triggerRecheck every time the CMP has a change in consent status, such as:
  //  - initial consent pop-up (implicit consent in opt-in model)
  //  - explicit consent changes
  //  - initial CMP load when a previous decision has been made
  // If this function isn't included in the window-scoped object, polling will be used instead
  function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
    // this example sets up a listener for cookie changes to stay consistent with the example, but you can listen for anything appropriate
    /*
    (function() {
        // Original document.cookie descriptor
        const originalCookieDescriptor = Object.getOwnPropertyDescriptor(Document.prototype, 'cookie');

        // Create a custom event
        function emitCookieChange(value) {
          const event = new CustomEvent('cookieUpdated', {
            detail: {
              cookies: value
            }
          });
          document.dispatchEvent(event);
        }

        // Override the document.cookie property
        Object.defineProperty(document, 'cookie', {
          get: function() {
            return originalCookieDescriptor.get.call(document);
          },
          set: function(value) {
            originalCookieDescriptor.set.call(document, value);
            emitCookieChange(value);
          }
        });
      })();

      // Example listener
      document.addEventListener('cookieUpdated', (e) => {
        // trigger the callback function when the opt-out cookie is updated (some false positives are fine here)
        if ((e.detail.cookies.indexOf(optOutCookieName)) !== -1) {
            triggerRecheck();
        }
      });
    */
  }

  // You shouldn't need to change this function, or anything below it
  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    // treat things we don't understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false

    tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
    return allowedGroups.indexOf(tiqGroupName) !== -1
  }
})(window)

/*
  // Debugging / development output - uncomment this block, then paste/repaste this entire template on your test pages
  var outputString = `${tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

  Checks:
    - id:          ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
    - well-formed: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - explicit:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - group list:  ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}
  `
  console.log(outputString);
*/
```


## Develop and debug before publishing

To create your custom CMP integration, edit the [custom integration template](#custom-integration-template) to meet your CMP requirements. See the comments in the custom template for a working example.

Complete the following steps to debug during development:
1. Uncomment the **Debugging** block at the end of the [custom integration template](#custom-integration-template).
1. Paste the template into the console of a website running the CMP you want to support.
1. The debugging code block outputs the consent decision.
1. Customize your decision and paste the template again to see the newly interpreted consent decision.
1. When you are satisfied with your template, comment out the debugging block again before pasting and publishing it to Tealium iQ.

You can also find the debugging snippet by saving your profile and [editing the template](https://docs.tealium.com/manage-templates/).

## Validate after publish

There are two ways to debug and validate your template after publishing: using debug mode or using the `window.tealiumCmpOutput` object.

### Using debug mode

To use [debug mode](https://docs.tealium.com/debugging/):
* Set the `utagdb` cookie to `true` with `document.cookie = "utagdb=true"` in the console.
* Set your console filter to see only the relevant output (the suggested filter is in the debug output).
* Test different options to make sure things work as expected.

### Using the `window.tealiumCmpOutput` object

To use the `window.tealiumCmpOutput` object:
* Paste the commented out debugging code block at the bottom of the template into the console to output only your decision and related output.
* If needed, you can also call the functions in the template individually or access the other useful properties of this object.

For more detailed debugging tips for prebuilt and custom integrations, see [Validate and debug consent integrations](https://docs.tealium.com/validate-and-debug-consent-integrations/).
