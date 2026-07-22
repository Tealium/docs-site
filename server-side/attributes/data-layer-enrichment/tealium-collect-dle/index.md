---
title: Add and configure the Tealium Collect tag
description: This article describes how to configure the Tealium Collect tag to enable data layer enchrichment.
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/tealium-collect-dle/
---
For detailed instructions see the [Tealium Collect Tag Setup Guide](https://docs.tealium.com/tealium-collect-tag/).

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-tealiumcollecttagconfiguration.png)

## Data enrichment frequency

To set up your Tealium Collect tag to enable data layer enrichment, you must determine how often to update your data layer with attribute information. Here are the options:

* **None** (Default)
  * Data layer enrichment does not occur.
* **Infrequent**
  * Data layer enrichment occurs once per visit (session).
  * The retrieved customer data is stored in local storage for use on subsequent tracking calls during the session.
* **Frequent** (Recommended)
  * Data layer enrichment occurs on every tracking call. Customer data that changes during the session is reflected in real-time in the Universal Data Object (UDO).  
  
<blockquote>
This option causes an additional HTTP request per page.
</blockquote>


## Selecting a load rule

We recommend leaving the default **Load on All Pages** load rule selected for the Tealium Collect tag. To ensure the data layer contains the necessary attributes, populate it with the most relevant data.

### Using AudienceStream attributes in Tealium iQ

AudienceStream attributes are treated as imported variables in Tealium iQ. These variables cannot be edited or deleted. To delete or modify an AudienceStream attribute, make the change in your AudienceStream profile. Attributes cannot be imported into a [profile library](https://docs.tealium.com/about-profile-libraries/), they can only be imported into a regular profile.

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-editaudiencestreamvariables.png)

### Which AudienceStream attribute types are imported?

The following attribute types are imported into Tealium iQ and made available in the data layer:

* Badges
* Numbers
* Strings
* Booleans
* Dates  


<blockquote>
Date attributes are imported into the data layer and visible in the UDO. They are not available for use in load rules or tag mappings.
</blockquote>


## Building load rules

You can use supported attributes to create load rules. The following rule operators are available for badges in load rules.

* **is badge assigned**  
`True` if the badge attribute is assigned to the visitor.  
      ![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-badgeisorisnotassigned.png)
* **is badge not assigned**  
`False` if the badge attribute is not assigned to the visitor.


<blockquote>
Deleting an attribute from AudienceStream automatically removes it from the data layer screen in Tealium iQ. However, load rules that reference the deleted attribute do not update automatically. You must manually update any load rules that still reference deleted attributes.
</blockquote>


## Callback function

The data layer enrichment request provides a callback method `window.tealium_enrichment()` that lets you execute code based on the response.

To use the callback function, create a [JavaScript Code extension](https://docs.tealium.com/advanced-javascript-code-extension/) scoped to Pre Loader with the following code:

```js
window.tealium_enrichment = function(data) {
    console.log("Data Layer Enrichment Callback");
    // Your code here...
};
```