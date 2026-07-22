---
title: Use Case — Supplementing Product Data
url: https://docs.tealium.com/iq-tag-management/data-layer/hosted-data-layer/use-case-supplementing-product-data/
---
The following is a use case to illustrate how to add new data layer variables to the page with hosted data layer.

* You have a database of information for the products you sell on your website.
* The basic product attributes, such as "ID", "Price", and "Name", are readily available to your web application and currently populated in the data layer on your page.
* An offline system that is not available to your web application contains additional product attributes that you want to add to the on-page data layer, such as "SKU", "In Store Availability", "Free Shipping Status", and "Brand".

The following steps describe the implementation process for this use case:

1. **Identify lookup variables**  
The on-page data layer contains `product_id`, which is also an identifier in the offline data and a good candidate for a lookup variable.
1. **Create/Upload hosted data layer objects**  
A program is created to export the offline product data into JSON data files, which are named according to the expected values of `product_id`.  
For example, if the on-page data layer contains `product_id=["PRD123"]`, then a matching hosted data layer file named PRD123.js is created. A separate file is created for every product.
1. **Configure hosted data layer Extension**  
With the lookup variable identified and hosted data layer objects uploaded, the hosted data layer extension is then added and configured to use `product_id`.  
Although your on-page data layer may only have `product_id` available, you have used the hosted data layer API to upload additional product data. The lookup variable is now `product_id`, which means that the values of the product identifier variable determines the names of the hosted data layer objects.  

The following shows the result of applying the enrichment process.

* On-Page data layer `utag_data`  
  ```json
  {
      "page_type"  : "product",
      "product_id" : ["PRD123"]
  }
  ```
* Hosted data layer object `PRD123.js`  
  ```json
  {
      "has_free_shipping"  : ["0"],
      "has_instore_pickup" : ["1"]
  }
  ```
* Merged data layer  
  ```js
  utag.view({
      "page_type"          : "product",
      "product_id"         : ["PRD123"],
      "has_free_shipping"  : ["0"],
      "has_instore_pickup" : ["1"]
  })
  ```