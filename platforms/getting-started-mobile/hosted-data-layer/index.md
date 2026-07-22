---
title: Hosted Data Layer
description: Learn about the hosted data layer feature for mobile.
url: https://docs.tealium.com/platforms/getting-started-mobile/hosted-data-layer/
---
## Supported Platforms

The following platforms support hosted data layer:

- [Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/)
- [iOS (Swift v2.x)](https://docs.tealium.com/platforms/ios-swift/)

## How it Works

Hosted data layer facilitates the use of statically-hosted data for the purpose of supplementing the dynamic data layer of your mobile app or for hosting JSON configuration files. While the data layer implemented in your mobile app is useful in capturing real-time information, it can be a challenge to include additional valuable information from offline systems. Hosted data layer provides a convenient mechanism to upload static data to Tealium, where it can be accessed by your mobile app to enrich data or power an application that uses JSON files.

Tealium for mobile supports a hosted data layer which stores certain data layer items remotely to be downloaded by your app. This feature is useful in any scenario where data layer attributes are not available in your native code, but can be made available from your organization. For example, your e-commerce system might have product attributes such as `product_is_in_stock` or `product_has_free_shipping` that are not easily accessed in native code, but can be uploaded as hosted data layer files.

A _lookup variable_ identifies which variable the data layer uses for fetching the corresponding hosted data layer object. The hosted data layer data items persist for 7 days by default, and are re-downloaded after expiration.  

Additional Information:  

- About [hosted data layer](https://docs.tealium.com/use-case-supplementing-product-data/)
- [Hosted data layer API](https://docs.tealium.com/about-hosted-data-layer-api/)


## Configuration

Prior to initializing the Tealium library, identify and configure the hosted data layer keys (lookup variables) by setting the following property. The key-values are used by the hosted data layer module to retrieve data layer IDs

- Android: [`hostedDataLayerEventMappings`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/#hosteddatalayereventmappings)
- Swift: [`hostedDataLayerKeys`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#hosteddatalayerkeys)

By default, data persists for 7 days in the hosted data layer data, and is re-downloaded after expiration. Configure an expiration time on hosted data layer data by setting the following property.

- Android: [`hostedDataLayerMaxCacheTimeMinutes`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/#hosteddatalayermaxcachetimeminutes)
- Swift: [`hostedDataLayerExpiry`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#hosteddatalayerexpiry)


<blockquote>
Setting a shorter expiration time reduces mobile device battery life due to increased network requests.
</blockquote>


## Use Case: Supplementing Product Data

Scenario:

- You have a database of information for the products you sell in your mobile app.
- The basic product attributes, such as `ID`, `Price`, and `Name`, are readily available to your mobile app and currently populated in the data layer.
- An offline system that is not available to your mobile app contains additional product attributes that you want to add to the data layer, such as `SKU`, `In Store Availability`, `Free Shipping Status`, and `Brand`.

The following steps describe the implementation process for this use case:

1. **Identify lookup variables**  
The data layer contains `product_id`, which is also an identifier in the offline data and a good candidate for a lookup variable.
2. **Create and upload hosted data layer objects**  
Export the offline product data into JSON files, which are named according to the expected values of `product_id`. For example, if the data layer contains `product_id=["PRD123"]` , then a matching hosted data layer file named `PRD123.js` is created. Create a separate file for each product.

The following table shows the end result of applying the enrichment process.

| Enrichment | Result |
| --- | --- |
| Data layer `utag_data`|`{ "page_type":"product", "product_id":["PRD123"]}` |
| Hosted data layer object `PRD123.js`|`{"has_free_shipping":["0"], "has_instore_pickup":["1"]}` |
| Merged data layer |`{"page_type":"product", "product_id":["PRD123"], "has_free_shipping":["0"], "has_instore_pickup":["1"]}` |

## Troubleshooting

The following are troubleshooting tips:

* Be aware that track calls where the dispatch contains hosted data layer components may be sent out of order, due to the additional time required to retrieve those remote files. This doesn't apply if a valid cache exists for an item, since lookup isn't required.
* If there are any server or connectivity errors when the hosted data layer request is made, the request retries up to 5 times. After 5 failed attempts, the track call is sent without the hosted data layer data.
* If a valid record on Tealium is not found for an item, the track call is sent without the hosted data layer data.
* If there is no valid cache available for the hosted data layer item being requested, the first request is queued and only sent when the queue is flushed. This behavior is automatic when the maximum number of batched events is reached or if the app is in the background.
