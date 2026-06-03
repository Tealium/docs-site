---
title: PebblePost Tag Setup Guide
description: This article describes how to configure PebblePost in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/pebblepost-tag/
---## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* PebblePost Marketer ID: This will be an integer value provided by PebblePost. For example: `123456`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

Recommended Load Rule: All Pages

## Data mappings

Mapping is the process of sending data from a [Data Layer Variable](/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor Tag. For instructions on how to map a Variable to a Tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the PebblePost Tag are built into its Data Mapping tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
|Customer Email (email)| The email address for the customer.|
|Synthetic Endpoint (end\_url)| The URL trigger for the transaction. The PebblePost tag triggers campaign logic based on URL value, if your page will not provide one, you may pass an artificial URL value here. For example: &#34;/thankyou&#34;.|
|Customer Tag (tags)| A custom value you may pass through the PebblePost tag.|

### E-Commerce

Because the PebblePost Tag is e-commerce enabled, it will automatically use the default E-Commerce Extension mappings. Manually mapping in this category is generally not needed unless:

* You want to override any Extension mappings
* An e-commerce variable you want is not offered in the extension

|**Destination Name**| **Description**|
|---| ---|
|Order ID (order\_id)| The ID for the order being placed.|
|Order Total (order\_total)| The total for the order being placed.|
|Customer Id (customer\_id)| The ID of the customer making the order being placed.|
