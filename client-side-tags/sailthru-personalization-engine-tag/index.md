---
title: Sailthru Personalization Engine Tag Setup Guide
description: This article describes how to set up the Sailthru Personalization Engine tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/sailthru-personalization-engine-tag/
---
## Tag tips

* Use mapping to:
  * Dynamically override standard configuration values
  * Set optional Personalization Engine configuration parameters. ([Learn more](https://getstarted.sailthru.com/site/personalization-engine/pe-setup/))
  * Dynamically add Sailthru meta tags to your site
  * Configure event triggers (including custom events)
  * Send required and optional event parameters

* Supports these E-Commerce extension parameters:
  * Order ID
  * Customer ID
  * List of Product IDs
  * List of Product Names
  * List of Product Quantities
  * List of Product Prices

* For a list of required and optional event parameters, see Sailthru's JavaScript API Library documentation here: [Sailthru JavaScript API Library](https://getstarted.sailthru.com/developers/api-client/javascript/)

## Tag configuration

First, go to Tealium's tag marketplace and add the Sailthru Personalization Engine tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Customer ID**
  * Your Sailthru Customer ID.

* **Pageview Tracking**
  * Manual page view tracking requires a mapping to Pageview URL (`pageview.url`) for the page being tracked.
  * Use data mapping to set additional optional parameters.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`init.customerId`|  <ul><li>Sailthru Customer ID</li></ul> |
|`pageviewTracking`|  <ul><li>Pageview Tracking</li><li>Options are **automatic** or **manual**.</li></ul> |
|`init.isCustom`|  <ul><li>Options are `true` or `false`.</li></ul> |
|`init.useStoredTags`|  <ul><li>Options are `true` or `false`.</li></ul> |
|`init.excludeContent`|  <ul><li>Options are `true` or `false`.</li></ul> |
|`pageview.url`|  <ul><li>Pageview URL</li></ul> |
|`pageview.tags`|  <ul><li>Pageview Tags</li></ul> |
|`pageview.onSuccess`|  <ul><li>Callback Function Name</li><li>Pageview onSuccess</li></ul> |
|`pageview.onError`|  <ul><li>Callback Function Name</li><li>Pageview onError</li></ul> |
|`meta.custom`|  <ul><li>Custom Meta Tag</li></ul> |

#### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order ID</li><li>Overrides `_corder`.</li></ul> |
|`customer_id`|  <ul><li>Customer ID</li><li>Overrides `_ccustid`.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of Product IDs</li><li>Overrides `_cprod`.</li></ul> |
|`product_name`|  <ul><li>Array</li><li>List of Product Names</li><li>Overrides `_cprodname`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Product Quantities</li><li>Overrides `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Product Prices</li><li>Overrides `_cprice`.</li></ul> |

#### Event Trigger

|Variable| Description|
|---| ---|
|`userSignUp`|  <ul><li>User Sign Up</li></ul> |
|`userSignUpConfirmedOptIn`|  <ul><li>User Sign Up Opt In Confirmed</li></ul> |
|`addToCart`|  <ul><li>Add to Cart</li></ul> |
|`purchase`|  <ul><li>Purchase</li></ul> |
|`customEvent`|  <ul><li>Custom Event</li></ul> |

#### Event Data: userSignUp

|Variable| Description|
|---| ---|
|`userSignUp.email`|  <ul><li>String</li><li>User Email</li><li>Overrides E-Commerce Customer ID</li></ul> |
|`userSignUp.id`|  <ul><li>String</li><li>User ID</li></ul> |
|`userSignUp.key`|  <ul><li>String</li><li>User ID Type</li></ul> |
|`userSignUp.lists`|  <ul><li>Object</li><li>Lists</li></ul> |
|`userSignUp.vars`|  <ul><li>Object</li><li>Vars</li></ul> |
|`userSignUp.source`|  <ul><li>String</li><li>Acquisition Source</li></ul> |
|`userSignUp.onSuccess`|  <ul><li>String</li><li>On Success Callback Function Name</li></ul> |
|`userSignUp.onError`|  <ul><li>String</li><li>On Error Callback Function Name</li></ul> |

#### Event Data: userSignUpConfirmedOptIn

|Variable| Description|
|---| ---|
|`userSignUpConfirmedOptIn.email`|  <ul><li>String</li><li>User Email</li><li>Overrides E-Commerce Customer ID.</li></ul> |
|`userSignUpConfirmedOptIn.id`|  <ul><li>String</li><li>User ID</li></ul> |
|`userSignUpConfirmedOptIn.key`|  <ul><li>String</li><li>User ID Type</li></ul> |
|`userSignUpConfirmedOptIn.template_name`|  <ul><li>String</li><li>Opt-In Template Name</li></ul> |
|`userSignUpConfirmedOptIn.template_vars`|  <ul><li>Object</li><li>Opt-In Template Vars</li></ul> |
|`userSignUpConfirmedOptIn.vars`|  <ul><li>Object</li><li>Vars</li></ul> |
|`userSignUpConfirmedOptIn.source`|  <ul><li>String</li><li>Acquisition Source</li></ul> |
|`userSignUpConfirmedOptIn.onSuccess`|  <ul><li>String</li><li>On Success Callback Function Name</li></ul> |
|`userSignUpConfirmedOptIn.onError`|  <ul><li>String</li><li>On Error Callback Function Name</li></ul> |

#### Event Data: addToCart

|Variable| Description|
|---| ---|
|`addToCart.email`|  <ul><li>String</li><li>User Email</li><li>Overrides E-Commerce Customer ID</li></ul> |
|`addToCart.reminder_time`|  <ul><li>String</li><li>Reminder Time</li></ul> |
|`addToCart.reminder_template`|  <ul><li>String</li><li>Reminder Template</li></ul> |
|`product_url`|  <ul><li>Array</li><li>List of Product URLs</li></ul> |
|`product_images`|  <ul><li>Array of Objects</li><li>List of Product Images</li></ul> |
|`product_vars`|  <ul><li>Array of Objects</li><li>List of Product Vars</li></ul> |
|`addToCart.vars`|  <ul><li>Object</li><li>Vars</li></ul> |
|`addToCart.onSuccess`|  <ul><li>String</li><li>On Success Callback Function Name</li></ul> |
|`addToCart.onError`|  <ul><li>String</li><li>On Error Callback Function Name</li></ul> |

#### Event Data: purchase

|Variable| Description|
|---| ---|
|`purchase.email`|  <ul><li>String</li><li>User Email</li><li>Overrides E-Commerce Customer ID.</li></ul> |
|`product_url`|  <ul><li>Array</li><li>List of Product URLs</li></ul> |
|`product_images`|  <ul><li>Array of Objects</li><li>List of Product Images</li></ul> |
|`product_vars`|  <ul><li>Array of Objects</li><li>List of Product Vars</li></ul> |
|`purchase.vars`|  <ul><li>Object</li><li>Vars</li></ul> |
|`purchase.onSuccess`|  <ul><li>String</li><li>On Success Callback Function Name</li></ul> |
|`purchase.onError`|  <ul><li>String</li><li>On Error Callback Function Name</li></ul> |

#### Event Data: customEvent

|Variable| Description|
|---| ---|
|`customEvent.name`|  <ul><li>String</li><li>Event Name</li></ul> |
|`customEvent.email`|  <ul><li>String</li><li>User Email</li><li>Overrides E-Commerce Customer ID.</li></ul> |
|`customEvent.id`|  <ul><li>String</li><li>User ID</li></ul> |
|`customEvent.key`|  <ul><li>String</li><li>User ID Type</li></ul> |
|`customEvent.vars`|  <ul><li>Object</li><li>Vars</li></ul> |
|`customEvent.onSuccess`|  <ul><li>String</li><li>On Success Callback Function Name</li></ul> |
|`customEvent.onError`|  <ul><li>String</li><li>On Error Callback Function Name</li></ul> |
