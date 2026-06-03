---
title: Zanox Tag Setup Guide
description: This article describes how to set up Zanox in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/zanox-tag/
---## Requirements

* Zanox Account


## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Title**: (Required) Enter a descriptive title to identify the Tag instance.
* **Tag Type**: (Required) From the drop-down list, choose the type of Tag you want to load.
  * Master Tag: This will load the MasterTag code provided to advertisers by Zanox.
  * PPS: Stands for Pay-per-Sale. This will load the PPS tracking pixel.
  * PPL: Stands for Pay-per-Lead. This will load the PPL tracking pixel.
* **PPS/PPL ID**: Enter the Tag identifier in this field if you select the PPS/PPL Tag Type. The id appears at the end of the tracking pixel provided by Zanox. If you select the MasterTag Type, leave this field blank. Example: The alphanumeric value at the end of this URL, //ad.zanox.com/ppl/?2173D3211067525 is your PPL ID.
* **Default zx\_class**: (Optional) Enter the value of the class attribute (excluding the &#39;zx&#39; prefix&#39;) in this field if you select the MasterTag Type. If you prefer to populate this field dynamically, you must map to the div container class id in the Mapping toolbox (see [Setting up Mappings](#mappings)) Example: 48EFE82D8GE72DE1BBE2

 Zanox recommends loading only one instance of MasterTag on a page. Do not use an iFrame to load MasterTag unless it renders all the parameters properly.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

**Best Practices**:

* For MasterTag, select the default &#34;Load on All Pages&#34; rule.
* For PPS Tag Type, set up Load Rules to load the Tag on order confirmation pages like the Thank You or Receipt page.
* For PPL Tag Type, set up load rule conditions to load the Tag on the Registration page.

## Data mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag. The destination variables for this Tag are available in the Mapping toolbox. For ease of use, the variables are grouped into different categories: Standard and MasterTag.

 This tag requires that the [E-Commerce Extension]() be configured beforehand. Setting up the appropriate Order and Product Variables (`_corder`, `_ccurrency`, `_cprod`, `_cprice`, and `_cquan`) makes it possible for the Extension to automatically map their values to the corresponding destinations. 

### Standard Tab

Map to the destination variable(s) in this tab if using the PPS or the PPL Tag.

| Parameter | Description |
|---|---|
| Category ID | The identifier of the category to which the Lead or the Sale belongs. |
| Customer ID | The customer&#39;s unique identifier. |
| Order ID | The order identifier. |
| SubOrder ID | The identifier for additional information about the order. |
| Currency Symbol | The currency applicable to the product. Example: USD for US dollars. |
| Total Price | The total value of the products in the order. |
| Commission Fix | The fixed commission applicable to the order. |
| Commission Percent | The percentage of commission based on the total price. |
| Session ID | The identifier of the session during which the transaction occurred. |
| Partner ID | The partner identifier value assigned by Zanox. |
| Review Note | Comments or individual remarks for the order |
| Maturity Date | The date-of-confirmation for the order. |

### MasterTag Tab

Map to the destination variable(s) in this tab if using the MasterTag.

| Parameter | Description |
|---|---|
| zx_class (div container class id) | The identifier of the div container. |
| zx_identifier | The product identifier. |
| zx_fn | The product name. |
| zx_brand | The brand name of the product. |
| zx_category | The category to which the product belongs. |
| zx_amount | The product price as a numerical value Example: 2.99. |
| zx_price | The product price together with the currency symbol Example: 2.99$ |
| zx_currency | The currency applicable to the order Example: USD |
| zx_description | The product description. |
| zx_url | The URL of the product&#39;s page. |
| zx_photo | The URL of the product&#39;s image. |
| zx_search_query | The search term/text. |


## Vendor documentation

* [FAQs for Advertisers](http://www.zanox.com/gb/advertisers/faq/)
* [Glossary Terms](http://wiki.zanox.com/en/Acronyms_and_Terms)
* [Support and Documentation (for Advertisers)](http://www.zanox.com/gb/advertisers/how-to-start/help/)

