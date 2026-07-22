---
title: Extole Tag Setup Guide
description: This article describes how to set up the Extole tag.
url: https://docs.tealium.com/client-side-tags/extole-tag/
---
Extole's platform powers rich, cross-channel referral programs for the world's biggest brands. With all the capabilities to market, measure, and optimize large-scale refer-a-friend, the Extole platform helps marketers turn the love existing customers have for your brand into new customers.

## Tag tips

* Select a method to use for identifying where the CTAs are placed.
  * For **Element ID**: Provide the element ID without the hash (`#`) character.
  * For **HTML Element**: Provide an element selector to query. This option requires loading jQuery on the page.
* Use event mapping to trigger the registration event. The conversion event fires automatically when an Order ID is detected.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Client Name**: Your unique Extole client name.
* **Target Content Method**: Select the method used to identify CTA placement.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `client_name` | Client Name  |
| `registration.custom` | Registration Custom Data  |
| `conversion.custom` | Conversion Custom Data  | 


<blockquote>
Replace `custom` with your variable name, for instance `registration.date`.
</blockquote>


### E-Commerce

Because the Extole tag is e-commerce enabled, it automatically uses the default E-Commerce Extension mappings. Manually mapping in this category is generally not needed unless:

* You want to override any Extension mappings.
* The e-commerce variable you need for your use case is not available in the extension.

| Variable | Description |
|:---------|:------------|
| `order_id` (Overrides `_corder`) |Order ID  |
| `order_total` (Overrides `_ctotal`) | Order total  |
| `customer_id` (Overrides `_ccustid`) | Customer ID  |
| `cart_value` (Overrides `_ctotal`) | Cart value  | 
| `coupon_code` (Overrides `_cpromo`) | Coupon code  | 

### Calls-To-Action

| Variable | Description |
|:---------|:------------|
|  `email` | Email  |
|  `first_name` | First name  |
|  `last_name` | Last name  |
|  `locale` | Locale  |
|  `cta.global_header.id` | Global header  |
|  `cta.global_footer.id` | Global footer  |
|  `cta.product.id` | Product  |
|  `cta.product.data.content.custom` | Product custom data  |
|  `cta.confirmation.id` | Confirmation  |
|  `cta.referral_page.id` | Referral page  |
|  `cta.my_account.id` | Account page  |
|  `cta.custom.id` | Custom CTA name |
|  `cta.CTAname.data.first_name` | Add CTA first name  |
|  `cta.CTAname.data.last_name` | Add CTA last name  |
|  `cta.CTAname.data.partner_user_id` | Add CTA partner user ID  |
|  `cta.CTAname.data.email` | Add CTA email  |
|  `cta.CTAname.data.locale` | Add CTA locale  |
|  `cta.CTAname.data.custom` | Add CTA custom data  |
|  `cta.overlay` | Overlay  |
|  `cta.mobile_menu` | Mobile menu  |


<blockquote>
If you are not mapping an element ID or selector, map the string `n/a`.
</blockquote>


#### Standard CTA Names

|**CTA Name**| **Value**|
|---| ---|
|Global Header | `global_header` |
|Global Footer | `global_footer` |
|Confirmation | `confirmation` |
|Referral Page | `referral_page` |
|Account Page | `my_account` |

If you want to send the date for a referral CTA, map to the **Referral Page** destination. Then map to the **Add CTA custom data** destination as: `cta.referral_page.data.date`.

### Event Triggers

To map events, see [Create an Event Mapping](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping).

Map to the following destinations for triggering specific events on a page. To trigger an event:

1. Select an event from the **Trigger** dropdown.
1. In the **Mapped Value** field, enter the value of the variable you are mapping.
1. Click **Add**.

| Variable | Description |
|:---------|:------------|
| Registration | Fires the registration event. |
| Conversion | Fires the conversion event. |
| Confirmation | Fires the confirmation event with no Element ID. |

## Vendor Documentation

[Extole Asyc Documentation](https://dev.extole.com/docs/tealium)
