---
title: How to Set up Facebook Dynamic Ads in Tealium iQ
description: Dynamic Ads are a retargeting service that provides product recommendations to your visitors based on the products that they have interacted with.
url: https://docs.tealium.com/client-side-tags/facebook-dynamic-ads-tag/
---
This article describes how to provide Facebook with data about the products a visitor interacted with in order for Facebook to take action on those events.

## Prerequisites

The steps describes in this article assume that you already have a Facebook account and that you have set up your Product Catalog in the Facebook Business Manager. This step allows Facebook to accurately retarget events based on the products a visitor has shown interest in. ([Learn more](https://business.facebook.com)).

## Set up Facebook Pixel in Tealium iQ

First, you will need to add the [Facebook tag]() in TiQ.

If you have already added the Facebook tag, you can use that one. You do not need to add another instance.

Ensure that you are using the latest version of the Facebook tag template. To check what version you are on, use the **Tag Status Checker**. If it is not the latest version, update your template.

## Set up Required Events

The Dynamic Ads service requires you to fire the following 3 Facebook events:

* ViewContent
* AddToCart
* Purchase

### Set up the ViewContent Event

The ViewContent event indicates that a visitor viewed a product and is typically fired on a product detail page. At a minimum, you must provide the `content_ids` and `content_type` parameters with this event for Dynamic Ads, as described below.

A ViewContent event is usually associated with the viewing of a product, which can be tied to a page load. For this reason, it is useful to examine the data sources present when the page load occurs.

Use the following steps to set up the mapping for the ViewContent event:

1. From the Facebook tag, click the edit icon.
1. Click the **Data Mappings** tab.
1. From the **Data Sources** drop-down list, select a data source that uniquely identifies a product page.  
In this example, `page_type` is used.
1. Click the **Events** tab.
1. In the **Trigger** field, enter the `page_type` value for the product page.  
1. From the **Event** drop-down list, select **ViewContent**.
1. Click **&#43; Add**.  
An orange text field displays your mapping.
1. Click **Close** to submit your mapping.  
1. Save and publish your changes to save your settings.

### Set up the AddToCart Event

The AddToCart event indicates that a visitor added a certain product to their cart or shopping basket. This event also requires `content_ids` and `content_type` parameters for Dynamic Ads, as described below.

The action of adding an item to a cart is typically tied to a button click on a product page. To fire an AddToCart event, you must key off of the value of a data source for that event. In this example, the `event_name` data source is used.

Use the following steps to set up the AddToCart event:

1. From the Facebook tag, click the edit icon.
1. Click the **Data Mappings** tab.
1. Select the data source that indicates when an AddToCart event fires.
1. Click the **Events** tab.
1. In the **Trigger** field, enter `event_name` value for an add-to-cart event.
1. From the **Event** drop-down list, select **AddToCart**.
1. Click **&#43; Add**. An orange text field displays with your mapping.
1. Click **Close** to submit your mapping.
1. Save and publish your changes to save your settings.

### The Purchase Event

You do not have to set up a mapping for the Purchase event if you already have the E-Commerce extension set up with the order ID mapped. If you have the e-commerce extension configured, the purchase event will automatically fire when an order ID is populated. ([Learn more]()).

If you do not have the E-Commerce extension, set up the Purchase event using theViewContent event setup steps as a guideline. Use a mapping based off of `page_type` equaling &#34;order confirmation&#34; as an example.

## Set up Required Parameters to Send with Events

Each of these events requires that you send certain parameters, namely `content_ids` and `content_type`. Setting up additional parameters such as `value`, `content_name`, and `currency` can help inform your analytics with more meaningful data. If you have the E-Commerce extension set up, these data sources will be automatically mapped for you.

### The content_ids Parameter

The `content_ids` parameter contains the IDs or SKUs of the products viewed by your visitor. If you have the e-commerce extension configured, these parameters are mapped and populated by the data source you selected for the List of Product IDs field in the extension.  ([Learn more]()).

If you do not have the E-Commerce extension or you want to use another data source, map a data source to the `content_ids` parameter for each of the three (3) events.

### The content_type Parameter

The `content_type` parameter indicates to Facebook whether the content/product IDs signify a single product or a group of products. You must set this parameter to either &#34; `product`&#34; or &#34; `product_group`&#34;, respectively. To accomplish this, use the Set Data Value extension..

This requirement is specific to Facebook. It is unlikely you already have a data source that is doing this for you.

Use the following steps to set `content_type` with a Set Data Value extension:

1. Add a Set Data Value extension. ([Learn more]()).
Use a descriptive title such as `Facebook: Setting content_type`.
1. Set the scope of the extension to your Facebook tag.
This extension is only needed for the Facebook tag and only needs to run when the Facebook tag loads.
1. To create a data source, click the plus (**&#43;**) button next to the **Set** drop-down list.
1. Use a meaningful name for the data source, such as `fb_content_type`.
The purpose of this data source is to provide the value for `content_type`.
1. In the **To:** field, ensure that **Text** is selected.
1. Enter `product` or `product_group` in the text field.
An extension that sets a data source with the proper value for `content_type` is now created.
1. To add this new data source in mapping for the Facebook tag, click the **Data Mappings** tab.
1. From the **Data Sources** drop-down list, select your `fb_content_type` data source.
1. Click the **Parameters** tab.
This lets you set up the parameter mappings for the event of your choice.
1. From the **Event** drop-down list, select the first event that you want to map content type to, starting with `ViewContent`.
1. From the **Parameter** drop-down list, select **Content Type**.
1. Click **&#43; Add.**
A blue text field appears in the **Mappings** dialog indicating that your mapping was successful.
1. Repeat the steps above for the `AddToCart` and `Purchase` events.
1. Click **Close**.
1. Click **Apply** to submit your mappings.
1. Save and publish your changes to save your settings.
  
## Troubleshooting

Facebook provides the Facebook Pixel Helper browser extension in Chrome. Adding this extension to your Chrome browser will provide information on the events that fired on a page, what parameters the events contained, and errors detected by Facebook. ([Learn more](https://developers.facebook.com/docs/ads-for-websites/pixel-troubleshooting)).

## Vendor Documentation

* [Facebook Dynamic Product Ads](https //developers.facebook.com/docs/facebook-pixel/pixel-with-ads/dynamic-product-ads)