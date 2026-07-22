---
title: GET Data Layer Enrichment Public API
description: GET Data Layer Enrichment Public API lets you get profile data for an active visitor.
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/get-data-layer-enrichment-api/
---
## How it works

Use the following GET method to retrieve a visitor profile:

```bash
GET https://visitor-service-{REGION}.tealiumiq.com/{ACCOUNT}/{PROFILE}/{VISITOR_ID}

```

To determine your region-specific host, go to **Admin menu > Server-Side Settings > Region**. You can then locate your region value in [Tealium IP addresses to allow](https://docs.tealium.com/ip-allow-list/).

You can find the visitor ID from the value of the `v_id` key from the `utag_main` cookie namespace, also known as `utag.data["cp.utag_main_v_id"]`.  


<blockquote>
If the supplied visitor ID is invalid, or if the visitor does not currently have an active visit, the API returns status code 200 and an empty JSON response.
</blockquote>


## Example request

```bash
curl https://visitor-service-us-west-2.tealiumiq.com/myaccount/main/015d1de1af41009e41015a38f658b0175002406d00fb3
```

## Example response

```json
   {
        "metrics" : {
            "5117" : 6.0,
            "22" : 6.0
        },
        "dates" : {
            "5111" : 1420223771043
        },
        "properties" : {
            "account" : "myaccount",
            "5123" : "set",
            "profile" : "main"
        },
        "flags" : { "5115" : true } ,
        "current_visit" : {
            "metrics" : {
                "7" : 6.0
            },
            "dates" : {
                "5202" : 1420225387000
            },
            "properties" : {
                "48" : "Chrome",
                "45" : "Mac OS X",
                "44" : "Chrome",
                "47" : "browser",
                "46" : "Mac desktop"
            },
            "flags" : { }
        },
        "badges" : { "5113" : true },
        "audiences" : {
            "myaccount_main_101" : "Sample Audience"
        }
    }

```