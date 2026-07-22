---
title: Airship Web Notify Tag Setup Guide
description: This article describes how to set up the Airship Web Notify tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/airship-web-notify-tag/
---Web push notifications help you deliver relevant, personalized, in-the-moment messaging wherever your users are online. Airship’s Web Notify provides the tools necessary to reach new web visitors with powerful engagement strategies, encouraging repeat visits and driving conversion.

## Tag tips

* All of the tag configurations can be set dynamically with mappings.
* `secureIframeUrl` is only needed if Airship Web Notify is loading on non-securepages.
* Safari support requires additional configuration within [your Airship dashboard](https://docs.urbanairship.com/tutorials/getting-started/channels/web-notify/#safari).
* After Safari configuration make sure to download your new SDK bundle containing new keys and tokens.
* Supports these E-Commerce extension parameters:
  * Order ID (\_corder)
  * Order Subtotal (\_csubtotal)
  * List of Product IDs (\_cprod)
  * List of Brands (\_cbrand)
  * List of Categories (\_ccat)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **appKey**: Your Airship-provided appKey. This identifies which Airship project this web site is connected to.
* **Token**: Your Airship-provided token. This is the bearer token that authenticates actions taken by the JS SDK against Urban Airship's platform APIs.
* **vapidPublicKey**: Your Airship-provided `vapidPublicKey` . This is the public half of a cryptographic key pair used by the browser and browser vendor when registering for and sending notifications.
* **secureIframeUrl**: The URL of the iframe used by Airship for non-HTTPS pages so that the SDK can post messages to its parent window. This is only used for non-secure domains.
* **Auto Prompt Enabled**: Select true to automatically prompt the user to register for push notifications, allowing the push-worker.js file to handle the frequency with which visitors are prompted. If you select false, then you must manually trigger the prompt.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Tag Configurations

|Variable| Description|
|---| ---|
|appKey (app\_key)| [string]|
|vapidPublicKey (vapid\_public\_key)| [string]|
|Token (token)| [string]|
|secureIframeUrl (secure\_iframe\_url)| [string]|
|Auto Prompt Flag (auto\_prompt)| ["true"/"false"]|

### E-Commerce

|Variable| Description|
|---| ---|
|Is New Item (is\_new\_item)| ["true"/"false"]|
|List of Product Brands (product\_brand) (Overrides \_cbrand)| [Array]|
|List of Product Categories (product\_category) (Overrides \_ccat)| [Array]|
|List of Product Descriptions (product\_description)| [Array]|
|List of Product IDs (product\_id) (Overrides \_cprod)| [Array]|
|Transaction/Order ID (transaction\_id) (Overrides \_corder)| [String]|
|Value/Order Subtotal (value) (Overrides \_csubtotal)| [String]|

### Media

|Variable| Description|
|---| ---|
|Author (media\_author)| [String]|
|Category (media\_category)| [String]|
|Description (media\_description)| [String]|
|Feature (media\_feature)| ["true"/"false"]|
|Identifier (media\_identifier)| [String]|
|Published Date (media\_published\_date)| [String]|
|Type (media\_type)| [String]|

### Social Media

|Variable| Description|
|---| ---|
|Source (source)| [String]|
|Medium (medium)| [String]|

### Account

|Variable| Description|
|---| ---|
|Category (account\_category)| [String]|

### Events

|Variable| Description|
|---| ---|
|register| register|
|BrowsedContentEvent| BrowsedContentEvent|
|ConsumedContentEvent| ConsumedContentEvent|
|SharedContentEvent| SharedContentEvent|
|StarredContentEvent| StarredContentEvent|
|AddedToCartEvent| AddedToCartEvent|
|BrowsedEvent| BrowsedEvent|
|PurchasedEvent| PurchasedEvent|
|SharedProductEvent| SharedProductEvent|
|StarredProductEvent| StarredProductEvent|
|RegisterEvent| RegisterEvent|
|Custom| Custom|
