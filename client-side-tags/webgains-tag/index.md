---
title: Webgains Tag Setup Guide
description: This article describes how to set up the Webgains tag.
url: https://docs.tealium.com/client-side-tags/webgains-tag/
---
## Tag tips

* Use the E-Commerce extension to set values for `_corder`, `_csubtotal`, `_ccustid`, `_cpromo`.
* Map an array value to `wgvouchercode` to set product-level vouchers.
* Requires that `_cprice` has list of prices.
* `wgitems` is set automatically using E-Commerce Extension values (`_cprice`, `_cprodname`, `_cprod`). To override these E-Commerce Extension values, map a string to this variable.
* To set an order-level discount, map a value to `wgDISCOUNT`. This is automatically converted to a negative value. A discount line item will be added to the list of products in the order.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Program ID**: The Webgains program ID.
* **Event ID**: Required value. Webgains uses this value to determine the commission rate.

## Load rules

Load the tag on all pages or set conditions for when the tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Data Type | Description |
|:---------|:------------|:------------|
| `wgsubdomain` | String |The subdomain of the server that is being tracked. |
| `wglang` |  String |The two-letter ISO 639-1 language code of the content being tracked. |
| `wgslang` | String |The two-letter ISO 639-1 sublanguage code of the content being tracked.  |
| `wgprogramid` |  String |The Webgains program ID.|
| `wgeventid` | String |The unique event ID.  |
| `wgvalue` |  String |The monetary value of the event.|
| `wgorderreference` |  String |The unique reference ID of the transaction in the event.|
| `wgcomment` | String |Comments about the event. |
| `wgmultiple` |  Boolean | Whether multiple occurrences of this event should be tracked or counted separately. A `1` indicates that every event should be tracked separately while a `0` indicates that only the first event should be tracked. |
| `wgitems` | String | Details about the items or products in this transaction. |
| `wgcustomerid` |  String | The customer ID. |
| `wgproductid` | String | The product ID. |
| `wgvouchercode` | String | The voucher or discount code for the event. |
| `wgchecksum` | String | The checksum for the event.  |
| `wgDISCOUNT`  | String | Adds a discount product with this value. |