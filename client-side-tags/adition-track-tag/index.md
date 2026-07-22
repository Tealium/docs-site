---
title: Adition (Track) Tag Setup Guide
description: This article describes how to set up the Adition (Track) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adition-track-tag/
---
## Tag Tips

* This is the Track version of Adition.
* Set the domain according to your agreement with Adition.

  * Default value: `adfarm1.adition.com`
  * AdfarmID: `ad<id>.adfarm1.adition.com`
  * Custom: `<subdomain>.<domain>.<tld>`

* The default return type is `img`.
* Uses the following E-Commerce Variables

  * `_cprod`
  * `_cquan`
  * `_cprice`
  * `_corder`

## Tag Configuration

First, go to Tealium's tag marketplace and add the Adition (Track) tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Domain**
  * Domain supplied by Adition.
  * Default domain is `adfarm1.adition.com`.

* **TID**
  * (Required) Represents the landing page within the Adition ad serving system.

* **SID**
  * (Required) Represents the tracking spot within the Adition ad serving system.

* **Tag Type**:

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|Tag Type|  <ul><li>Tag Type</li></ul> |
|Domain|  <ul><li>Domain</li></ul> |
| `tid` |  <ul><li>Landing Page ID</li></ul> |
| `sid` |  <ul><li>Tracking Spot ID</li></ul> |
|`orderid`|  <ul><li>Order ID</li><li>Overrides `_corder` .</li></ul> |
|`descr`|  <ul><li>Array</li><li>Item description.</li><li>Overrides `_cprod` .</li></ul> |
| `quantity` |  <ul><li>Array</li><li>Item quantity.</li><li>Overrides `_cquan` .</li></ul> |
|`price`|  <ul><li>Array</li><li>Item price.</li><li>Overrides `_cprice` .</li></ul> |
|`total`|  <ul><li>Array</li><li>Total price.</li></ul> |
|`param`|  <ul><li>Param</li><li>Values are 1 - 20.</li></ul> |
