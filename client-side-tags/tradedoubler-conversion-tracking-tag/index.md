---
title: TradeDoubler Conversion Tracking Tag Setup Guide
description: This article describes how to set up the TradeDoubler Conversion Tracking tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/tradedoubler-conversion-tracking-tag/
---
## Migrating from the legacy Trackback tag


<blockquote>
The Trackback Tag is now deprecated in favor of the new Conversion Tracking version and no longer offered in the tag marketplace. Be sure to deactivate any Trackback Tag instances before adding the new Conversion Tracking Tag.
</blockquote>


## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

After adding the tag, configure the following settings:

* **Tag Type**: (Required) Choose the type of tag you want to load.
  * `Sale`: Loads the Sales tracking pixel hosted on `tbs.tradedoubler.com`.
  * `Lead`: Loads the Leads tracking pixel hosted on `tbl.tradedoubler.com`.
  * `Product`: Loads the product level tracking pixel.

* **Organization ID**: (Required) The numeric organization ID provided by TradeDoubler. This field applies only if **Tag Type** is set to `Sale` or `Lead`.
* **Event ID**: (Required) The numeric identifier assigned to the sale/lead event you want to track. This field applies only if **Tag Type** is set to `Sale` or `Lead`. If you prefer to set this value through data mappings, you must leave this field blank.
* **Tracking Consent**: Enable or disable tracking consent. Use mappings to override this field, including the mode

## Load rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this Tag. The **Load on All Pages** rule is the default Rule. If you prefer to load this Tag on a specific page, create a new rule with the relevant conditions.

### Best practices

* Place the sale tag on the confirmation page, one that appears post completion of a sale.
* Place the lead tag on pages that allow site visitors to sign-up or register.
* Place the product tag on a page where you want to track visitor interactions with products and product categories.

## Data mappings

Mapping is the process of sending data from a [Data Layer Variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a Variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The destination variables for the Tradedoubler Conversion Tracking Tag are built into its Data Mapping tab.

### Standard

| Variable           | Type                | Description                             |
|:-------------------|:--------------------|:----------------------------------------|
| `tracking_consent` | Boolean             | Whether the visitor has given tracking consent. |
| `organization`     | String              | Organization ID.                        |
| `programId`        | String              | Program ID.                             |
| `tdevent`          | String              | Event ID.                               |
| `tagtype`          | String              | Tag type.                               |
| `tduid`            | String              | Tradedoubler unique tracking ID.        |
| `chksum`           | String              | Checksum.                               |
| `extid`            | String              | Email address using SHA-256 hash.       |
| `exttype`          | Integer             | ID type. Possible values are `0` or `1`.|
| `voucher`          | String              | Voucher code.                           |
| `validOn`          | String              | Valid on. Uses `YYYY-MM-DD` format      |
| `validOn`          | String              | Validation date in `YYYY-MM-DD` format. |
| `cdt`              | String              | Parent of `extid` and `exttype`.        |
| `cdt`              | String              | TradeDoubler-specific field used with `extid` and `exttype`. Use the exact value and format provided in your TradeDoubler implementation. |
| `fallback_url`     | String              | Fallback URL.                           |
| `program`          | Boolean             | Whether the conversion tracking tag is associated with a specific affiliate program. |

### E-commerce

Because the Tradedoubler Conversion Tracking Tag is e-commerce enabled, it will automatically use the default [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) mappings. Manually mapping in this category is generally not needed unless:

* You want to override any extension mappings.
* An e-commerce variable you want is not offered in the extension.

| Variable             | Type    | Description                                 |
|:---------------------|:--------|:--------------------------------------------|
| `order_id`           | String  | Order ID (overrides `_corder`).             |
| `order_subtotal`     | Number  | Subtotal (overrides `_csubtotal`).           |
| `order_currency`     | String  | Currency (overrides `_ccurrency`).           |
| `order_promo_code`   | String  | Promo code (overrides `_cpromo`).            |
| `product_id`         | Array   | List of product IDs (overrides `_cprod`).    |
| `product_sku`        | Array   | List of SKUs (overrides `_csku`).            |
| `product_quantity`   | Array   | List of quantities (overrides `_cquan`).     |
| `product_unit_price` | Array   | List of prices (overrides `_cprice`).        |
| `gr`                 | Array   | List of product group IDs.                   |

## Vendor documentation

* [TradeDoubler: Conversion Tracking](http://dev.tradedoubler.com/tracking/advertiser/)
* [TradeDoubler: Developer Resources](http://dev.tradedoubler.com/)
