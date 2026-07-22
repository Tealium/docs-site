---
title: GDPR Functions
description: Reference guide for GDPR functions provided by Tealium for JavaScript.
url: https://docs.tealium.com/platforms/javascript/api/gdpr-functions/
---
The following `utag.gdpr` functions are available:

| Function | Description |
| --- | --- |
| [`dns.getDnsState()`](#utaggdprdnsgetdnsstate) | Returns the value of the `dns` consent cookie. |
| [`dns.setDnsState()`](#utaggdprdnssetdnsstate) | Sets the value of the `dns` consent cookie. |
| [`getCategories()`](#utaggdprgetcategories) | Returns an `Array` with the list of compliance categories available for grouping tags.|
| [`getCategoryLanguage()`](#utaggdprgetcategorylanguage) | Returns an `Object` with the category name and description in the active language. |
| [`getConsentState()`](#utaggdprgetconsentstate) | Returns the consent given by the user either as full, declined, no consent, or partial consent. |
| [`getCookieValues()`](#utaggdprgetcookievalues) | Returns an `Object` representing the consent cookie. |
| [`getLanguage()`](#utaggdprgetlanguage) | Returns a `String` with the language used for displaying the consent manager content. |
| [`getSelectedCategories()`](#utaggdprgetselectedcategories) | Returns an `Array` with the categories selected by the customer. |
| [`setAllCategories()`](#utaggdprsetallcategories) | Sets all categories to the same consent state of either consented or declined, and (optionally) calls the Collect API to track the consent. |
| [`setConsentValue()`](#utaggdprsetconsentvalue) | Sets the consent cookie value to enabled or disabled. |
| [`setCookie()`](#utaggdprsetcookie) | Internal function that writes directly to the cookie `Object`. |
| [`setCookieValue()`](#utaggdprsetcookievalue) | Sets an individual value in the consent cookie. |
| [`setPreferencesFromList()`](#utaggdprsetpreferencesfromlist) | Sets the consent state to `allowed` for a list of categories. |
| [`setPreferencesValues()`](#utaggdprsetpreferencesvalues) | Sets the cookie values from an `Object` of categories and their consent state. |
| [`showConsentPreferences()`](#utaggdprshowconsentpreferences) | Displays the preferences manager pop-up. |
| [`showDoNotSellBanner()`](#utaggdprshowdonotsellbanner) | Displays the CCPA banner. | 
| [`showDoNotSellPrompt()`](#utaggdprshowdonotsellprompt) | Displays the CCPA banner. |
| [`showExplicitConsent()`](#utaggdprshowexplicitconsent) | Displays the explicit consent pop-up. |
| [`updateConsentCookie()`](#utaggdprupdateconsentcookie) | Updates mobile consent from an app using hidden webview. |


## `utag.gdpr.dns.getDnsState()`

Returns the value of the `dns` consent cookie (`true` or `false`).


## `utag.gdpr.dns.setDnsState()`

Sets the value of the `dns` consent cookie. Recognized values: `true`, `false`, `1`, `0`, `"true"`, `"false"`.

Example:
```js
utag.gdpr.dns.setDnsState(true);
```

## `utag.gdpr.getCategories()`

Returns an `Array` with the list of compliance categories available for grouping tags. All categories are returned if no parameter is provided. Pass `true` or `1` as a parameter to only return enabled (active) categories in the Tealium Consent Preference Manager interface.

```js
utag.gdpr.getCategories(onlyEnabledCats)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `onlyEnabledCats` | `Boolean` | (Optional) Set to `true` or `1` to return enabled (active) categories. |


The following example shows the results when `utag.gdpr.getCategories()` returns all categories:  
```js
["analytics", "affiliates", "display_ads", "search", "email", "personalization", "social", "big_data", "misc", "cookiematch", "cdp", "mobile", "engagement", "monitoring", "crm"]
```

The following example shows the results when `utag.gdpr.getCategories()` returns the enabled categories:    
```js
["analytics", "affiliates", "personalization"]
```

## `utag.gdpr.getCategoryLanguage()`

Returns an `Object` with the category name and description in the active language. The language of the category is the language returned by the `getLanguage()` function.

For more information on categories, see [Manage consent preferences](https://docs.tealium.com/iq-tag-management/consent-management/consent-preferences-dialog/manage#categories).

```js
utag.gdpr.getCategoryLanguage(category)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `category` | `String` | Name of category. |

The following example shows the `Object` returned by `utag.gdpr.getCategoryLanguage("analytics")` when the language is English:

```js
{name: "Cookies that help us improve our website", notes: "These cookies help us understand how people use our website."}
```
The following example shows the `Object` returned by `utag.gdpr.getCategoryLanguage("analytics")` when the language is Polish:

```js
{name: "Pliki cookie dotyczące wydajności", notes: "Te pliki cookie gromadzą informacje o tym, jak odw…dynie w celu ulepszania działania naszej witryny."}
```

## `utag.gdpr.getConsentState()`

Returns one of two data types, as follows:

* A numeric value indicating the consent state (full, declined, or no consent).
* For partial consent, an `Array` of `Objects` specifying consent by category.

When full, declined, or no consent is given, one of the following consent state values is returned:

| Consent State | Consent Value | Description |
|---| --- | --- |
| Full | `1` | Full consent was given (`consent:true` on the cookie). |
| Decline | `-1` | Consent was declined (`consent:false` on the cookie). |
| None Given | `0` | No consent is given (no cookie present). |

When partial consent is given, an `Array` of `Objects` is returned. Each `Object` represents a consent category. For each `Object` in the `Array`, the `"ct"` key represents the consent value (`1`/`0`), and the `"name"` key specifies the consent category.

```js
utag.gdpr.getConsentState()
```

The following example shows an `Array` of `Objects` returned for partial consent:

```js
[{"ct":"1","name":"analytics"},
{"ct":"0","name":"affiliates"},
{"ct":"0","name":"display_ads"},
{"ct":"0","name":"search"},
{"ct":"0","name":"email"},
{"ct":"0","name":"personalization"},
{"ct":"0","name":"social"},
{"ct":"0","name":"big_data"},
{"ct":"0","name":"misc"},
{"ct":"0","name":"cookiematch"},
{"ct":"0","name":"cdp"},
{"ct":"0","name":"mobile"},
{"ct":"0","name":"engagement"},
{"ct":"0","name":"monitoring"},
{"ct":"0","name":"crm"}]
```

## `utag.gdpr.getCookieValues()`


<blockquote>
Instead of using this function directly, it is recommended that you use a function such as `utag.gdpr.getConsentState()`, which calls the `getCookieValues()` function to read the cookie.
</blockquote>


Returns an `Object` representing the consent cookie as key-value pairs. This function uses the default cookie namespace (`CONSENTMGR`) or the value provided in `window.utag_cfg_ovrd.cmcookiens`. The reverse function (writing into the cookie) is `utag.gdpr.setCookie()`.

```js
utag.gdpr.getCookieValues()
```

The following example shows the `Array` returned by `utag.gdpr.getCookieValues()` for partial consent:  

```js
{
    "c1":"1",
    "c2":"0",
    "c3":"0",
    "c4":"0",
    "c5":"0",
    "c6":"0",
    "c7":"0",
    "c8":"0",
    "C9":"0",
    "c10":"0",
    "c11":"0",
    "c12":"0",
    "c13":"0",
    "c14":"0",
    "c15":"0",
    "ts":"1586965568213",
    "consent":"true"
}
```
The following example shows the `Array` returned by `utag.gdpr.getCookieValues()` for full consent:  
```js
utag.gdpr.getCategories(true)

{"consent":"true","ts":"1587026030058"}
```

## `utag.gdpr.getLanguage()`

Returns a `String` with the language used for displaying the consent manager content. Ordered by precedence of the language as set up in the data layer, the language from the browser, or the default language.

```js
utag.gdpr.getLanguage()
```

The following example shows the `String` returned when the language is English (United Kingdom):

```js
"en-gb"
```

## `utag.gdpr.getSelectedCategories()`

Returns an `Array` that contains the categories selected by the customer.

```js
utag.gdpr.getSelectedCategories()
```

The following example shows an `Array` returned by `utag.gdpr.getSelectedCategories()`:

```js
["analytics", "personalization"]
```

## `utag.gdpr.setAllCategories()`

Sets all categories to the same consent state of either consented or declined, and (optionally) calls the Collect API to track the consent.

```js
utag.gdpr.setAllCategories(state, noCollect)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `state` | `Boolean` | Set to `true` to allow consent to all categories, set to `false` to decline consent. |
| `noCollect` | `Boolean` | (Optional) Set to `true` to not call the Collect API to track the consent. |

The following example specifies consent for all categories, with no call to the Collect API:  
```js
utag.gdpr.setAllCategories(true,true)
```

The following example declines consent for all categories, and calls the Collect API to track the consent:
```js
utag.gdpr.setAllCategories(false)
```

## `utag.gdpr.setConsentValue()`

Sets the consent cookie value to enabled or disabled. The function also updates the timestamp of consent, and generates a tracking call to the Collect API, and replays tags that are kept in the queue `utag.gdpr.queue`.


<blockquote>
`utag.gdpr.setConsentValue()` doesn’t change the consent value of individual categories. The consent value needs to be disabled through the relevant API call (`setPreferencesFromList()` or `setPreferencesValues()`).
</blockquote>


```js
utag.gdpr.setConsentValue(_response)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `_response` | `Boolean` | Set to `true` enable consent, or `false` to disable consent. |

The following example sets the cookie to the value `"consent:true"` and updates the timestamp:  
```js
utag.gdpr.setConsentValue(true)
```
The following example sets the cookie to the value `"consent:false"` and updates the timestamp:  
```js
utag.gdpr.setConsentValue(0)
```

## `utag.gdpr.setCookie()`


<blockquote>
We do not recommend calling  this function directly.
</blockquote>


Internal function that writes directly to the cookie `Object`. It uses an `Object` to represent the consent state, the timestamp, and the various categories for partial consent. It automatically uses the correct cookie name and expiry period.

```js
utag.gdpr.setCookie(onlyEnabledCats)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `cookieData` | `Object` | List of key-values representing the data stored in the consent cookie. |

Example:

```js
var object = {"c6":"1","c1":"0","c2":"0","ts":1587133550264,"consent":"false","c3":"0","c4":"0","c5":"0","c7":"0","c8":"0","c9":"0","c10":"0","c11":"0","c12":"0","c13":"0","c14":"0","c15":"0"}

utag.gdpr.setCookie(object)
```

## `utag.gdpr.setCookieValue()`

Sets an individual value in the consent cookie.


<blockquote>
This function is used by other higher level functions such as `setConsentValue()`. Use this method cautiously and only if higher level functions do not fulfill the initial needs.
</blockquote>


```js
utag.gdpr.setCookieValue(key, value);
```

| Parameter | Type | Description |
| --- | --- | --- |
| `key` | `String` | Key used in the cookie that is set to either `consent`, `ts` or any of the categories specified by the `c` value representation, such as `c1` for Analytics or `c2` for Affiliates. |
| `value` | `String` | The value to set in the cookie key. |

The following example sets the consent cookie to `"consent:false"`:  
```js
utag.gdpr.setCookieValue("consent", false);
```

The following example sets consent cookie to `"c1:0"`:  
```js
utag.gdpr.setCookieValue("c1", 0);
```

## `utag.gdpr.setPreferencesFromList()`

Sets the consent state to `allowed` for the list of categories passed in the parameter. The consent state of the categories that are not in the list is set to `declined`. This is used for partial consent. This function relies on the `setPreferencesValues()` function and provides the reverse functionality of `getSelectedCategories()`.

```js
utag.gdpr.setPreferencesFromList(list)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `List` |`Array` | `Array` of valid categories. |

The following example sets the consent state for the `"analytics"` category in the consent cookie:

```js
utag.gdpr.setPreferencesFromList(["analytics"])
```

## `utag.gdpr.setPreferencesValues()`

Sets the cookie preferences values from an `Object` of categories and their consent state. This function is mainly called by the `setPreferencesFromList()` function. This function replays the tags that are kept in the queue `utag.gdpr.queue`.

```js
utag.gdpr.setPreferencesValues(state, noCollect)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `state` | `Object` | Key-value pairs in the format `category:consentState`. |
| `noCollect` | `Boolean` | (Optional) Set to `true` to not call the Collect API to track the consent. |

The following example sets the cookie value for the `"analytics"`, `"affiliates"`, and `"personalization"` categories:  
```js
Var cats = {"analytics":"1","affiliates":"0","personalization":"0"}
utag.gdpr.setPreferencesValues(cats)
```

## `utag.gdpr.showConsentPreferences()`

Displays the consent preferences pop-up. This function injects the CSS, the HTML and the Javascript defined in the customizations in the page. It is called by the explicit consent javascript listener or from any point in the page where the user wants to modify their preferences.

```js
utag.gdpr.showConsentPreferences(_lang)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `_lang` | `String` | (Optional) Language specified in ISO format, such as `en` or `en-gb`. |

The following example displays consent in the default language or the language set up in the data layer:  
```js
utag.gdpr.showConsentPreferences()
```

The following example displays consent in French:  
```js
utag.gdpr.showConsentPreferences("fr-fr")
```

## `utag.gdpr.showDoNotSellBanner()`

Displays the CCPA banner. By default, this function is called when the enforcement rule evaluates to `true`.

```js
utag.gdpr.showDoNotSellBanner(_lang)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `_lang` | `String` | (Optional) Language specified in ISO format, such as `en` or `en-gb`. |

The following example displays the CCPA banner in the default language or the language set up in the data layer:  

```js
utag.gdpr.showDoNotSellBanner()
```

The following example displays the Opt-out banner in French:  
```js
utag.gdpr.showDoNotSellBanner("fr-fr")
```

## `utag.gdpr.showDoNotSellPrompt()`

Displays the Opt-out popup. If you are not using the banner, integrate this function into your site banner to provide visitors a way to change their consent setting.

```js
utag.gdpr.showDoNotSellPrompt(_lang)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `_lang` | `String` | (Optional) Language specified in ISO format, such as `en` or `en-gb`. |

The following example displays the CCPA popup in the default language or the language set up in the data layer:  

```js
<a href="javascript: utag.gdpr.showDoNotSellPrompt()">Change Consent</a>
```

The following example displays the Opt-out Model popup in French:  
```js
<a href="javascript: utag.gdpr.showDoNotSellPrompt('fr-fr')">Change Consent</a>
```

## `utag.gdpr.showExplicitConsent()`

Displays the explicit consent pop-up. This function injects the CSS, the HTML and the Javascript defined in the customizations in the page. It is natively called by the Tealium Universal Tag `utag.js` on `DOM READY` event when the explicit consent is set up.

```js
utag.gdpr.showExplicitConsent(_lang)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `_lang` | `String` | (Optional) Language specified in ISO format, such as `en` or `en-gb`. |

The following example displays explicit consent in the default language or the language set up in the data layer:   
```js
utag.gdpr.showExplicitConsent()
```
The following example displays explicit consent in French:  
```js
utag.gdpr.showExplicitConsent("fr-fr")
```

## `utag.gdpr.updateConsentCookie()`

Updates mobile consent from an app using hidden webview.

```js
utag.gdpr.updateConsentCookie()
```
