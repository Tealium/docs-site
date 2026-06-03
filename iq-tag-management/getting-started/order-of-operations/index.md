---
title: Order of operations
description: This article describes the order of operations for the Universal Tag (utag.js) and how it relates to your configuration in iQ Tag Management.
url: https://docs.tealium.com/iq-tag-management/getting-started/order-of-operations/
---
For information about managing the load order of your configuration see the [Load Order Manager]().

## Understanding web page processing order

To understand how the Universal Tag (`utag.js`) loads, it is important to know how a browser loads a web page. Here are the main concepts to know that relate to `utag.js`:

1. **Request and Response**  
The browser requests the page located at a URL and the raw page content (HTML) is returned.
1. **Build**
    * The browser begins to parse the HTML document, from the top to the bottom. It must process various elements as they are encountered, such as images, links, text, or scripts like the Universal Tag (`utag.js`).
    * The browser continues to download these elements as it encounters them while it downloads the HTML document itself. 
    * Synchronous scripts force the browser to stop and interpret the script before continuing. Asynchronous scripts, like utag.js, allow the browser to continue processing while the script is loaded.
    * When the browser is done building the HTML of the page it is commonly called the &#34;DOM Ready&#34; event.
1. **Render**  
The browser renders the web page (DOM) on the screen.

## Order of operations overview

The default order of operations:

* **utag Sync** (when enabled)
* **Pre Loader** (extensions)
    * Prompt for Privacy Consent
    * Process Data Layer
* **Before Load Rules** (extensions)
    * Process Load Rules
* **After Load Rules** (extensions)
* **Prioritized Tags**
* **DOM Ready** (tags and extensions)
* **After Tags** (extensions)

## Order of operations details

The following sections provide a step-by-step overview of the order of operations of the Universal Tag (`utag.js`) to show how it processes the data layer and executes extensions and tags.

Within each scope, tags and extensions run in the order that they appear in the [Load Order Manager]().

### utag Sync (Optional)

Extensions scoped to **utag Sync** load from the `utag.sync.js` file. These extensions run once before anything else is processed, including extensions scoped to **Pre Loader**.

Learn more about [using utag.sync.js]().

### Pre loader

Extensions scoped to **Pre Loader** run before anything else is processed. Due to this, it is important that they do not have dependencies on other parts of `utag.js` that run later (data layer, other extensions, et cetera.).

#### Prompt for privacy consent (Optional)

After Pre Loader extensions are complete, and if you have the consent manager enabled, the prompt for consent is run.

#### Process data layer

After Pre Loader extensions are complete, the Universal Tag is initialized and the data layer is processed. During this step the Universal Data Object (`utag_data`) is combined with data from the rest of the web page such as, first-party cookies, meta tags, query string parameters, and global JavaScript variables, to form the final data layer object, `utag.data`. The data from this object can be used in your iQ configuration.

### Before load rules

After the data layer object is processed, the extensions scoped to **Before Load Rules** are run. The effects of these extensions can impact all tags and load rules.

#### Process load rules

Load rules are evaluated to determine which tags to load. If a tag is configured to load at the DOM Ready event, its load rule will be re-evaluated at that time using the current data object values.

### After load rules

After the load rules are evaluated, the extensions scoped to **After Load Rules** are run. The effects of these extensions can impact all tags.

### Prioritized tags

Tags with **Tag Timing** set to **Prioritized** are run based on the evaluated load rules.

Learn more about [tag timing](#tag-timing).

### DOM ready (tags and extensions)

Tags and extensions scoped to **DOM Ready** are run when the browser signals the DOM Ready event. Tags are loaded into the page as separate files, such as `utag.21.js`, and are loaded asynchronously to optimize page performance and visitor experience. The exact order of the DOM Ready extensions and tags cannot be guaranteed.

Each tag loaded on the page runs its tag-scoped extensions and applies its data mappings before it fires.

### After tags

After the tags are run the extensions scoped to **After Tags** are run.

### About single page applications

When you use `utag.view()` to track screen views manually, load rules are re-evaluated upon each call. [`utag.js` versions 4.26](/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2014-01-01) and later. Versions of the Universal Tag prior to 4.26 do not re-evaluate load rules when calling `utag.view()` .

Additionally, the behavior of load rules can be controlled using a configuration option called `load_rules_at_wait`, available in versions 4.26 and later of the Universal Tag. This is a legacy customization and we recommend that you contact your customer success manager before implementing it.

Learn more about the [configuration settings of the Universal Tag](/platforms/javascript/settings/).

## Glossary of terms

### Data mappings

When you map a Tealium variable to a vendor variable, you create a connection between them called a data mapping. Data mappings are how you configure what data gets sent to your tags.

### DOM

DOM is an acronym for Document Object Model. The DOM is the hierarchical representation of a web page that provides a way to interact with its elements.

### Extension scope

Extension scope indicates when an extension executes during the processing of utag.js. Extensions can be scoped to Pre Loader, Before Load Rules, After Load Rules, a specific vendor tag (tag-scope), or to the DOM Ready event.

### Tag bundling

Tag bundling is a setting that reduces the number of requests to fetch utag files. Rather than making individual requests for each tag (`utag.#.js`), the contents of those files are included (bundled) in the original file, `utag.js`.

### Tag timing

**Tag Timing** is an advanced tag setting that determines when the tag fires in the order of operations. The options are: `Prioritized` and `DOM Ready`.

Learn more about [advanced tag settings]().

### utag.view()

The `utag.view()` function is used to track page view events. When the utag.js file loads on a page, it automatically calls this function to track the initial page load as a page view event.

![](/images/iq-tag-management/utag.js-order-of-operations-simplified.jpg)

#### utag Waterfall - Tag Timing = &#34;Prioritized&#34;

![](/images/iq-tag-management/utag-waterfall-non-ready-wait.png)

#### utag Waterfall - Tag Timing = &#34;DOM Ready&#34;

![](/images/iq-tag-management/utag-waterfall-with-ready-wait.png)
