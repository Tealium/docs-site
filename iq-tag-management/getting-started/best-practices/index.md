---
title: Best Practices for Tealium iQ
description: A guide to best practices for implementing Tealium iQ.
url: https://docs.tealium.com/iq-tag-management/getting-started/best-practices/
---
## Organization

### Save As vs. Overwrite

There are two methods to save your changes:

* **Save As** – Saves the changes in a new version, preserving the previous version.
* **Overwrite** – Saves the changes to the current version, overwriting it. You cannot undo changes to the version.

Scenarios to use **Save As**:

* When the current version has been published to production, to preserve the option to revert back, use **Save As**.
* When beginning a new project, use **Save As** to create a new version to separate it from the previous work.
* When you are unsure which option to choose, the **Save As** method is safest because it lets you revert to the previous version.

For more information, see [About saving]() and [About publishing]().

#### Example: Save As vs Overwrite to preserve the Prod version

In this example, there is a version published to Prod and we want to preserve that version so we can revert it back if necessary.

##### Correct

&#34;Version A&#34; is published to all three environments (Dev, QA, and Prod). After making changes, a **Save As** is performed to create a new version, &#34;Version B&#34;. It is then published to all environments again. This provides the option to rollback to the previous Prod version (Version A) if necessary.

##### Incorrect

&#34;Version A&#34; is published to Prod multiple times using an **Overwrite**. There is no way to roll back to the previous Prod version if needed.

|Pros| Cons|
|---| ---|
| The ability to revert to previous version. | None |
| Better organization on the Versions screen. | |

### Labels and titles

Use labels to categorize related tags, load rules, and extensions, especially those that require a sequential order.

Use descriptive titles, such as `Step 1 of 3`.

|Pros| Cons|
|---| ---|
| Helps maintain the order of operations for extensions. |  Minimal effort to assign labels. |
| Ability to filter on labels to easily find tags and extensions. | |

For more information, see [About Labels]().

## Data layer object

See [Data layer best practices]().

## Event tracking

### Event names

Tealium uses the variable `tealium_event` to uniquely identify each event type that is tracked on the site. Set this variable to a value identifying the event being tracked (Tealium naming convention applies).

Suggested values include, but are not limited to:

| Event Type |  tealium_event |
|------------|----------------|
| Cart/Basket Add |  `cart_add` |
| Cart/Basket Remove | `cart_remove`|
| Cart/Basket Empty | `cart_empty`|
| Cart/Basket View | `cart_view`|
| Registration Event |  `user_register` |
| Login Event |  `user_login` |
| Logout Event |  `user_logout` |
| Link Clicked |  `link_click` |

Standardized event names offer the following benefits:

* Implementation is clearer due to consistent variable names and values.
* Data mapping is easier because there is a single identifier for event types.
* Events are grouped into categories by the prefix of the name (`product_`, `cart_`, `user_`).

#### Sample event tracking script

```js
utag.link({
    tealium_event    : &#34;cart_add&#34;,
    product_id       : [&#34;shrt123&#34;],
    product_price    : [&#34;12.50&#34;],
    product_quantity : [&#34;2&#34;]
});
```

## Performance

### Update utag.js

We recommend that you keep current with the [latest version of `utag.js`](/release-notes/?filter=tealium-universal-tag) to reduce your QA work and to ensure that your profile contains the test optimizations and features.

For more information, see [Manage Templates]().

### Update tag templates to latest version

We recommend that you update all tags and tag templates to the latest versions to ensure that tags fire correctly. Run the [Template Status Checker]() tool to see which tags need to be updated. Also, check the [release notes]() for news of updated or deprecated tags.

For more information, see [Update a template]().

### Combine multiple vendor tags

When you combine multiple tags from one vendor into a single instance of the tag, the page performance improves because fewer `utag.#.js` files are loaded on the page. This approach also makes it easier to maintain the configuration for the vendor tag in Tealium iQ.

For more information, see [Configuring Multiple Floodlight Tags]()

### Load utag.js asynchronously

The best practice is to load all tags and vendor code asynchronously. In this method, tags are loaded in parallel to the rest of the page content. Even if the tag is slow to respond or to load, it will not slow down the rest of the site.

Synchronous loading is necessary is when tags or vendor code are dependent on each other to load, such as when code to retrieve data for personalization of page content is needed. This option will slow down the loading of the site, but it will ensure that the correct data is loaded (for example, the visitor&#39;s name or shipping location) before the rest of the page is displayed.

For more information, see [Synchronous Load]().

|Pros| Cons|
|---| ---|
| Asynchronously loaded files will not affect page load speeds. | Less control over the timing of loading file. Mainly affects A/B testing vendors.|
| External files that are slow to respond will not halt page load or break the page. |If granular control is required, use `utag.sync` and include any personalization or A/B testing functionality in there. |
| | External vendor scripts and files that respond slowly may miss tracking calls. |

### Bundle tags

The **Bundle Tags** feature is set within the publish settings of the profile. Enabling this feature will cause the vendor tag code to be included in the main `utag.js` file. This reduces the number of HTTP requests that are sent from your page and improves performance.

For more information, see [Bundle Flag]().

|Pros| Cons|
|---| ---|
| Reduces the overall size of Tealium files that load on your site due to more efficient gzip compression. | None |
| Important tags (analytics) execute sooner which improves tracking on landing pages. |
|  |

### Page code placement

We recommend that the Universal Tag (`utag.js`) be placed at the top of the body tag (as opposed to the head or footer), keeping in mind that the data layer object must be declared and populated prior to this. This placement provides the best compatibility with the greatest number of vendors.

For more information, see .

|Pros| Cons|
|---| ---|
| More control over when tags fire (early in the page or later). | Could require extra development to ensure the data layer object is available before `utag.js` is loaded.|
| Better compatibility with multivariate testing tags. | |

### Tag timing

The **Tag Timing** setting determines if a tag is fired immediately or at DOM Ready. When **Tag Timing** is set to `Prioritized`, the tag is executed as soon as it&#39;s loaded into the page. When **Tag Timing** is set to `DOM Ready`, the tag waits until the DOM Ready event to execute. This setting is found in the [Advanced Settings for each tag]().

To prioritize the execution of important tags (such as analytics), set the **Wait Flag** to off.

For more information, see [Tag Timing]().

|Pros| Cons|
|---| ---|
| Important tags can be prioritized to execute as soon as possible to maximize data collection. | The browser could prioritize loading a tag over loading an image to display which may have a slight impact on user experience|
| On landing pages, where tag files most likely have not been cached, the tags will execute sooner. | | 

### Only load event listeners when necessary

If you do not set any event rules for an event listener, it will load on every page. Loading event listeners on every page will slow down delivery of pages on the site and collect unnecessary data. We recommend that you use rules to load event listeners only on pages where you expect the trigger&#39;s actions to happen or where you require visitor action data.

For more information, see [Event Rules]().

## Extensions

### Use built-in extensions

Tealium is designed for both non-technical users with limited coding experience and for developers who are comfortable writing their own JavaScript. While many of the built-in extensions could easily be re-written as custom JavaScript Code extensions, we recommend using the built-in extensions whenever possible and only writing custom JavaScript when you require additional functionality not offered by the existing options.

Built-in extensions offer the following benefits:

* **Managed Dependencies**  
If the name of a data layer variable is changed, all built-in extensions that reference that variable are automatically updated because they contain a reference to the original variable.  
Data layer variables referenced in code, such as `b[&#39;user_login_status&#39;]`, must be updated manually if the name of the variable ever changes.
* **Friendly Variable Names**  
Built-in extensions will always display the user-friendly name of a variable (Alias) if it exists. This improves readability of the configuration.  
Variables referenced in code must use the actual name, which can be cryptic or unclear, making it more difficult to understand what the code does or to identify its dependencies.
* **No Syntax Errors**  
Built-in extensions are guaranteed to generate the same consistent code every time you publish, eliminating the risk of syntax errors.  
Custom JavaScript code always runs the risk of introducing unexpected syntax errors (although the publish engine will usually catch these) or runtime errors.

For more information, see [About Extensions]().

|Pros| Cons|
|---| ---|
| Easier to understand and maintain for most users. | None |
| Easier to debug when an issue arises. | |
| Built-in extensions are safe and will not introduce JavaScript errors. | |

### Remove tag code from extensions

We recommend that you run tag code from the tag marketplace or a custom container instead of running the code snippet from an extension. This makes it easier for you to maintain tags.

### Global vs. local JavaScript variables

In JavaScript Code extensions, be sure to explicitly define global and local variables using `var` and `window`. This prevents naming conflicts with the variables declared in `utag.js` or globally in the page.

Incorrect:

```js
variable_name = &#34;some value&#34;;
```

Correct:

```js
var variable_name = &#34;local value&#34;;
```

```js
window.variable_name = &#34;global value&#34;;
```

|Pros| Cons|
|---| ---|
| Avoids collisions with other variables elsewhere on the site. |None |

## Load rules

### Check variables to ensure they exist

We recommend that you verify that a variable exists before you check the value of that variable. The following example verifies if `MyVariable` is defined before checking if its value is equal to 1000: ![](/images/iq-tag-management/load-rules/variable-is-defined.png)

If you do not verify that the variable exists and its value is `null`, the code throws an error and may cause the tag not to fire.

For more information, see [About Load Rules]().

|Pros| Cons|
|---| ---|
| Avoids error condition if the variable is not defined. |None |

