---
title: Tealium + Adobe Target integration guide
description: Use data layer enrichment to inject visitor data into Adobe Target for client-side personalization.
url: https://docs.tealium.com/partners-and-industries/tech-partners/tealium-adobe-target-dle-integration-guide/
---
## About

Use this guide to personalize Adobe Target experiences with visitor audiences, badges, and properties from Tealium. The integration runs in-session, on the client side, with no server-side connector required. Data layer enrichment (DLE) makes visitor data available in the browser, and the Adobe Target `dataProviders` hook lets you pass that data into mbox requests before `at.js` fires.

## Requirements

This integration requires the following:

* An active Tealium CDP profile with visit and visitor attributes defined.
* DLE enabled in Tealium Tag Management publish settings. For more information, see [Enable data layer enrichment](https://docs.tealium.com/enable-data-layer-enrichment/).
* Tealium Collect tag deployed on all pages with DLE enabled. For more information, see [Add and configure the Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/).
* Visitor attributes synced as data layer variables in Tealium Tag Management.
* Adobe Target deployed with `at.js` 2.x.


<blockquote>
`dataProviders` is available in `at.js` 1.3 and later. This guide uses `at.js` 2.x and does not apply to `mbox.js` implementations.
</blockquote>


## How it works

When DLE is active, the Tealium Collect tag asynchronously fetches the visitor profile and stores it in `localStorage` under the key `tealium_va`. The stored value is a stringified JSON object with `audiences` and `badges` objects, plus a `properties` object keyed by attribute ID.

`at.js` supports a `dataProviders` configuration hook inside `targetGlobalSettings`. Each `dataProviders` entry is an object with `name`, `version`, and `provider(callback)`. Adobe Target runs the provider before the global mbox request and merges the key-value pairs passed to the callback into the request.

The integration registers a data provider object that reads `tealium_va`, parses it, and passes flattened key-value parameters to the callback. Adobe Target appends those parameters to the mbox call before sending the request.


<blockquote>
DLE fetches the visitor profile asynchronously. On a new visitor's first page view, `tealium_va` is likely empty when `at.js` fires. Visitor data is available starting on the second page view, or on subsequent SPA route changes.
</blockquote>


## Add the data provider

The following JavaScript reads `tealium_va` from `localStorage` and registers a data provider. Replace the placeholder attribute IDs with your AudienceStream string attribute IDs. The code must execute before `at.js` loads.

```javascript
window.targetGlobalSettings = window.targetGlobalSettings || {};
window.targetGlobalSettings.dataProviders = window.targetGlobalSettings.dataProviders || [];

window.targetGlobalSettings.dataProviders.push({
  name: "tealium-dle",
  version: "1.0.0",
  provider: function(callback) {
    var tealiumTargetData = {};
    var attributeIdMap = {
      tealium_ltv: "ATTRIBUTE_ID_FOR_CUSTOMER_LTV",
      profile_tealium_lifecycle: "ATTRIBUTE_ID_FOR_LIFECYCLE_STAGE"
    };

    try {
      var dleString = localStorage.getItem("tealium_va");

      if (dleString) {
        var dleObject = JSON.parse(dleString);
        var audienceNames = dleObject.audiences ? Object.keys(dleObject.audiences).map(function(key) {
          return dleObject.audiences[key];
        }) : [];
        var badgeIds = dleObject.badges ? Object.keys(dleObject.badges) : [];

        if (audienceNames.length > 0) {
          tealiumTargetData["profile.tealium_audiences"] = audienceNames.join("|");
        }

        if (badgeIds.length > 0) {
          tealiumTargetData["profile.tealium_badges"] = badgeIds.join("|");
        }

        if (dleObject.properties) {
          if (dleObject.properties[attributeIdMap.tealium_ltv]) {
            tealiumTargetData.tealium_ltv = dleObject.properties[attributeIdMap.tealium_ltv];
          }
          if (dleObject.properties[attributeIdMap.profile_tealium_lifecycle]) {
            tealiumTargetData["profile.tealium_lifecycle"] = dleObject.properties[attributeIdMap.profile_tealium_lifecycle];
          }
        }
      }
    } catch (e) {
      console.error("Adobe Target Data Provider: Error parsing Tealium DLE data", e);
    }

    callback(tealiumTargetData);
  }
});
```

Deploy the snippet using one of the following options.

* **Direct page placement**  
Add the snippet in the `<head>` of the page, above the `<script>` tag that loads `at.js`.
* **Tealium iQ Pre-Loader extension**  
Create a [JavaScript Code extension](https://docs.tealium.com/javascript-code-extension/) scoped to **Pre Loader**, paste the snippet into the extension editor, and save and publish the changes. This option keeps the code managed inside Tealium.

## About parameter types

Adobe Target supports two types of parameters in mbox requests. The type determines how long Target retains the value and where it is available for targeting.

**Profile parameters** use the `profile.` prefix. Adobe Target stores profile parameters persistently in the visitor's Target profile across sessions. Profile parameter values remain available even if `localStorage` is cleared. Use profile parameters for audiences and badges that drive long-term targeting, for example `profile.tealium_audiences` or `profile.tealium_badges`.

**Mbox parameters** have no prefix. Adobe Target evaluates mbox parameters only for the current page or mbox call. Use mbox parameters for values that change frequently or apply only to the current page view, for example `tealium_ltv`.

Adobe Target does not accept nested JSON in mbox calls. Flatten all values from the DLE object into direct key-value string pairs before passing them to the `dataProviders` callback. Join multi-value fields with a pipe (`|`) or comma delimiter.

## Related information

* [About data layer enrichment](https://docs.tealium.com/about-data-layer-enrichment/)
* [Enable data layer enrichment](https://docs.tealium.com/enable-data-layer-enrichment/)
* [Add and configure the Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/)
* [Adobe Target tag setup guide](https://docs.tealium.com/adobe-target-tag/)
* [Adobe Target connector](https://docs.tealium.com/adobe-target-connector/): Use the server-side connector for next-session personalization or offline profile updates. For in-session, next-page personalization, use this DLE pattern.
