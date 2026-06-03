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

* For a list of required and optional event parameters, see Sailthru&#39;s JavaScript API Library documentation here: [Sailthru JavaScript API Library](https://getstarted.sailthru.com/developers/api-client/javascript/)

## Tag configuration

First, go to Tealium&#39;s tag marketplace and add the Sailthru Personalization Engine tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Customer ID**
  * Your Sailthru Customer ID.

* **Pageview Tracking**
  * Manual page view tracking requires a mapping to Pageview URL (`pageview.url`) for the page being tracked.
  * Use data mapping to set additional optional parameters.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`init.customerId`|  &lt;ul&gt;&lt;li&gt;Sailthru Customer ID&lt;/li&gt;&lt;/ul&gt; |
|`pageviewTracking`|  &lt;ul&gt;&lt;li&gt;Pageview Tracking&lt;/li&gt;&lt;li&gt;Options are **automatic** or **manual**.&lt;/li&gt;&lt;/ul&gt; |
|`init.isCustom`|  &lt;ul&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`init.useStoredTags`|  &lt;ul&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`init.excludeContent`|  &lt;ul&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`pageview.url`|  &lt;ul&gt;&lt;li&gt;Pageview URL&lt;/li&gt;&lt;/ul&gt; |
|`pageview.tags`|  &lt;ul&gt;&lt;li&gt;Pageview Tags&lt;/li&gt;&lt;/ul&gt; |
|`pageview.onSuccess`|  &lt;ul&gt;&lt;li&gt;Callback Function Name&lt;/li&gt;&lt;li&gt;Pageview onSuccess&lt;/li&gt;&lt;/ul&gt; |
|`pageview.onError`|  &lt;ul&gt;&lt;li&gt;Callback Function Name&lt;/li&gt;&lt;li&gt;Pageview onError&lt;/li&gt;&lt;/ul&gt; |
|`meta.custom`|  &lt;ul&gt;&lt;li&gt;Custom Meta Tag&lt;/li&gt;&lt;/ul&gt; |

#### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product Names&lt;/li&gt;&lt;li&gt;Overrides `_cprodname`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product Quantities&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product Prices&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |

#### Event Trigger

|Variable| Description|
|---| ---|
|`userSignUp`|  &lt;ul&gt;&lt;li&gt;User Sign Up&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn`|  &lt;ul&gt;&lt;li&gt;User Sign Up Opt In Confirmed&lt;/li&gt;&lt;/ul&gt; |
|`addToCart`|  &lt;ul&gt;&lt;li&gt;Add to Cart&lt;/li&gt;&lt;/ul&gt; |
|`purchase`|  &lt;ul&gt;&lt;li&gt;Purchase&lt;/li&gt;&lt;/ul&gt; |
|`customEvent`|  &lt;ul&gt;&lt;li&gt;Custom Event&lt;/li&gt;&lt;/ul&gt; |

#### Event Data: userSignUp

|Variable| Description|
|---| ---|
|`userSignUp.email`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User Email&lt;/li&gt;&lt;li&gt;Overrides E-Commerce Customer ID&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User ID&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.key`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User ID Type&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.lists`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Lists&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.vars`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Vars&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.source`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Acquisition Source&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.onSuccess`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;On Success Callback Function Name&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.onError`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;On Error Callback Function Name&lt;/li&gt;&lt;/ul&gt; |

#### Event Data: userSignUpConfirmedOptIn

|Variable| Description|
|---| ---|
|`userSignUpConfirmedOptIn.email`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User Email&lt;/li&gt;&lt;li&gt;Overrides E-Commerce Customer ID.&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User ID&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.key`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User ID Type&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.template_name`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Opt-In Template Name&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.template_vars`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Opt-In Template Vars&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.vars`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Vars&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.source`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Acquisition Source&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.onSuccess`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;On Success Callback Function Name&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.onError`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;On Error Callback Function Name&lt;/li&gt;&lt;/ul&gt; |

#### Event Data: addToCart

|Variable| Description|
|---| ---|
|`addToCart.email`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User Email&lt;/li&gt;&lt;li&gt;Overrides E-Commerce Customer ID&lt;/li&gt;&lt;/ul&gt; |
|`addToCart.reminder_time`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Reminder Time&lt;/li&gt;&lt;/ul&gt; |
|`addToCart.reminder_template`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Reminder Template&lt;/li&gt;&lt;/ul&gt; |
|`product_url`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product URLs&lt;/li&gt;&lt;/ul&gt; |
|`product_images`|  &lt;ul&gt;&lt;li&gt;Array of Objects&lt;/li&gt;&lt;li&gt;List of Product Images&lt;/li&gt;&lt;/ul&gt; |
|`product_vars`|  &lt;ul&gt;&lt;li&gt;Array of Objects&lt;/li&gt;&lt;li&gt;List of Product Vars&lt;/li&gt;&lt;/ul&gt; |
|`addToCart.vars`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Vars&lt;/li&gt;&lt;/ul&gt; |
|`addToCart.onSuccess`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;On Success Callback Function Name&lt;/li&gt;&lt;/ul&gt; |
|`addToCart.onError`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;On Error Callback Function Name&lt;/li&gt;&lt;/ul&gt; |

#### Event Data: purchase

|Variable| Description|
|---| ---|
|`purchase.email`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User Email&lt;/li&gt;&lt;li&gt;Overrides E-Commerce Customer ID.&lt;/li&gt;&lt;/ul&gt; |
|`product_url`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product URLs&lt;/li&gt;&lt;/ul&gt; |
|`product_images`|  &lt;ul&gt;&lt;li&gt;Array of Objects&lt;/li&gt;&lt;li&gt;List of Product Images&lt;/li&gt;&lt;/ul&gt; |
|`product_vars`|  &lt;ul&gt;&lt;li&gt;Array of Objects&lt;/li&gt;&lt;li&gt;List of Product Vars&lt;/li&gt;&lt;/ul&gt; |
|`purchase.vars`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Vars&lt;/li&gt;&lt;/ul&gt; |
|`purchase.onSuccess`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;On Success Callback Function Name&lt;/li&gt;&lt;/ul&gt; |
|`purchase.onError`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;On Error Callback Function Name&lt;/li&gt;&lt;/ul&gt; |

#### Event Data: customEvent

|Variable| Description|
|---| ---|
|`customEvent.name`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Event Name&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.email`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User Email&lt;/li&gt;&lt;li&gt;Overrides E-Commerce Customer ID.&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User ID&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.key`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User ID Type&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.vars`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Vars&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.onSuccess`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;On Success Callback Function Name&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.onError`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;On Error Callback Function Name&lt;/li&gt;&lt;/ul&gt; |
