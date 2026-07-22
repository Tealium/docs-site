---
title: Veritonic Connector Setup Guide
description: This article describes how to set up the Veritonic connector.
url: https://docs.tealium.com/server-side-connectors/veritonic-connector/
---

## API Information

This connector uses the following vendor API:

* API Name: Veritonic
* API Version: v1
* API Endpoint: `https://atr.veritonicmetrics.com`

## Configuration

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:
* **Client ID**  
A unique identifier from the Veritonic dashboard.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action - Send Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | A string that indicates the type of action that the user performed. |

### Event Attributes

| **Parameter** | **Description** |
| --- | --- |
| User IP Address | The network address of the user’s device. |
| Timestamp | A numerical value that represents the date and time of the action. |
| User Agent | A string that identifies the browser and operating system of the user. |
| Page URL | URL of the page where the action took place. |
| GDPR consent | A string that indicates the user’s consent for data processing. |
| Event Type Attributes | Optional event type attributes. |

### Event Type Attributes

| **Event Type** | **Additional Parameters (Optional)** |
| --- | --- |
| `view` | <ul><li>None</li></ul> |
| `addtocart` | <ul><li>`value`, `currency`, `quantity`, `product_id`, `product_name`, `product_type`, `product_vendor`, `variant_id`, `variant_name`</li></ul> |
| `checkout` | <ul><li>`value`, `currency`, `discount_code`, `quantity`, `line_items`</li><li>`line_items` is an array of objects with the following optional attributes: `value`, `quantity`, `product_id`, `product_name`, `product_type`, `product_vendor`, `variant_id`, `variant_name`</li><li>The user must be able to map an array of numbers or array of strings to each of the following parameters:<ul><li>`line_items.value`</li><li>`line_items.quantity`</li><li>`line_items.product_id`</li><li>`line_items.product_name`</li><li>`line_items.product_type`</li><li>`line_items.product_vendor`</li><li>`line_items.variant_id`</li><li>`line_items.variant_name`</li></ul></li><li>The final array of objects needs to be built in the backend, so for instance, if you have:<ul><li>`line_items.quantity` = [1,2]</li><li>`line_items.product_id` = [a,b]</li><li>The line_items array will look like this: `[{product_id:a,quantity:1},{product_id:b,quantity:2}]`</ul></li></li></ul> |
| `lead` | <ul><li>`value`, `currency`, `type`,`category`</li></ul>  |
| `product` | <ul><li>`value`, `currency`, `product_id`, `product_name`, `product_type`, `product_vendor`</li></ul> |
| `purchase` | <ul><li>`value`, `currency`, `discount_code`, `quantity`, `line_items`</li><li>`line_items`: Same as the checkout event</li></ul> |
| `app_install` | <ul><li>`app_name`, `app_id`, `integration`</li></ul> |
