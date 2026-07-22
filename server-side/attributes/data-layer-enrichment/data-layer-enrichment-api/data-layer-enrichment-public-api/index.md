---
title: About Data Layer Enrichment Public API
description: The Data Layer Enrichment Public API lets you retrieve profile data for an active visitor.
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/data-layer-enrichment-public-api/
---
## How it works

After a visitor triggers an event on your site, you can use the Data Layer Enrichment API to retrieve the visitor profile. API visitor data is available for two minutes after the last activity within a visit is received as an AudienceStream event.

The returned AudienceStream visitor profile differs from the typical visitor profile in the following ways:

* Badges and audiences are returned as objects
* Timelines and funnels have been removed
* [Restricted attributes](https://docs.tealium.com/data-layer-enrichment-object/) are not returned

If the visitor profile of an active visitor is not yet available when you submit a GET request, the API will return an empty JSON object.

For more information about JSON objects, see [Data Layer Enrichment API objects](https://docs.tealium.com/data-layer-enrichment-object/).


<blockquote>
If you intend to use the Data Layer Enrichment API from a browser, you may need to set up an allow list. For more information, see [About Data Layer Enrichment - Domain Allow List](https://docs.tealium.com/about-data-layer-enrichment/).
</blockquote>


### Combine with the Profile Definition API

The API returns a visitor profile that includes any badge IDs associated with the visitor. To retrieve the corresponding names of these badges, use the [Profile Definition API](https://docs.tealium.com/get-profile-definition-api/). 


<blockquote>
The Profile Definition API returns badge and audience data associated with a Tealium profile and is not restricted to any specific visitor.
</blockquote>


For example, a request for a visitor profile that has two assigned badges will return the following using the Data Layer Enrichment Public API:

```json
{ 
  "badges" : {
    "8879": true
  }
}
```

The Profile Definition API returns badge IDs and their names defined in the Tealium profile. In this example, the API would return:

```json
{
    "badges" : [
        {
            "id" : 24935,
            "name" : "Cart abandoner"
        },
        {
            "id" : 8879,
            "name" : "Frequent visitor"
        }
    ]
}
```




