---
title: JavaScript Code Extension
description: The JavaScript Code extension is designed for implementing custom JavaScript ES5 code through Tealium iQ Tag Management. It comes with a built-in code editor and configuration options for when and where to run the code.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/javascript-code-extension/
---
## Prerequisites

* [Permission to Manage JS Code Extension]()
  * This permission is required to add or edit a JavaScript Code extension in your account.
* utag version 4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
  * This version provides support for the execution options under the All Tags scope
  * Upgrade to this version if you have not already done so.

This is the basic version of the JavaScript Code extension. For advanced needs, see the [Advanced JavaScript Code Extension]().

### JavaScript code extension comparison

The following table highlights the key differences between the JavaScript Code extension and the Advanced JavaScript Code extension to help you choose the one that best suits your needs.

| Feature | JavaScript Code extension | Advanced JavaScript Code extension |
| ----- | ----- | ----- |
| Editor | Basic text editor | Advanced code editor with syntax checking and code diffs |
| Publish workflow | [Publish locations]() | [Promote drafts to be approved for publishing]() |
| Remote code integration | [Tealium API v3]() |[Link to GitHub repository]() |
| Permission | Account-level  | Profile-level  |

## How it works

The JavaScript Code extension gives you the power to create custom code to be included in the files that load on your site. Depending on the scope of the extension, the code loads in either `utag.js` or in a vendor `utag.#.js` file. The code entered into the text box of the extension is included in the `utag` files just as it appears. It is important to note that the code is run from an anonymous function wrapper, which ensures that the code is isolated and does not interfere with other scripts, as shown in the following example:

```js
function(a, b) {
    // content of JavaScript Code extension runs here
}
```

The parameters represent the following:

* `a`: indicates which tracking call was made, where &#34;view&#34; corresponds to the `utag.view()` method for tracking page views, and &#34;link&#34; corresponds to the `utag.link()` method for tracking link clicks.
* `b`: a reference to the data object passed to the tracking call.

While the JavaScript Code extension is flexible and can be used for most anything you would want to accomplish within your tag management solution, it is important to understand the impact it could have on your account. We recommend that you try to use the other built-in extensions to accomplish your task before turning to the JavaScript Code extension.

### Conditions

Conditions add an extra layer of control on top of the scope. These conditions control when the JavaScript Code extension runs.

### Scope

The JavaScript Code extension offers the following options for determining the timing of when the code runs: 

* utag Sync
* Pre Loader
* Before Load Rules
* After Load Rules (default)
* DOM Ready
* Tag Scoped
* After Tags

To learn about the order of operations in `utag.js`, see [Order of Operations]().

### Occurrence

By default, a JavaScript Code extension runs for every [tracking call](/platforms/javascript/track/), including in-page event tracking, which would potentially cause it to run more than once per page load. If you want to prevent multiple executions of your code, select **Run Once**.

You cannot change occurrence for extensions that use the following scopes:

* utag Sync
* Pre Loader
* DOM Ready
* Tag Scoped

## Before You Begin

Consider the following before you begin:

* Do not surround the code with `&lt;script&gt;` tags since the content of the text box will be included in a JavaScript file exactly as you enter it.
* If you are referencing a variable from the `utag_data` object, such as `page_name` or `language`, use `b[&#39;VARIABLE&#39;]`.  
Learn more about [the b object]().
* If you are referencing a variable defined in the tag template of the scoped tag, such as `account_id` or `base_url`, use `u[&#39;VARIABLE&#39;]`.

## Configuration Steps

Use the following steps to configure the JavaScript code extension:

1. Go to the **Extensions Marketplace** and [add the JavaScript Code extension from the Advanced tab]().
1. **Title**: Enter a name for this extension.
1. **Scope**: Choose from the following options:  
    * utag Sync
    * Pre-Loader
    * Before Load Rules
    * After Load Rules (default)
    * DOM Ready
    * Tag Scoped
    * After Tags
1. **Occurrence**: Select when to run the extension:
    * **Run Always**: Run the extension for every tracking call on a page.
    * **Run Once**:  Run the extension only once per page.
1. Enter your JavaScript code in the editor. The editor displays any errors and warnings.
1. **Condition** (Optional)
    * Click **Add Condition** and create a conditional statement.
    * The first drop-down list is populated with variables and the second drop-down list provides a list of [evaluating operators]().
    * If you are running the conditional logic against a value, enter it in the text field.
    * To apply multiple conditions, choose between the **AND** and **OR** logic.
1. Save and publish the changes.

## Troubleshooting

#### Why can&#39;t I edit the code in the editor?

You do not have the [Manage JS Code Extension permission]() in your Tealium iQ account. Contact your Tealium account administrator to obtain the permission.

#### Why can&#39;t I set the scope to **Pre Loader**?

If you have a condition defined, the **Pre Loader** option is no longer available. In **Pre Loader** scope, the data layer is not yet populated so there is no data object with which to evaluate the conditional logic. Likewise, the **Add Condition** option is disabled when the scope is set to **Pre Loader**.

#### What&#39;s the difference between an extension run in the **Pre Loader** scope and one run in **Before Load Rules** scope with occurrence set to **Run Once**?

In both cases, the extension to runs once before load rules are evaluated. The differences between the scopes are:

* The **Pre Loader** scope does not support conditions.
* Extensions in the **Pre Loader** scope execute before the data layer is processed and cannot access the data layer `b` object (it doesn&#39;t exist yet).
* The code in an extension scoped to **Pre Loader** is not wrapped in the anonymizing function and is executed exactly as it appears in the editor. For more information, see [Code Execution]().