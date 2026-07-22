---
title: Amazon Ads Server Tag Setup Guide
description: This article describes how to set up the Amazon Ads Server tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/amazon-ads-server-tag/
---
## How it works

Amazon Ads Server is a single and secure tool to deploy, manage, and update digital marketing tags on a site without having to continuously update your website code.

## Tag Tips

* Supports the following E-Commerce extension values:
  * Order ID
  * List of Product IDs
  * List of Product Names
  * List of Quantities
  * List of Product Prices

* Use mapping to:
  * Dynamically override the E-Commerce extension values
  * Define the contents of the Activity Params object
    * Using `act`
  * Define the contents of the Retargeting Params object
    * Using `rtp`
  * Define the contents of the Dynamic Retargeting Params object
    * Using `drtp`
  * Define the contents of the Conditional Params object
    * Using `cp`
  * Dynamic Pages and Events
    * Set a value for url (overrides `url`)

## Tag Configuration

First, go to Tealium's tag marketplace and add the Amazon Ads Server tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **AAS Tag Manager ID**
  * Example: `123`

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `id` |  <ul><li>VersaTag ID</li></ul> |
|`url`|  <ul><li>URL</li></ul> |
|`mobile`|  <ul><li>Mobile</li><li>Default value is `0`.</li></ul> |
|`sync`|  <ul><li>Sync</li><li>Default value is `0`.</li></ul> |
|`dispType`|  <ul><li>Display type.</li><li>Default value is `js`.</li></ul> |
|`ActivityID`|  <ul><li>Activity ID</li></ul> |
|`Session`|  <ul><li>Session</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order ID.</li><li>Overrides `_corder`.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of Product IDs.</li><li>Overrides `_cprod`.</li></ul> |
|`product_name`|  <ul><li>Array</li><li>List of Names.</li><li>Overrides `_cprodname`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities.</li><li>Overrides `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices.</li><li>Overrides `_cprice`.</li></ul> |

### Configurable Parameters

|Variable| Description|
|---| ---|
|`act.###`|  <ul><li>String</li><li>Activity Params.</li></ul> |
|`rtp.###`|  <ul><li>String</li><li>Retargeting Params.</li></ul> |
|`drtp.###`|  <ul><li>String</li><li>Dynamic Retargeting Params.</li></ul> |
|`cp.###`|  <ul><li>String</li><li>Conditional Params.</li></ul> |
|`activityParams`|  <ul><li>Object</li><li>Activity Params.</li></ul> |
|`retargetParams`|  <ul><li>Object</li><li>Retargeting Params.</li></ul> |
|`dynamicRetargetParams`|  <ul><li>Object</li><li>Dynamic Retargeting Params.</li></ul> |
|`conditionalParams`|  <ul><li>Object</li><li>`meta charset="utf-8"`</li><li>Conditional Params.</li></ul> |
