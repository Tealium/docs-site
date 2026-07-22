---
title: X Universal Website Tag Setup Guide
description: This article describes how to configure the X Universal Website Tag (UWT) in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/twitter-universal-website-tag/
---

<blockquote>
This tag is now deprecated. For the current tag, see the [X Pixel tag](https://docs.tealium.com/x-pixel-tag/).
</blockquote>


## Requirements

* X Ads Account
* X UWT Pixel ID
* A fully configured [E-Commerce extension](https://docs.tealium.com/e-commerce-extension/)

## Supported versions

* v1.0.0

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

1. **Title**: Enter a unique name to identify the Tag. This is important if you are adding multiple instances of this Tag.
1. **X Pixel ID**: Enter the pixel ID value from your universal website tag code snippet. For example, `twq('init','1a2b3');`


<blockquote>
If you prefer to set the Tag Settings dynamically, use the Data Mappings (see below).
</blockquote>


## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

### Data mappings

Mapping is the process of sending data from a [Data Layer Variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor Tag. For instructions on how to map a Variable to a Tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The destination variables for the X Universal Website Tag are built into its Data Mapping tab. Available categories are:

### Standard

|Destination Name| Description|
|---| ---|
|X Pixel ID|  The Universal Website Tag pixel ID associated with your X Ads account, for example: "1a2b3" |
|Event Value|  The value to the advertiser of a user performing this event, for example: "19.99" |
|Number of Items|  The number of items associated with this on-site event, for example: "3" |
|Content Type|  The value should be either "product" or "product\_group". <ul><li>If the product IDs are being passed, then content\_type should be "product".</li><li>If product group IDs are being passed, then content\_type should be "product\_group".</li></ul> |
|Event Status|  The status of an on-site registration event, for example: "submitted" |

### E-Commerce

Because the X Universal Website Tag is e-commerce enabled, it will automatically use the default [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) mappings. Manually mapping in this category is generally not needed unless:

* you want to override any Extension mappings.
* an e-commerce variable you want is not offered in the extension.

|Destination Name| Description| E-commerce Extension Variable|
|---| ---| ---|
|Order ID| The advertiser's order ID associated with a purchase, signup, or download event| `corder`|
|Order Total| For Purchase events, this E-Commerce extension parameter will be passed to the Event Value destination| `ctotal`|
|Currency| The currency for the Event Value attribute (ISO 4217 standard)| `ccurrency`|
|List of Product IDs| Product IDs associated with the event| `cprod`|
|List of Names| Product names associated with the event| `cprodname`|
|List of Categories| Category of the product| `ccat`|
|List of Quantities| For Purchase and Download events, the values in this array (from the E-Commerce extension) will be added together and passed to the Number of Items destination| `cquan`|

### **Event Triggers (and Required Parameters)**

Map to these destinations for triggering specific events on a page, including Page View events. Here's how to map an event trigger:

1. Select an event from the **Trigger** list.
1. In the **Mapped Value** field, enter the value of the variable you are mapping to this destination. When value of the mapped variable matches the value you've entered into the **Mapped Value** field, the event will be triggered on the page.
1. To map more events, click **+Add** and repeat steps #1 and #2.


<blockquote>
The PageView event is triggered automatically on each page load.
</blockquote>


Some events require specific parameters and will not be triggered if those parameters are missing or blank. In the table below, parameters marked by an asterisk will be populated by the E-Commerce extension unless explicitly mapped.

|X Event Variable| Description| Required| Optional|
|---| ---| ---| ---|
|PageView (default)| Generic catch-all event type for pages that do not have a more specific event type.| None|  <ul><li>event\_value</li><li>currency\*</li><li>num\_items</li></ul> |
|Purchase|  When a purchase is made or the checkout flow is completed. |  <ul><li>content\_ids\*</li><li>content\_type</li><li>event\_value\*</li><li>currency\*</li></ul> |  <ul><li>content\_name\*</li><li>num\_items\*</li><li>order\_id\*</li></ul> |
|Signup| When a user sign up is completed.| None|  <ul><li>content\_name\*</li><li>content\_category\*</li><li>event\_value</li><li>currency\*</li><li>order\_id\*</li></ul> |
|Download|  When a download link has been clicked. Examples: software download, document download | None|  <ul><li>content\_ids\*</li><li>content\_name\*</li><li>content\_category\*</li><li>event\_value</li><li>currency\*</li><li>num\_items\*</li><li>order\_id\*</li></ul> |

## Vendor documentation

* [Conversion tracking for websites](https://business.x.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites)
