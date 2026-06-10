---
title: Data Layer
description: Learn about the built-in variables of the Universal Data Object.
url: https://docs.tealium.com/platforms/javascript/data-layer/
---The Universal Data Object (UDO) contains built-in variables that collect basic information about the page where it is loaded. These variables include cookies created by `utag.js`, standard DOM variables from the page, and Tealium-specific variables about the loaded configuration.

[Learn more]() about the types of data layer variables available.

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
| `dom.pathname` | The path of the URL, excludes the query parameters and domain. Source: `location.pathname` | `&#34;/path/file.html&#34;` |
| `dom.query_string`| The full query string of the URL. Source: `location.search` |  `param1=value1` |
| `dom.referrer` | URL of previous page. Source: `document.referrer` |   |
| `dom.title` | Text contained between the `&lt;title&gt;` tags. Source: `document.title`| `&#34;Test Page Name&#34;`|
| `dom.url` | The full URL of the page. Source: `document.URL` | `http://www.example.com/` `PATH/FILE.html?param1=VALUE#hash=FRAGMENT` |
| `dom.viewport_height` | The height of the browser view port. Source: `window.innerHeight` or `document.documentElement. clientHeight` | `1320` |
| `dom.viewport_width` | The width of the browser view port. Source: `window.innerWidth` or `document.documentElement. clientWidth` | `1278` |

## Cookies

The following variables are stored and maintained in a single cookie named `utag_main`, or as standalone cookies in the `utag_main_` cookie namespace (from version 4.50). All variables appear in the data object as separate variables, all prefixed with `cp.utag_main_`.

To add these variables to your iQ configuration, [use the data bundle]() named `Tealium Built-in Data` from the **Data Layer** tab.

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

Add the `ut.*` variables to your iQ configuration [using the data bundle]() named `Tealium Built-in Data` from the **Data Layer** tab.

| Variable | Name | Example |
| --- | --- | --- |
| `tealium_account` | Account Name | `sandbox` |
| `tealium_datasource` | Data Source Key | `&#34;abc123&#34;` |
| `tealium_environment` | Publish Environment | `prod` |
| `tealium_event` | Tealium Event Name (Defaults to &#34;view&#34; or &#34;link&#34; if not set directly) | `view` |
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
| `ut.version` | The publish version (`utag.js` version &#43; timestamp) | `ut4.44.201710171745` |
| `ut.visitor_id` | Copy of `tealium_visitor_id` |`016297481...` (45 characters) |

## Local and Session Storage

Local and session storage keys appear automatically in the data layer using `localStorage` and `sessionStorage` variables.

To use these storage variables, navigate to **Tag Management &gt; Data Layer &gt; &#43;Add Variable**. Select **UDO Variable** and enter in a source variable name. Use `ls.variable_name` for local storage and `ss.variable_name` for session storage.

For more information about local and session storage variables, see [Data Layer Variables]().

## Sample

The following is a sample of the built-in data found within `utag.data`.

```json
{  
    &#34;cp.utag_main_v_id&#34;       : &#34;015da2e1daf10020914ce74dfaf00207900780700093c&#34;,
    &#34;cp.utag_main__sn&#34;        : &#34;389&#34;,
    &#34;cp.utag_main__ss&#34;        : &#34;0&#34;,
    &#34;cp.utag_main__st&#34;        : &#34;1522970376944&#34;,
    &#34;cp.utag_main__se&#34;        : &#34;2&#34;,
    &#34;cp.utag_main_ses_id&#34;     : &#34;1522915346545&#34;,
    &#34;cp.utag_main__pn&#34;        : &#34;8&#34;,
    &#34;qp.param1&#34;               : &#34;value1&#34;,
    &#34;qp.hash1&#34;                : &#34;val1&#34;,
    &#34;dom.referrer&#34;            : &#34;&#34;,
    &#34;dom.title&#34;               : &#34;Test Page&#34;,
    &#34;dom.domain&#34;              : &#34;www.example.com&#34;,
    &#34;dom.query_string&#34;        : &#34;param1=value1&#34;,
    &#34;dom.hash&#34;                : &#34;hash=fragment&#34;,
    &#34;dom.url&#34;                 : &#34;http://www.example.com/path/file.html?param1=value1#hash=fragment&#34;,
    &#34;dom.pathname&#34;            : &#34;/path/file.html&#34;,
    &#34;dom.viewport_height&#34;     : 780,
    &#34;dom.viewport_width&#34;      : 1436,
    &#34;ut.domain&#34;               : &#34;example.com&#34;,
    &#34;ut.version&#34;              : &#34;ut4.44.201710171745&#34;,
    &#34;ut.event&#34;                : &#34;view&#34;,
    &#34;ut.visitor_id&#34;           : &#34;015da2e1daf10020914ce74dfaf00207900780700093c&#34;,
    &#34;ut.session_id&#34;           : &#34;1522965346545&#34;,
    &#34;ut.account&#34;              : &#34;sandbox&#34;,
    &#34;ut.profile&#34;              : &#34;main&#34;,
    &#34;ut.env&#34;                  : &#34;prod&#34;,
    &#34;tealium_event&#34;           : &#34;view&#34;,
    &#34;tealium_visitor_id&#34;      : &#34;015da2e1daf10020914ce74dfaf00207900780700093c&#34;,
    &#34;tealium_session_id&#34;      : &#34;1522915346545&#34;,
    &#34;tealium_datasource&#34;      : &#34;abc123&#34;,
    &#34;tealium_account&#34;         : &#34;sandbox&#34;,
    &#34;tealium_profile&#34;         : &#34;main&#34;,
    &#34;tealium_environment&#34;     : &#34;prod&#34;,
    &#34;tealium_random&#34;          : &#34;7421526627003796&#34;,
    &#34;tealium_library_name&#34;    : &#34;utag.js&#34;,
    &#34;tealium_library_version&#34; : &#34;4.44.0&#34;,
    &#34;tealium_timestamp_epoch&#34; : 1522968576,
    &#34;tealium_timestamp_utc&#34;   : &#34;2018-04-05T22:49:36.945Z&#34;,
    &#34;tealium_timestamp_local&#34; : &#34;2018-04-05T15:49:36.945&#34;
}
```
