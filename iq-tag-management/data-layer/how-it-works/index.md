---
title: How the data layer works
description: This article explains how the data layer works for websites.
url: https://docs.tealium.com/iq-tag-management/data-layer/how-it-works/
---
The following terms are related to a website data layer and your [installation of `utag.js`](/platforms/javascript/install/):

* **Universal Data Object (`utag_data`)**  
The Universal Data Object (UDO) is the JavaScript object that represents the data layer on your site. You populate this object across all the pages of your site with dynamic values that describe the page and visitor interactions.  
Learn more about [how the UDO works](/platforms/javascript/about-utag-data/).

* **Variable types**   
Data available directly from your web page (other than your customized UDO) through DOM data, query strings, meta data tags, cookies, and JavaScript variables.  
Learn more about the [data layer variable types]().

* **`utag.data`**   
The final data object that combines variables from the UDO with all other variable types from the page. This data is used to evaluate load rules.  
Learn more about the [built-in variables available in the UDO](/platforms/javascript/built-in-variables/).

* **`b` object**   
A JavaScript object used by functions within `utag.js`. The `b` object is a copy of `utag.data` that is used for each vendor tag. The `b` variable can be referenced in JavaScript extensions.  
Learn more about [the `b` object and how it&#39;s used](/platforms/javascript/the-b-object/).

The following graphic shows how individual variables come together to create your Data Layer and how that data flows out to your vendor tags.

![](/images/iq-tag-management/dataflow-b&amp;w.jpeg)

## Data layer flow

When you install Tealium on a web page, the data layer object behaves as follows:

1. All variables defined in Tealium iQ Tag Management are identified.
1. Variables are combined into `utag.data`.
1. `utag.data` is copied to the locally scoped `b` object as needed.
1. Extensions run, which might modify the `b` object.
1. Load rules evaluate variables to determine which tags to load and fire.
1. Load rules evaluate whether to load event listeners.
1. Variable values are mapped to destinations in vendor tags.
1. Vendor tags fire and pass variable values according to your data mappings.

Learn more about the [order of operations of the Tealium Javascript library]().
