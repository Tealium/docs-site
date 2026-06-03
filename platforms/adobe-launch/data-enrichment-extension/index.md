---
title: Tealium Data Enrichment extension for Adobe Launch
description: Learn about the Tealium Data Layer Enrichment extension for Adobe Experience Platform Launch.
url: https://docs.tealium.com/platforms/adobe-launch/data-enrichment-extension/
---
The Tealium Data Enrichment extension brings server-side attributes from Tealium AudienceStream and injects them into the data layer.

To install the Tealium Data Enrichment extension, use the following steps:

1. Search for the **Tealium Data Enrichment** extension in the Adobe Extension Catalog.
1. Click the **Install** button to add the extension.
1. Add a **Rule and Action** for **Tealium Data Enrichment**.
1. Hover over an installed extension and click **Configure**, then set the following options:
      * **Tealium Account**: (Required) Your Tealium account name.
      * **Tealium Profile**: (Required) Your Tealium profile name.
      * **Endpoint**: (Optional) Override the default endpoint with your own custom first-party endpoint, such as `https://visitor-service.collect.example.co.uk`.
1. Add a data element in Adobe Launch to read the data in local storage. For more information, see [Adobe: Data Elements](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements).

The [data layer enrichment object]() is stored in `localStorage` under the key `teal_adobe_enrichment_data`. Retrieving the key returns the data layer enrichment object.

The following example retrieves the data layer enrichment object from `localStorage` and then stores all the audiences in an array:

```javascript
var dle_object = JSON.parse(localStorage.getItem(
   &#34;teal_adobe_enrichment_data&#34;));

var data = {audiences: []};
if (dle_object.audiences) {
  for (var id in dle_object.audiences) {
    if (dle_object.audiences.hasOwnProperty(id)) {
     data.audiences.push(id);
    }
  }
}
```

If the data layer enrichment object contains nested values, it is automatically flattened before it is sent to the Tealium Collect endpoint.

For more information, see [Adobe: Adobe Experience Platform Launch object reference](https://experienceleague.adobe.com/docs/launch/using/reference/client-side-info/launch-object-reference.html?lang=en#buildinfo).

