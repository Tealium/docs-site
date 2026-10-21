---
title: Supported vendor integrations
description: This article describes the supported CMPs in client-side consent integrations and how to easily gather the relevant vendor-specific information to complete your consent integrations setup.
url: https://docs.tealium.com/consent/client-side/consent-integrations/supported-vendors/
---
## How it works

Client-side consent integrations support integration with various consent management platforms (CMPs). You can access relevant vendor-specific information from the user interface of the supported consent management platforms (CMP) or the web page. To keep this documentation reliable and user-friendly, this section only covers the steps to retrieve vendor specific information from the web page. For steps to retrieve your Vendor ID and Purposes in the user interface of each partner CMP, see the respective CMP documentation.

To retrieve the relevant information from the web page, follow these steps:

1. Visit your website where the CMP is implemented.
1. Accept all tracking.
1. Open the Developer Tools JavaScript console.
1. Paste the CMP-specific code from the code snippets below into the Developer Tools JavaScript console.
1. Enter the displayed **Vendor ID**, **Purpose Keys** and **Purpose Names** into your consent integration.


<blockquote>
After you update your consent decision, paste the code again to see the latest interpretation.
</blockquote>


## Integration-specific instructions and code snippets

### Cookiebot

Test this snippet on [cookiebot.com](https://www.cookiebot.com/) or on your website by following the instructions in the [How it works section](#how-it-works) to check compatibility and get the information needed for integration.


```js

;(function cookiebotIntegration (window) {
    window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}
    window.tealiumCmpIntegration.cmpName = 'Cookiebot'
    window.tealiumCmpIntegration.cmpIntegrationVersion = 'v1.0.0'
    window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
    window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
    window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
    window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
    window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
    window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
    window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
    // Should return a boolean, true if the CMP is running the 'Opt-in' model (GDPR style)
    function cmpCheckIfOptInModel () {
      if (!window.Cookiebot || !window.Cookiebot.regulations || typeof window.Cookiebot.regulations.gdprApplies !== 'boolean') return false
      return Cookiebot.regulations.gdprApplies
    }
    // Should return some CMP-specific raw object (must be an object) that contains the needed information about the decision.
    // This output is used as the cmpRawOutput argument in functions below.
    function cmpFetchCurrentConsentDecision () {
      if (!window.Cookiebot || typeof window.Cookiebot.hasResponse !== 'boolean') return false
      return cmpRawOutput = window.Cookiebot.consent;
    }
    // Should return a string that helps Tealium iQ confirm that it's got the right CMP configuration (and not one from some other page / customer of the CMP)
    function cmpFetchCurrentLookupKey() {
        if (!window.Cookiebot || typeof window.Cookiebot.serial !== 'string') return false
        return Cookiebot.serial
    }
    // Should return a boolean - true if the raw decision meets our expectations for the CMP
    function cmpCheckForWellFormedDecision (cmpRawOutput) {
      return typeof cmpRawOutput === 'object' &&  typeof cmpRawOutput.stamp ==='string'
    }
    // Should return a boolean - true if the consent decision was explicitly made by the user
    function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
      // The only way we can tell if the decision is explicit in this example is to check if an opt-out cookie is set
      return cmpRawOutput.method === 'explicit'? true : false;
    }
    // Should return an array of consented vendors/purposes - these should match the Purposes in Tealium iQ exactly
    function cmpConvertResponseToGroupList(cmpRawOutput) {
        var consentDecision = []
        // very simple check for a non-empty opt-out cookie to determine if tags that sell data are allowed
        if (cmpRawOutput.necessary) {
            consentDecision.push('necessary') // we don't see a cookie, so we have to assume selling/sharing data is fine
        }
        if (cmpRawOutput.preferences) {
            consentDecision.push('preferences') // we don't see a cookie, so we have to assume selling/sharing data is fine
        }
        if (cmpRawOutput.marketing) {
            consentDecision.push('marketing') // we don't see a cookie, so we have to assume selling/sharing data is fine
        }
        if (cmpRawOutput.statistics) {
            consentDecision.push('statistics') // we don't see a cookie, so we have to assume selling/sharing data is fine
        }
        return consentDecision
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


### Didomi (legacy)

Test this snippet on [didomi.io](https://didomi.io) or on your website by [following the instructions above](#how-it-works) to check compatibility and get the information needed for integration.

The Didomi (legacy) integration uses **Vendors** as **Purposes**.


<blockquote>
Didomi (legacy) does not return implicitly consented purposes or vendors. To enable implicit triggering, this integration unconditionally adds the purpose key `always_consented` to outbound consent decisions. For new setups, use [Didomi v2](#didomi-v2). The v2 integration does not need this workaround.
</blockquote>



```js
;(function didomiIntegration (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Didomi'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'didomi-1.0.1'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject

  function cmpCheckIfOptInModel () {
    if (!window.Didomi || typeof window.Didomi.getConfig !== 'function') return false
    return window.Didomi.getConfig().notice.type === 'optin'
  }

  function cmpFetchCurrentConsentDecision () {
    if (!window.Didomi || typeof window.Didomi.getUserStatus !== 'function') return false
    if (typeof window.Didomi.getConfig !== 'function') return false
    var cmpRawOutput = {}
    cmpRawOutput.userStatus = window.Didomi.getUserStatus()
    cmpRawOutput.vendorInfo = window.Didomi.getVendors()
    cmpRawOutput.shouldConsentBeCollected = window.Didomi.shouldConsentBeCollected()
    return cmpRawOutput
  }

  function cmpFetchCurrentLookupKey () {
    if (!window.Didomi || typeof window.Didomi.getConfig !== 'function') return ''
    var id = window.Didomi.getConfig().app.deploymentId
    return id || ''
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    // treat things we don't understand as an opt-out
    if (typeof cmpRawOutput !== 'object') return false
    if (typeof cmpRawOutput.userStatus !== 'object') return false
    // do more checks than strictly necessary to confirm expectations
    if (typeof cmpRawOutput.userStatus.purposes !== 'object') return false
    if (typeof cmpRawOutput.userStatus.vendors !== 'object') return false
    if (typeof cmpRawOutput.userStatus.purposes.global !== 'object') return false
    if (typeof cmpRawOutput.userStatus.vendors.global !== 'object') return false
    if (toString.call(cmpRawOutput.userStatus.purposes.global.enabled) !== '[object Array]') return false
    if (toString.call(cmpRawOutput.userStatus.vendors.global.enabled) !== '[object Array]') return false

    if (typeof cmpRawOutput.vendorInfo !== 'object') return false

    if (typeof cmpRawOutput.shouldConsentBeCollected !== 'boolean') return false
    return true
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    // treat things we don't understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
    return cmpRawOutput.shouldConsentBeCollected === false // false after an explicit decision is made
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    // Didomi handles checking each vendor's required purposes
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return []
    // enforce strings, even for IAB vendor ids

    const decision = cmpRawOutput.userStatus.vendors.global.enabled.map(function (vendorId) {
      return String(vendorId)
    })

    decision.push('always_consented')
    return decision
  }

  function cmpConvertResponseToLookupObject (cmpRawOutput) {
    var allowedVendors = cmpConvertResponseToGroupList(cmpRawOutput)
    var allVendors = cmpRawOutput.vendorInfo
    var lookupObject = {}
    // WORKAROUND to allow implicit triggering until the Didomi bug is fixed
    lookupObject.always_consented = 'Always consented (to allow strictly needed triggering)'
    allVendors.forEach(function (vendorObject) {
      if (allowedVendors.indexOf(String(vendorObject.id)) === -1) return
      lookupObject[vendorObject.id] = vendorObject.name || 'iab-vendor-' + vendorObject.id
    })
    return lookupObject
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    // treat things we don't understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
    tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
    return allowedGroups.indexOf(tiqGroupName) !== -1
  }
})(window)

// Debugging / development output - repaste the integration on your test pages each time you make a change to your consent state
var outputString = `CMP Found: ${window.tealiumCmpIntegration.cmpName} (${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model)

Checks:
  - id:          ${window.tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
  - well-formed: ${window.tealiumCmpIntegration.cmpCheckForWellFormedDecision(window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - explicit:    ${window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - group list:  ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToGroupList(window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}

  - name lookup: ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToLookupObject(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()), null, 6)}
`
console.log(outputString)
```


### Didomi v2

Test this snippet on [didomi.io](https://didomi.io) or on your website by [following the instructions above](#how-it-works) to check compatibility and get the information needed for integration.

The Didomi v2 integration uses **Vendors** as **Purposes**.

We recommend Didomi v2 for new Didomi setups. To use Didomi v2, create a new consent integration and select **Didomi v2** as the vendor. Existing Didomi (legacy) integrations continue to work without changes.

Didomi v2 differs from Didomi (legacy) in the following ways:

* No **Vendor ID** field.
* No default purpose group. Purpose keys are vendor-specific and vary across Didomi configurations.
* Callback support. The integration listens for `consent.changed` events from Didomi and rechecks consent automatically. For more information, see [Monitor and trigger consent updates](https://docs.tealium.com/custom-cmp-integrations/#monitor-and-trigger-consent-updates).


```js
;(function didomiIntegration (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Didomi'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'didomiv2-1.0.0'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject
  window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck

  // defaults to opt-in model to be safe if we can't determine the model, since opt-in works (less efficiently) for opt-out cases but not vice versa
  function cmpCheckIfOptInModel () {
      if (!window.Didomi || typeof window.Didomi.getConfig !== 'function') return true
      var config = window.Didomi.getConfig()
      if (typeof config !== "object" || config === null || !config.regulation || !config.regulation.group || !config.regulation.group.name) return true
      return config.regulation.group.name !== 'none' // even 'mixed' might need the opt-in type handling, see https://support.didomi.io/processing-rule-override
  }

  function cmpFetchCurrentConsentDecision () {
      if (!window.Didomi || typeof window.Didomi.getCurrentUserStatus !== 'function') return false
      if (typeof window.Didomi.getConfig !== 'function') return false
      var cmpRawOutput = {}
      cmpRawOutput.userStatus = window.Didomi.getCurrentUserStatus()
      cmpRawOutput.vendorInfo = window.Didomi.getRequiredVendors()
      cmpRawOutput.shouldUserStatusBeCollected = window.Didomi.shouldUserStatusBeCollected()
      return cmpRawOutput
  }

  // Didomi has chosen not to support this feature in their integration
  function cmpFetchCurrentLookupKey () {
    // return whatever Vendor ID is expected be active to short-circuit the ID-based double check
    return (window.tealiumCmpIntegration && window.tealiumCmpIntegration.map && Object.keys(window.tealiumCmpIntegration.map)[0]) || '(Vendor ID check disabled)'
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
      // treat things we don't understand as an opt-out
      if (typeof cmpRawOutput !== 'object') return false
      if (typeof cmpRawOutput.userStatus !== 'object') return false
      if (typeof cmpRawOutput.vendorInfo !== 'object') return false
      if (typeof cmpRawOutput.shouldUserStatusBeCollected !== 'boolean') return false
      return true
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
      // treat things we don't understand as an opt-out
      if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
      return cmpRawOutput.shouldUserStatusBeCollected === false // false after an explicit decision is made
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
      return Object.keys(cmpConvertResponseToLookupObject(cmpRawOutput))
  }

  function cmpConvertResponseToLookupObject (cmpRawOutput) {
    // Didomi handles checking each vendor's required purposes
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return {}

    // Since the friendly names are stored as part of a (long) array of objects, we want to avoid unneeded looping by converting it once
    var fullLookup = {}
    cmpRawOutput.vendorInfo.forEach(function (vendor) {
        fullLookup[vendor.didomiId] = { name: vendor.name || 'iab-vendor-' + vendor.id, id: String(vendor.id), didomiId: vendor.didomiId }
    })

    var consentedVendors = {}
    // enforce strings, even for IAB vendor ids
    Object.values(cmpRawOutput.userStatus.vendors || {}).forEach(function (vendor) {
        if (vendor.enabled === true) {
          var ref = fullLookup[vendor.id] || {}
          consentedVendors[ref.id] = ref.name || '(missing)'
        }
    })
    return consentedVendors
  }

  function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
    if (typeof triggerRecheck !== 'function') return false; // don't do anything unless we have a function to call when it's time to trigger

    // Guard against duplicate registration
    if (window.tealiumCmpIntegration._callbacksRegistered) return false
    window.tealiumCmpIntegration._callbacksRegistered = true

    // Docs: https://developers.didomi.io/cmp/web-sdk/reference/events#event-types
    window.didomiEventListeners = window.didomiEventListeners || [];
    window.didomiEventListeners.push({
      event: 'consent.changed',
      listener: triggerRecheck
    });
    window.didomiOnReady = window.didomiOnReady || [];
    window.didomiOnReady.push(triggerRecheck);
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
      // treat things we don't understand as an opt-out
      if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
      tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
      var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
      return allowedGroups.indexOf(tiqGroupName) !== -1
  }
})(window)

/*
// DEBUG OUTPUT - uncomment this block, then paste/repaste this entire template on your test pages to get console output
// of the CMP decision and how it's being processed by our integration code. You can use this output to debug and adjust
// the cmp* functions above as needed during development of the integration

var setCallback = window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck(function () {
  setTimeout(consoleOut, 200)
})
if (!setCallback) consoleOut() // if we weren't able to set the callback, output the decision for the debugging user


function consoleOut () {
  // Debugging / development output - uncomment this block, then paste/repaste this entire template on your test pages
  var decision = window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision()
  var outputString = `\n${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

Checks:
  - well-formed: ${window.tealiumCmpIntegration.cmpCheckForWellFormedDecision(decision)}
  - explicit:    ${window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(decision)}
  - lookup:      ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToLookupObject(decision), null, 8)}:
  - group list:  ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToGroupList(decision), null, 8)}

`
  console.log(outputString);
}
*/
```


### Digital Control Room

Test this snippet on [digitalcontrolroom.com](https://www.digitalcontrolroom.com/) or on your website by following the instructions in the [How it works section](#how-it-works) to check compatibility and get the information needed for integration.


```js
;(function digitalControlRoom(window) {
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {};
  window.tealiumCmpIntegration.cmpName = 'Digital Control Room';
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'v1.0.0';
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel;
  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision;
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey;
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision;
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision;
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent;
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList;
  function cmpCheckIfOptInModel() {
    return (
      window._cookiereports &&
      window._cookiereports.panels &&
      window._cookiereports.panels[0].consent &&
      window._cookiereports.panels[0].consentExplicit
    );
  }
  // This output is used as the cmpRawOutput argument in functions below.
  function cmpFetchCurrentConsentDecision() {
    if (!window._cookiereports) {
      return {};
    }
    var levels = window._cookiereports.loadConsent();
    levels[1] = true;
    var output = { "levels": levels };
    output.panels = window._cookiereports.panels;
    return output;
  }
  // Should return a string that helps Tealium iQ confirm that it's got the right CMP configuration (and not one from some other page / customer of the CMP)
  function cmpFetchCurrentLookupKey() {
    if (window._cookiereports && window._cookiereports.panels && window._cookiereports.panels.length > 0)
      return window._cookiereports.panels[0].storagekey;
    return "";
  }
  function cmpCheckForWellFormedDecision(cmpRawOutput) {
    if (typeof cmpRawOutput.levels !== "object" || cmpRawOutput.levels === null || typeof cmpRawOutput.panels !== "object" || cmpRawOutput.panels === null) {
      return false;
    }
    return true;
  }
  // Should return a boolean - true if the consent decision was explicitly made by the user
  function cmpCheckForExplicitConsentDecision(cmpRawOutput) {
    if (cmpRawOutput && cmpRawOutput.panels)
      return cmpRawOutput.panels[0].consentDecisionIsExplicit();
    return false;
  }
  function cmpConvertResponseToGroupList(cmpRawOutput) {
    if (!cmpCheckForWellFormedDecision(cmpRawOutput)) {
      return ["1"];
    }
    var levels = cmpRawOutput.levels;
    var consentDecision = [];
    for (var key in levels) {
      if (levels.hasOwnProperty(key)) {
        if (levels[key] === true) {
          consentDecision.push(key);
        }
      }
    }
    return consentDecision;
  }
  // You shouldn't need to change this function, or anything below it
  function cmpCheckForTiqConsent(cmpRawOutput, tiqGroupName) {
    // treat things we don't understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false;
    tiqGroupName = tiqGroupName || "tiq-group-name-missing";
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput);
    return allowedGroups.indexOf(tiqGroupName) !== -1;
  }
})(window);
// Debugging / development output - uncomment this block, then paste/repaste this entire template on your test pages
/*
var outputString = `${tealiumCmpIntegration.cmpCheckIfOptInModel() ? "Opt-in" : "Opt-out"} Model
  Checks:
    - id:          ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
    - well-formed: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - explicit:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - group list:  ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}
  `;
console.log(outputString);
*/
```


### OneTrust

Test this snippet on https://onetrust.com or on your website by [following the instructions above](#how-it-works) to check compatibility and get the information needed for integration.


<blockquote>
OneTrust provides a test mode to preview settings, activated by adding `-test` to your Vendor ID. To simplify integration, OneTrust consent integrations remove the `-test` suffix from Vendor IDs. For seamless integration, enter your Vendor ID without `-test` in the consent integrations UI when setting up your integration, even if you use the `-test` suffix on your pages. Mismatched Vendor IDs between the Tealium iQ UI and your active integrations prevent Tealium iQ Tag Management from setting cookies or triggering tags on the page.
</blockquote>


OneTrust supports callback functions through `cmpAddCallbackToTriggerRecheck`. This callback enables Tealium iQ to receive real-time updates on consent status changes without polling. For more information, see [Monitor and trigger consent updates](https://docs.tealium.com/custom-cmp-integrations/#monitor-and-trigger-consent-updates).


```js
;(function oneTrust(window) {
    // allows simple adjustment of the name/id behavior
    var useNamesInsteadOfKeys = false;
    // allow the safety check of the expected Vendor ID to be circumvented to simplify setup at the cost of increased risk
    var disableVendorIdValidation = false;
    // CMP specific functionality and labels
    window.tealiumCmpIntegration = window.tealiumCmpIntegration || {};
    window.tealiumCmpIntegration.cmpName = "OneTrust";
    window.tealiumCmpIntegration.cmpIntegrationVersion = "onetrust-2.1.0";
    window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision;
    window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey;
    window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel;
    window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision;
    window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision;
    window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent;
    window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList;
    window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject;
    window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck;
    function cmpCheckIfOptInModel() {
        var decision = cmpFetchCurrentConsentDecision();
        if (decision && decision.ConsentModel && decision.ConsentModel.Name === "opt-out") {
            return false;
        }
        return true;
    }
    function cmpFetchCurrentConsentDecision() {
        if (!window.OneTrust || typeof window.OneTrust.GetDomainData !== "function") return false;
        var cmpRawOutput = window.OneTrust.GetDomainData();
        cmpRawOutput.dataLayer = window.dataLayer;
        return cmpRawOutput;
    }
    function cmpFetchCurrentLookupKey() {
        // newer versions of OneTrust, starting at the end of 2022 no longer have cctId defined
        // but this HTML attribute is the way OneTrust can tell
        var scrapeOneTrustVendorId = function () {
            var allScripts = document.getElementsByTagName("script");
            var re = /\/otSDKStub\.js(\?.*)*$/;
            for (var i = 0; i < allScripts.length; i++) {
                var isOneTrustScript = re.test(allScripts[i].src); // can be null
                if (isOneTrustScript) {
                    var fullVendorId = allScripts[i].getAttribute("data-domain-script"); // parse it from the script
                    return fullVendorId.split("-test")[0];
                }
            }
            return "error-not-found";
        }
        if (disableVendorIdValidation) {
            // just return whatever Vendor ID is expected be active
            return (window.tealiumCmpIntegration && window.tealiumCmpIntegration.map && Object.keys(window.tealiumCmpIntegration.map)[0]) || "(Vendor ID check disabled)";
        }
        return scrapeOneTrustVendorId();
    }
    function cmpCheckForWellFormedDecision(cmpRawOutput) {
        // treat things we don't understand as an opt-out
        if (typeof cmpRawOutput !== "object") return false;
        if (toString.call(cmpRawOutput.Groups) !== "[object Array]") return false;
        if (toString.call(cmpRawOutput.dataLayer) !== "[object Array]") return false;
        return true;
    }
    function cmpCheckForExplicitConsentDecision(cmpRawOutput) {
        // treat things we don't understand as implicit
        if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false;
        return window.OneTrust && typeof window.OneTrust.IsAlertBoxClosed === "function" && window.OneTrust.IsAlertBoxClosed();
    }
    function cmpConvertResponseToLookupObject(cmpRawOutput) {
        // convert from array of objects to object for easier lookups
        var decisionString = "";
        var foundOneTrustEntry = false;
        if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return {};
        for (var i = cmpRawOutput.dataLayer.length - 1; i >= 0; i--) {
            if (["OneTrustGroupsUpdated", "OneTrustLoaded"].indexOf(cmpRawOutput.dataLayer[i].event) !== -1) {
                decisionString = cmpRawOutput.dataLayer[i].OnetrustActiveGroups;
                foundOneTrustEntry = true;
                break;
            }
        }
        var permittedPurposeIds = decisionString.split(",").filter(function (group) {
            return group !== "";
        });
        if (decisionString === "" && cmpRawOutput.dataLayer.length === 1000 && foundOneTrustEntry === false) {
            permittedPurposeIds = window.tealiumConsentRegister && window.tealiumConsentRegister.getCurrentDecision();
        }
        var permittedPurposesWithNames = {};
        cmpRawOutput.Groups.forEach(function (groupInfo) {
            if (permittedPurposeIds.indexOf(groupInfo.OptanonGroupId) !== -1) {
                permittedPurposesWithNames[groupInfo.OptanonGroupId] = groupInfo.GroupName || "ERROR-MISSING";
            }
        })
        return permittedPurposesWithNames; // keys are IDs, values are names
    }
    function cmpConvertResponseToGroupList(cmpRawOutput) {
        var permittedPurposesWithNames = cmpConvertResponseToLookupObject(cmpRawOutput);
        var keysOrValues = useNamesInsteadOfKeys ? "values" : "keys";
        return Object[keysOrValues](permittedPurposesWithNames); // keys are IDs, values are names
    }
    function cmpAddCallbackToTriggerRecheck(triggerRecheck) {
        if (typeof triggerRecheck !== 'function') return false;
        // An official Google dataLayer listener, pulled from https://github.com/google/data-layer-helper/blob/master/dist/data-layer-helper.js, see https://github.com/google/data-layer-helper
        (function () {/*
         Copyright The Closure Library Authors.
         SPDX-License-Identifier: Apache-2.0
        */
            'use strict';/*
         jQuery v1.9.1 (c) 2005, 2012
         jQuery Foundation, Inc. jquery.org/license.
        */
            var f = /\[object (Boolean|Number|String|Function|Array|Date|RegExp|Arguments)\]/; function g(a) { return null == a ? String(a) : (a = f.exec(Object.prototype.toString.call(Object(a)))) ? a[1].toLowerCase() : "object" } function m(a, b) { return Object.prototype.hasOwnProperty.call(Object(a), b) } function n(a) { if (!a || "object" != g(a) || a.nodeType || a == a.window) return !1; try { if (a.constructor && !m(a, "constructor") && !m(a.constructor.prototype, "isPrototypeOf")) return !1 } catch (c) { return !1 } for (var b in a); return void 0 === b || m(a, b) }; function p(a, b) { var c = {}, d = c; a = a.split("."); for (var e = 0; e < a.length - 1; e++)d = d[a[e]] = {}; d[a[a.length - 1]] = b; return c } function q(a, b) { var c = !a._clear, d; for (d in a) if (m(a, d)) { var e = a[d]; "array" === g(e) && c ? ("array" === g(b[d]) || (b[d] = []), q(e, b[d])) : n(e) && c ? (n(b[d]) || (b[d] = {}), q(e, b[d])) : b[d] = e } delete b._clear };/* Copyright 2012 Google Inc. All rights reserved. */
            function r(a, b, c) {
                b = void 0 === b ? {} : b; "function" === typeof b ? b = { listener: b, listenToPast: void 0 === c ? !1 : c, processNow: !0, commandProcessors: {} } : b = { listener: b.listener || function () { }, listenToPast: b.listenToPast || !1, processNow: void 0 === b.processNow ? !0 : b.processNow, commandProcessors: b.commandProcessors || {} }; this.a = a; this.l = b.listener; this.j = b.listenToPast; this.g = this.i = !1; this.c = {}; this.f = []; this.b = b.commandProcessors; this.h = u(this); var d = this.a.push, e = this; this.a.push = function () {
                    var k = [].slice.call(arguments,
                        0), l = d.apply(e.a, k); v(e, k); return l
                }; b.processNow && this.process()
            } r.prototype.process = function () { this.registerProcessor("set", function () { var c = {}; 1 === arguments.length && "object" === g(arguments[0]) ? c = arguments[0] : 2 === arguments.length && "string" === g(arguments[0]) && (c = p(arguments[0], arguments[1])); return c }); this.i = !0; for (var a = this.a.length, b = 0; b < a; b++)v(this, [this.a[b]], !this.j) }; r.prototype.get = function (a) { var b = this.c; a = a.split("."); for (var c = 0; c < a.length; c++) { if (void 0 === b[a[c]]) return; b = b[a[c]] } return b };
            r.prototype.flatten = function () { this.a.splice(0, this.a.length); this.a[0] = {}; q(this.c, this.a[0]) }; r.prototype.registerProcessor = function (a, b) { a in this.b || (this.b[a] = []); this.b[a].push(b) };
            function v(a, b, c) {
                c = void 0 === c ? !1 : c; if (a.i && (a.f.push.apply(a.f, b), !a.g)) for (; 0 < a.f.length;) {
                    b = a.f.shift(); if ("array" === g(b)) a: { var d = a.c; g(b[0]); for (var e = b[0].split("."), k = e.pop(), l = b.slice(1), h = 0; h < e.length; h++) { if (void 0 === d[e[h]]) break a; d = d[e[h]] } try { d[k].apply(d, l) } catch (w) { } } else if ("arguments" === g(b)) { e = a; k = []; l = b[0]; if (e.b[l]) for (d = e.b[l].length, h = 0; h < d; h++)k.push(e.b[l][h].apply(e.h, [].slice.call(b, 1))); a.f.push.apply(a.f, k) } else if ("function" == typeof b) try { b.call(a.h) } catch (w) { } else if (n(b)) for (var t in b) q(p(t,
                        b[t]), a.c); else continue; c || (a.g = !0, a.l(a.c, b), a.g = !1)
                }
            } r.prototype.registerProcessor = r.prototype.registerProcessor; r.prototype.flatten = r.prototype.flatten; r.prototype.get = r.prototype.get; r.prototype.process = r.prototype.process; window.DataLayerHelper = r; function u(a) { return { set: function (b, c) { q(p(b, c), a.c) }, get: function (b) { return a.get(b) } } };
        })();
        function listener(model, message) {
            // Message has been pushed. 
            // The helper has merged it onto the model.
            // Now use the message and the updated model to do something.
            if (["OneTrustGroupsUpdated", "OneTrustLoaded"].indexOf(message.event) !== -1) {
                triggerRecheck()
            }
        }
        window.dataLayer = window.dataLayer || [];
        const helper = new DataLayerHelper(window.dataLayer, { listener: listener });
        var oldWrapper = window.OptanonWrapper || function () { }
        window.OptanonWrapper = function () {
            oldWrapper();
            triggerRecheck();
        }
        return true;
    }
    function cmpCheckForTiqConsent(cmpRawOutput, tiqGroupName) {
        // treat things we don't understand as an opt-out
        if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false;
        tiqGroupName = tiqGroupName || "tiq-group-name-missing";
        var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput);
        return allowedGroups.indexOf(tiqGroupName) !== -1;
    }
})(window);


/*
// Debugging / development output - paste into the console, or uncomment and paste the whole template during development of a custom integration
function outputDebuggingInfo () {
  var outputString = `${tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model
  Checks:
    - id:                 ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
    - well-formed:        ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - explicit:           ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - using callback:     ${typeof tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck === 'function'}
    - consented purposes: ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}
  `
  console.log(outputString);
}
// use the callback function to avoid console posting while debugging and allow testing of the callback function itself
if (typeof tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck === 'function') {
    tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck(outputDebuggingInfo)
}
outputDebuggingInfo();
*/
```




### Opt-out Cookie + GPC

This integration supports simple opt-out models such as CCPA/CPRA. It interprets the **Vendor ID** field as the cookie name of an opt-out cookie, and is case sensitive. A user is considered to have opted out if this cookie is found with any value, or if the [Global Privacy Control (GPC)](https://docs.tealium.com/about-global-privacy-control/) opt-out signal is found.

The **Purpose Keys** used in the integration and included in the default **Purpose Group** are:

* `no-selling` - For tags to allow regardless of the user's opt-out signal. These tags don't sell/share data or are considered strictly necessary by your legal team, etc.
* `yes-selling` - For tags to block for opt-out users because applicable regulations or policies prohibit tracking after a user has opted out.

### Securiti

Test this snippet on your website by following the instructions in the [How it works](#how-it-works) section to check compatibility and get the information needed for integration.

Securiti supports callback functions through `cmpAddCallbackToTriggerRecheck`. This callback enables Tealium iQ to receive real-time updates on consent status changes without polling. For more information, see [Monitor and trigger consent updates](https://docs.tealium.com/custom-cmp-integrations/#monitor-and-trigger-consent-updates).

The **Purpose Keys** in the default **Purpose Group** are:

* `essential`: Essential
* `analytics_customization`: Analytics & Customization
* `advertising`: Advertising
* `performance_functionality`: Performance & Functionality
* `unclassified`: Unclassified


```js
;(function securitiIntegration (window) {
    // CMP specific functionality and labels
    window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

    window.tealiumCmpIntegration.cmpName = 'Securiti'
    window.tealiumCmpIntegration.cmpIntegrationVersion = 'securiti-1.0.0'

    window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
    window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
    window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
    window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
    window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
    window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
    window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
    window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck

    // only exposed for the console output
    window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject

    // Should return a boolean, true if the CMP is running the 'Opt-in' model (GDPR style)
    function cmpCheckIfOptInModel () {
      var isOptInModel = window.tealiumCmpIntegration && window.tealiumCmpIntegration.decisionCache && window.tealiumCmpIntegration.decisionCache.isOptInModel
      return !isOptInModel
    }

    // Should return some CMP-specific raw object (must be an object) that contains the needed information about the decision.
    // This output is used as the cmpRawOutput argument in functions below.
    function cmpFetchCurrentConsentDecision () {
      window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}
      window.tealiumCmpIntegration.decisionCache = window.tealiumCmpIntegration.decisionCache || {}
      return window.tealiumCmpIntegration.decisionCache
    }

    // Don't support this feature in this integration for now at least
    function cmpFetchCurrentLookupKey () {
      // return whatever Vendor ID is expected be active to short-circuit the ID-based double check
      return (window.tealiumCmpIntegration && window.tealiumCmpIntegration.map && Object.keys(window.tealiumCmpIntegration.map)[0]) || '(Vendor ID check disabled)'
    }

    // Should return a boolean - true if the raw decision meets our expectations for decisions from this particular CMP
    function cmpCheckForWellFormedDecision (cmpRawOutput) {
      return typeof cmpRawOutput === 'object' &&
             typeof cmpRawOutput.category === 'object' &&
             typeof cmpRawOutput.isExplicit === 'boolean' &&
             typeof cmpRawOutput.isOptInModel === 'boolean'
    }

    // Should return a boolean - true if the consent decision was explicitly made by the user
    function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
      if (typeof cmpRawOutput === 'object' && cmpRawOutput.isExplicit === true) return true
      return false
    }

    function cmpConvertResponseToGroupList (cmpRawOutput) {
      return Object.keys(cmpConvertResponseToLookupObject(cmpRawOutput))
    }

    function cmpConvertResponseToLookupObject (cmpRawOutput) {
        // Turns 'Performance & Analytics' into 'performance_analytics'
      var tokenizeName = function (name) {
        if (typeof name !== 'string') return name
        return name.toLowerCase().replace(https://docs.tealium.com/[^a-z0-9]+/g, '_')
      }
      if (!cmpCheckForWellFormedDecision(cmpRawOutput)) return []
      var consentedCategoryNames = Object.keys(cmpRawOutput.category).filter(function (categoryName) { return cmpRawOutput.category[categoryName] === "granted" });
      var lookupObject = {}
      consentedCategoryNames.forEach(function (name) {
        lookupObject[tokenizeName(name)] = name
      })
      return lookupObject
    }

    function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
        if (typeof triggerRecheck !== 'function') return false; // don't do anything unless we have a function to call when it's time to trigger

        window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

        // Guard against duplicate registration
        if (window.tealiumCmpIntegration._callbacksRegistered) return false
        window.tealiumCmpIntegration._callbacksRegistered = true

        // a helper, to be called on the callbacks
        var fetchAndCacheDecision = function (sdk) {
          var isExplicit = sdk.isConsentGiven()
          var defaultConsentState = sdk.getDefaultConsentState()
          var consentDecision = isExplicit ? sdk.getConsent() : defaultConsentState
          // Atomic assignment – no intermediate empty-object window
          window.tealiumCmpIntegration.decisionCache = {
            category: (consentDecision && consentDecision.category) || {},
            isExplicit: !!isExplicit,
            isOptInModel: defaultConsentState && defaultConsentState.category ? (Object.keys(defaultConsentState.category).filter(function (categoryName) { return defaultConsentState.category[categoryName] === "granted" }).length === Object.keys(defaultConsentState.category).length) : undefined
          }
          setTimeout(triggerRecheck, 1) // let the current processing finish before we trigger the recheck
        }

        // if it's already loaded, attach the callback immediately to ensure it works reliably
        if (typeof window.SecuritiSDK !== 'undefined' && typeof window.SecuritiSDK.onReady === 'function') {
          window.SecuritiSDK.onReady(function (sdk) {
            fetchAndCacheDecision(sdk)
          })
        }

        window.SecuritiDataLayer = window.SecuritiDataLayer || [];
        SecuritiDataLayer.push(['onReady', fetchAndCacheDecision]);
        SecuritiDataLayer.push(['onConsentGiven', fetchAndCacheDecision]);
        return true
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
// DEBUG OUTPUT - uncomment this block, then paste/repaste this entire template on your test pages to get console output
// of the CMP decision and how it's being processed by our integration code. You can use this output to debug and adjust
// the cmp* functions above as needed during development of the integration

  var setCallback = window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck(function () {
    consoleOut()
  })
  if (!setCallback) consoleOut() // if we weren't able to set the callback, output the decision for the debugging user


 function consoleOut () {
    // Debugging / development output - uncomment this block, then paste/repaste this entire template on your test pages
    var decision = window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision()
    var outputString = `\n${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

  Checks:
    - well-formed: ${window.tealiumCmpIntegration.cmpCheckForWellFormedDecision(decision)}
    - explicit:    ${window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(decision)}
    - lookup:      ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToLookupObject(decision), null, 8)}
    - group list:  ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToGroupList(decision), null, 8)}

  `
    console.log(outputString);
  }
  */
```


### TrustArc

Test this snippet on [trustarc.com](https://trustarc.com/) or on your website by following the instructions in the [How it works section](#how-it-works) to check compatibility and get the information needed for integration.


```js
;(function trustarcIntegration (window) {

  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'TrustArc'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'trustarc-1.0.4'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject

  function cmpCheckIfOptInModel () {
    var preferredButNewMethod = window.truste && window.truste.eu && window.truste.eu.bindMap && window.truste.eu.bindMap.consentModel;
    if (typeof preferredButNewMethod === 'string' && preferredButNewMethod !== 'none') return preferredButNewMethod !== 'opt-out'; 
    var modeCookieValue = ((window.truste && window.truste.util && typeof window.truste.util.readCookie === 'function' && window.truste.util.readCookie('notice_behavior')) || 'expressed|eu')
    return modeCookieValue.indexOf('expressed') === 0
  }

  var trustArcMap = {
      0: 'Required',
      1: 'Functional',
      2: 'Personalization/Advertising'
  }

  function cmpFetchCurrentConsentDecision () {
    if (!window.truste || !window.truste.util || typeof window.truste.util.readCookie !== 'function') return false;

    var cookieValue =  window.truste.util.readCookie(truste.eu.COOKIE_GDPR_PREF_NAME) || '0,'

    if (cmpCheckIfOptInModel() === false && cmpCheckForExplicitConsentDecision() === false) {
      cookieValue = Object.keys(trustArcMap).join(',') 
    }

    return {
      cookie: cookieValue
    }
  }

  function cmpFetchCurrentLookupKey () {
    return (window.tealiumCmpIntegration && window.tealiumCmpIntegration.map && Object.keys(window.tealiumCmpIntegration.map)[0]) || '(Vendor ID check disabled for this integration)'
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    if (typeof cmpRawOutput !== 'object') return false
    if (typeof cmpRawOutput.cookie !== 'string') return false
    return true
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    if (!window.truste || !window.truste.util || typeof window.truste.util.readCookie !== 'function') return false
    return typeof window.truste.util.readCookie(truste.eu.COOKIE_GDPR_PREF_NAME) === 'string'
  }

  function cmpConvertResponseToLookupObject (cmpRawOutput) {
    if (!cmpCheckForWellFormedDecision(cmpRawOutput)) return []
    const cookieConsentValues = cmpRawOutput.cookie.split(':')[0].split(',')
    const extraSplit = []
    cookieConsentValues.forEach((el) => {
      if (!el) return
      extraSplit.push.apply(extraSplit, el.split('|'))
    })

    const output = {}

    extraSplit.forEach((key) => {
      if (key !== '') {
        output[key] = trustArcMap[key] || 'Category name unknown'
      }
    })

    return output
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    var permittedPurposesWithNames = cmpConvertResponseToLookupObject(cmpRawOutput)
    var keysOrValues = 'keys'
    return Object[keysOrValues](permittedPurposesWithNames) 
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false

    tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
    return allowedGroups.indexOf(tiqGroupName) !== -1
  }
})(window)

/*
// Debugging - uncomment this code and paste the integration into the console on your test pages each time you make a change to your consent state to test without publishing
var outputString = `CMP Found: ${window.tealiumCmpIntegration.cmpName} (${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model)

    Checks:
      - id:          ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
      - well-formed: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
      - explicit:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
      - group list:  ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}

      - name lookup: ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToLookupObject(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()), null, 6)}
    `
console.log(outputString)
*/
```



### Usercentrics v2

Test this snippet on your website by following the instructions in the [How it works](#how-it-works) section to check compatibility and get the information needed for integration.

The Usercentrics v2 integration is for the Usercentrics Browser SDK v1 and v2 and uses **Vendors** as **Purposes**.

Usercentrics v2 supports callback functions through `cmpAddCallbackToTriggerRecheck`. This callback enables Tealium to receive real-time updates on consent status changes without polling.


```js
;(function usercentricsBrowserSdk (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Usercentrics Browser SDK (v2)'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'usercentrics-1.1.0'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck

  function cmpFetchCurrentConsentDecision () {
    if (!window.UC_UI || typeof window.UC_UI.getServicesBaseInfo !== 'function') return false
    const cmpRawOutput = window.UC_UI.getServicesBaseInfo()
    return cmpRawOutput
  }

  function cmpFetchCurrentLookupKey () {
    var v2 = window.UC_UI && typeof window.UC_UI.getSettingsCore === 'function' && window.UC_UI.getSettingsCore().id
    // var v3 = window.UC_UI && typeof window.UC_UI.getControllerId === 'function' && window.UC_UI.getControllerId()
    // return v2 || v3 || ''
    return v2
  }

  function cmpCheckIfOptInModel () {
    return true // only opt-in for now
    // return window.UC_UI && typeof window.UC_UI.isConsentRequired === 'function' && window.UC_UI.isConsentRequired() === true
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    // treat things we don't understand as an opt-out
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    // use the first entry as a proxy for all
    if (cmpRawOutput && cmpRawOutput[0] && typeof cmpRawOutput[0].name === 'string' && cmpRawOutput[0].name.length > 0) {
      return true
    }
    return false
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    // treat things we don't understand as an opt-out
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    // use the first entry as a proxy for all
    if (!Array.isArray(window.dataLayer)) return false;
    const latestConsentStatus = [...window.dataLayer]
      .reverse()
      .find(entry => entry.event === 'consent_status');
    return latestConsentStatus && latestConsentStatus.type ? latestConsentStatus.type.toLowerCase() === 'explicit' : false;
    // the old code below isn't reliable across all versions (check usercentrics.de for example)
    /*
    const consentHistory = (cmpRawOutput && cmpRawOutput[0] && cmpRawOutput[0].consent && cmpRawOutput[0].consent.history) || []
    const lastHistoryEntryType = (consentHistory && consentHistory.length && consentHistory[consentHistory.length - 1].type) || ''
    if (lastHistoryEntryType === 'explicit') {
      return true
    }
    return false
    */
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    let foundOptIn = false
    // treat things we don't understand as an opt-out
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    // use the mapping if found, with a fallback (Usercentrics default value) if not specified in the mapping

    tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
    // check vendors if there's an object, look for at least one
    cmpRawOutput.forEach(function (tagInfo) {
      if ((tagInfo.consent && tagInfo.consent.status === true) && tagInfo.name === tiqGroupName) {
        foundOptIn = true
      }
    })
    return foundOptIn
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    const vendorArray = []
    cmpRawOutput && cmpRawOutput.forEach(function (tagConsent) {
      if (tagConsent.consent && tagConsent.consent.status === true) {
        vendorArray.push(tagConsent.name)
      }
    })
    return vendorArray
  }

  // see https://docs.usercentrics.com/#/v2-events
  function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
    if (typeof triggerRecheck !== 'function') return false; // don't do anything unless we have a function to call when it's time to trigger

    // Guard against duplicate registration
    if (window.tealiumCmpIntegration._callbacksRegistered) return false
    window.tealiumCmpIntegration._callbacksRegistered = true

    window.addEventListener("ucEvent", function (e) {
      if( e.detail && e.detail.event && e.detail.event === "consent_status" ) {
        triggerRecheck()
      }
    })

    window.addEventListener('UC_UI_CMP_EVENT', function(e) {
      triggerRecheck()
    });

    window.addEventListener('UC_UI_INITIALIZED', function(e) {
      triggerRecheck()
    });
    return true;
  }
})(window)

/*
  // DEBUG OUTPUT - uncomment this block, then paste/repaste this entire template on your test pages to get console output
  // of the CMP decision and how it's being processed by our integration code. You can use this output to debug and adjust
  // the cmp* functions above as needed during development of the integration

  var setCallback = window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck(function () {
    consoleOut()
  })
  if (!setCallback) consoleOut() // if we weren't able to set the callback, output the decision for the debugging user


 function consoleOut () {
    // Debugging / development output - uncomment this block, then paste/repaste this entire template on your test pages
    var decision = window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision()
    var outputString = `\n${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

  Checks:
    - vendor id:   ${window.tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
    - well-formed: ${window.tealiumCmpIntegration.cmpCheckForWellFormedDecision(decision)}
    - explicit:    ${window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(decision)}
    - group list:  ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToGroupList(decision), null, 8)}

  `
    console.log(outputString);
  }
*/
```


### Usercentrics v3

Test this snippet on your website by following the instructions in the [How it works](#how-it-works) section to check compatibility and get the information needed for integration.

The Usercentrics v3 integration is for the Usercentrics Browser SDK V3 and uses **Vendors** as **Purposes**.


```js
// tv:1.0.0
// base:usercentricsv3
;(function usercentricsBrowserSdk (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Usercentrics Browser SDK (v3)'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'usercentricsv3-1.0.0'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  // just for internal/debugging use
  window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject
  // callbacks supported!
  window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck


  // use the previously cached value, set by callbacks from the CMP
  function cmpFetchCurrentConsentDecision () {
    window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}
    window.tealiumCmpIntegration.decisionCache = window.tealiumCmpIntegration.decisionCache || {}
    return window.tealiumCmpIntegration.decisionCache
  }

  function cmpFetchCurrentLookupKey () {
   return window.tealiumCmpIntegration.decisionCache && cmpCheckForWellFormedDecision(window.tealiumCmpIntegration.decisionCache) ? window.tealiumCmpIntegration.decisionCache.consent.setting.id : 'ERROR: Vendor ID not found!'
  }

  function cmpCheckIfOptInModel () {
    return true
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    if (typeof cmpRawOutput !== 'object' || cmpRawOutput === null) return false
    if (typeof cmpRawOutput.services !== 'object' || cmpRawOutput.services === null) return false
    if (typeof cmpRawOutput.consent !== 'object' || cmpRawOutput.consent === null) return false
    if (typeof cmpRawOutput.consent.setting !== 'object' || cmpRawOutput.consent.setting === null) return false
    if (typeof cmpRawOutput.consent.setting.id !== 'string' || cmpRawOutput.consent.setting.id.length === 0) return false
    return true
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    return cmpRawOutput && cmpRawOutput.consent && cmpRawOutput.consent.type && cmpRawOutput.consent.type.toLowerCase() === 'explicit' ? true : false;
  }

  function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
    if (typeof triggerRecheck !== 'function') return false;

    // Guard against duplicate registration
    if (window.tealiumCmpIntegration._callbacksRegistered) return false;
    window.tealiumCmpIntegration._callbacksRegistered = true;

    // if the CMP has already loaded, get the current decision and cache it immediately
    window.__ucCmp && window.__ucCmp.getConsentDetails && window.__ucCmp.getConsentDetails().then(function (consentDetails) {
      if (consentDetails) {
        window.tealiumCmpIntegration.decisionCache = consentDetails
        triggerRecheck()
      }
    })

    // Docs: https://usercentrics.com/docs/web/features/events/uc-consent/
    window.addEventListener('UC_CONSENT', function (event) {
      if (event && event.detail && event.detail.services) {
        // Cache the decision details in a known location for later retrieval by cmpFetchCurrentConsentDecision
        window.tealiumCmpIntegration.decisionCache = event.detail
      }
      triggerRecheck()
    });
    return true;
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    if (!cmpCheckForWellFormedDecision(cmpRawOutput)) return []
    var consentedGroups = cmpConvertResponseToLookupObject(cmpRawOutput)
    return Object.keys(consentedGroups)
  }

  function cmpConvertResponseToLookupObject (cmpRawOutput) {
    if (!cmpCheckForWellFormedDecision(cmpRawOutput)) return []
    var consentedGroups = {}
    Object.keys(cmpRawOutput.services).forEach(function (key) {
      if (cmpRawOutput.services[key].consent.given === true) {
        consentedGroups[key] = cmpRawOutput.services[key].name
      }
    })
    return consentedGroups
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
// DEBUG OUTPUT - uncomment this block, then paste/repaste this entire template on your test pages to get console output
// of the CMP decision and how it's being processed by our integration code. You can use this output to debug and adjust
// the cmp* functions above as needed during development of the integration

  var setCallback = window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck(function () {
    consoleOut()
  })
  if (!setCallback) consoleOut() // if we already set the callback, output the decision for the (debugging) user


 function consoleOut () {
    var decision = window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision()
    var outputString = `\n${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

  Checks:
    - vendor id:   ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
    - well-formed: ${window.tealiumCmpIntegration.cmpCheckForWellFormedDecision(decision)}
    - explicit:    ${window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(decision)}
    - lookup:      ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToLookupObject(decision), null, 8)}
    - group list:  ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToGroupList(decision), null, 8)}

  `
    console.log(outputString);
  }
  */
```


### Custom Integration template

For more information about the custom integration template and how to use it, see [Custom integration](https://docs.tealium.com/custom-cmp-integrations/).