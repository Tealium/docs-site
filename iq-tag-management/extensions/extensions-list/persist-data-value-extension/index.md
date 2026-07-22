---
title: Persist Data Value Extension
description: The Persist Data Value extension is used to set a value in a first-party cookie.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/persist-data-value-extension/
---
## Prerequisites

* Version 4.38 or later of `utag.js`. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* [How extensions work]()
* [Data Layer Variables: First-party cookies](https://docs.tealium.com/data-layer-variables/#first-party-cookies)

## How it works

The Persist Data Value extension sets first-party cookies using text values or values from a data layer variable. The cookie you set must also be created as a data layer variable. For more information, see [first-party cookie variables](https://docs.tealium.com/data-layer-variables/#first-party-cookies).

The expiration of the cookie is based either on the user's session or a duration of time in hours or days. The cookie can be set once, updated on every page view, or set based on a condition.

## Using the extension

After the extension is added, the following configuration options are available:

* **Persist**: Select the type of value to save in the cookie:
    * **Text**: Set the cookie value to the text you enter.
    * **Variable**: Set the cookie to the value of a data layer variable.
* **Duration**: Set the length of time that the data persists in the cookie.
    * **Session**: The data remains in the cookie until the visitor closes their browser window.  
    
<blockquote>
Session cookies are deleted when the current session ends. The browser defines when the current session ends, and some browsers use session restoring when restarting. Session restoring can cause session cookies to last indefinitely.
</blockquote>

    * **Visitor**: The data remains in the cookie until the visitor or the browser deletes the cookie.
    * **Hours**: The data remains in the cookie for the number of hours you specify or until the browser deletes it.
    * **Days**: The data remains in the cookie for the number of days you specify or until the browser deletes it.
* **Update**: Select when to set or update the value.
    * **Allow Update on Page View**: Every time the visitor views a page, the data is updated. The duration timer resets with each update.
    * **Keep First Value Set**: Only the data from the first visit is saved. Subsequent visits do not alter this value.
* **Condition**: Click **Add Condition** to specify when to run this extension. You may only add one condition.
* **Store in Cookie**: Select the cookie variable to set. Click the **+** button to create a new one.

### Version 4.49 and earlier

In versions 4.49 and earlier of `utag.js`, the Tealium cookie is a single multi-value cookie named `utag_main`. To store a value in the Tealium cookie, name the cookie variable in the format `utag_main_NAME`, where `NAME` is the name of your cookie.

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-tealium-cookies-add-first-party-cookie-variable.jpg)

For more information, see [Tealium cookies]().

## Example: Visitor location cookie

This example demonstrates how to persist the visitor's location to a cookie. The location is retrieved from an existing data layer variable named `city_state_zip`. This variable might only be available on one page, but the value is needed on all pages throughout the site, so the Persist Data Value extension is used to save it to a cookie that will last for the life of the session.

To create the location cookie:

1. Add the Persist Data Values extension.
1. From the **Persist** drop-down list, select **Variable** and then select the variable `city_state_zip (js)`.
1. Set the **Duration** to **Session**.
1. Set **Update** to **Allow Update on Page View**.
1. In the **Store in Cookie** field, click the **+** button to create the variable `utag_main_location`.

![](https://docs.tealium.com/images/iq-tag-management/no-title-465i1c7944ae10209e84.png)

![](https://docs.tealium.com/images/iq-tag-management/no-title-466i43807063317f396a.png)
