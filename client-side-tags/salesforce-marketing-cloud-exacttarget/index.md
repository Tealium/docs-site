---
title: Salesforce Marketing Cloud (ExactTarget) tag setup guide
description: This article describes how to set up the Salesforce Marketing Cloud (ExactTarget) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/salesforce-marketing-cloud-exacttarget/
---
Salesforce Marketing Cloud (formerly ExactTarget) is the platform for 1:1 customer journeys, connecting companies with customers in whole new ways.

## Tag tips

* Supports these E-Commerce extension parameters:
    * Order ID
    * List of Product IDs
    * List of Prices
* Add this tag to your landing pages and your conversion page.
* Automatically stores visitor information in a cookie and sends it on the confirmation page.
* Use mapping to dynamically override the standard config values or the E-Commerce extension values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Account**: ExactTarget member ID. Should match `mid = param` in landing page query string.
* **Conversion Page ID**: A unique number used to differentiate multiple conversion pages.
* **Conversion Page Alias**: The name to be displayed in ExactTarget for this conversion page.
* **Conversion Page Order**: A number that represents the order in which the conversion pages will be displayed in ExactTarget.
* **Use S4**: Default is **No**. Set to **Yes** to use the pixel location `click.s4.exacttarget.com` instead of `click.exacttarget.com`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
|  `account` |Account ID  |
|  `convid` |Conversion Link ID  |
|  `alias` |Link Alias  |
|  `displayorder` |Display Order  |
|   `s4` |Use S4 |

### E-Commerce

| Variable | Description |
|:---------|:------------|
|  `order_id` (Overrides `_corder`) |Order ID  |
| `product_id` (Overrides `_cprod`)  | List of Product IDs  |
|  `product_unit_price` (Overrides `_cprice`)  | List of Prices |

