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

To determine your region-specific host, go to **Admin menu &gt; Server-Side Settings &gt; Region**. You can then locate your region value in [Tealium IP addresses to allow]().

You can find the visitor ID from the value of the `v_id` key from the `utag_main` cookie namespace, also known as `utag.data[&#34;cp.utag_main_v_id&#34;]`.  

If the supplied visitor ID is invalid, or if the visitor does not currently have an active visit, the API returns status code 200 and an empty JSON response.

## Example request

```bash
curl https://visitor-service-us-west-2.tealiumiq.com/myaccount/main/015d1de1af41009e41015a38f658b0175002406d00fb3
```

## Example response

```json
   {
        &#34;metrics&#34; : {
            &#34;5117&#34; : 6.0,
            &#34;22&#34; : 6.0
        },
        &#34;dates&#34; : {
            &#34;5111&#34; : 1420223771043
        },
        &#34;properties&#34; : {
            &#34;account&#34; : &#34;myaccount&#34;,
            &#34;5123&#34; : &#34;set&#34;,
            &#34;profile&#34; : &#34;main&#34;
        },
        &#34;flags&#34; : { &#34;5115&#34; : true } ,
        &#34;current_visit&#34; : {
            &#34;metrics&#34; : {
                &#34;7&#34; : 6.0
            },
            &#34;dates&#34; : {
                &#34;5202&#34; : 1420225387000
            },
            &#34;properties&#34; : {
                &#34;48&#34; : &#34;Chrome&#34;,
                &#34;45&#34; : &#34;Mac OS X&#34;,
                &#34;44&#34; : &#34;Chrome&#34;,
                &#34;47&#34; : &#34;browser&#34;,
                &#34;46&#34; : &#34;Mac desktop&#34;
            },
            &#34;flags&#34; : { }
        },
        &#34;badges&#34; : { &#34;5113&#34; : true },
        &#34;audiences&#34; : {
            &#34;myaccount_main_101&#34; : &#34;Sample Audience&#34;
        }
    }

```