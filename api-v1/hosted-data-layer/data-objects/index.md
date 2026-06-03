---
title: Hosted Data Layer objects
description: Create a data layer object or JSON file on Tealium's servers.
url: https://docs.tealium.com/api-v1/hosted-data-layer/data-objects/
---
This is an older version of the [current Tealium Hosted Data Layer API]().


## Creating a Hosted Data Layer object

Use the following steps to create a data layer object:

1. Define the new variables in a flat JSON file, as shown in the following example:  
      The JSON payload should not exceed 1 MB.

        ```json
      {
          &#34;product_category&#34;           : [&#34;Accessories&#34;],
          &#34;product_brand&#34;              : [&#34;Acme&#34;],
          &#34;product_sku&#34;                : [&#34;GEN-PRD-BLU&#34;],
          &#34;product_has_free_shipping&#34;  : [&#34;0&#34;],
          &#34;product_has_instore_pickup&#34; : [&#34;1&#34;]
      }
        ```
  
1. Set the file name according to the naming guidelines. For example: &#34;prod123456.json&#34;. 
1. Make an HTTPS POST request to upload the object to Tealium.
1. (Optional) Preview the uploaded JSON URL of the following format:  
`https://tags.tiqcdn.com/dle/{account}/{profile}/{dl_id}.js`

The account name, profile name, and `dl_id` names combined should not exceed 250 characters.