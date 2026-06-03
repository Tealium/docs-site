---
title: GET Profile Definition API
description: GET Profile Definition API lets you retrieve audience and badge data from a Tealium profile.
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/get-profile-definition-api/
---
## How it works

The Data Layer Enrichment Public API returns audience and badge data using only IDs. To reference the names of badges in the visitor data, you can request profile data using the Profile Definition API.

The Profile Definition API returns badge and audience data associated with a Tealium profile and is not restricted to any specific user.

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
        &#34;audiences&#34; : [
            {
                &#34;id&#34; : &#34;myaccount_main_101&#34;,
                &#34;name&#34; : &#34;Sample Audience&#34;
            }
        ],
        &#34;badges&#34; : [
            {
                &#34;id&#34; : 5113,
                &#34;name&#34; : &#34;Cart abandoner&#34;
            },
            {
                &#34;id&#34; : 32,
                &#34;name&#34; : &#34;Unbadged&#34;
            },
            {
                &#34;id&#34; : 31,
                &#34;name&#34; : &#34;Frequent visitor&#34;
            },
            {
                &#34;id&#34; : 30,
                &#34;name&#34; : &#34;Fan&#34;
            }
        ]
    }

```


