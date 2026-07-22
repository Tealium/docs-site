---
title: Shopzilla Tag Setup Guide
description: This article describes how to set up the Shopzilla tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/shopzilla-tag/
---
## Tag Specifications

* **Name**: Shopzilla
* **Vendor**: Shopzilla
* **Type**: ROI Tracker

## Required

* Shopzilla Merchant Account
* Merchant ID

## Add the Tag

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

## Configure the Tag

1. **Title**: (Required) Enter a descriptive title to identify the tag instance.
1. **Merchant ID**: (Optional) Enter the numeric merchant identifier provided to you by Shopzilla. This can be found in your Shopzilla Merchant account. For example, `170739`.
1. **Tracker Domain**: Choose the domain that your code snippet is pointing to. The default selection is `shopzilla.com`.


<blockquote>
You have the option to dynamically set the Merchant ID and Tracker Domain values with the **Data Mappings** toobox. Refer to the [Setting up Mappings](#mappings) section below.
</blockquote>


## Apply Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag. The 'Load on All Pages' rule is the default Load Rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

### Best Practice

Set up load rule conditions to load this tag on the order confirmation page, one that appears post conversion (Thank You/Receipt page).

## Set up Mappings

Mapping is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag. The destination variables for this tag are available in the Mapping toolkit.


<blockquote>
For instructions on how to map a Data Source to a tag destination, see [Mapping Data Sources](https://docs.tealium.com/about-data-mappings/).
</blockquote>


* **Merchant ID**: This is the `mid` parameter in the tracking code. Map to this variable to send your Shopzilla merchant identifier.
* **Tracker Domain**: This is the domain specified in your code snippet.


<blockquote>
We recommend the use of [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) for mapping Order Value, Order ID and Units Ordered destinations. When the Extension is properly configured and your site is utilizing E-commerce parameters in the utag data object, the Extension will automatically map those variables to the appropriate destinations. The following mappings, however, are available to this tag should you need to override the equivalent Extension variables.
</blockquote>


* **Customer Type** (1=new 0=returning): This indicates the `cust_type` parameter with two possible values:
  * `1` for New customer
  * `0` for Repeat customer.  
Mapping to this destination overrides the Extension's `_ctype` variable.

* **Order Value**: This is order subtotal amount (for example, the order total minus shipping and tax).  
Mapping to this destination overrides the Extension's `_csubtotal` variable.
* **Order ID**: This is the unique identifier assigned to the transaction.  
Mapping to this destination overrides the Extension's `_corder` variable.
* **Units Ordered**: This is the number of units (quantity) ordered for the item.  
Mapping to this destination overrides the Extension's `_cquan` variable.

## Vendor Documentation

* [Getting Started with Shopzilla](https://support.shopzilla.com/forums/21589186-Getting-Started-With-Shopzilla)
* [How to track conversion and overall performance](https://support.shopzilla.com/entries/26154976-Merchant-FAQs#0_7)
* [Shopzilla Merchant Support](https://support.shopzilla.com/home)
