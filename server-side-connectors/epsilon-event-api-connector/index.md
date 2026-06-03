---
title: Epsilon Event API Connector Setup Guide
description: This article describes how to set up the Epsilon Event API connector.
url: https://docs.tealium.com/server-side-connectors/epsilon-event-api-connector/
---
Epsilon is a marketing services provider. Use the Epsilon Event API to pass information to Epsilon regarding what customers view and purchase on your website.

## Configure settings

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Company ID**: Company ID (`dtm_cid`) to identify your calls.
* **Secondary Company ID**: Separate identifier (`dtm_cmagic`) to confirm company ID.

## Actions

| **Action Name** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| Send Browsing Event | ✗ | ✓ |
| Send Transaction Event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Browsing Event

#### Event Data

| **Parameter** | **Description** |
| --- | --- |
| Form ID (`dtm_fid`) | (Required) The form ID for the browsing event. |
| URL (`dtmc_loc`) | (Required) URL of the page the user is viewing. |
| IP Address (`dtm_user_ip`) | (Required) IP address of the user. |
| Cookie ID (`dtm_cookie_id`) | (Required) Unique ID for the user. |
| Promo ID (`dtm_promo_id`) | Value that identifies the page type or promotion context. |
| Brand (`dtmc_brand`) | Brand associated with the product or content viewed. |
| Canonical URL (`dtmc_canonical_url`) | Canonical URL for the page being viewed. |
| Category (`dtmc_category`) | Primary product or content category. |
| Customer ID (`dtm_user_id`) | Unique identifier for the known customer (for example, CRM ID or loyalty ID). |
| Department (`dtmc_department`) | Department or line of business associated with the product (for example, `Electronics`, `Home`). |
| Email (apply SHA256 hash) | Plain-text email address to be SHA256 hashed before sending to Epsilon. |
| Email (already SHA256 hashed) | Email address already hashed with SHA256; sent to Epsilon as provided. |
| GDPR consent (`dtmc_tcf_string`) | IAB TCF consent string that represents the visitor’s GDPR consent state. |
| Manufacturer Model Part Number (`dtmc_mpn`) | Manufacturer’s model or part number for the product. |
| Manufacturer UPC (`dtmc_upc`) | Manufacturer’s UPC for the product. |
| Product ID (`dtmc_product_id`) | Unique identifier for the product being viewed. |
| Referring URL (`dtm_referrer`) | URL of the page that referred the visitor to the current page. |
| Subcategory (`dtmc_sub_category`) | Subcategory for the product or content (for example, `Shoes` within `Apparel`). |
| User Agent (`dtm_user_agent`) | Browser user agent string from the visitor’s device. |
| Cachebuster | Random or timestamp value used to prevent response caching. |
| GPP String | (Required) The Global Privacy Platform (GPP) consent string. |
| Custom Query Parameters | Custom values to add as query string parameters to the base URL. |

### Send Transaction Event

#### Event Data

| **Parameter** | **Description** |
| --- | --- |
| Form ID (`dtm_fid`) | (Required) The form ID for the transaction event. |
| URL (`dtmc_loc`) | (Required) The URL of the page where the transaction occurs (for example, a confirmation page). |
| IP Address (`dtm_user_ip`) | (Required) The IP address of the user. |
| Cookie ID (`dtm_cookie_id`) | (Required) The advertiser-supplied cookie ID used to identify the user. |
| Promo ID (`dtm_promo_id`) | A value that identifies the page type or promotion associated with the transaction. |
| Brand (`dtmc_brand`) | The brand associated with the purchased products. |
| Canonical URL (`dtmc_canonical_url`) | The canonical URL for the transaction page. |
| Category (`dtmc_category`) | The primary product or content category. |
| Customer ID (`dtm_user_id`) | The unique identifier for the known customer (for example, CRM ID or loyalty ID). |
| Department (`dtmc_department`) | The department or line of business associated with the products. |
| Email (apply SHA256 hash) | Plain-text email address to be SHA256 hashed before sending to Epsilon. |
| Email (already SHA256 hashed) | Email address already hashed with SHA256; sent to Epsilon as provided. |
| GDPR consent (`dtmc_tcf_string`) | The IAB TCF consent string that represents the visitor’s GDPR consent state. |
| Manufacturer Model Part Number (`dtmc_mpn`) | The manufacturer’s model or part number for the product. |
| Manufacturer UPC (`dtmc_upc`) | The manufacturer’s UPC for the product. |
| Product ID (`dtmc_product_id`) | The unique identifier for the purchased product. |
| Referring URL (`dtm_referrer`) | The URL that referred the visitor to the transaction page. |
| Subcategory (`dtmc_sub_category`) | The product or content subcategory. |
| User Agent (`dtm_user_agent`) | The browser user agent string from the visitor’s device. |
| Cachebuster | Random or timestamp value used to prevent response caching. |
| GPP String | (Required) The Global Privacy Platform (GPP) consent string. |

#### Transaction Data

| **Parameter** | **Description** |
| --- | --- |
| Transaction ID (`dtmc_transaction_id`) | The advertiser’s unique identifier for each conversion. |
| Order Subtotal (`dtm_conv_val`) | The total price for all items purchased. Do not include tax or shipping costs. |
| Conversion Type (`dtmc_conv_type`) | Used to differentiate between types of online purchases, such as delivery or pickup. |
| Currency Code (`dtm_conv_curr`) | The ISO 4217 currency code (for example, EUR or USD). |
| Store Location (`dtmc_conv_store_location`) | The store location for pickup type conversions. |

#### Item Data

| **Parameter** | **Description** |
| --- | --- |
| Item IDs | Array of item IDs in the transaction. |
| Item Prices | Array of item prices in the transaction. |
| Item Quantities | Array of item quantities in the transaction. |
| Item Discounts | Array of item discounts in the transaction. |
| Custom Query Parameters | Custom values to add as query string parameters to the base URL. |