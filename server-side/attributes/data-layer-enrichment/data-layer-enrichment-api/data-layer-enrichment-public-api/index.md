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
* [Restricted attributes]() are not returned

If the visitor profile of an active visitor is not yet available when you submit a GET request, the API will return an empty JSON object.

For more information about JSON objects, see [Data Layer Enrichment API objects]().

 If you intend to use the Data Layer Enrichment API from a browser, you may need to set up an allow list. For more information, see [About Data Layer Enrichment - Domain Allow List](). 

### Combine with the Profile Definition API

The API returns a visitor profile that includes any badge IDs associated with the visitor. To retrieve the corresponding names of these badges, use the [Profile Definition API](). 

The Profile Definition API returns badge and audience data associated with a Tealium profile and is not restricted to any specific visitor.

For example, a request for a visitor profile that has two assigned badges will return the following using the Data Layer Enrichment Public API:

```json
{ 
  &#34;badges&#34; : {
    &#34;8879&#34;: true
  }
}
```

The Profile Definition API returns badge IDs and their names defined in the Tealium profile. In this example, the API would return:

```json
{
    &#34;badges&#34; : [
        {
            &#34;id&#34; : 24935,
            &#34;name&#34; : &#34;Cart abandoner&#34;
        },
        {
            &#34;id&#34; : 8879,
            &#34;name&#34; : &#34;Frequent visitor&#34;
        }
    ]
}
```




