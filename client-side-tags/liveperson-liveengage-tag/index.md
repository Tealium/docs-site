---
title: LivePerson LiveEngage 2.0 Tag Setup Guide
description: This article describes how to set up the LivePerson LiveEngage 2.0 tag.
url: https://docs.tealium.com/client-side-tags/liveperson-liveengage-tag/
---
Deliver a personalized user experience throughout your customer’s life cycle by proactively engaging visitors with real time solutions for chat, voice and content, plus a full range of open APIs.

## Tag Tips

Use mapping to override the standard configurations values dynamically.

* Current Library Version: 1.10
* Uses the following E-Commerce variables
  * `_corder`
  * `_ctotal`
  * `_ccustid`
  * `_cprodname`
  * `_ccat`
  * `_csku`
  * `_cquan`
  * `_cprice`

* Market Source - Channel
  * `0`-Direct
  * `1`-Search
  * `2`-Social
  * `3`-Email
  * `4`-Referral
  * `5`-Paid Search
  * `6`-Display

* Service - Status
  * `0`-Complete
  * `1`-In Progress
  * `2`-Approved
  * `3`-Cancelled
  * `4`-Not Approved
  * `5`-Reviewed
  * `6`-Missing Details
  * `7`-Closed
  * `8`-Removed
  * `9`-Assigned

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

After adding the tag, configure the following settings:

* **Site ID**: The site value (for example, `23954343`)
* **Section**: Comma-separated list of section values
* **Allow Mappings**:
  * `True` - Allow Site ID to be mapped, library loaded on send  
  * `False` - Library is loaded on tag load
* **Merge E-Commerce**:
  * `True` - Use E-Comm extension for basis of all mappings  
  * `False` - Does not use the E-Comm Extension as the data base

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|Site ID| (`site`)|
|Event Type| (`type`)|
|Section (`section`)| [Array/CSV]|
|Taglets| (`taglets`)|
|Page URL| (`page_url`) (Overrides `dom.url`)|

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

|Variable| Description|
|---| ---|
|Cart (`cart`)| `cart`|
|Purchase (`purchase`)| `purchase`|
|Product View (`prodView`)| `prodView`|
|Customer Info (`ctmrinfo`)| `ctmrinfo`|
|Marketing Source (`mrktinfo`)| `mrktinfo`|
|Personal (`personal`)| `personal`|
|Lead (`lead`)| `lead`|
|Service (`service`)| `service`|
|Search (`searchInfo`)| `searchInfo`|
|Error (`error`)| `error`|

### E-Commerce

|Variable| Description|
|---| ---|
|Order ID| (`order_id`) (Overrides `_corder`)|
|Order Total| (`order_total`) (Overrides `_ctotal`)|
|List of Names (`product_name`) (Overrides `_cprodname`)| [Array]|
|List of SKUs (`product_sku`) (Overrides `_csku`)| [Array]|
|List of Categories (`product_category`) (Overrides `_ccat`)| [Array]|
|List of Quantities (`product_quantity`) (Overrides `_cquan`)| [Array]|
|List of Prices (`product_unit_price`) (Overrides `_cprice`)| [Array]|

### Cart E-Commerce

|Variable| Description|
|---| ---|
|Order Total| (`cart.order_total`) (Overrides `_ctotal`)|
|List of Names (`cart.product_name`) (Overrides `_cprodname`)| [Array]|
|List of SKUs (`cart.product_sku`) (Overrides `_csku`)| [Array]|
|List of Categories (`cart.product_category`) (Overrides `_ccat`)| [Array]|
|List of Quantities (`cart.product_quantity`) (Overrides `_cquan`)| [Array]|
|List of Prices (`cart.product_unit_price`) (Overrides `_cprice`)| [Array]|

### Purchase E-Commerce

|Variable| Description|
|---| ---|
|Order ID| (`purchase.order_id`) (Overrides `_corder`)|
|Order Total| (`purchase.order_total`) (Overrides `_ctotal`)|
|List of Names (`purchase.product_name`) (Overrides `_cprodname`)| [Array]|
|List of SKUs (`purchase.product_sku`) (Overrides `_csku`)| [Array]|
|List of Categories (`purchase.product_category`) (Overrides `_ccat`)| [Array]|
|List of Quantities (`purchase.product_quantity`) (Overrides `_cquan`)| [Array]|
|List of Prices (`purchase.product_unit_price`) (Overrides `_cprice`)| [Array]|

### Prod View E-Commerce

|Variable| Description|
|---| ---|
|List of Names (`prodView.product_name`) (Overrides `_cprodname`)| [Array]|
|List of SKUs (`prodView.product_sku`) (Overrides `_csku`)| [Array]|
|List of Categories (`prodView.product_category`) (Overrides `_ccat`)| [Array]|
|List of Prices (`prodView.product_unit_price`) (Overrides `_cprice`)| [Array]|

### Customer Info

|Variable| Description|
|---| ---|
|Customer ID| (`customer_id`) (Overrides `_ccustid`)|
|Customer Lifecycle Status| (`vi.cstatus`)|
|Customer Type| (`vi.ctype`)|
|Financial Balance (`vi.balance`)| [Float]|
|Social ID| (`vi.socialId`)|
|Unique Device Or Phone Identifier| (`vi.imei`)|
|Username| (`vi.userName`)|
|Company Size (`vi.companySize`)| [Integer]|
|Company Name| (`vi.accountName`)|
|Role/Title| (`vi.role`)|
|Last Payment Date - Day (`vi.lpd_day`)| [Integer]|
|Last Payment Date - Month (`vi.lpd_month`)| [Integer]|
|Last Payment Date - Year (`vi.lpd_year`)| [Integer]|
|Registration Date - Day (`vi.rd_day`)| [Integer]|
|Registration Date - Month (`vi.rd_month`)| [Integer]|
|Registration Date - Year (`vi.rd_year`)| [Integer]|

### Marketing Source

|Variable| Description|
|---| ---|
|Channel| (`ms.channel`)|
|Affiliate| (`ms.affiliate`)|
|Campaign ID| (`ms.campaignId`)|

### Personal Info

|Variable| Description|
|---| ---|
|First Name| (`per.firstname`)|
|last Name| (`per.lastname`)|
|Age| (`per.age`)|
|Year of Birth| (`per.year`)|
|Month of Birth| (`per.month`)|
|Day of Birth| (`per.day`)|
|Email Address| (`per.email`)|
|Phone Number| (`per.phone`)|
|Gender| (`per.gender`)|
|Company| (`per.company`)|
|Language| (`per.language`)|

### Lead

|Variable| Description|
|---| ---|
|Topic| (`lead.topic`)|
|Value| (`lead.value`)|
|Lead ID| (`lead.id`)|

### Service

|Variable| Description|
|---| ---|
|Topic| (`serv.topic`)|
|Status| (`serv.status`)|
|Category| (`serv.category`)|
|Service ID| (`serv.id`)|

### Search

|Variable| Description|
|---| ---|
|Search Keywords| (`search.keywords`)|

### Error

|Variable| Description|
|---| ---|
|Message| (`err.msg`)|
|Code| (`err.code`)|
