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


### Didomi

Test this snippet on [didomi.io](https://didomi.io) or on your website by [following the instructions above](#how-it-works) to check compatibility and get the information needed for integration.

The Didomi integration uses **Vendors** as **Purposes**.


<blockquote>
The current integration with Didomi does not return implicitly consented purposes or vendors, as this was the only option available at the time. To support customers using older versions, and until an update allows a new approach, this integration unconditionally adds the purpose key `always_consented` to outbound consent decisions. This acts as a workaround to enable implicit triggering.
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


OneTrust supports callback functions through `cmpAddCallbackToTriggerRecheck`. This enables Tealium iQ to receive real-time updates on consent status changes without polling. For more information, see .


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

This integration intends to provide support for very simple opt-out models such as CCPA/CPRA. It interprets the **Vendor ID** field as the cookie name of an opt-out cookie, and is case sensitive. A user is considered to have opted out if this cookie is found with any value, or if the [Global Privacy Control (GPC)](https://docs.tealium.com/about-global-privacy-control/) opt-out signal is found.

The **Purpose Keys** used in the integration and included in the default **Purpose Group** are:

* `no-selling` - For tags to allow regardless of the user's opt-out signal. These tags don't sell/share data or are considered strictly necessary by your legal team, etc.
* `yes-selling` - For tags to block for opt-out users because applicable regulations or policies prohibit tracking after a user has opted out.

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



### Usercentrics

Test this snippet on your website by following the instructions in the [How it works](#how-it-works) section to check compatibility and get the information needed for integration.
The Usercentrics integration uses **Vendors** as **Purposes**.


```js
;(function usercentricsBrowserSdkV2 (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Usercentrics Browser SDK'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'usercentrics-1.0.3'

  function cmpFetchCurrentConsentDecision () {
    if (!window.UC_UI || typeof window.UC_UI.getServicesBaseInfo !== 'function') return false
    var cmpRawOutput = window.UC_UI.getServicesBaseInfo()
    return cmpRawOutput
  }

  function cmpFetchCurrentLookupKey () {
    return (window.UC_UI && typeof window.UC_UI.getSettingsCore === 'function' && window.UC_UI.getSettingsCore().id) || ''
  }

  // only support opt-In model for Usercentrics for now, can be added if needed
  function cmpCheckIfOptInModel () {
    return window.UC_UI && typeof window.UC_UI.isConsentRequired === 'function' && window.UC_UI.isConsentRequired() === true
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    // treat things we don't understand as an opt-out
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    // use the first entry as a proxy for all
    if (cmpRawOutput && cmpRawOutput[0] && typeof cmpRawOutput[0].name === 'string') {
      return true
    }
    return false
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    // treat things we don't understand as an opt-out
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    // use the first entry as a proxy for all
    var consentHistory = (cmpRawOutput && cmpRawOutput[0] && cmpRawOutput[0].consent && cmpRawOutput[0].consent.history) || []
    var lastHistoryEntryType = (consentHistory && consentHistory.length && consentHistory[consentHistory.length - 1].type) || ''
    if (lastHistoryEntryType === 'explicit') {
      return true
    }
    return false
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    var foundOptIn = false
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
    var vendorArray = []
    cmpRawOutput && cmpRawOutput.forEach(function (tagConsent) {
      if (tagConsent.consent && tagConsent.consent.status === true) {
        vendorArray.push(tagConsent.name)
      }
    })
    return vendorArray
  }

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
})(window)

var outputString = `${tealiumCmpIntegration.cmpName} - ${tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

Checks:
  - vendor id:            ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
  - well-formed decision: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - explicit decision:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - consented purposes:   ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()).sort(),null, 8)}
`
console.log(outputString)
```


### Custom Integration template

For more information about the custom integration template and how to use it, see [Custom integration](https://docs.tealium.com/custom-cmp-integrations/).