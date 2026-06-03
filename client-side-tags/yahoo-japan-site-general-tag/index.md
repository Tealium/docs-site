---
title: Yahoo! Japan Site General Tag Setup Guide
description: This article describes how to set up the Yahoo! Japan Site General Tag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/yahoo-japan-site-general-tag/
---

## Tag tips

* **IMPORTANT:** To trigger a particular tag, set up the trigger condition in the **Tag Types** tab in the mapping toolbox. Otherwise, no tags will be triggered.
* Use mappings to override the standard configurations.
* You may enter more than one ID or Label in a comma-separated list. If you enter one ID and multiple Labels, you will trigger one call for each Label, each using the same ID. If you enter multiple IDs and a single Label, you will trigger a call for each ID, each using the same Label. If you enter multiple IDs and Labels for a single tag type, make certain the numbers of IDs and Labels match.
* Supports these E-Commerce extension values:
  * Order ID (`_corder)`
  * Order Subtotal (`_csubtotal`)
  * List of Product IDs (`_cprod`)
  * List of Product Categories (`_ccat`)
  * List of Product Quantities (`_cquan`)
  * List of Product Prices (`_cprice`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Auto Tagging**: Enable or disable auto tagging. Enabling this setting performs the `ytag({&#34;type&#34;:&#34;ycl_cookie&#34;});` call after the tag loads.
* **Display Network Conversion IO**: Enter your Yahoo! Japan Display Network (YDN) Conversion IO.
* **Display Network Conversion Label**: Enter your Yahoo! Japan Display Network (YDN) Conversion Label.
* **Display Network Retargeting ID**: Enter your Yahoo! Japan Display Network (YDN) Retargeting ID.
* **Display Network Retargeting Label**: Enter your Yahoo! Japan Display Network (YDN) Retargeting Label.
* **Sponsored Search Conversion ID**: Enter your Yahoo! Japan Sponsored Search (YSS) Conversion ID.
* **Sponsored Search Conversion Label**: Enter your Yahoo! Japan Sponsored Search (YSS) Conversion Label.
* **Sponsored Search Retargeting ID**: Enter your Yahoo! Japan Sponsored Search (YSS) Retargeting ID.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

To fire any tags, you must set up the trigger condition in the **Tag Type** category.

The available categories are:

### Display Network (YDN) Conversion

|Variable| Description|
|---| ---|
|Conversion IO (`yahoo_ydn_conv_io`)| [String]|
|Conversion Label (`yahoo_ydn_conv_label`)| [String]|
|Conversion Transaction ID (`yahoo_ydn_conv_transaction_id`)| [String]|
|Conversion Value (`yahoo_ydn_conv_value`)| [String]|

### Display Network (YDN) Retargeting

|Variable| Description|
|---| ---|
|Retargeting ID (`yahoo_retargeting_id`)| [String]|
|Retargeting Label (`yahoo_retargeting_label`)| [String]|
|Retargeting Page Type (`yahoo_retargeting_page_type`)| [String]|
|Retargeting Items (`yahoo_retargeting_items`)| [Array]|
|Category ID (`category_id`) (Overrides `_ccat`)| [Array]|
|Item ID (`item_id`) (Overrides `_cprod`)| [Array]|
|Price (`price`) (Overrides `_cprice`)| [Array]|
|Quantity (`quantity`) (Overrides `_cquan`)| [Array]|

### Sponsored Search (YSS) Conversion

|Variable| Description|
|---| ---|
|Conversion ID (`yahoo_conversion_id`)| [String]|
|Conversion Label (`yahoo_conversion_label`)| [String]|
|Conversion Value (`yahoo_conversion_value`)| [String]|

### Sponsored Search (YSS) Retargeting

|Variable| Description|
|---| ---|
|Retargeting ID (`yahoo_ss_retargeting_id`)| [String]|
|Custom Params| (`yahoo_sstag_custom_params`)|

### E-Commerce

|Variable| Description|
|---| ---|
|Order ID (`order_id`) (Overrides `_corder`)| [String]|
|Sub Total (`order_subtotal`) (Overrides `_csubtotal`)| [String]|
|List of Product Categories (`product_category`) (Overrides `_ccat`)| [Array]|
|List of Product IDs (`product_id`) (Overrides `_cprod`)| [Array]|
|List of Product Quantities (`product_quantity`) (Overrides `_cquan`)| [Array]|
|List of Product Prices (`product_unit_price`) (Overrides `_cprice`)| [Array]|

### Tag Types

|Variable| Description|
|---| ---|
|Display Network Conversion| `yjad_conversion`|
|Display Network Retargeting| `yjad_retargeting`|
|Sponsored Search Conversion| `yss_conversion`|
|Sponsored Search Retargeting| `yss_retargeting`|
|Custom| Custom|

### Type-Specific Parameters

|Variable| Description|
|---| ---|
|Conversion IO (`yahoo_ydn_conv_io`)| `yahoo_ydn_conv_io`|
|Conversion Label (`yahoo_ydn_conv_label`)| `yahoo_ydn_conv_label`|
|Conversion Transaction ID (`yahoo_ydn_conv_transaction_id`)| `yahoo_ydn_conv_transaction_id`|
|Conversion Value (`yahoo_ydn_conv_value`)| `yahoo_ydn_conv_value`|
|Retargeting ID (`yahoo_retargeting_id`)| `yahoo_retargeting_id`|
|Retargeting Label (`yahoo_retargeting_label`)| `yahoo_retargeting_label`|
|Retargeting Page Type (`yahoo_retargeting_page_type`)| `yahoo_retargeting_page_type`|
|Retargeting Items (`yahoo_retargeting_items`)| `yahoo_retargeting_items`|
|Item ID (`item_id`)| `item_id`|
|Category ID (`category_id`)| `category_id`|
|Price (`price`)| `price`|
|Quantity (`quantity`)| `quantity`|
|Conversion ID (`yahoo_conversion_id`)| `yahoo_conversion_id`|
|Conversion Label (`yahoo_conversion_label`)| `yahoo_conversion_label`|
|Conversion Value (`yahoo_conversion_value`)| `yahoo_conversion_value`|
|Retargeting ID (`yahoo_ss_retargeting_id`)| `yahoo_ss_retargeting_id`|
|Custom Parameters (`yahoo_sstag_custom_params`)| `yahoo_sstag_custom_params`|
|Custom Parameter| `Custom_Parameter`|
|Display Network (YDN) Conversion| `yjad_conversion`|
|Display Network (YDN) Retargeting| `yjad_retargeting`|
|Sponsored Search (YSS) Conversion| `yss_conversion`|
|Sponsored Search (YSS) Retargeting| `yss_retargeting`|
|Custom Tag Type| `Custom_Type`|

## Use cases

### Trigger YDN Retargeting on every page that matches load rules

To set up a tag which fires on every page according to load rules:

1. On the **Tag Configuration** tab, enter the appropriate value for the **Display Network Retargeting ID** box.
1. Set **Auto Tagging** to **True**. This will trigger the `ytag({&#34;type&#34;:&#34;ycl_cookie&#34;});` call.
1. Set up your load rules as needed.
1. On the **Data Mappings** tab in the **Variables** dropdown, click **Use Custom Value**.
1. In the upper-left section of the dialog, enter **true** in the box.
1. In the **Category** section, select **Tag Types**.
1. In the **When mapped variables equals** box, enter **true**.
1. In the **Trigger tag type** dropdown, select **Display Network Retargeting**.
1. Click **&#43;Add**.
1. Click **Done**.
1. Click **Apply**.

![](/images/client-side-tags/screen-shot-2022-07-06-at-13.35.19.png)

### Trigger YDB Conversion on a purchase event while retargeting on other pages

To set up a YDN Conversion tag which fires on a page with a `tealium_event` variable value of `purchase` and a Retargeting tag on every other page according to load rules:

1. Set up your Retargeting tag as described in the Trigger YDN Retargeting on every page that matches load rules section above.
1. On the **Tag Configuration** tab, enter the appropriate values for the **Display Network Conversion IO** and **Conversion Label** boxes.
1. On the **Data Mappings** tab in the **Variables** dropdown, select `tealium_event`.
1. Click **&#43;Select Destination**.
1. In the **Category** section, select **Tag Types**.
1. In the **When mapped variables equals** box, enter `purchase`.
1. In the **Trigger tag type** dropdown, select **Display Network Conversion**.
1. Click **&#43;Add**.
1. Repeat steps 3 through 8 for similar mappings, such as **Conversion Transaction ID** and **Conversion Value**, by **Selecting Display Network (YDN) Conversion** from the **Category** section.
1. To fire the conversion on multiple pages, either repeat these steps or create a vendor-specific variable (for example: `yahoo_conversion_value`), which can be dynamically assigned by extensions.
1. Click **Done**.
1. Click **Apply**.

![](/images/client-side-tags/screen-shot-2022-07-06-at-13.42.31.png)

Trigger YDB Conversion on a specific page&#39;s URL while retargeting on other pages

To set up a YDN Conversion tag which fires on a specific page&#39;s URL (for example: `/cart/thankyou`) and a Retargeting tag on every other page according to load rules:

1. Set up your Retargeting tag as described in the Trigger YDN Retargeting on every page that matches load rules section above.
1. On the **Tag Configuration** tab, enter the appropriate values for the **Display Network Conversion IO** and **Conversion Label** boxes.
1. On the **Data Mappings** tab in the **Variables** dropdown, select **Custom Value**.
1. Click **&#43;Select Destination**.
1. In the **Category** section, select **Tag Types**.
1. In the **When mapped variables equals** box, enter the path to the page where your version should be triggered (for example: `/cart/thankyou`).
1. In the **Trigger tag type** dropdown, select **Display Network Conversion**.
1. Click **&#43;Add**.
1. Repeat steps 3 through 8 for similar mappings, such as **Conversion Transaction ID** and **Conversion Value**, by **Selecting Display Network (YDN) Conversion** from the **Category** section.
1. To fire the conversion on multiple pages, either repeat these steps or create a vendor-specific variable (for example: `yahoo_conversion_value`), which can be dynamically assigned by extensions.
1. Click **Done**.
1. Click **Apply**.

![](/images/client-side-tags/screen-shot-2022-07-06-at-13.43.38.png)
