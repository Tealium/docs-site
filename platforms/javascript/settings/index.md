---
title: Settings
description: Learn about the available settings that adjust the behavior of `utag.js`.
url: https://docs.tealium.com/platforms/javascript/settings/
---
## How it works

Many of the behaviors of `utag.js` are controlled with settings in the `utag.cfg` object. The default behaviors controlled by these settings are overridden using a new object called `utag_cfg_ovrd`. To use this object, set it in your page code prior to loading `utag.js` or within a [JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/) scoped to **Pre Loader** with the following:

```js
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
```

## List of options

The following table summarizes the available settings:

| Setting | Description |
| ------- | ----------- |
| [`always_set_v_id`](#always_set_v_id)| Set the `utag_main_v_id` cookie or `v_id` component of `utag_main`. Default: `false` |
| [`cmcookiens`](#cmcookiens) | Consent management cookie name. |
| [`consentPeriod`](#consentperiod) | Set the number of days to retain the user's consent preference. |
| [`disable_tealium_attribute_override`](#disable_tealium_attribute_override) | Prevent system-defined attributes `tealium_*` from being overwritten by incoming data. |
| [`dom_complete`](#dom_complete) | Delay tags until the DOM complete (load) event. |
| [`domain`](#domain) | Override the domain used to set cookies. |
| [`gdprDLRef`](#gdprdlref) | Specify the name of the data layer variable which stores the language setting to be used by the consent manager. |
| [`ignoreLocalStorage`](#ignorelocalstorage) | Do not add local storage variables to the data layer. |
| [`ignoreSessionStorage`](#ignoresessionstorage) | Do not add session storage variables to the data layer. |
| [`load_rules_ajax`](#load_rules_ajax) |Disable load rules after page load (legacy). |
| [`load_rules_at_wait`](#load_rules_at_wait) | Run load rules after extensions (legacy). |
| [`lowermeta`](#lowermeta)| Lower-case meta tag names and values (legacy). |
| [`lowerqp`](#lowerqp)| Lower-case query string parameter names and values (legacy). |
| [`noload`](#noload) | Disable all functionality. |
| [`noview`](#noview) | Disable the automatic tracking call on initial page load. |
| [`nocookie`](#nocookie) | Disable the `utag_main` cookie. |
| [`nonblocking_tags`](#nonblocking_tags) | Make all tags nonblocking to improve performance and Interaction to Next Paint (INP) scores in extreme cases. Default: `false`. |
| [`path`](#path) | Specifies the publishing path. |
| [`readywait`](#readywait) | Halt operations until the DOM-ready browser event. |
| [`secure_cookie`](#secure_cookie) | Set the attribute string to `secure` for all `utag_main` cookies set by the [Persist Data Values extension](https://docs.tealium.com/persist-data-value-extension/) and the [`utag.loader.SC`](https://docs.tealium.com/platforms/javascript/api/cookie-functions/#utagloadersc) method. |
| [`session_timeout`](#session_timeout)| Set the session expiration time (in milliseconds). |
| [`split_cookie`](#split_cookie)| Splits the `utag_main` cookie into standalone cookies. Default: `true` |
| [`split_cookie_allowlist`](#split_cookie_allowlist)| An array of allowed `utag_main` subcookies or standalone cookies. |
| [`suppress_before_load_rules_with_uids`](#suppress_before_load_rules_with_uids) | Force legacy behavior that skips extensions scoped to **Before Load Rules** when tracking tags by UID. Default: `false`. |
| [`waittimer`](#waittimer) | Set a time to delay (in milliseconds) before loading tags.|

### `always_set_v_id`

**Force `utag.js` to set the `utag_main_v_id` cookie or `v_id` component of `utag_main`**  
(New in [`utag.js` 4.50](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2023-09-01))  
The `v_id` variable of `utag_main` is set by the Tealium Collect tag to ensure that it complies with data privacy and consent purposes. Setting this to `true` forces `utag.js` to set this cookie for all visitors. (Default: `false`)

```js
window.utag_cfg_ovrd.always_set_v_id = true;
```

### `cmcookiens`

**Consent management cookie name**  
Customize the consent management cookie name. If you have multiple profiles on the same domain name, give each profile a unique consent management cookie name to prevent conflicts between the cookies and potential data leaks.

```js
window.utag_cfg_ovrd.cmcookiens = "CONSENTMGR_NL-CMB-CG1";
```

### `consentPeriod`

**Consent preference retention period**  
Set the number of days to retain GDPR and CCPA consent status. The built-in expiry is 365 days for GDPR and 395 days for CCPA.

```js
window.utag_cfg_ovrd.consentPeriod = 60;
```

### `disable_tealium_attribute_override`

**Prevent overrides of system-defined attributes**  

(New in [`utag.js` 4.54](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2025-10-22))

When set to `true`, this setting blocks incoming data from overwriting system-defined attributes that start with `tealium_`, such as `tealium_visitor_id`.  

In `utag.js` versions 4.52 and 4.53, this protection was enabled by default, which caused issues in some mobile webview environments. In version 4.54, the protection is now opt-in, allowing full control.

(Default: `false`)

```js
window.utag_cfg_ovrd.disable_tealium_attribute_override = true;
```

### `dom_complete`

**Delay tags until the DOM complete (load) browser event**  
Load tags at the [document load event](https://developer.mozilla.org/en-US/docs/Web/Events/load) rather than at DOM Ready. This also delays any extensions scoped to DOM Ready. (Default: `false`)

```js
window.utag_cfg_ovrd.dom_complete = true;
```

### `domain`

**Override the cookie domain**  
Sets the domain where `utag_main` cookie is set. Useful for sites on root domains that do not accept cookies. For example, `amazonaws.com`. (Default: The top-level domain of `location.hostname`)

```js
window.utag_cfg_ovrd.domain = "mysite.amazonaws.com";
```

### `gdprDLRef`

**Override language preference in the consent manager**  
Specify the name of the data layer variable which stores the language to be used in the consent manager.

For example, if your data layer contains a variable named `site_language`:

```js
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {}
window.utag_cfg_ovrd.gdprDLRef = "site_language";
```


<blockquote>
Do not set the language code directly. This override setting expects a variable name, not a language code value.
</blockquote>


### `ignoreLocalStorage`

**Ignore local storage variables**
Ignores any local storage variables. (Default: `false`)

```js
window.utag_cfg_ovrd.ignoreLocalStorage = true;
```


### `ignoreSessionStorage`

**Ignore session storage variables**
Ignores any session storage variables. (Default: `false`)

```js
window.utag_cfg_ovrd.ignoreSessionStorage = true;
```


### `load_rules_ajax`

**Disable load rules after page load (legacy)**  
Controls if load rules are reprocessed on each call to `utag.view` and `utag.link` within the same page load. It's possible that a newly triggered Load Rule loads a new tag into the page. Use this setting to replicate behavior from versions of `utag.js` older than 4.2x. (Default: `true`)

```js
window.utag_cfg_ovrd.load_rules_ajax = false;
```

### `load_rules_at_wait`

**Run load rules after extensions (legacy)**  
Evaluates Load Rules after extensions. Used for older versions of `utag.js` and for installations where the data layer object is populated after loading `utag.js`. Newer versions of `utag.js` make use of extension execution order instead of this setting. (Default: `false`)

```js
window.utag_cfg_ovrd.load_rules_at_wait = true;
```

### `lowermeta`

**Lower-case meta tag data (legacy)**  
Lower-case all meta data variable names and values. Replicates behavior in `utag.js` versions prior to 4.2x. (Default: `false`)

Example meta tag:
```html
<meta content="iQ Tag Management" property="Article:Section">
```

Resulting value:
```js
utag.data['meta.article:section']="iq tag management"
```

```js
window.utag_cfg_ovrd.lowermeta = true;
```

### `lowerqp`

**Lower-case query string parameter names and values (legacy)**  
Lower-case all query string variable names and values. Replicates behavior in `utag.js` versions prior to 4.2x. (Default: `false`)

Example query string parameter: `&RefId=Abc123`
Resulting value: `utag.data['qp.refid']="abc123"`

```js
window.utag_cfg_ovrd.lowerqp = true;
```

### `noload`

**Halt all operations**  
The execution of all code halts after the extensions scoped to **Pre Loader**. Extensions scoped to **DOM Ready** still run. This is normally adjusted using the publish setting for **Prevent Tag Load**. (Default: `0`)

```js
window.utag_cfg_ovrd.noload = true;
```

### `noview`

**Disable automatic tracking call on initial page load**  
Suppresses the tracking call that occurs automatically on initial page load. This setting is commonly used on single page application sites. (Default: `false`)

```js
window.utag_cfg_ovrd.noview = true;
```

### `nocookie`

**Cookie opt-out**  
Only set this option if a visitor has explicitly opted out of all cookies. (Default: `false`)

<blockquote>
Using this option inflates visitor and session counts, making all visits look like "single page sessions".
</blockquote>


This option disables _all_ cookies from being stored by `utag.js`, including cookies set with the [Persist Data Value extension](https://docs.tealium.com/persist-data-value-extension/), and session cookies. It also sets a new timestamp for the variables `ut.visitor_id`, `tealium_visitor_id`, and `cp.utag_main_v_id` when the cookie is not available.

```js
window.utag_cfg_ovrd.nocookie = true
```

### `nonblocking_tags`

**Load tags asynchronously**  
(New in [`utag.js` 4.52](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2024-12-18))  
This option enables non-blocking behavior for all tags, which can improve INP scores and overall page performance. Use this setting for pages with resource-intensive tags that slow down user interactions and reduce INP scores, but ensure you test exit link tracking thoroughly. (Default: `false`)

```js
window.utag_cfg_ovrd.nonblocking_tags = true;
```

#### Best practices

Use the following best practices with the `nonblocking_tags` setting:

* Measure and monitor your pages, and make your tag implementation lighter before you consider using the `nonblocking_tags` setting.
* Only use `nonblocking_tags` for pages with resource-intensive tags that exceed INP scores above 200 ms and don’t need to block DOM rendering.
* Consider navigation delays on critical navigation and exit events, since non-blocking tags load without holding the page for tracking (which is why they improve the INP score).

### `path`

**Publish URL path**  
Sets the publishing URL path for your tag templates, overriding the Publish URLs fields in the [Publish Configuration dialog](), if specified. Setting the publishing URL path can be useful for self-hosting and [First Party Domains]() customers.

```js
window.utag_cfg_ovrd.path = '//tags.example.com/main/prod';
```

### `readywait`

**Delay operations until DOM-ready**  
Halt all operations until the DOM-ready signal is received from the browser. Extensions scoped to **Pre Loader** still run when `utag.js` loads. (Default: `0`)

```js
window.utag_cfg_ovrd.readywait = true;
```

### `secure_cookie`

**Secure cookie**  
(New in [`utag.js` 4.48](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2021-04-01))  
Set the attribute string to `secure` for all `utag_main` cookies set by the [Persist Data Values extension](https://docs.tealium.com/persist-data-value-extension/) and the [`SC()`](https://docs.tealium.com/platforms/javascript/api/cookie-functions/#utag-loader-sc) function. Secure cookies can only be set and accessed on HTTPS pages. (Default: `false`)

```js
window.utag_cfg_ovrd.secure_cookie = true;
```

### `session_timeout`

**Session timeout** 
Sets how long to wait, in milliseconds, before expiring the current session. This is normally adjusted using the publish configuration setting for Session Timeout. (Default: `1800000` (30 minutes))

Example to set the timeout to 900000 milliseconds (15 minutes):
```js
window.utag_cfg_ovrd.session_timeout = 900000;
```

### `split_cookie`

**Standalone cookies**  
(New in [`utag.js` 4.50](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2023-09-01))  
Determines if `utag_` namespace cookies (like the built-in `utag_main` cookie) should be written as multi-value cookies or as standalone cookies by [`utag.loader.SC`](https://docs.tealium.com/platforms/javascript/api/cookie-functions/#utagloadersc). (Default: `true`)

```js
window.utag_cfg_ovrd.split_cookie = false;
```

### `split_cookie_allowlist`

**`utag_main` subcookies**  
(New in [`utag.js` 4.50](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2023-09-01))  
Specifies an array of allowed `utag_main` subcookies. The allow list is enforced only if `split_cookie` is set to `true`, which is the default setting in version 4.50 and later. 

If `split_cookie_allowlist` is defined and active, the following applies:

* `utag.loader.SC` sets only `utag_main` cookies.
* Only subcookies in this list are set in the `utag_main` namespace.

If `split_cookie_allowlist` is not defined or `split_cookie` is not `true`, all `utag_` namespace cookies are allowed.


<blockquote>
Using this option without allowing `ses_id`, `_st`, and `_ss` inflates visitor and session counts, making all visits look like single page sessions.
</blockquote>


```js
window.utag_cfg_ovrd.split_cookie_allowlist = ["v_id", "_ss", "_st", "ses_id"];
```

### `suppress_before_load_rules_with_uids`

**Skip Before Load Rules extensions when tracking tags by UID**  
(New in [`utag.js` 4.52](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2024-12-18))  

By default, extensions scoped to **Before Load Rules** execute for all tracking calls, even when [tracking tags by UID](https://docs.tealium.com/tracking-functions/). Previously, those extensions did not run when tracking tags by UID. 

Set this option to `true` to skip extensions scoped to **Before Load Rules** when tracking tags by UID (legacy behavior). (Default: `false`)

```js
window.utag_cfg_ovrd.suppress_before_load_rules_with_uids = true;
```


### `waittimer`

**Delay tags with timer**
Sets how long to wait (in milliseconds) after the DOM Ready event before loading tags. (Default: not set)

```js
window.utag_cfg_ovrd.waittimer = 1000;
```
