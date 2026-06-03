---
title: Cookie Functions
description: Reference guide for cookie functions provided by Tealium for JavaScript.
url: https://docs.tealium.com/platforms/javascript/api/cookie-functions/
---
## `utag.loader.RC`

The method `utag.loader.RC` reads and returns all accessible cookies and groups cookies in the `utag_` namespace into objects.

```javascript
&gt; utag.loader.RC()
&lt; {
    &#34;trace_id&#34;: &#34;123456&#34;,
    &#34;utagdb&#34;: &#34;true&#34;,
    &#34;utag_main&#34;: {
        &#34;_sn&#34;: &#34;1&#34;,
        &#34;ses_id&#34;: &#34;1686564817915&#34;,
        &#34;persist_data_value&#34;: &#34;1686564817918&#34;,
        &#34;_se&#34;: &#34;2&#34;,
        &#34;_ss&#34;: &#34;0&#34;,
        &#34;_st&#34;: &#34;1686566634755&#34;,
        &#34;_pn&#34;: &#34;2&#34;
    },
    &#34;utag_custom&#34;: {
        &#34;testval1&#34;: &#34;abc123&#34;,
        &#34;testval2&#34;: &#34;bcd234&#34;
    },
    &#34;some_other_cookie&#34;: &#34;someval&#34;
}
```

The optional first argument returns the specified cookie if it exists, or an empty object if it doesn&#39;t.

```javascript
&gt; utag.loader.RC(&#34;trace_id&#34;)
&lt; &#34;123456&#34;

&gt; utag.loader.RC(&#34;some_other_cookie&#34;)
&lt; &#34;someval&#34;

&gt; utag.loader.RC(&#34;utag_custom&#34;)
&lt; {
    &#34;testval1&#34;: &#34;abc123&#34;,
    &#34;testval2&#34;: &#34;bcd234&#34;
}

&gt; utag.loader.RC(&#34;this_cookie_does_not_exist&#34;)
&lt; {}

```

## `utag.loader.SC`

The `utag.loader.SC` method sets and deletes cookies within the `utag_` namespace. 

When set to use multi-value cookies, the `utag.js` script creates and manages a single cookie called `utag_main`. This cookie contains multiple values that keep track of the visitor session. Standalone cookies split this multi-value cookie into individual cookies that are easier to explain, audit and understand.

Regardless of the `utag.js` version or the `split_cookie` setting, the changes take place behind the scenes in these cookie functions - all existing behavior is preserved, except for the way cookies are stored.


Migration to utag 4.50 doesn&#39;t require a technical update of existing implementations, but any cookie notices that inform your users about specific cookies should be updated.&lt;br&gt;&lt;br&gt;For more information about updating the `utag.js` template, see our [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470) knowledge base article.


The following format demonstrates how to set a cookie by identifying the cookie&#39;s namespace, name, value, optional expiration time, and optional flag for specifying additional functionality:  
```js
utag.loader.SC(namespace, {&#34;name&#34;: &#34;value;exp-expiry&#34;}, flag);
```

| Parameter | Type   | Description | Example |
| ---       | ---    | ---         | ---     |
| `namespace`    | `String` | The namespace of the cookie, which must start with `utag_`. | `&#34;utag_multi&#34;` |
| `name:value`   | `Object` | An object of key-value pairs representing a multi-value cookie. | `{&#34;uid&#34;: &#34;012345689&#34;, &#34;aff&#34;: &#34;SiteAff1;exp-7d&#34;}` |
| `expiry`  | `String` | (Optional) The expiration of the cookie, which must start with `exp-`.| `exp-12h` |
| `flag`    | `String` | (Optional) A flag to delete one or more cookies. | `&#34;d&#34;` |


This is the same function used by the [Persist Data Value extension]().


### Expiry Options

The following cookie expiry options are available:

| Expiry unit| Description | Example |
| --- | --- | --- |
| `#d` | Expiry time in days (default unit, if none provided)  | `exp-7d` or `exp-7` (7 days)|
| `#h` | Expiry time in hours | `&#34;exp-8h&#34;` (8 hours) |
| `#u` | Expiry time at [Unix timestamp](https://www.epochconverter.com/) | `&#34;exp-1549271521u&#34;` (Midnight (GMT) on Dec 22, 2022) |
| `session` | Expiry time at end of session (default [session timeout](/platforms/javascript/settings/#session-timeout): 30 minutes)| `&#34;exp-session&#34;` |

Timestamp-based expiration, such as `&#34;exp-1549271521u&#34;`, has a trailing `u` indicates Unix timestamp. Do not confuse it with the value set in the cookie itself such as `&#34;exp-1549271521&#34;`

If no expiry option is set, then the default behavior is based on the version of `utag.js`:

- **4.27&#43;** - default expiry is 1 year after the creation of the cookie.
- **4.26 or older** - default expiry is the year 2099.

### Set a Cookie
To set a cookie, pass an object of key-value pairs to the `value` parameter as shown below:

```js
utag.loader.SC(&#34;utag_cookie&#34;, {
    &#34;uid&#34;      : &#34;012345689&#34;,      // default expiry
    &#34;test_seg&#34; : &#34;groupA;exp-12h&#34;, // 12 hour expiry
    &#34;aff&#34;      : &#34;SiteAff1;exp-7d&#34; // 7 day expiry
});
```

**Standalone Cookies (Recommended)**

If the `split_cookie` setting is set to `true` (the default value in utag version 4.50 or later), the example above creates the following standalone cookies:

* `utag_cookie_uid`
* `utag_cookie_test_seg`
* `utag_cookie_aff`

**Multi-value Cookie**

If the `split_cookie` setting is set to `false` or the utag version is 4.49 or earlier, the example above creates a multi-value cookie named `utag_cookie` with three built-in values `uid`, `test_seg`, and `aff`.

### Delete a Cookie
To delete one or more cookie values, use the optional `flag` parameter.

Delete one or more values from a `utag_` cookie namespace. Each key-value pair specified is deleted:
```js
utag.loader.SC(&#34;utag_cookie&#34;, {&#34;test_seg&#34;:&#34;&#34;, &#34;aff&#34;:&#34;&#34;}, &#34;d&#34;);
```

Delete all values in a `utag_` cookie namespace or a specified standalone cookie:
```js
utag.loader.SC(&#34;utag_cookie&#34;, {}, &#34;da&#34;);
```
