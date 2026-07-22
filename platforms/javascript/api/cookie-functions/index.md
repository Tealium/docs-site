---
title: Cookie Functions
description: Reference guide for cookie functions provided by Tealium for JavaScript.
url: https://docs.tealium.com/platforms/javascript/api/cookie-functions/
---
## `utag.loader.RC`

The method `utag.loader.RC` reads and returns all accessible cookies and groups cookies in the `utag_` namespace into objects.

```javascript
> utag.loader.RC()
< {
    "trace_id": "123456",
    "utagdb": "true",
    "utag_main": {
        "_sn": "1",
        "ses_id": "1686564817915",
        "persist_data_value": "1686564817918",
        "_se": "2",
        "_ss": "0",
        "_st": "1686566634755",
        "_pn": "2"
    },
    "utag_custom": {
        "testval1": "abc123",
        "testval2": "bcd234"
    },
    "some_other_cookie": "someval"
}
```

The optional first argument returns the specified cookie if it exists, or an empty object if it doesn't.

```javascript
> utag.loader.RC("trace_id")
< "123456"

> utag.loader.RC("some_other_cookie")
< "someval"

> utag.loader.RC("utag_custom")
< {
    "testval1": "abc123",
    "testval2": "bcd234"
}

> utag.loader.RC("this_cookie_does_not_exist")
< {}

```

## `utag.loader.SC`

The `utag.loader.SC` method sets and deletes cookies within the `utag_` namespace. 

When set to use multi-value cookies, the `utag.js` script creates and manages a single cookie called `utag_main`. This cookie contains multiple values that keep track of the visitor session. Standalone cookies split this multi-value cookie into individual cookies that are easier to explain, audit and understand.

Regardless of the `utag.js` version or the `split_cookie` setting, the changes take place behind the scenes in these cookie functions - all existing behavior is preserved, except for the way cookies are stored.


<blockquote>
Migration to utag 4.50 doesn't require a technical update of existing implementations, but any cookie notices that inform your users about specific cookies should be updated.<br><br>For more information about updating the `utag.js` template, see our [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470) knowledge base article.
</blockquote>


The following format demonstrates how to set a cookie by identifying the cookie's namespace, name, value, optional expiration time, and optional flag for specifying additional functionality:  
```js
utag.loader.SC(namespace, {"name": "value;exp-expiry"}, flag);
```

| Parameter | Type   | Description | Example |
| ---       | ---    | ---         | ---     |
| `namespace`    | `String` | The namespace of the cookie, which must start with `utag_`. | `"utag_multi"` |
| `name:value`   | `Object` | An object of key-value pairs representing a multi-value cookie. | `{"uid": "012345689", "aff": "SiteAff1;exp-7d"}` |
| `expiry`  | `String` | (Optional) The expiration of the cookie, which must start with `exp-`.| `exp-12h` |
| `flag`    | `String` | (Optional) A flag to delete one or more cookies. | `"d"` |


<blockquote>
This is the same function used by the [Persist Data Value extension](https://docs.tealium.com/persist-data-value-extension/).
</blockquote>


### Expiry Options

The following cookie expiry options are available:

| Expiry unit| Description | Example |
| --- | --- | --- |
| `#d` | Expiry time in days (default unit, if none provided)  | `exp-7d` or `exp-7` (7 days)|
| `#h` | Expiry time in hours | `"exp-8h"` (8 hours) |
| `#u` | Expiry time at [Unix timestamp](https://www.epochconverter.com/) | `"exp-1549271521u"` (Midnight (GMT) on Dec 22, 2022) |
| `session` | Expiry time at end of session (default [session timeout](https://docs.tealium.com/platforms/javascript/settings/#session-timeout): 30 minutes)| `"exp-session"` |


<blockquote>
Timestamp-based expiration, such as `"exp-1549271521u"`, has a trailing `u` indicates Unix timestamp. Do not confuse it with the value set in the cookie itself such as `"exp-1549271521"`
</blockquote>


If no expiry option is set, then the default behavior is based on the version of `utag.js`:

- **4.27+** - default expiry is 1 year after the creation of the cookie.
- **4.26 or older** - default expiry is the year 2099.

### Set a Cookie
To set a cookie, pass an object of key-value pairs to the `value` parameter as shown below:

```js
utag.loader.SC("utag_cookie", {
    "uid"      : "012345689",      // default expiry
    "test_seg" : "groupA;exp-12h", // 12 hour expiry
    "aff"      : "SiteAff1;exp-7d" // 7 day expiry
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
utag.loader.SC("utag_cookie", {"test_seg":"", "aff":""}, "d");
```

Delete all values in a `utag_` cookie namespace or a specified standalone cookie:
```js
utag.loader.SC("utag_cookie", {}, "da");
```
