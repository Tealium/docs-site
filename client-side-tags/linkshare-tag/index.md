---
title: LinkShare Tag Setup Guide
description: This article describes how to set up the LinkShare tag.
url: https://docs.tealium.com/client-side-tags/linkshare-tag/
---
## Tag Specifications and Requirements

### Specifications

* **Name**: LinkShare
* **Vendor**: Rakuten
* **Type**: Affiliate Marketing

### Required

**Services**: LinkShare Network Account

**Configurations**:

* Merchant ID

## Tag Configuration in Tealium iQ

### Adding the Tag

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

### Configuring the Tag

1. **Title**: (Required) Enter a descriptive title to identify the tag instance.
1. **Merchant ID**: (Required) Enter the Advertiser&#39;s unique ID assigned by LinkShare.

#### Applying Load Rules

[Load Rules]() determine when and where to load an instance of this tag. The **Load on All Pages** rule is the default load rule. To load this Tag on a specific page of your site, create a new load rule with the relevant conditions.

**Best Practices**: The following best practices come highly recommended for this Tag.

* Load this tag on a conversion page (Order Confirmation/Checkout) and the page following a conversion (Receipt/Thank-You).
* Load the tag only once per conversion page for optimized performance.

#### Setting up Mappings

[Mapping](/iq-tag-management/data-mappings/manage/) is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag. The destination variables for this tag are available in the Mapping toolkit. For ease of use, the variables are grouped into different categories.

Be sure to configure the [E-commerce Extension]() for this tag.

As long as you properly add and configure the [E-Commerce Extension](), you do not have to map anything in the tag configurations; the E-Commerce Extension will take care of it. However, if you want to override certain E-commerce variables or you are not using the E-Commerce Extension, map to the following destination variables.

* **ord**: Map to this variable to send the unique ID of the order/transaction.
* **cur**: Map to this variable to send the alphanumeric, three-character currency value.   
 `&#34;cur&#34;=USD`
* **skulist**: Map to this variable to send a list of item SKUs. Each SKU in the list must be unique to the item.   
 `&#34;skulist&#34;=sku1|sku2|sku3`
* **qlist**: Map a list of item quantities to this variable. The quantities must be listed in the same order as their corresponding SKUs.   
 `&#34;qlist&#34;=2|4|8`
* **amtlist**: Map a list of item subtotals to this variable. The subtotals must be listed in the same order as their corresponding SKUs and formatted as `price*quantity*100`.   
 `&#34;amtlist&#34;=1000|2000|4000`
* **namelist**: Map a list of item names to this variable. The item names must be listed in the same order as their corresponding SKUs.  
 `&#34;namelist&#34;=XXX|YYY|ZZZ`

### Vendor Documentation

* [About Rakuten LinkShare](http://www.linkshare.com/about/)
* [Glossary](http://helpcenter.linkshare.com/publisher/glossary.php)
* [Affiliate Marketing Tracking Technology:Video Tutorial](https://rakutenlinkshare.zendesk.com/hc/en-us/articles/200694358-Understanding-Affiliate-Marketing-Tracking-Technology-VIDEO-)
* [Affiliate Marketing resources](http://www.linkshare.com/campus/performance_marketing_resources/) (Login required to view articles and videos)