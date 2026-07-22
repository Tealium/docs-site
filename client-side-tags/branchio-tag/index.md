---
title: Branch.io Tag
description: This article describes how to set up the Branch.io tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/branchio-tag/
---

Branch provides the leading mobile linking platform, with solutions that unify user experience and measurement across different devices, platforms, and channels.

## Tag Configuration

First, go to the tag marketplace and add the Branch.io tag (learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Branch key**: Your Branch live key, or (deprecated) your app ID.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Initial

| Variable                                            | Description |
|:----------------------------------------------------|:------------|
| Branch key                                          |             |
| Branch View ID (`branch_view_id`)                   | [String]    |
| Branch Match ID (`branch_match_id`)                 | [String]    |
| No Journeys (`no_journeys`)                         | [Boolean]   |
| Disable Entry Animation (`disable_entry_animation`) | [Boolean]   |
| Disable Exit Animation (`disable_exit_animation`)   | [Boolean]   |
| Retries (`retries`)                                 | [Integer]   |
| Retry Delay (`retry_delay`)                         | [Integer]   |
| Timeout (`timeout`)                                 | [Integer]   |
| Metadata (`metadata`)                               | [Object]    |
| Nonce (`nonce`)                                     | [String]    |
| Tracking Disabled (`tracking_disabled`)             | [Boolean]   |

### Metadata

| Variable                                       | Description |
|:-----------------------------------------------|:------------|
| Transaction Id (`transaction_id`)              | [String]    |
| Currency (`currency`) (Overrides `_ccurrency`) | [String]    |
| Revenue (`revenue`) (Overrides `_ctotal`)      | [String]    |
| Shipping (`shipping`) (Overrides `_cship`)     | [String]    |
| Tax (`tax`) (Overrides `_ctax`)                | [String]    |
| Coupon (`coupon`) (Overrides `_cpromo`)        | [Number]    |
| Affiliation (`affiliation`)                    | [Number]    |
| Description (`description`)                    | [Array]     |
| Purchase loc (`purchase_loc`)                  | [String]    |
| Store pickup (`store_pickup`)                  | [Object]    |
| Registration Id (`registration_id`)            | [Object]    |
| Customer Event Alias (`customer_event_alias`)  | [String]    |

### E-Commerce

| Variable                                                            | Description     |
|:--------------------------------------------------------------------|:----------------|
| Content Schema (`$content_schema`)                                  | [String]        |
| Og Title (`$og_title`)                                              | [String]        |
| Og Description (`$og_description`)                                  | [String]        |
| Og Image Url (`$og_image_url`)                                      | [String]        |
| Canonical Identifier (`$canonical_identifier`) (Overrides `_cprod`) | [String]        |
| Publicly Indexable (`$publicly_indexable`)                          | [Boolean]       |
| Price (`$price`) (Overrides `_cprice`)                              | [Number, Array] |
| Locally Indexable (`$locally_indexable`)                            | [Boolean]       |
| Quantity (`$quantity`) (Overrides `_cquan`)                         | [Number, Array] |
| Sku (`$sku`) (Overrides `_csku`)                                    | [String, Array] |
| Product Name (`$product_name`) (Overrides `_cprodname`)             | [String, Array] |
| Product Brand (`$product_brand`) (Overrides `_cbrand`)              | [String, Array] |
| Product Category (`$product_category`) (Overrides `_ccat`)          | [String, Array] |
| Product Variant (`$product_variant`)                                | [String]        |
| Rating Average (`$rating_average`)                                  | [Number]        |
| Rating Count (`$rating_count`)                                      | [Number]        |
| Rating Max (`$rating_max`)                                          | [Number]        |
| Creation Timestamp (`$creation_timestamp`)                          | [Number]        |
| Exp Date (`$exp_date`)                                              | [String]        |
| Keywords (`$keywords`)                                              | [Array]         |
| Address Street (`$address_street`)                                  | [String]        |
| Address City (`$address_city`) (Overrides `_ccity`)                 | [String]        |
| Address Region (`$address_region`) (Overrides `_cstate`)            | [String]        |
| Address Country (`$address_country`) (Overrides `_ccountry`)        | [String]        |
| Address Postal Code (`$address_postal_code`) (Overrides `_czip`)    | [String]        |
| Latitude (`$latitude`)                                              | [Number]        |
| Longitude (`$longitude`)                                            | [Number]        |
| Image Captions (`$image_captions`)                                  | [Array]         |
| Condition (`$condition`)                                            | [String]        |
| Custom fields (`$custom_fields`)                                    | [Object]        |

### Events

| Variable              | Description             |
|:----------------------|:------------------------|
| Add To Cart           | `add_to_cart`           |
| Add To Wishlist       | `add_to_wishlist`       |
| View Cart             | `view_cart`             |
| Initiate Purchase     | `initiate_purchase`     |
| Add Payment Info      | `add_payment_info`      |
| Click Ad              | `click_ad`              |
| Purchase              | `purchase`              |
| Reserve               | `reserve`               |
| Spend Credits         | `spend_credits`         |
| View Ad               | `view_ad`               |
| Search                | `search`                |
| View Item             | `view_item`             |
| View Items            | `view_items`            |
| Rate                  | `rate`                  |
| Share                 | `share`                 |
| Initiate Stream       | `initiate_stream`       |
| Complete Stream       | `complete_stream`       |
| Complete Registration | `complete_registration` |
| Complete Tutorial     | `complete_tutorial`     |
| Achieve Level         | `achieve_level`         |
| Unlock Achievement    | `unlock_achievement`    |
| Invite                | `invite`                |
| Login                 | `login`                 |
| Start Trial           | `start_trial`           |
| Subscribe             | `subscribe`             |
| Custom                | `custom`                |

### Event Parameters

| Variable              | Description             |
|:----------------------|:------------------------|
| Add To Cart           | `add_to_cart`           |
| Add To Wishlist       | `add_to_wishlist`       |
| View Cart             | `view_cart`             |
| Initiate Purchase     | `initiate_purchase`     |
| Add Payment Info      | `add_payment_info`      |
| Click Ad              | `click_ad`              |
| Purchase              | `purchase`              |
| Reserve               | `reserve`               |
| Spend Credits         | `spend_credits`         |
| View Ad               | `view_ad`               |
| Search                | `search`                |
| View Item             | `view_item`             |
| View Items            | `view_items`            |
| Rate                  | `rate`                  |
| Share                 | `share`                 |
| Initiate Stream       | `initiate_stream`       |
| Complete Stream       | `complete_stream`       |
| Complete Registration | `complete_registration` |
| Complete Tutorial     | `complete_tutorial`     |
| Achieve Level         | `achieve_level`         |
| Unlock Achievement    | `unlock_achievement`    |
| Invite                | `invite`                |
| Login                 | `login`                 |
| Start Trial           | `start_Trial`           |
| Subscribe             | `subscribe`             |
| Custom                | `custom`                |
