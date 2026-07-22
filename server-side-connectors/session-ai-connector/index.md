---
title: Session AI Connector Setup Guide
description: This article describes how to set up the Session AI connector.
url: https://docs.tealium.com/server-side-connectors/session-ai-connector/
---
## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Update CCPA consent | ✓ | ✓ |
| Send Event | ✓ | ✓ |

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Host**  
 (Required) Select the host associated with your environment.
To point to the Session AI sandbox environment, use `https://csb.zineone.com`. To point to the production environment, use `https://cloud.zineone.com`.
* **API KEY**  
To generate an API key, create a channel in **Session AI > Integrations > Data Channel**.

## Actions

The following section lists the supported parameters for each action.

### Update CCPA consent

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Opt-In Action | Possible values:<ul><li>`true` - Select to make an opt-in request.</li><li>`false` - Select to make an opt-out request.</li></ul> |

#### User Identifier

| **Parameter** | **Description** |
| --- | --- |
| `id` | The unique ID of the customer profile. |
| `email` | The unique email ID of the customer. |
| `deviceId` | The unique device ID of the customer. |

### Send Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Data Channel | Channel used to send an event. |
| Event Name | Choose event name or enter custom name. |

#### Common Attributes

| **Parameter** | **Description** |
| --- | --- |
| `session_id `| (Required) The ID that uniquely identifies a session or visit. |
| `visitor_id `| (Required) The ID that identifies the user when not signed-in. |
| `customer_id` | The ID that identifies the user when signed-in. |
| `user_agent` | Browser user agent string, if available. |
| `device_channel` | (Required) The type of device, for example: desktop, tablet, mobile, or app. |
| `referrer_url` | (Required) The URL that refers to the previous page URL. For example, if the user first visits your site from a third-party website, this would be the third-party URL. If the user is in the middle of a session on your site, the previous page URL becomes the referrer URL for current page. |
| `campaign_info` | Campaign name or structure. For example, the `utm_campaign` value. |
| `os` | The operating system of the device. |
| `os_version` | The version of the operating system. |
| `platform_os` | The platform of the operating system. |
| `language` | The language of the device. |
| `tz` | The timezone of the device. |
| `devicetype` | The type of the device. |
| `browser` | The browser used on the device. |
| `browserversion` | The version of the browser used on the device. |
| `resolution` | The resolution of the display on the device. |

#### Event Attributes

| **Parameter** | **Description** |
| --- | --- |
| `logged_in` | (Required) Indicates whether the user is logged in.<br> Possible values: `Y`, `N`, or a mapped boolean type attribute.  |
| `pagename` | The page name where the event triggered. |
| `pagepath` | The page path where the event triggered. |
| `category` | The category of the product. |
| `product_id` | The ID of the product. |
| `price_sale` | The sale price of the product. |
| `price_orig` | The original price of the product. |
| `sku` | The SKU of the product. |
| `search_term` | The search term used to find the product. |
| `name` | The name of the product. |
| `price` | The price of the product. |
| `list_price` | The list price of the product. |
| `sort_field` | The property used for sorting. |
| `sort_order` | The sorting order. |
| Filter Attributes | This group contains information about the filters applied. |

#### Variant Attributes

| **Parameter** | **Description** |
| --- | --- |
| `color` | The color of the variant. |
| `brand` | The brand of the variant. |
| `size` | The size of the variant. |

#### Cart Attributes

| **Parameter** | **Description** |
| --- | --- |
| `quantity` | The quantity of the item in cart. |
| `product_id`| The ID of the product in cart. |
| `list_price`| The sale price of the item in cart. |
| `price` | The original price of the item in cart. |
| `sku` | The SKU of the item in cart. |
| `name` | The name of the product.|
| `category` | The category of the product. |
| `item_coupon_code` | The coupon code. |
| `item_coupon_value` | The value of the coupon. |
| `item_coupon_currency` | The currency in which the coupon value is expressed. |
| `item_coupon_type` | The type of the coupon. |
| `item_coupon_terms` | The terms and conditions of the coupon. |
| `item_coupon_method` | The method of the coupon. |
| `variant_color` | The color of the variant. |
| `variant_brand` | The brand of the variant. |
| `variant_size` | The size of the variant. |

#### Items Attributes

| **Parameter** | **Description** |
| --- | --- |
| `quantity` | The quantity of the item purchased. |
| `product_id` | The ID of the product purchased. |
| `list_price` | The original price of the item purchased. |
| `price` | The sale price of the item purchased. |
| `sku` | The SKU of the item purchased. |
| `name` | The name of the item purchased. |
| `category` | The category of the product. |
| `item_coupon_code` | The coupon code. |
| `item_coupon_value`| The value of the coupon. |
| `item_coupon_currency`| The currency in which the coupon value is expressed. |
| `item_coupon_type `| The type of the coupon. |
| `item_coupon_terms `| The terms and conditions of the coupon. |
| `item_coupon_method` | The method of the coupon. |
| `variant_color `| The color of the variant. |
| `variant_brand` | The brand of the variant. |
| `variant_size`| The size of the variant. |

#### Purchase Attributes

| **Parameter** | **Description** |
| --- | --- |
| `order_id` | The ID of the order. |
| `order_total` | The total amount paid for the order. |
| `discount` | The discount applied to the order. |
| `taxes` | The taxes applied to the order. |
| `shipping` | The shipping cost for the order. |
| `item_total` | The total number of items in the order. |
| `referred_id` | The ID of the referrer. |

#### Purchase Coupons Attributes

| **Parameter** | **Description** |
| --- | --- |
| `code` | The coupon code. |
| `value` | The value of the coupon. |
| `currency` | The currency in which the coupon value is expressed. |
| `type` | The type of the coupon. |
| `terms` | The terms and conditions of the coupon. |
| `method` | The method of the coupon. |
| Custom Event Attributes | Map optional custom attributes. |
| Custom Event Attributes Template Variables | Use template names to create more complex data structures and provide template variables as data input.<ul><li>Name nested template variables with the dot notation. For example, `items.name`.</li><li>Nested template variables are typically built from data layer list attributes.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li></ul> |
| Custom Event Attributes Templates | Provide templates to be referenced in **Custom Event Attributes**.<ul><li>Templates are injected by name with double curly braces into supported fields. For example `{{SomeTemplateName}}`.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li></ul> |