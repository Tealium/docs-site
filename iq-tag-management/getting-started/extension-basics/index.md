---
title: Extension basics
description: Learn the basics about extensions.
url: https://docs.tealium.com/iq-tag-management/getting-started/extension-basics/
---
Extensions provide a user-friendly interface to add customizations to your data layer and tags without the need for coding. Extensions have a variety of purposes, such as modifying data layer values, setting cookies, and even setting up click tracking. Think of extensions as your tag management toolbox.

## Scope

The effects of extensions are either global or local, meaning they are applied to all tags globally or to individual tags. In extensions, this setting is called _scope_.

* **Global Scope**  
The effects of an extension apply to all tags. The scope is simply called `All Tags`.
* **Local Scope**  
The effects of an extension only apply to a specific tag. The scope is called `Tag Scope`. 

To get comfortable using extensions, it is important to understand the order of operations of the main components of TiQ and when the &#34;All Tags&#34; scope occurs. The following details a simplified version of the order of operations in TiQ that shows when the data layer object is processed by each component.

1.  Page loads the following:
    *   UDO – `utag_data`
    *   Tealium Tag – `utag.js`
2.  Tealium Tag (`utag.js`) runs the following:
    *   **Data Layer** variables are evaluated (cookies, meta, query string, etc.)
    *   **Load Rules** are evaluated
    *   `&#34;All Tags&#34;` extensions run (**Global scope**)
    *   **Tags** run
        *   &#34;Tag Scope&#34; extensions run (**Local scope**)
        *   Tags fire

A link to a detailed version of the order of operations is provided in the Additional Resources section at the end of this guide.

In summary:

*   &#34;All Tags&#34; extensions affect all tags.
*   &#34;Tag Scoped&#34; extensions only affect the associated tags.

There are two other global scopes called &#34;Pre Loader&#34; and &#34;DOM Ready&#34; that are used for more advanced scenarios. Also, within the &#34;All Tags&#34; scope there is an _execution_ setting that provides more granular control for running tags before load rules or after all tags.

Additional details about these settings are found at the end of this guide.
