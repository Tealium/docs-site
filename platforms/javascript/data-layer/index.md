---
title: Data Layer
description: Learn about the built-in variables of the Universal Data Object.
url: https://docs.tealium.com/platforms/javascript/data-layer/
---The Universal Data Object (UDO) contains built-in variables that collect basic information about the page where it is loaded. These variables include cookies created by `utag.js`, standard DOM variables from the page, and Tealium-specific variables about the loaded configuration.

[Learn more](https://docs.tealium.com/data-layer-variables/) about the types of data layer variables available.

## Standard Page Data

The following variables are generated from the standard JavaScript properties available in the web page. These variables appear automatically within the iQ interface for use with load rules, extensions, data mappings, and conditions.

These values assume the URL of the page:

```
http://www.example.com/path/file.html?param1=value1#hash=fragment
```

| Variable | Description | Example |
| --- | --- | --- |
| `dom.domain`| The full domain of the URL. Source: `location.hostname` | `www.example.com` |
| `dom.hash` | The hash fragment of the URL (excluding the # character). Source: `location.hash` | `hash=fragment` |
| `dom.pathname` | The path of the URL, excludes the query parameters and domain. Source: `location.pathname` | `"/path/file.html"` |
| `dom.query_string`| The full query string of the URL. Source: `location.search` |  `param1=value1` |
| `dom.referrer` | URL of previous page. Source: `document.referrer` |   |
| `dom.title` | Text contained between the `<title>` tags. Source: `document.title`| `"Test Page Name"`|
| `dom.url` | The full URL of the page. Source: `document.URL` | `http://www.example.com/` `PATH/FILE.html?param1=VALUE#hash=FRAGMENT` |
| `dom.viewport_height` | The height of the browser view port. Source: `window.innerHeight` or `document.documentElement. clientHeight` | `1320` |
| `dom.viewport_width` | The width of the browser view port. Source: `window.innerWidth` or `document.documentElement. clientWidth` | `1278` |

## Cookies

The following variables are stored and maintained in a single cookie named `utag_main`, or as standalone cookies in the `utag_main_` cookie namespace (from version 4.50). All variables appear in the data object as separate variables, all prefixed with `cp.utag_main_`.

To add these variables to your iQ configuration, [use the data bundle](https://docs.tealium.com/data-bundles/) named `Tealium Built-in Data` from the **Data Layer** tab.

| Variable | Description | Example |
| --- | --- | --- |
| `cp.utag_main__pn` | **Session Page View Count** - The number of pages viewed in the current session | `2` |
| `cp.utag_main__se` | **Session Event Count** - The number of events tracked in the current session | `2` |
| `cp.utag_main__sn` | **Session Count** - The number of sessions for this unique visitor | `1` |
| `cp.utag_main__ss` | **Is Start of Session** - A flag that indicates whether or not a page view is the start of a session (1=yes, 0=no) | `0` |
| `cp.utag_main__st` | **Timestamp** - The Unix/Epoch time stamp in milliseconds | `1522968400449` |
| `cp.utag_main_ses_id` | **Session ID** - A unique identifier for the session | `1522965346545` |
| `cp.utag_main_v_id` | **Visitor ID** - A unique identifier for each visitor | `016297481...` (45 characters) |

## Tealium Data

The following variables contain information about the `utag.js` loaded in the page, along with other values used internally.

Add the `ut.*` variables to your iQ configuration [using the data bundle](https://docs.tealium.com/data-bundles/) named `Tealium Built-in Data` from the **Data Layer** tab.

| Variable | Name | Example |
| --- | --- | --- |
| `tealium_account` | Account Name | `sandbox` |
| `tealium_datasource` | Data Source Key | `"abc123"` |
| `tealium_environment` | Publish Environment | `prod` |
| `tealium_event` | Tealium Event Name (Defaults to "view" or "link" if not set directly) | `view` |
| `tealium_library_name` | Library Name | `utag.js` |
| `tealium_library_version` | Library Version | `4.44.0` |
| `tealium_profile` | Account Profile | `main` |
| `tealium_random` | Random Number | `7782219635308327` |
| `tealium_session_id` | Copy of `utag_main_ses_id` | `1522965346545` |
| `tealium_timestamp_epoch` | Current Unix timestamp in seconds | `1522956509` |
| `tealium_timestamp_local` | Local Timestamp | `2018-04-05T12:28:29.019` |
| `tealium_timestamp_utc` | UTC Timestamp  | `2018-04-05T19:28:29.019Z` |
| `tealium_visitor_id` | Copy of `utag_main_v_id` | `016297481...` (45 characters) |
| `ut.account` | Copy of tealium_account | `sandbox` |
| `ut.domain` | The top level domain used for setting cookies. | `example.com` |
| `ut.env` | Copy of `tealium_environment` | `prod` |
| `ut.event` | Copy of `tealium_event` | `view` |
| `ut.profile` | Copy of `tealium_profile` | `main` |
| `ut.session_id` | Copy of `tealium_session_id` | `1522956509018` |
| `ut.version` | The publish version (`utag.js` version + timestamp) | `ut4.44.201710171745` |
| `ut.visitor_id` | Copy of `tealium_visitor_id` |`016297481...` (45 characters) |

## Local and Session Storage

Local and session storage keys appear automatically in the data layer using `localStorage` and `sessionStorage` variables.

To use these storage variables, navigate to **Tag Management > Data Layer > +Add Variable**. Select **UDO Variable** and enter in a source variable name. Use `ls.variable_name` for local storage and `ss.variable_name` for session storage.

For more information about local and session storage variables, see [Data Layer Variables](https://docs.tealium.com/data-layer-variables/).

## Sample

The following is a sample of the built-in data found within `utag.data`.

```json
{  
    "cp.utag_main_v_id"       : "015da2e1daf10020914ce74dfaf00207900780700093c",
    "cp.utag_main__sn"        : "389",
    "cp.utag_main__ss"        : "0",
    "cp.utag_main__st"        : "1522970376944",
    "cp.utag_main__se"        : "2",
    "cp.utag_main_ses_id"     : "1522915346545",
    "cp.utag_main__pn"        : "8",
    "qp.param1"               : "value1",
    "qp.hash1"                : "val1",
    "dom.referrer"            : "",
    "dom.title"               : "Test Page",
    "dom.domain"              : "www.example.com",
    "dom.query_string"        : "param1=value1",
    "dom.hash"                : "hash=fragment",
    "dom.url"                 : "http://www.example.com/path/file.html?param1=value1#hash=fragment",
    "dom.pathname"            : "/path/file.html",
    "dom.viewport_height"     : 780,
    "dom.viewport_width"      : 1436,
    "ut.domain"               : "example.com",
    "ut.version"              : "ut4.44.201710171745",
    "ut.event"                : "view",
    "ut.visitor_id"           : "015da2e1daf10020914ce74dfaf00207900780700093c",
    "ut.session_id"           : "1522965346545",
    "ut.account"              : "sandbox",
    "ut.profile"              : "main",
    "ut.env"                  : "prod",
    "tealium_event"           : "view",
    "tealium_visitor_id"      : "015da2e1daf10020914ce74dfaf00207900780700093c",
    "tealium_session_id"      : "1522915346545",
    "tealium_datasource"      : "abc123",
    "tealium_account"         : "sandbox",
    "tealium_profile"         : "main",
    "tealium_environment"     : "prod",
    "tealium_random"          : "7421526627003796",
    "tealium_library_name"    : "utag.js",
    "tealium_library_version" : "4.44.0",
    "tealium_timestamp_epoch" : 1522968576,
    "tealium_timestamp_utc"   : "2018-04-05T22:49:36.945Z",
    "tealium_timestamp_local" : "2018-04-05T15:49:36.945"
}
```
