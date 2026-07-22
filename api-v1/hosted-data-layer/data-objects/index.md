---
title: Hosted Data Layer objects
description: Create a data layer object or JSON file on Tealium's servers.
url: https://docs.tealium.com/api-v1/hosted-data-layer/data-objects/
---
This is an older version of the [current Tealium Hosted Data Layer API](https://docs.tealium.com/about-hosted-data-layer-api/).


## Creating a Hosted Data Layer object

Use the following steps to create a data layer object:

1. Define the new variables in a flat JSON file, as shown in the following example:  
      
<blockquote>
The JSON payload should not exceed 1 MB.
</blockquote>


        ```json
      {
          "product_category"           : ["Accessories"],
          "product_brand"              : ["Acme"],
          "product_sku"                : ["GEN-PRD-BLU"],
          "product_has_free_shipping"  : ["0"],
          "product_has_instore_pickup" : ["1"]
      }
        ```
  
1. Set the file name according to the naming guidelines. For example: "prod123456.json". 
1. Make an HTTPS POST request to upload the object to Tealium.
1. (Optional) Preview the uploaded JSON URL of the following format:  
`https://tags.tiqcdn.com/dle/{account}/{profile}/{dl_id}.js`


<blockquote>
The account name, profile name, and `dl_id` names combined should not exceed 250 characters.
</blockquote>
