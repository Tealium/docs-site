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

After you update your consent decision, paste the code again to see the latest interpretation.

## Integration-specific instructions and code snippets

### Cookiebot

Test this snippet on [cookiebot.com](https://www.cookiebot.com/) or on your website by following the instructions in the [How it works section](#how-it-works) to check compatibility and get the information needed for integration.


```js

;(function cookiebotIntegration (window) {
    window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}
    window.tealiumCmpIntegration.cmpName = &#39;Cookiebot&#39;
    window.tealiumCmpIntegration.cmpIntegrationVersion = &#39;v1.0.0&#39;
    window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
    window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
    window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
    window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
    window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
    window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
    window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
    // Should return a boolean, true if the CMP is running the &#39;Opt-in&#39; model (GDPR style)
    function cmpCheckIfOptInModel () {
      if (!window.Cookiebot || !window.Cookiebot.regulations || typeof window.Cookiebot.regulations.gdprApplies !== &#39;boolean&#39;) return false
      return Cookiebot.regulations.gdprApplies
    }
    // Should return some CMP-specific raw object (must be an object) that contains the needed information about the decision.
    // This output is used as the cmpRawOutput argument in functions below.
    function cmpFetchCurrentConsentDecision () {
      if (!window.Cookiebot || typeof window.Cookiebot.hasResponse !== &#39;boolean&#39;) return false
      return cmpRawOutput = window.Cookiebot.consent;
    }
    // Should return a string that helps Tealium iQ confirm that it&#39;s got the right CMP configuration (and not one from some other page / customer of the CMP)
    function cmpFetchCurrentLookupKey() {
        if (!window.Cookiebot || typeof window.Cookiebot.serial !== &#39;string&#39;) return false
        return Cookiebot.serial
    }
    // Should return a boolean - true if the raw decision meets our expectations for the CMP
    function cmpCheckForWellFormedDecision (cmpRawOutput) {
      return typeof cmpRawOutput === &#39;object&#39; &amp;&amp;  typeof cmpRawOutput.stamp ===&#39;string&#39;
    }
    // Should return a boolean - true if the consent decision was explicitly made by the user
    function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
      // The only way we can tell if the decision is explicit in this example is to check if an opt-out cookie is set
      return cmpRawOutput.method === &#39;explicit&#39;? true : false;
    }
    // Should return an array of consented vendors/purposes - these should match the Purposes in Tealium iQ exactly
    function cmpConvertResponseToGroupList(cmpRawOutput) {
        var consentDecision = []
        // very simple check for a non-empty opt-out cookie to determine if tags that sell data are allowed
        if (cmpRawOutput.necessary) {
            consentDecision.push(&#39;necessary&#39;) // we don&#39;t see a cookie, so we have to assume selling/sharing data is fine
        }
        if (cmpRawOutput.preferences) {
            consentDecision.push(&#39;preferences&#39;) // we don&#39;t see a cookie, so we have to assume selling/sharing data is fine
        }
        if (cmpRawOutput.marketing) {
            consentDecision.push(&#39;marketing&#39;) // we don&#39;t see a cookie, so we have to assume selling/sharing data is fine
        }
        if (cmpRawOutput.statistics) {
            consentDecision.push(&#39;statistics&#39;) // we don&#39;t see a cookie, so we have to assume selling/sharing data is fine
        }
        return consentDecision
    }
    // You shouldn&#39;t need to change this function, or anything below it
    function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
      // treat things we don&#39;t understand as an opt-out
      if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
      tiqGroupName = tiqGroupName || &#39;tiq-group-name-missing&#39;
      var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
      return allowedGroups.indexOf(tiqGroupName) !== -1
    }
  })(window)
  /*
    // Debugging / development output - uncomment this block, then paste/repaste this entire template on your test pages
    var outputString = `${tealiumCmpIntegration.cmpCheckIfOptInModel() ? &#39;Opt-in&#39; : &#39;Opt-out&#39;} Model
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

The current integration with Didomi does not return implicitly consented purposes or vendors, as this was the only option available at the time. To support customers using older versions, and until an update allows a new approach, this integration unconditionally adds the purpose key `always_consented` to outbound consent decisions. This acts as a workaround to enable implicit triggering.


```js
;(function didomiIntegration (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = &#39;Didomi&#39;
  window.tealiumCmpIntegration.cmpIntegrationVersion = &#39;didomi-1.0.1&#39;

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject

  function cmpCheckIfOptInModel () {
    if (!window.Didomi || typeof window.Didomi.getConfig !== &#39;function&#39;) return false
    return window.Didomi.getConfig().notice.type === &#39;optin&#39;
  }

  function cmpFetchCurrentConsentDecision () {
    if (!window.Didomi || typeof window.Didomi.getUserStatus !== &#39;function&#39;) return false
    if (typeof window.Didomi.getConfig !== &#39;function&#39;) return false
    var cmpRawOutput = {}
    cmpRawOutput.userStatus = window.Didomi.getUserStatus()
    cmpRawOutput.vendorInfo = window.Didomi.getVendors()
    cmpRawOutput.shouldConsentBeCollected = window.Didomi.shouldConsentBeCollected()
    return cmpRawOutput
  }

  function cmpFetchCurrentLookupKey () {
    if (!window.Didomi || typeof window.Didomi.getConfig !== &#39;function&#39;) return &#39;&#39;
    var id = window.Didomi.getConfig().app.deploymentId
    return id || &#39;&#39;
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    // treat things we don&#39;t understand as an opt-out
    if (typeof cmpRawOutput !== &#39;object&#39;) return false
    if (typeof cmpRawOutput.userStatus !== &#39;object&#39;) return false
    // do more checks than strictly necessary to confirm expectations
    if (typeof cmpRawOutput.userStatus.purposes !== &#39;object&#39;) return false
    if (typeof cmpRawOutput.userStatus.vendors !== &#39;object&#39;) return false
    if (typeof cmpRawOutput.userStatus.purposes.global !== &#39;object&#39;) return false
    if (typeof cmpRawOutput.userStatus.vendors.global !== &#39;object&#39;) return false
    if (toString.call(cmpRawOutput.userStatus.purposes.global.enabled) !== &#39;[object Array]&#39;) return false
    if (toString.call(cmpRawOutput.userStatus.vendors.global.enabled) !== &#39;[object Array]&#39;) return false

    if (typeof cmpRawOutput.vendorInfo !== &#39;object&#39;) return false

    if (typeof cmpRawOutput.shouldConsentBeCollected !== &#39;boolean&#39;) return false
    return true
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    // treat things we don&#39;t understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
    return cmpRawOutput.shouldConsentBeCollected === false // false after an explicit decision is made
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    // Didomi handles checking each vendor&#39;s required purposes
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return []
    // enforce strings, even for IAB vendor ids

    const decision = cmpRawOutput.userStatus.vendors.global.enabled.map(function (vendorId) {
      return String(vendorId)
    })

    decision.push(&#39;always_consented&#39;)
    return decision
  }

  function cmpConvertResponseToLookupObject (cmpRawOutput) {
    var allowedVendors = cmpConvertResponseToGroupList(cmpRawOutput)
    var allVendors = cmpRawOutput.vendorInfo
    var lookupObject = {}
    // WORKAROUND to allow implicit triggering until the Didomi bug is fixed
    lookupObject.always_consented = &#39;Always consented (to allow strictly needed triggering)&#39;
    allVendors.forEach(function (vendorObject) {
      if (allowedVendors.indexOf(String(vendorObject.id)) === -1) return
      lookupObject[vendorObject.id] = vendorObject.name || &#39;iab-vendor-&#39; &#43; vendorObject.id
    })
    return lookupObject
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    // treat things we don&#39;t understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
    tiqGroupName = tiqGroupName || &#39;tiq-group-name-missing&#39;
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
    return allowedGroups.indexOf(tiqGroupName) !== -1
  }
})(window)

// Debugging / development output - repaste the integration on your test pages each time you make a change to your consent state
var outputString = `CMP Found: ${window.tealiumCmpIntegration.cmpName} (${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? &#39;Opt-in&#39; : &#39;Opt-out&#39;} Model)

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
  window.tealiumCmpIntegration.cmpName = &#39;Digital Control Room&#39;;
  window.tealiumCmpIntegration.cmpIntegrationVersion = &#39;v1.0.0&#39;;
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel;
  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision;
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey;
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision;
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision;
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent;
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList;
  function cmpCheckIfOptInModel() {
    return (
      window._cookiereports &amp;&amp;
      window._cookiereports.panels &amp;&amp;
      window._cookiereports.panels[0].consent &amp;&amp;
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
    var output = { &#34;levels&#34;: levels };
    output.panels = window._cookiereports.panels;
    return output;
  }
  // Should return a string that helps Tealium iQ confirm that it&#39;s got the right CMP configuration (and not one from some other page / customer of the CMP)
  function cmpFetchCurrentLookupKey() {
    if (window._cookiereports &amp;&amp; window._cookiereports.panels &amp;&amp; window._cookiereports.panels.length &gt; 0)
      return window._cookiereports.panels[0].storagekey;
    return &#34;&#34;;
  }
  function cmpCheckForWellFormedDecision(cmpRawOutput) {
    if (typeof cmpRawOutput.levels !== &#34;object&#34; || cmpRawOutput.levels === null || typeof cmpRawOutput.panels !== &#34;object&#34; || cmpRawOutput.panels === null) {
      return false;
    }
    return true;
  }
  // Should return a boolean - true if the consent decision was explicitly made by the user
  function cmpCheckForExplicitConsentDecision(cmpRawOutput) {
    if (cmpRawOutput &amp;&amp; cmpRawOutput.panels)
      return cmpRawOutput.panels[0].consentDecisionIsExplicit();
    return false;
  }
  function cmpConvertResponseToGroupList(cmpRawOutput) {
    if (!cmpCheckForWellFormedDecision(cmpRawOutput)) {
      return [&#34;1&#34;];
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
  // You shouldn&#39;t need to change this function, or anything below it
  function cmpCheckForTiqConsent(cmpRawOutput, tiqGroupName) {
    // treat things we don&#39;t understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false;
    tiqGroupName = tiqGroupName || &#34;tiq-group-name-missing&#34;;
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput);
    return allowedGroups.indexOf(tiqGroupName) !== -1;
  }
})(window);
// Debugging / development output - uncomment this block, then paste/repaste this entire template on your test pages
/*
var outputString = `${tealiumCmpIntegration.cmpCheckIfOptInModel() ? &#34;Opt-in&#34; : &#34;Opt-out&#34;} Model
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

OneTrust provides a test mode to preview settings, activated by adding `-test` to your Vendor ID. To simplify integration, OneTrust consent integrations remove the `-test` suffix from Vendor IDs. For seamless integration, enter your Vendor ID without `-test` in the consent integrations UI when setting up your integration, even if you use the `-test` suffix on your pages. Mismatched Vendor IDs between the Tealium iQ UI and your active integrations prevent Tealium iQ Tag Management from setting cookies or triggering tags on the page.

OneTrust supports callback functions through `cmpAddCallbackToTriggerRecheck`. This enables Tealium iQ to receive real-time updates on consent status changes without polling. For more information, see .


```js
;(function oneTrust(window) {
    // allows simple adjustment of the name/id behavior
    var useNamesInsteadOfKeys = false;
    // allow the safety check of the expected Vendor ID to be circumvented to simplify setup at the cost of increased risk
    var disableVendorIdValidation = false;
    // CMP specific functionality and labels
    window.tealiumCmpIntegration = window.tealiumCmpIntegration || {};
    window.tealiumCmpIntegration.cmpName = &#34;OneTrust&#34;;
    window.tealiumCmpIntegration.cmpIntegrationVersion = &#34;onetrust-2.1.0&#34;;
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
        if (decision &amp;&amp; decision.ConsentModel &amp;&amp; decision.ConsentModel.Name === &#34;opt-out&#34;) {
            return false;
        }
        return true;
    }
    function cmpFetchCurrentConsentDecision() {
        if (!window.OneTrust || typeof window.OneTrust.GetDomainData !== &#34;function&#34;) return false;
        var cmpRawOutput = window.OneTrust.GetDomainData();
        cmpRawOutput.dataLayer = window.dataLayer;
        return cmpRawOutput;
    }
    function cmpFetchCurrentLookupKey() {
        // newer versions of OneTrust, starting at the end of 2022 no longer have cctId defined
        // but this HTML attribute is the way OneTrust can tell
        var scrapeOneTrustVendorId = function () {
            var allScripts = document.getElementsByTagName(&#34;script&#34;);
            var re = /\/otSDKStub\.js(\?.*)*$/;
            for (var i = 0; i &lt; allScripts.length; i&#43;&#43;) {
                var isOneTrustScript = re.test(allScripts[i].src); // can be null
                if (isOneTrustScript) {
                    var fullVendorId = allScripts[i].getAttribute(&#34;data-domain-script&#34;); // parse it from the script
                    return fullVendorId.split(&#34;-test&#34;)[0];
                }
            }
            return &#34;error-not-found&#34;;
        }
        if (disableVendorIdValidation) {
            // just return whatever Vendor ID is expected be active
            return (window.tealiumCmpIntegration &amp;&amp; window.tealiumCmpIntegration.map &amp;&amp; Object.keys(window.tealiumCmpIntegration.map)[0]) || &#34;(Vendor ID check disabled)&#34;;
        }
        return scrapeOneTrustVendorId();
    }
    function cmpCheckForWellFormedDecision(cmpRawOutput) {
        // treat things we don&#39;t understand as an opt-out
        if (typeof cmpRawOutput !== &#34;object&#34;) return false;
        if (toString.call(cmpRawOutput.Groups) !== &#34;[object Array]&#34;) return false;
        if (toString.call(cmpRawOutput.dataLayer) !== &#34;[object Array]&#34;) return false;
        return true;
    }
    function cmpCheckForExplicitConsentDecision(cmpRawOutput) {
        // treat things we don&#39;t understand as implicit
        if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false;
        return window.OneTrust &amp;&amp; typeof window.OneTrust.IsAlertBoxClosed === &#34;function&#34; &amp;&amp; window.OneTrust.IsAlertBoxClosed();
    }
    function cmpConvertResponseToLookupObject(cmpRawOutput) {
        // convert from array of objects to object for easier lookups
        var decisionString = &#34;&#34;;
        var foundOneTrustEntry = false;
        if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return {};
        for (var i = cmpRawOutput.dataLayer.length - 1; i &gt;= 0; i--) {
            if ([&#34;OneTrustGroupsUpdated&#34;, &#34;OneTrustLoaded&#34;].indexOf(cmpRawOutput.dataLayer[i].event) !== -1) {
                decisionString = cmpRawOutput.dataLayer[i].OnetrustActiveGroups;
                foundOneTrustEntry = true;
                break;
            }
        }
        var permittedPurposeIds = decisionString.split(&#34;,&#34;).filter(function (group) {
            return group !== &#34;&#34;;
        });
        if (decisionString === &#34;&#34; &amp;&amp; cmpRawOutput.dataLayer.length === 1000 &amp;&amp; foundOneTrustEntry === false) {
            permittedPurposeIds = window.tealiumConsentRegister &amp;&amp; window.tealiumConsentRegister.getCurrentDecision();
        }
        var permittedPurposesWithNames = {};
        cmpRawOutput.Groups.forEach(function (groupInfo) {
            if (permittedPurposeIds.indexOf(groupInfo.OptanonGroupId) !== -1) {
                permittedPurposesWithNames[groupInfo.OptanonGroupId] = groupInfo.GroupName || &#34;ERROR-MISSING&#34;;
            }
        })
        return permittedPurposesWithNames; // keys are IDs, values are names
    }
    function cmpConvertResponseToGroupList(cmpRawOutput) {
        var permittedPurposesWithNames = cmpConvertResponseToLookupObject(cmpRawOutput);
        var keysOrValues = useNamesInsteadOfKeys ? &#34;values&#34; : &#34;keys&#34;;
        return Object[keysOrValues](permittedPurposesWithNames); // keys are IDs, values are names
    }
    function cmpAddCallbackToTriggerRecheck(triggerRecheck) {
        if (typeof triggerRecheck !== &#39;function&#39;) return false;
        // An official Google dataLayer listener, pulled from https://github.com/google/data-layer-helper/blob/master/dist/data-layer-helper.js, see https://github.com/google/data-layer-helper
        (function () {/*
         Copyright The Closure Library Authors.
         SPDX-License-Identifier: Apache-2.0
        */
            &#39;use strict&#39;;/*
         jQuery v1.9.1 (c) 2005, 2012
         jQuery Foundation, Inc. jquery.org/license.
        */
            var f = /\[object (Boolean|Number|String|Function|Array|Date|RegExp|Arguments)\]/; function g(a) { return null == a ? String(a) : (a = f.exec(Object.prototype.toString.call(Object(a)))) ? a[1].toLowerCase() : &#34;object&#34; } function m(a, b) { return Object.prototype.hasOwnProperty.call(Object(a), b) } function n(a) { if (!a || &#34;object&#34; != g(a) || a.nodeType || a == a.window) return !1; try { if (a.constructor &amp;&amp; !m(a, &#34;constructor&#34;) &amp;&amp; !m(a.constructor.prototype, &#34;isPrototypeOf&#34;)) return !1 } catch (c) { return !1 } for (var b in a); return void 0 === b || m(a, b) }; function p(a, b) { var c = {}, d = c; a = a.split(&#34;.&#34;); for (var e = 0; e &lt; a.length - 1; e&#43;&#43;)d = d[a[e]] = {}; d[a[a.length - 1]] = b; return c } function q(a, b) { var c = !a._clear, d; for (d in a) if (m(a, d)) { var e = a[d]; &#34;array&#34; === g(e) &amp;&amp; c ? (&#34;array&#34; === g(b[d]) || (b[d] = []), q(e, b[d])) : n(e) &amp;&amp; c ? (n(b[d]) || (b[d] = {}), q(e, b[d])) : b[d] = e } delete b._clear };/* Copyright 2012 Google Inc. All rights reserved. */
            function r(a, b, c) {
                b = void 0 === b ? {} : b; &#34;function&#34; === typeof b ? b = { listener: b, listenToPast: void 0 === c ? !1 : c, processNow: !0, commandProcessors: {} } : b = { listener: b.listener || function () { }, listenToPast: b.listenToPast || !1, processNow: void 0 === b.processNow ? !0 : b.processNow, commandProcessors: b.commandProcessors || {} }; this.a = a; this.l = b.listener; this.j = b.listenToPast; this.g = this.i = !1; this.c = {}; this.f = []; this.b = b.commandProcessors; this.h = u(this); var d = this.a.push, e = this; this.a.push = function () {
                    var k = [].slice.call(arguments,
                        0), l = d.apply(e.a, k); v(e, k); return l
                }; b.processNow &amp;&amp; this.process()
            } r.prototype.process = function () { this.registerProcessor(&#34;set&#34;, function () { var c = {}; 1 === arguments.length &amp;&amp; &#34;object&#34; === g(arguments[0]) ? c = arguments[0] : 2 === arguments.length &amp;&amp; &#34;string&#34; === g(arguments[0]) &amp;&amp; (c = p(arguments[0], arguments[1])); return c }); this.i = !0; for (var a = this.a.length, b = 0; b &lt; a; b&#43;&#43;)v(this, [this.a[b]], !this.j) }; r.prototype.get = function (a) { var b = this.c; a = a.split(&#34;.&#34;); for (var c = 0; c &lt; a.length; c&#43;&#43;) { if (void 0 === b[a[c]]) return; b = b[a[c]] } return b };
            r.prototype.flatten = function () { this.a.splice(0, this.a.length); this.a[0] = {}; q(this.c, this.a[0]) }; r.prototype.registerProcessor = function (a, b) { a in this.b || (this.b[a] = []); this.b[a].push(b) };
            function v(a, b, c) {
                c = void 0 === c ? !1 : c; if (a.i &amp;&amp; (a.f.push.apply(a.f, b), !a.g)) for (; 0 &lt; a.f.length;) {
                    b = a.f.shift(); if (&#34;array&#34; === g(b)) a: { var d = a.c; g(b[0]); for (var e = b[0].split(&#34;.&#34;), k = e.pop(), l = b.slice(1), h = 0; h &lt; e.length; h&#43;&#43;) { if (void 0 === d[e[h]]) break a; d = d[e[h]] } try { d[k].apply(d, l) } catch (w) { } } else if (&#34;arguments&#34; === g(b)) { e = a; k = []; l = b[0]; if (e.b[l]) for (d = e.b[l].length, h = 0; h &lt; d; h&#43;&#43;)k.push(e.b[l][h].apply(e.h, [].slice.call(b, 1))); a.f.push.apply(a.f, k) } else if (&#34;function&#34; == typeof b) try { b.call(a.h) } catch (w) { } else if (n(b)) for (var t in b) q(p(t,
                        b[t]), a.c); else continue; c || (a.g = !0, a.l(a.c, b), a.g = !1)
                }
            } r.prototype.registerProcessor = r.prototype.registerProcessor; r.prototype.flatten = r.prototype.flatten; r.prototype.get = r.prototype.get; r.prototype.process = r.prototype.process; window.DataLayerHelper = r; function u(a) { return { set: function (b, c) { q(p(b, c), a.c) }, get: function (b) { return a.get(b) } } };
        })();
        function listener(model, message) {
            // Message has been pushed. 
            // The helper has merged it onto the model.
            // Now use the message and the updated model to do something.
            if ([&#34;OneTrustGroupsUpdated&#34;, &#34;OneTrustLoaded&#34;].indexOf(message.event) !== -1) {
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
        // treat things we don&#39;t understand as an opt-out
        if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false;
        tiqGroupName = tiqGroupName || &#34;tiq-group-name-missing&#34;;
        var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput);
        return allowedGroups.indexOf(tiqGroupName) !== -1;
    }
})(window);


/*
// Debugging / development output - paste into the console, or uncomment and paste the whole template during development of a custom integration
function outputDebuggingInfo () {
  var outputString = `${tealiumCmpIntegration.cmpCheckIfOptInModel() ? &#39;Opt-in&#39; : &#39;Opt-out&#39;} Model
  Checks:
    - id:                 ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
    - well-formed:        ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - explicit:           ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - using callback:     ${typeof tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck === &#39;function&#39;}
    - consented purposes: ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}
  `
  console.log(outputString);
}
// use the callback function to avoid console posting while debugging and allow testing of the callback function itself
if (typeof tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck === &#39;function&#39;) {
    tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck(outputDebuggingInfo)
}
outputDebuggingInfo();
*/
```




### Opt-out Cookie &#43; GPC

This integration intends to provide support for very simple opt-out models such as CCPA/CPRA. It interprets the **Vendor ID** field as the cookie name of an opt-out cookie, and is case sensitive. A user is considered to have opted out if this cookie is found with any value, or if the [Global Privacy Control (GPC)]() opt-out signal is found.

The **Purpose Keys** used in the integration and included in the default **Purpose Group** are:

* `no-selling` - For tags to allow regardless of the user&#39;s opt-out signal. These tags don&#39;t sell/share data or are considered strictly necessary by your legal team, etc.
* `yes-selling` - For tags to block for opt-out users because applicable regulations or policies prohibit tracking after a user has opted out.

### TrustArc

Test this snippet on [trustarc.com](https://trustarc.com/) or on your website by following the instructions in the [How it works section](#how-it-works) to check compatibility and get the information needed for integration.


```js
;(function trustarcIntegration (window) {

  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = &#39;TrustArc&#39;
  window.tealiumCmpIntegration.cmpIntegrationVersion = &#39;trustarc-1.0.4&#39;

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject

  function cmpCheckIfOptInModel () {
    var preferredButNewMethod = window.truste &amp;&amp; window.truste.eu &amp;&amp; window.truste.eu.bindMap &amp;&amp; window.truste.eu.bindMap.consentModel;
    if (typeof preferredButNewMethod === &#39;string&#39; &amp;&amp; preferredButNewMethod !== &#39;none&#39;) return preferredButNewMethod !== &#39;opt-out&#39;; 
    var modeCookieValue = ((window.truste &amp;&amp; window.truste.util &amp;&amp; typeof window.truste.util.readCookie === &#39;function&#39; &amp;&amp; window.truste.util.readCookie(&#39;notice_behavior&#39;)) || &#39;expressed|eu&#39;)
    return modeCookieValue.indexOf(&#39;expressed&#39;) === 0
  }

  var trustArcMap = {
      0: &#39;Required&#39;,
      1: &#39;Functional&#39;,
      2: &#39;Personalization/Advertising&#39;
  }

  function cmpFetchCurrentConsentDecision () {
    if (!window.truste || !window.truste.util || typeof window.truste.util.readCookie !== &#39;function&#39;) return false;

    var cookieValue =  window.truste.util.readCookie(truste.eu.COOKIE_GDPR_PREF_NAME) || &#39;0,&#39;

    if (cmpCheckIfOptInModel() === false &amp;&amp; cmpCheckForExplicitConsentDecision() === false) {
      cookieValue = Object.keys(trustArcMap).join(&#39;,&#39;) 
    }

    return {
      cookie: cookieValue
    }
  }

  function cmpFetchCurrentLookupKey () {
    return (window.tealiumCmpIntegration &amp;&amp; window.tealiumCmpIntegration.map &amp;&amp; Object.keys(window.tealiumCmpIntegration.map)[0]) || &#39;(Vendor ID check disabled for this integration)&#39;
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    if (typeof cmpRawOutput !== &#39;object&#39;) return false
    if (typeof cmpRawOutput.cookie !== &#39;string&#39;) return false
    return true
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    if (!window.truste || !window.truste.util || typeof window.truste.util.readCookie !== &#39;function&#39;) return false
    return typeof window.truste.util.readCookie(truste.eu.COOKIE_GDPR_PREF_NAME) === &#39;string&#39;
  }

  function cmpConvertResponseToLookupObject (cmpRawOutput) {
    if (!cmpCheckForWellFormedDecision(cmpRawOutput)) return []
    const cookieConsentValues = cmpRawOutput.cookie.split(&#39;:&#39;)[0].split(&#39;,&#39;)
    const extraSplit = []
    cookieConsentValues.forEach((el) =&gt; {
      if (!el) return
      extraSplit.push.apply(extraSplit, el.split(&#39;|&#39;))
    })

    const output = {}

    extraSplit.forEach((key) =&gt; {
      if (key !== &#39;&#39;) {
        output[key] = trustArcMap[key] || &#39;Category name unknown&#39;
      }
    })

    return output
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    var permittedPurposesWithNames = cmpConvertResponseToLookupObject(cmpRawOutput)
    var keysOrValues = &#39;keys&#39;
    return Object[keysOrValues](permittedPurposesWithNames) 
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false

    tiqGroupName = tiqGroupName || &#39;tiq-group-name-missing&#39;
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
    return allowedGroups.indexOf(tiqGroupName) !== -1
  }
})(window)

/*
// Debugging - uncomment this code and paste the integration into the console on your test pages each time you make a change to your consent state to test without publishing
var outputString = `CMP Found: ${window.tealiumCmpIntegration.cmpName} (${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? &#39;Opt-in&#39; : &#39;Opt-out&#39;} Model)

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

  window.tealiumCmpIntegration.cmpName = &#39;Usercentrics Browser SDK&#39;
  window.tealiumCmpIntegration.cmpIntegrationVersion = &#39;usercentrics-1.0.3&#39;

  function cmpFetchCurrentConsentDecision () {
    if (!window.UC_UI || typeof window.UC_UI.getServicesBaseInfo !== &#39;function&#39;) return false
    var cmpRawOutput = window.UC_UI.getServicesBaseInfo()
    return cmpRawOutput
  }

  function cmpFetchCurrentLookupKey () {
    return (window.UC_UI &amp;&amp; typeof window.UC_UI.getSettingsCore === &#39;function&#39; &amp;&amp; window.UC_UI.getSettingsCore().id) || &#39;&#39;
  }

  // only support opt-In model for Usercentrics for now, can be added if needed
  function cmpCheckIfOptInModel () {
    return window.UC_UI &amp;&amp; typeof window.UC_UI.isConsentRequired === &#39;function&#39; &amp;&amp; window.UC_UI.isConsentRequired() === true
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    // treat things we don&#39;t understand as an opt-out
    if (toString.call(cmpRawOutput) !== &#39;[object Array]&#39;) return false
    // use the first entry as a proxy for all
    if (cmpRawOutput &amp;&amp; cmpRawOutput[0] &amp;&amp; typeof cmpRawOutput[0].name === &#39;string&#39;) {
      return true
    }
    return false
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    // treat things we don&#39;t understand as an opt-out
    if (toString.call(cmpRawOutput) !== &#39;[object Array]&#39;) return false
    // use the first entry as a proxy for all
    var consentHistory = (cmpRawOutput &amp;&amp; cmpRawOutput[0] &amp;&amp; cmpRawOutput[0].consent &amp;&amp; cmpRawOutput[0].consent.history) || []
    var lastHistoryEntryType = (consentHistory &amp;&amp; consentHistory.length &amp;&amp; consentHistory[consentHistory.length - 1].type) || &#39;&#39;
    if (lastHistoryEntryType === &#39;explicit&#39;) {
      return true
    }
    return false
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    var foundOptIn = false
    // treat things we don&#39;t understand as an opt-out
    if (toString.call(cmpRawOutput) !== &#39;[object Array]&#39;) return false
    // use the mapping if found, with a fallback (Usercentrics default value) if not specified in the mapping

    tiqGroupName = tiqGroupName || &#39;tiq-group-name-missing&#39;
    // check vendors if there&#39;s an object, look for at least one
    cmpRawOutput.forEach(function (tagInfo) {
      if ((tagInfo.consent &amp;&amp; tagInfo.consent.status === true) &amp;&amp; tagInfo.name === tiqGroupName) {
        foundOptIn = true
      }
    })
    return foundOptIn
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    var vendorArray = []
    cmpRawOutput &amp;&amp; cmpRawOutput.forEach(function (tagConsent) {
      if (tagConsent.consent &amp;&amp; tagConsent.consent.status === true) {
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

var outputString = `${tealiumCmpIntegration.cmpName} - ${tealiumCmpIntegration.cmpCheckIfOptInModel() ? &#39;Opt-in&#39; : &#39;Opt-out&#39;} Model

Checks:
  - vendor id:            ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
  - well-formed decision: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - explicit decision:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - consented purposes:   ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()).sort(),null, 8)}
`
console.log(outputString)
```


### Custom Integration template

For more information about the custom integration template and how to use it, see [Custom integration]().