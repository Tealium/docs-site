---
title: Optimizely Sync Tag Setup Guide (Deprecated)
description: IMPORTANT  This Tag is now deprecated. Please use the [utag.sync.js for implementing Optimizely Synchronous](/client-side-tags/optimizely-synchronous-implementation/). We will continue to support existing instances of the Tag.
url: https://docs.tealium.com/client-side-tags/optimizely-sync-tag/
---
Tealium's tag marketplace offers two versions of the Optimizely Tag, one that loads on your page asynchronously, and one that loads synchronously. So which one to use?

* **Async**: Loading a Tag asynchronously removes the risk of a Tag load failure breaking your site.
* **Sync**: This version is best suited if avoiding content flicker is your primary concern. Keep in mind that any time you load something synchronously, you introduce the risk of breaking your site if the browser is unable to retrieve the element for some reason. Talk to your Account Manager for a custom solution if necessary.

### Prerequisites

* Optimizely Account
* Project ID

### Adding the Tag

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

### Configuring the Tag

![](https://docs.tealium.com/images/client-side-tags/sync-tag-config.png)

1. **Title**: (Required) Enter a descriptive title to identify the Tag instance.
1. **Project ID**: (Required) Enter the numeric Project identifier provided to you by Optimizely.

### Applying Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this Tag. The 'Load on All Pages' rule is the default Load Rule. To load this Tag on a specific page, create a new load rule with the relevant conditions.

**Best Practice**: We recommend loading this Tag on all your pages, so leave the 'Load on All Pages' load rule selected. Also, place the Optimizely Tag at the top of your Tag list on the Tags tab.

### Setting up Mappings

[Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/) is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag.

NOTE: If you plan to track E-Commerce data with the Optimizely Tag, we recommend that you use the [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) to automatically map that data.

For instructions on how to map to a Tag destination, please refer [Mapping Data Source](https://docs.tealium.com/about-data-sources/).

**![](https://docs.tealium.com/images/client-side-tags/sync-tag-mapping.png)**

* **Event Name for trackEvent (EVENT\_NAME)**
Map the data source that identifies the event.

* **Event Value for trackEvent (EVENT\_VALUE)**
Map the data source that identifies the value of the event.

----

### Vendor Documentation

* [Optimizely documentation](http://developers.optimizely.com/)
* [Implementing Optimizely with Tealium iQ](https://help.optimizely.com/hc/en-us/articles/206420397-Implementing-Optimizely-with-Tealium-iQ-or-Ensighten)
