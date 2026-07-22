---
title: Branch Mobile Remote Command Tag Setup Guide
description: This article describes how to set up the Branch Mobile Remote Command tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/branch-mobile-remote-command-tag/
---
Branch provides the leading mobile linking platform, with solutions that unify user experience and measurement across different devices, platforms, and channels.

## Tag Tips

* Use mappings to:
  * Override standard configuration values and set custom parameters
  * Trigger standard and custom events

* Supports the following E-Commerce extension values:
  * Currency (`_ccurrency`)
  * Customer ID (`_ccustid`)
  * Promo Code (`_cpromo`)
  * List of Brands (`_cbrand`)
  * List of Categories (`_ccat`)
  * List of SKUs (`_csku`)
  * List of Names (`_cprodname`)
  * List of Categories 2 (`_ccat2`)
  * List of Prices (`_cprice`)
  * List of Quantities (`_cquan`)
  * Tax Amount (`_ctax`)

* This is a Mobile Remote Command companion tag for the native mobile app SDK.

## Tag Configuration

First, go to the tag marketplace and add the Branch Mobile Remote Command tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Branch Key:**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Link

| Variable                                       | Description |
|:-----------------------------------------------|:------------|
| Channel (`link.channel`)                       | [String]    |
| Feature (`link.feature`)                       | [String]    |
| Campaign (`link.campaign`)                     | [String]    |
| Stage (`link.stage`)                           | [String]    |
| Duration (`link.duration`)                     | [String]    |
| Control parameters (`link.control_parameters`) | [String]    |

### Settings

| Variable                                         | Description |
|:-------------------------------------------------|:------------|
| Branch Key (`dev_key`)                           | [String]    |
| Enable Logging (`settings.enable_logging`)       | [Boolean]   |
| Collect Device Id (`settings.collect_device_id`) | [Boolean]   |

### Event

| Variable                                                  | Description |
|:----------------------------------------------------------|:------------|
| Tealium Event (`event.description`)                       | [String]    |
| Customer Id (`event.user_id`) (Overrides `_ccustid`)      | [String]    |
| Product Quantity (`event.quantity`) (Overrides `_cquan`)  | [String]    |
| Currency Type (`event.currency`) (Overrides `_ccurrency`) | [String]    |
| Order Tax (`event.tax`) (Overrides `_ctax`)               | [Number]    |
| Revenue (`event.revenue`)                                 | [Number]    |
| Search Query (`event.search_query`)                       | [String]    |

### Buo

| Variable                                | Description |
|:----------------------------------------|:------------|
| Title (`buo.title`)                       | [String]    |
| Description (`buo.description`)           | [String]    |
| Item Id (`buo.canonical_identifier`)      | [String]    |
| Item Url (`buo.canonical_url`)            | [String]    |
| Image Url (`buo.image_url`)               | [String]    |
| Content Metadata (`buo.content_metadata`) | [String]    |

### Metadata

| Variable                                                       | Description |
|:---------------------------------------------------------------|:------------|
| Latitude (`metadata.latitude`)                                   | [Number]    |
| Longitude (`metadata.longitude`)                                 | [Number]    |
| Currency Code (`metadata.currency_type`) (Overrides `_ccurrency`)  | [String]    |
| Coupon (`metadata.coupon`) (Overrides `_cpromo`)                   | [String]    |
| Product Brand (`metadata.product_brand`) (Overrides `_cbrand`)     | [String]    |
| Product Category (`metadata.product_category`) (Overrides `_ccat`) | [String]    |
| Product Id (`metadata.sku`) (Overrides `_csku`)                    | [String]    |
| Product Name (`metadata.product_name`) (Overrides `_cprodname`)    | [String]    |
| Product Variant (`metadata.product_variant`) (Overrides `_cprice`) | [String]    |
| Product Unit Price (`metadata.price`) (Overrides `_ccustid`)      | [Number]    |

### Events

| Variable                                     | Description          |
|:---------------------------------------------|:---------------------|
| Initialize (`initialize`)                      | initialize           |
| Set User Id (`setuserid`)                      | setuserid            |
| Logout (`logout`)                              | logout               |
| Create Deep Link (`createdeeplink`)            | createdeeplink       |
| Achieve Level (`achievelevel`)                 | achievelevel         |
| Add Payment Info (`addpaymentinfo`)            | addpaymentinfo       |
| Add to Cart (`addtocart`)                      | addtocart            |
| Add to Wish List (`addtowishlist`)             | addtowishlist        |
| Tutorial Complete (`completetutorial`)         | completetutorial     |
| Ad Click (`clickad`)                           | clickad              |
| Complete Registration (`completeregistration`) | completeregistration |
| Complete Stream (`completestream`)             | completestream       |
| Initiate Purchase (`initiatepurchase`)         | initiatepurchase     |
| Initiate Stream (`initiatestream`)             | initiatestream       |
| Invite (`invite`)                              | invite               |
| Login (`login`)                                | login                |
| Purchase (`purchase`)                          | purchase             |
| Rate (`rate`)                                  | rate                 |
| Reserve (`reserve`)                            | reserve              |
| Search (`search`)                              | search               |
| Share (`share`)                                | share                |
| Spend Credits (`spendcredits`)                 | spendcredits         |
| Start Trial (`starttrial`)                     | starttrial           |
| Subscribe (`subscribe`)                        | subscribe            |
| Unlock Achievement (`unlockachievement`)       | unlockachievement    |
| View Ad (`viewad`)                             | viewad               |
| View Cart (`viewcart`)                         | viewcart             |
| View Item (`viewitem`)                         | viewitem             |
| View Items (`viewitems`)                       | viewitems            |
| Custom                                       | custom               |

### Event Parameters

| Variable                                     | Description          |
|:---------------------------------------------|:---------------------|
| Initialize (`initialize`)                      | initialize           |
| Set User Id (`setuserid`)                      | setuserid            |
| Logout (`logout`)                              | logout               |
| Create Deep Link (`createdeeplink`)            | createdeeplink       |
| Achieve Level (`achievelevel`)                 | achievelevel         |
| Add Payment Info (`addpaymentinfo`)            | addpaymentinfo       |
| Add to Cart (`addtocart`)                      | addtocart            |
| Add to Wish List (`addtowishlist`)             | addtowishlist        |
| Tutorial Complete (`completetutorial`)         | completetutorial     |
| Ad Click (`clickad`)                           | clickad              |
| Complete Registration (`completeregistration`) | completeregistration |
| Complete Stream (`completestream`)             | completestream       |
| Initiate Purchase (`initiatepurchase`)         | initiatepurchase     |
| Initiate Stream (`initiatestream`)             | initiatestream       |
| Invite (`invite`)                              | invite               |
| Login (`login`)                                | login                |
| Purchase (`purchase`)                          | purchase             |
| Rate (`rate`)                                  | rate                 |
| Reserve (`reserve`)                            | reserve              |
| Search (`search`)                              | search               |
| Share (`share`)                                | share                |
| Spend Credits (`spendcredits`)                 | spendcredits         |
| Start Trial (`starttrial`)                     | starttrial           |
| Subscribe (`subscribe`)                        | subscribe            |
| Unlock Achievement (`unlockachievement`)       | unlockachievement    |
| View Ad (`viewad`)                             | viewad               |
| View Cart (`viewcart`)                         | viewcart             |
| View Item (`viewitem`)                         | viewitem             |
| View Items (`viewitems`)                       | viewitems            |
| Custom                                       | custom               |
