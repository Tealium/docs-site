---
title: Version 4.26 notes
description: Learn about the changes in version 4.26 and how to update to the latest version.
url: https://docs.tealium.com/platforms/javascript/version-4-26/
---
For all release notes, see [Tealium for Javascript release notes](?filter=tealium-universal-tag).

----

## Overview

Load rules are re-evaluated for both `utag.view()` and `utag.link()` calls.

Changes to the way the `utag.js` 4.26 file handles query string parameters and meta tags means that they are no longer lower-cased by default. If you have query string parameters or meta tags identified as data sources in your profile, you may need to update those data source names in the Data Layer tab to match upper case and lower case letters exactly. 

## Custom script source is a blocking tag

A blocking tag is a tag that must run before any other tags run. When you enter the location for the [custom script source advanced setting](https://docs.tealium.com/manage-templates/) for a tag, this tag automatically becomes a blocking tag. This tag still loads asynchronously, but subsequent asynchronous scripts. For example, `utag.10.js` does not load until the blocking tag is complete.

**Best Practice:** If you want to load custom JavaScript for a tag but you do not want it to be a blocking tag, use the [Tealium Generic Tag](https://docs.tealium.com/tealium-generic-tag/) to load it.

## Wait flag improvement

The [wait flag is an advanced setting](https://docs.tealium.com/manage-templates/) within tag configuration.

Tags whose **Wait Flag** is set to  "No" load and fire immediately after the `utag.js` file loads. Those tags, whose **Wait Flag** is set to "No," that load sooner may fire sooner, regardless of their order in Tealium iQ. For example, if Tag 2 loads before Tag 1, and Tag 1 is placed higher in the Tags tab in Tealium iQ, Tag 2 may still fire sooner, despite the order they're in. Previously, tags executed in the order specified in Tealium iQ. These tags then waited for tags placed higher in the order to load before loading themselves.

This means that you may now have a mixture of tags with their Wait Flag set to 'No' and tags with their Wait Flag set to 'Yes' in the same profile. 

## Tracking calls load new tags

After the initial page load, subsequent calls to `utag.view()` re-evaluate load rules to load new tags. In previous versions, calls to `utag.view` could not load new tags. This feature is enabled by default in `utag.js` 4.26.

Disable this feature to keep current behavior. See [`utag.cfg.load_rules_ajax` flag](https://docs.tealium.com/platforms/javascript/settings/) details below for more information.


<blockquote>
A `utag.link()` call does not load a new tag. Only a `utag.view()` call does this.
</blockquote>


## Load a tag by UID

For advanced implementations, especially those using AJAX, use the `utag.view()` call to bring in a new tag and fire it based on the tag's UID (as seen in the Tags tab of Tealium iQ). This bypasses all load rules.

```javascript
utag.view({page_name : "New Page"}, null, [5]);
```

* Param 1: Data Layer
* Param 2: Callback function (or null)
* Param 3: Array of UIDs to load and fire

## Read new meta tags

These types of meta tags with "name=" were picked up in a previous version of `utag.js`:

```html
<meta name="keywords" content="Apple,Tab" />
```

The new `utag.js` 4.26 now picks up those with `property= `(see "Open Graph" meta tags)

```html
<meta property="og:type" content="video.movie" /> 
```

## Lowercase query string or meta variables

This is a logic change in the default behavior of `utag.data`. Set the [`utag.cfg.lowerqp` flag](#utagcfglowerqp) to `true` to automatically lowercase. However, the default setting keeps the mixed case.


<blockquote>
Set the `utag.cfg.lowerqp` flag to true for backward compatibility with previous `utag.js` behavior.
</blockquote>


Set the `utag.cfg.lowermeta` flag to `true` to enable lower-casing for the meta tags. This only applies to the name of the name/value pair for that meta tag.


<blockquote>
If you have mixed-case query string parameters, you need to update the data source's name in the Data Sources tab to match exactly. Any code that refers to this query string type data source must also be updated.
</blockquote>


## New cookie values

There are new cookie name/value pairs in the `utag_main` cookie:

* **`utag_main_vid`**  
A long string to uniquely identify the visitor, such as `013efdc67183001adeec0eef13010a051001b00f0093c`)
* **`utag_main__ss`**  
A "Session Start" flag. Set to `"1"` for the first page view of a new session. Default session time is 30 minutes elapsed with no activity.
* The session ID value in the `utag_main_ses_id` cookie
* The visitor ID value in the `utag_main_v_id` cookie
* The session start flag (0 or 1) found in the `utag_main__ss` cookie

(The previous cookie values `utag_main__st` and `utag_main_ses_id` are still set.)

## Session tracking

A request for an empty file, `utag.v.js`, is made once at the start of a visitor session. This is used internally by Tealium to log the session count. The HTTP request URL looks like this:

```bash
http://tags.tiqcdn.com/utag/tiqapp/utag.v.js?a=tealium/main/201306012057&cb=1370276499302
```

The new cookie value `utag_main__ss`, is used to determine when to fire. This is only sent on the first event of a session. This request is sent last, after all tags have fired.

## URL fragments

key-value pairs found after the `#` sign are added as `qp.` variables. This is important for AJAX sites.

Example URL: `http://www.example.com?param1=value1&param2=value2#hash1=value3)`

Previous:

```javascript
utag.data = { "qp.param1" : "value1", "qp.param2" : "value2"}
```

New:

```javascript
utag.data = { "qp.param1" : "value1", "qp.param2" : "value2", "qp.hash1"  : "value3"}
```

## All page data available to tracking calls

Previously, `utag.view` and `utag.link` calls only knew about the data you passed them. Items like `b["qp.campaign"]` were not available. Now, all "built-in" data points such as URL, meta, or cookie values are added to the data layer for the `utag.link` and `utag.view` calls.

Also, dynamic items that may have changed for AJAX sites (such as `b["dom.url"]`) are re-built so they use the current value. The current value may be different from the value at the time of the initial landing on an AJAX page. 

## New override settings

Use a JavaScript Code extension scoped to "Pre Loader" and the global variable `window.utag_cfg_ovrd`.

```javascript
window.utag_cfg_ovrd = {
    "noview"          : true,
    "lowerqp"         : true,
    "load_rules_ajax" : false
};
```

## Additional settings

* `utag.cfg.load_rules_ajax`  
Set this flag to `false` when you do not want to re-evaluate load rules for every `utag.view` and `utag.link` call. For `utag.view`, this may also load a new `utag.X.js` file if it did not load on the initial page view.
* `utag.udoname`  
The name of the data object. The `utag.js` code assumes the data object is a global variable. For example, not an object within another object. By default, this is set to `utag_data`
* `utag.cfg.load_rules_at_wait`  
Set this flag to `true` when you want to re-evaluate load rules at Wait (DOM Ready). This enables legacy support where data may have been set after `utag.js` loads and you want to use this data to fire a Tag set to wait for DOM Ready.
* `utag.cfg.lowerqp`  
Set this flag to `true` if you want to lowercase your query string name/value pairs. This used to be the default behavior.
* `utag.cfg.lowermeta`  
Set this flag to `true` if you want to lowercase your meta tags' names. The value of the name/value pair for the meta tag is not lowercased.
* `utag.cfg.noview`  
Set this flag to `true` if you want to control when the initial `utag.view` call is made. This is common for AJAX sites where your application controls the page view event (not the initial page load action.) 

##  Considerations

* Accidentally Firing Multiple Orders - The `utag.link` and `utag.view` calls now have all of the "DOM" type of data points available in every call. For example, the query string data such as `b["qp.order_id"]` is read on the page load and trigger an order event. However, if you fire a `utag.link` call on that same order page, it also has the `b["qp.order_id"]` data set and trigger a second order event.
* For most intuitive behavior, we recommend setting all `utag_data` values before you load in the `utag.js` file. And keep `utag.cfg.load_rules_at_wait` at "false," which is the default.
* Be aware that updating to `utag.js` 4.26 changes the default behavior for lower casing your query string params. Values are no longer automatically lower-cased.
* "All Tags"-scoped Extensions may or may not run before DOM Ready-scoped extensions. Order is not guaranteed. If you manipulate a data layer element in an All Tags-scoped extension, then it may affect your Content Modification Extension's criteria.

**Best Practice:** Do not modify the original data layer object. If you need to modify a value, use a new variable instead.

## Known issues

* The `utag_data` object becomes a reference to `utag.data`, and changing one changes the other.
* Internet Explorer 8 may introduce timing issues if your Data Layer is defined at the end of your `<body>` element, just before DOM Ready (and the `utag.js` is already loaded). As a best practice, always declare your `utag_data` object before you load the `utag.js` file.
