---
title: Yandex.Metrica Tag Setup Guide
description: This article describes how to set up the Yandex.Metrica tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/yandex-metrica-tag/
---
Yandex.Metrica is a free tool that helps you increase the conversion rate of your site. Metrica lets you monitor the key effectiveness indicators of your website, analyze user behavior, and evaluate the efficiency of your ad campaigns.

## Tag tips

Use mapping to override the standard config values dynamically.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Tag ID**: Yandex Tag ID
* **Click Map**: Detailed recordings of user activity on the site: mouse movement, scrolling, and clicks
* **Track Links**: Setting tracking of outbound links and download links
* **Accurate Track Bounce**: Enable the accurate bounce rate, with a non-bounce event registered after 15000 ms (15 s)
* **Webvisor**: Webvisor reproduces user actions in video format and lets you know what they do on the site: how they move around the page, how they move the mouse cursor and click through links.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
| --- | --- |
| Base Url (base\_url) | \[String\] |
| Hit Event Url (url) | \[String\] |
| Tag ID (tagId) | \[String\] |
| Click Map (clickmap) | \[Boolean\] |
| Track Links (trackLinks) | \[Boolean\] |
| Accurate Track Bounce (accurateTrackBounce) | \[Boolean\] |
| Webvisor (webvisor) | \[Boolean\] |
| E-commerce Data Layer (ecommerce) | \[String/Boolean\] |

### E-commerce

| Variable | Description |
| --- | --- |
| Order Id (order\_id) (override \_corder) | \[String/Number\] |
| Order Coupon Code (order\_coupon\_code) (override \_cpromo) | \[String\] |
| Order Total (order\_total) (override \_ctotal) | \[Number/String\] |
| Order Currency (order\_currency) (override \_ccurrency) | \[String\] |
| Goal ID (goal\_id) | \[Number/String\] |
| List of Product IDs (id) (override \_csku) | \[Array\] |
| List of Product Names (name) (override \_cprodname) | \[Array\] |
| List of Product Brands (brand) (override \_cbrand) | \[Array\] |
| List of Product Categories (category) (override \_ccat) | \[Array\] |
| List of Product Coupons (coupon) | \[Array\] |
| List of Product Prices (price) (override \_cprice) | \[Array\] |
| List of Product Quantities (quantity) (override \_cquan) | \[Array\] |
| List of Product Positions (position) | \[Array\] |
| List of Product Variants (variant) | \[Array\] |

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

| Variable | Description |
| --- | --- |
| Hit (Send Page View Event) (hit) | hit |
| View Product (detail) | detail |
| Add Product (add) | add |
| Remove Product (remove) | remove |
| Purchase (purchase) | purchase |

### Event-specific parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

| Variable | Description |
| --- | --- |
| Hit (hit) | hit |
| View Product (detail) | detail |
| Add Product (add) | add |
| Remove Product (remove) | remove |
| Purchase (purchase) | purchase |