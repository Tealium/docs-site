---
title: About extensions
description: Extensions provide a variety of ways to customize your implementation by offering a simple configuration interface to add complex logic without the need for coding.
url: https://docs.tealium.com/iq-tag-management/extensions/about/
---
Extensions have many purposes, from setting and updating data layer variables, to adding advanced event tracking to your site. The available extensions are presented in the **Extensions Marketplace**, where they are grouped by category with brief descriptions of their functionality.

The extensions categories are:

* **Standard Data**  
Set and modify data layer variables and cookies in a variety of ways.
* **Advanced**  
Extensions that require some knowledge of JavaScript and/or advanced marketing strategies.
* **Events**  
Extensions related to event tracking, either using jQuery, built-in tracking, or mapping the standard Tealium events.
* **Tag Specific**  
Extended functionality for use with certain tags, such as Adobe Test &amp; Target, or tags that require currency conversion.
* **Privacy**  
Extensions to offer opt-in/opt-out, Do Not Track, or tracking preferences for your users.

Use the search box to find an extension across any tab.

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-extensionsstandarddata.png)

The extension marketplace is like a toolbox filled with a variety of different tools to help you with tag management. We encourage you to familiarize yourself with all of the available extensions so that you'll know exactly how to solve your next tag management challenge.

For additional information, see the [List of available extensions](https://docs.tealium.com/iq-tag-management/extensions/extensions-list/).

## How it works

When an extension is added to your configuration, then saved and published, the logic in the extension is converted to JavaScript code that then runs in the utag files that load on your website. The timing of the extension depends on several factors, including: the scope setting, the execution order setting, and the position of the extension in the list.

## Understanding scope

When adding an extension it is important to understand the **scope** setting. The scope determines which utag file the extension is published in and when the extension runs. Extensions within the same scope will run in the order that they appear in the user interface. The following scope options are available:

* **utag Sync**: For use with the JavaScript Code or Advanced JavaScript Code extensions. Associates an extension to the `utag.sync.js` file.
* **Pre Loader**: Runs before the data layer is processed and results are applied globally (code appears in utag.js).
* **Before Load Rules**
* **After Load Rules**
* **DOM Ready Extensions**: Runs once, at the [DOMContentLoaded browser event](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded), the code appears in `utag.js`.
* **Tag Scoped Extensions**: Runs only when the specified tags run and changes are only applied for that tag (code appears in tag-specific `utag.#.js`). Any data layer values modified in this scope will not affect other tags.
    * Check **Tag Scoped Extensions** to display **All Tags**, which run after the data layer is processed and changes are applied globally (code appears in `utag.js`). See Execution Order for more information about exact timing.
* **After Tags Extensions**: Runs after tags are triggered.


<blockquote>
If you set **Scope** to **utag Sync**, **Pre Loader**, or **DOM Ready Extensions** you must set **Occurrence** to **Run Once**.
</blockquote>


The scopes Pre Loader, All Tags (except for After Tags execution order), and Tag Scope are guaranteed to run in that order, but DOM Ready extensions will execute independently from the other three. In most standard implementations the DOM Ready scope likely occurs sequentially after the other three, but this timing should not be assumed.


<blockquote>
Some extensions, such as E-Commerce, Pathname Tokenizer, jQuery, and onHandler 1.7, have a pre-set scope that cannot be changed.
</blockquote>


## Understanding execution order

The **execution** setting offers more granular control of the timing of an All Tags extension.

The following options are available:

* **Before Load Rules** - runs after the data layer is processed (For example, after Pre Loader, but prior to evaluating load rules).
* **After Load Rules (default)** - runs after load rules are evaluated.
* **After Tags** - runs after tags have been triggered.
* **utag Sync** - runs first when using with JavaScript Code or Advanced JavaScript Code extensions by associating the extension to the `utag.sync.js` file.

For a detailed overview of extension execution order see [Order of Operations]().

## Conditions

Some extensions support conditions. Conditions are like load rules, but only applied to extensions. A condition applied to an extension will determine if the extension should run within the given scope and execution order.