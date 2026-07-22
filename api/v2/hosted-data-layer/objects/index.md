---
title: Hosted Data Layer objects
description: Create a data layer object or JSON file on the Tealium's servers.
url: https://docs.tealium.com/api/v2/hosted-data-layer/objects/
---
## Create a Hosted Data Layer object

Use the following steps to create a hosted data layer object:

1. Define the new variables in a flat JSON file, as shown in the following example:  
The JSON payload should not exceed 1 MB.
  
      ```json
      {
          "product_category"           : ["Accessories"],
          "product_brand"              : ["Acme"],
          "product_sku"                : ["GEN-PRD-BLU"],
          "product_has_free_shipping"  : ["0"],
          "product_has_instore_pickup" : ["1"]
      }
      ```

1. Save the file with a name following the naming guidelines.  
Example: `prod123456.json`  
The `account`, `profile`, and `datalayer_id` names combined should not exceed 250 characters.
1. Make an HTTPS POST request to upload the hosted data layer object to Tealium.
1. (Optional) Type in the following URL to preview the uploaded data layer object:  
      ```bash
      https://tags.tiqcdn.com/dle/{account}/{profile}/{datalayer_id}.js
      ```
For JSON files, use the _.json_ file extension.
