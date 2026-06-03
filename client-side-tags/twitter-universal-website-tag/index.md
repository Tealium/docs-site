---
title: X Universal Website Tag Setup Guide
description: This article describes how to configure the X Universal Website Tag (UWT) in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/twitter-universal-website-tag/
---
This tag is now deprecated. For the current tag, see the [X Pixel tag]().

## Requirements

* X Ads Account
* X UWT Pixel ID
* A fully configured [E-Commerce extension]()

## Supported versions

* v1.0.0

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

1. **Title**: Enter a unique name to identify the Tag. This is important if you are adding multiple instances of this Tag.
1. **X Pixel ID**: Enter the pixel ID value from your universal website tag code snippet. For example, `twq(&#39;init&#39;,&#39;1a2b3&#39;);`

If you prefer to set the Tag Settings dynamically, use the Data Mappings (see below).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

### Data mappings

Mapping is the process of sending data from a [Data Layer Variable]() to the corresponding destination variable of the vendor Tag. For instructions on how to map a Variable to a Tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the X Universal Website Tag are built into its Data Mapping tab. Available categories are:

### Standard

|Destination Name| Description|
|---| ---|
|X Pixel ID|  The Universal Website Tag pixel ID associated with your X Ads account, for example: &#34;1a2b3&#34; |
|Event Value|  The value to the advertiser of a user performing this event, for example: &#34;19.99&#34; |
|Number of Items|  The number of items associated with this on-site event, for example: &#34;3&#34; |
|Content Type|  The value should be either &#34;product&#34; or &#34;product\_group&#34;. &lt;ul&gt;&lt;li&gt;If the product IDs are being passed, then content\_type should be &#34;product&#34;.&lt;/li&gt;&lt;li&gt;If product group IDs are being passed, then content\_type should be &#34;product\_group&#34;.&lt;/li&gt;&lt;/ul&gt; |
|Event Status|  The status of an on-site registration event, for example: &#34;submitted&#34; |

### E-Commerce

Because the X Universal Website Tag is e-commerce enabled, it will automatically use the default [E-Commerce Extension]() mappings. Manually mapping in this category is generally not needed unless:

* you want to override any Extension mappings.
* an e-commerce variable you want is not offered in the extension.

|Destination Name| Description| E-commerce Extension Variable|
|---| ---| ---|
|Order ID| The advertiser&#39;s order ID associated with a purchase, signup, or download event| `corder`|
|Order Total| For Purchase events, this E-Commerce extension parameter will be passed to the Event Value destination| `ctotal`|
|Currency| The currency for the Event Value attribute (ISO 4217 standard)| `ccurrency`|
|List of Product IDs| Product IDs associated with the event| `cprod`|
|List of Names| Product names associated with the event| `cprodname`|
|List of Categories| Category of the product| `ccat`|
|List of Quantities| For Purchase and Download events, the values in this array (from the E-Commerce extension) will be added together and passed to the Number of Items destination| `cquan`|

### **Event Triggers (and Required Parameters)**

Map to these destinations for triggering specific events on a page, including Page View events. Here&#39;s how to map an event trigger:

1. Select an event from the **Trigger** list.
1. In the **Mapped Value** field, enter the value of the variable you are mapping to this destination. When value of the mapped variable matches the value you&#39;ve entered into the **Mapped Value** field, the event will be triggered on the page.
1. To map more events, click **&#43;Add** and repeat steps #1 and #2.

The PageView event is triggered automatically on each page load.

Some events require specific parameters and will not be triggered if those parameters are missing or blank. In the table below, parameters marked by an asterisk will be populated by the E-Commerce extension unless explicitly mapped.

|X Event Variable| Description| Required| Optional|
|---| ---| ---| ---|
|PageView (default)| Generic catch-all event type for pages that do not have a more specific event type.| None|  &lt;ul&gt;&lt;li&gt;event\_value&lt;/li&gt;&lt;li&gt;currency\*&lt;/li&gt;&lt;li&gt;num\_items&lt;/li&gt;&lt;/ul&gt; |
|Purchase|  When a purchase is made or the checkout flow is completed. |  &lt;ul&gt;&lt;li&gt;content\_ids\*&lt;/li&gt;&lt;li&gt;content\_type&lt;/li&gt;&lt;li&gt;event\_value\*&lt;/li&gt;&lt;li&gt;currency\*&lt;/li&gt;&lt;/ul&gt; |  &lt;ul&gt;&lt;li&gt;content\_name\*&lt;/li&gt;&lt;li&gt;num\_items\*&lt;/li&gt;&lt;li&gt;order\_id\*&lt;/li&gt;&lt;/ul&gt; |
|Signup| When a user sign up is completed.| None|  &lt;ul&gt;&lt;li&gt;content\_name\*&lt;/li&gt;&lt;li&gt;content\_category\*&lt;/li&gt;&lt;li&gt;event\_value&lt;/li&gt;&lt;li&gt;currency\*&lt;/li&gt;&lt;li&gt;order\_id\*&lt;/li&gt;&lt;/ul&gt; |
|Download|  When a download link has been clicked. Examples: software download, document download | None|  &lt;ul&gt;&lt;li&gt;content\_ids\*&lt;/li&gt;&lt;li&gt;content\_name\*&lt;/li&gt;&lt;li&gt;content\_category\*&lt;/li&gt;&lt;li&gt;event\_value&lt;/li&gt;&lt;li&gt;currency\*&lt;/li&gt;&lt;li&gt;num\_items\*&lt;/li&gt;&lt;li&gt;order\_id\*&lt;/li&gt;&lt;/ul&gt; |

## Vendor documentation

* [Conversion tracking for websites](https://business.x.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites)
