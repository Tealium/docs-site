---
title: Salsify Tag Setup Guide
description: This article describes how to set up the Salsify tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/salsify-tag/
---
Salsify Enhanced Content offers a unified solution for brands to build and publish authentic, engaging below-the-fold brand experiences that increase conversion rates. With Enhanced Content you can receive images, videos, comparison charts, and interactive product tours from any Salsify supplier or brand leveraging the Enhanced Content offering.

Enhanced Content can be served through a JavaScript tag or NPM integration provided by Salsify.

## Tag tips

* Supports the following E-Commerce extension values:
  * Product ID
  * Product Category
  * Product Quantity
  * Product Brand
  * Product Price

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Client ID**: Your Salsify Experiences SDK Client ID.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available destination categories are:

### Standard

|Variable| Description|
|---| ---|
|Client ID| (`clientId`)|
|ID Type| (`idType`)|
|Enhanced Content Container| (`enhancedContentContainer`)|

### E-Commerce

|Variable| Description|
|---| ---|
|Product ID (`productId`) (Overrides `_cprod`)| [Array]|
|Product Category (`category`) (Overrides `_ccat`)| [Array]|
|Product Quantity (`quantity`) (Overrides `_cquan`)| [Array]|
|Product Brand (`brand`) (Overrides `_cbrand`)| [Array]|
|Product Price (`price`) (Overrides _cprice`)| [Array]|

### Events

|Variable| Description|
|---| ---|
|Add to Cart| `addToCart`|
|Page Navigation| `navigation`|

### Event-specific Parameters

|Variable| Description|
|---| ---|
|Add to Cart| `addToCart`|
|Page Navigation| `navigation`|
