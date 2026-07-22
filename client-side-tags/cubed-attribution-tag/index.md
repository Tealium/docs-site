---
title: CUBED Attribution Tag Setup Guide
description: This article describes how to set up the CUBED Attribution tag.
url: https://docs.tealium.com/client-side-tags/cubed-attribution-tag/
---
## Tag Configuration

First, go to the tag marketplace and add the CUBED tag to your profile (See [Add a tag](https://docs.tealium.com/manage-tags/#add-a-tag)).

After adding the tag, configure the below settings:

* **Account Token**: Your unique token provided by CUBED
* **Send Event Details**: Choose whether details about products are sent with your events. Default is **false**

## Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **All Pages**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/about-data-mappings/).

The destination variables for the CUBED tag are built into its data mapping tab. Available categories are:

### Standard

| **Destination Name**                         | **Description**                                                                                                                                                   |
|:---------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Account Token (`account_token`)              | Map to this if you want to dynamically override your account token                                                                                                |
| Forward Params (`forward_param`)             | An array of the landing page URL parameters used to classify marketing channels                                                                                   |
| Integer Labels (`addIntLabel.custom`)        | An integer label value you want to send with your CUBED data. Replace custom in the mapping with the key name for the label                                       |
| Float Labels (`addFloatLabel.custom`)        | A float label value you want to send with your CUBED data. Replace custom in the mapping with the key name for the label                                          |
| String Labels (`addStringLabel.custom`)      | A string label value you want to send with your CUBED data. Replace custom in the mapping with the key name for the label                                         |
| Date/Time Labels (`addDataTimeLabel.custom`) | A date/time label value you want to send with your CUBED data. Replace custom in the mapping with the key name for the label. The date must be ISO 8601 formatted |
| Boolean Labels (`addBoolLabel.custom`)       | A boolean label value you want to send with your CUBED data. Replace custom in the mapping with the key name for the label                                        |
| Sync Ids (`sync_ids`)                        | An array of unique identifiers for joining customer records across devices and platforms                                                                          |

### E-Commerce

Since the CUBED tag is e-commerce enabled, it will automatically use the default E-Commerce Extension mappings. Manually mapping in this category is generally not needed unless:

* You want to override any extension mappings
* An e-commerce variable you want is not offered in the extension

| **Destination Name**                    | **Description**                                                                                                                                                                         |
|:----------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Order ID/Transaction ID (`order_id`)    | The unique ID associated with an event. This value will default to the E-Commerce value `_corder` if not mapped                                                                         |
| Order Total/Revenue (`order_total`)     | The revenue associated with an event. This value will default to the E-Commerce value `_ctotal` if not mapped                                                                           |
| List of Names (`product_name`)          | This is the list of product names associated with an event. This is required if you are sending event details. This value will default to the E-Commerce value `_cprodname` if not mapped |
| List of SKUs (`product_sku`)            | This is the list of product SKUs associated with an event. This value will default to the E-Commerce value `_csku` if not mapped                                                        |
| List of Quantities (`product_quantity`) | This is the list of quantities of products associated with an event. This value will default to the E-Commerce value `_cquan` if not mapped                                             |
| List of Prices (`product_unit_price`)   | This is the list of product prices associated with an event. This value will default to the E-Commerce value `_cprice` if not mapped                                                    |

### Event Data: Custom Events

| **Destination Name**                | **Description**                                                                                             |
|:------------------------------------|:------------------------------------------------------------------------------------------------------------|
| Event Name (`event_name`)           | The name of the event being sent. This should match one of your preconfigured events in the CUBED interface |
| Send Event Details (`send_details`) | A Boolean determining if the product specific E-Commerce details are sent with an event                     |

## Vendor Documentation

* [Script Implementation Guide](http://tag.docs.withcubed.com/)
