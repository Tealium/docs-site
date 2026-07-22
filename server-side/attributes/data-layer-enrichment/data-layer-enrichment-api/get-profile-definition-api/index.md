---
title: GET Profile Definition API
description: GET Profile Definition API lets you retrieve audience and badge data from a Tealium profile.
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/get-profile-definition-api/
---
## How it works

The Data Layer Enrichment Public API returns audience and badge data using only IDs. To reference the names of badges in the visitor data, you can request profile data using the Profile Definition API.


<blockquote>
The Profile Definition API returns badge and audience data associated with a Tealium profile and is not restricted to any specific user.
</blockquote>


Use the following GET command to retrieve a profile definition:

```bash
GET https://visitor-service.tealiumiq.com/datacloudprofiledefinitions/{ACCOUNT}/{PROFILE}
```

## Example request

```bash
curl https://visitor-service.tealiumiq.com/datacloudprofiledefinitions/myaccount/main/
```
## Example response

```json
    {
        "audiences" : [
            {
                "id" : "myaccount_main_101",
                "name" : "Sample Audience"
            }
        ],
        "badges" : [
            {
                "id" : 5113,
                "name" : "Cart abandoner"
            },
            {
                "id" : 32,
                "name" : "Unbadged"
            },
            {
                "id" : 31,
                "name" : "Frequent visitor"
            },
            {
                "id" : 30,
                "name" : "Fan"
            }
        ]
    }

```


