---
title: Adobe Target Extension
description: The Adobe Target Extension lets you control your tests loaded by the Adobe Target Tag, all through Tealium iQ. This article describes how to configure the Adobe Target Extension in your Tealium iQ account.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/adobe-target-extension/
---

<blockquote>
If your website currently uses the Adobe Test & Target extension and tag, there are special considerations to make before implementing Adobe Target. Please see the section on [Migrating from Adobe Test & Target](#migration).
</blockquote>


## Adding and configuring the extension

![](https://docs.tealium.com/images/iq-tag-management/tealium-iq---tag-management.png)

1. **Title:** This is a Tealium-specific field. Enter a descriptive title to make the extension easily identifiable, especially if you have multiple instances of the same extension.
1. **Scope:** You must set the scope of this extension to **Adobe Target**.
1. **Element Type:** Select either **DOM ID** or **xPath**. We recommend using DOM ID to identify an element, as the xPath identifier can change if the structure of the page changes.  
    
<blockquote>
If the element is not found in the page, the tag will not trigger a call to the mbox.
</blockquote>


1. **Identifier:** Enter the element's DOM ID or xPath identifier value here.
1. **Mod Position:** Specify where you want the new content to go in relation to the element you identified:
    * **Before Node**: Place the content before the element you identified.
    * **After Node**: Place the content after the element you identified.
    * **Beginning of Node**: Place the content at the beginning of the element you identified.
    * **End of Node**: Place the content at the end of the element you identified.
    * **Replace Node Content**: Replace the element's content.
    * **Replace Node**: Replace the entire element.
    * **Replace Node Content (leave default)**: Replace the element's content, but if Adobe's Target service is temporarily unavailable, the default content will appear instead of the test content. If you want to use the Flicker Free functionality, you must select this Mod Position.   
    
<blockquote>
In most cases, we recommend setting and leaving the **Mod Position** option to **Replace Node Content (leave default)**.
</blockquote>


1. **mBox Div ID:** Enter the mBox ID of your test. Adobe provides this to you.
1. **Static Params:** You can add static parameters in this field in query string format, which means you separate them with an ampersand (`&`).
1. **Conditions:** Create the logic statement that determines when and where the extension will modify content.

To add more content modification entries, click the plus button in the upper-right corner of the extension settings. You can duplicate the extension for each entry instead, but keeping multiple entries in the one extension is neater as all of the entries in this extension share the extension's load condition.

### utag.sync.js Requirement

Like many A/B testing tools implemented in Tealium iQ, Adobe Target requires use the synchronous version of `utag.js`, known as `utag.sync.js`. When adding the Adobe Target extension, it will automatically toggle on the **Generate utag.sync.js File** option in your profile's [Publish Configuration](). If you're already using `utag.sync.js` in the `<head>` section of your pages, no further action is required. Otherwise, you'll need to update the utag code generated in your Code Center.

For more information, see our articles on [using utag.sync.js]() and [accessing the Code Center]().

## Using Adobe Enterprise Cloud

For customers using Adobe Enterprise Cloud alongside Adobe Target, be aware that the Adobe Enterprise Cloud tags must be loaded before the Adobe Target tags. Use of Adobe Enterprise Cloud is optional.

## Migrating from Adobe Test and Target

The Adobe Target tag and extension are complete replacements of the Adobe Test & Target solution previously available in Tealium iQ. The following are a list of considerations for migrating to Adobe Target from an existing Adobe Test & Target implementation.

### Compatibility with Adobe Test and Target

Adobe Target and Test & Target tags may coexist on the same profile. However, they each require the use of their own respective extensions.

## Changes in tag and extension availability

### Tag

The Adobe Test & Target tag—formerly labeled in the tag marketplace as two variants, "Adobe Target (async)" and "Adobe Target (sync)"— is deprecated by the release of Adobe Target, and has been replaced in the tag marketplace by a single tag simply called **Adobe Target**. Existing Test & Target tags on your Tealium iQ profiles will remain active and continue to function as usual, as long as the Adobe Test & Target extension is also active on those profiles.

### Extension

The Test & Target extension will continue to be offered in the extension marketplace alongside the Adobe Target extension, and will work only with Test & Target tags. However, both extensions cannot be active at the same time. Please see the next section on migration steps for details.

## Order of migration steps

To switch from an Adobe Test & Target to Adobe Target implementation, you must perform the following steps in order:

1. Deactivate the Test & Target extension in your Tealium iQ profile.
1. Add the Adobe Target tag from the tag marketplace.
1. Add the Adobe Target extension and scope it to the new Adobe Target tag.
1. At this point, you may remove any Adobe Test & Target tags on your Tealium iQ profile, as they will no longer be functional without the Test & Target extension.
