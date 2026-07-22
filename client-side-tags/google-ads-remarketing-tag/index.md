---
title: Google Ads Remarketing Tag Setup Guide
description: This article describes setting up the Google Ads Remarketing tag in Tealium iQ Tag Management and how to use the Chrome Google Tag Assistant extension to check if custom parameters are being captured.
url: https://docs.tealium.com/client-side-tags/google-ads-remarketing-tag/
---
## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Conversion ID**
  * Enter the value of the `google_conversion_id`.
  * This value is provided in your code snippet and also available in your Ads control panel.
* **Page Type**
  * Select the page type of your site where you are tracking conversions with this tag instance.
  * This is also the value of the custom `ecomm_pagetype` parameter in your code snippet.
* **Conversion Value**
  * Enter a value that you want to assign to the conversion action.
  * You can leave this field blank if you prefer to use the order subtotal value or otherwise set it dynamically with the Data Mapping toolbox.


<blockquote>
Optionally, set all of the above settings in the Data Mappings toolbox.
</blockquote>


## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/about-data-mappings/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

### Standard

Map to these destinations for dynamically sending (or overriding) the values under tag settings.

The following table describes destination names and descriptions for Standard variables.

|Destination Name| Description|
|---| ---|
| Conversion ID `google_conversion_id` |  <ul><li>Value of the `google_conversion_id` parameter.</li></ul> |
|Conversion Label|  <ul><li>Set a default label here and use mapping to dynamically override this value.</li><li>Use a comma-separated list to send data for multiple labels.</li><li>This list can use a matching number of Conversion Labels as Conversion IDs or use a single label for all Conversion IDs.</li></ul> |
|Conversion Value (value)|  <ul><li>Set a default value here or leave this blank to use the Subtotal value from the E-Commerce extension.</li><li>Use mapping to dynamically override this value and the E-Commerce extension value.</li><li>When you use conversion tracking, you can assign the same value to all conversion actions of a certain type (a static value) or let a conversion action have different values (dynamic, representing transaction-specific values).</li><li>If you assign values to your conversions, you will be able to distinguish the total value driven by your advertising across different conversions and be able to identify and focus on high-value conversions.</li><li>If you leave this field empty, the tag will auto-fill using the E-commerce value for subtotal ( `_csubtotal`).</li></ul> |
|Global Object|  <ul><li>The name of the Global Object used for the event queue.</li><li>If not specified, "gtag" is used.</li><li>Not required for most implementations.</li></ul> |
|Data Layer Name|  <ul><li>By default, the data layer initiated and referenced by the global site tag is named **dataLayer**.</li><li>Rename the data layer only if your project requires a separate name.</li></ul> |
|Enable Remarketing|  <ul><li>Values are **On** or **Off**.</li><li>Default value is **Off**.</li><li>When Remarketing is enabled, this tag will automatically pull in data from the E-Commerce Extension to populate the Google Ads "Retail" parameters (prefix `ecomm_`).</li><li>Mapping directly to the "Retail" tab in the toolbox will override the data pulled in through the E-Commerce Extension.</li></ul> |
| Page Type `pagetype` |  <ul><li>Type of page where you are tracking conversions.</li><li>Select a default page type here and use mapping to dynamically override this value.</li></ul> |
|Cross-Tracking Domains|  <ul><li>A comma-separated list of domains to use with Cross-Domain Tracking (setAllowLinker).</li><li>Should be the top level domain, such as "tealiumiq.com".</li></ul> |
|Custom|  <ul><li>You may define customized parameters not predefined by Google Ads.</li><li>See "Advanced" below for more information.</li></ul> |

### Retail

We recommend setting up the [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) for this tag since it will automatically send the necessary product and order details to the appropriate Ads parameters. You also have the option to override the Extension variables with a mapping.

The following table describes destination names and descriptions for Retail variables.

|Destination Name| Description|
|---| ---|
|`ecomm.prodid`|  <ul><li>(Required) This is the product ID of the product or products displayed on the current page - the IDs used here should match the IDs in your feed.</li><li>When using the E-commerce extension, mapping this parameter overrides `_cprod`.</li></ul> |
|`ecomm.totalvalue`|  <ul><li>This parameter should be used on product, cart and purchase page types and should contain the value of a single product on product pages, or the total sum of the values of one or more products on the cart and purchase pages.</li></ul> |
|`ecomm.category`|  <ul><li>This parameter contains the category of the currently viewed product or category pages.</li><li>When using the E-commerce extension, this parameter overrides `_ccat`.</li></ul> |
|`ecomm.pagetype`|  <ul><li>Recommended.</li><li>Indicates the type of page that the tag is on.</li><li>Use one of the following values:</li> <ul><li>`home`</li><li>`searchresults`</li><li>`category`</li><li>`product`</li><li>`cart`</li><li>`purchase`</li></ul> <ul><li>`other` Used when your page does not fit into the page types listed above, for example, a "Contact Us" or "About Us" page.</li></ul> <li>If you choose to include this parameter, map your data source to `ecomm.pagetype`.</li></ul> |
|`ecomm.value`|  <ul><li>Deprecated.</li><li>This parameter is no longer used by Google Ads for this Remarketing tag.</li></ul> |
|`ecomm.quantity`|  <ul><li>Deprecated.</li><li>This parameter is no longer used by Google Ads for this Remarketing tag.</li></ul> |
|`Custom`|  <ul><li>You may define customized parameters not predefined by Google Ads.</li><li>See "Advanced" below for more information.</li></ul> |

### Education

The following table describes destination names and descriptions for Education variables.

|Destination Name| Description|
|---| ---|
|`edu.pid`|  <ul><li>(Required) This parameter is the ID of the program that the visitor is currently viewing on either the program or lead page types.</li><li>This ID must match a value in the "Education Program" in your feed.</li></ul> |
|`edu.plocid`|  <ul><li>This parameter is the ID for the location of the program that the user is currently viewing on either the program or lead page types.</li><li>This ID must match a value in the "Location ID" in your feed.</li></ul> |
|`edu.pagetype`|  <ul><li>Recommended.</li><li>Indicates the type of page that the tag is on.</li><li>Use one of the following values:</li> <ul><li>`home`</li><li>`searchresults`</li><li>`program`</li><li>`lead`</li><li>`complete` or</li></ul> <ul><li>`other` Used when your page does not fit into the page types listed above, for example, a "Contact Us" or "About Us" page.</li></ul> <li>If you choose to include this parameter map your data source to `edu.pagetype`.</li></ul> |

### Flights

The following table describes destination names and descriptions for Flights variables.

|Destination Name| Description|
|---| ---|
|`flight.originid`|  <ul><li>This parameter is the origin of the flight itinerary being viewed on search results, cart and purchase page types.</li><li>This ID must match a value in your feed though Google recommends you use three-letter airport codes.</li></ul> |
|`flight.destid`|  <ul><li>(Required) This parameter is the destination of the flight itinerary being viewed on search results, cart and purchase page types.</li><li>This ID must match a value in your feed though Google recommends you use three-letter airport codes.</li></ul> |
|`flight.totalvalue`|  <ul><li>This parameter should be used on the cart and purchase page type and should contain the total value of the flight itinerary.</li><li>Do not include any currency symbols.</li></ul> |
|`flight.startdate`|  <ul><li>The date when the flight itinerary starts.</li><li>Should be in the `YYYY-MM-DD` format.</li></ul> |
|`flight.enddate`|  <ul><li>The date when the flight itinerary ends.</li><li>Should be in the `YYYY-MM-DD` format.</li></ul> |
|`flight.pagetype`|  <ul><li>Recommended.</li><li>Indicates the type of page that the tag is on.</li><li>Use one of the following values:  <ul><li>`home`</li><li>`searchresults`</li><li>`offerdetail`</li><li>`cart`</li><li>`purchase`</li><li>`cancel` or</li><li>`other` Used when your page does not fit into the page types listed above, for example, a "Contact Us" or "About Us" page.</li></ul> </li><li>If you choose to include this parameter map your data source to `flight.pagetype`.</li></ul> |

### Hotels and rental

The following table describes destination names and descriptions for Hotels and Rental variables.

|Destination Name| Description|
|---| ---|
|`hrental.id`|  <ul><li>(Required) This parameter is the ID of the hotel or rental property that the visitor is currently viewing on the property page type.</li><li>This ID must match a value in your feed.</li></ul> |
|`hrental.startdate`|  <ul><li>The date when the booking is to begin.</li><li>Should be in the `YYYY-MM-DD` format.</li></ul> |
|`hrental.enddate`|  <ul><li>The date when the booking is to end.</li><li>Should be in the `YYYY-MM-DD` format.</li></ul> |
|`hrental.totalvalue`|  <ul><li>This parameter should be used on the conversion intent and conversion page types and should contain the total sum of the values of all properties in the visitor's cart.</li><li>Do not include any currency symbols.</li></ul> |
|`hrental.pagetype`|  <ul><li>Recommended.</li><li>Indicates the type of page that the tag is on.</li><li>Use one of the following values:  <ul><li>`home`</li><li>`searchresults`</li><li>`offerdetail`</li><li>`conversionintent`</li><li>`conversion` or</li><li>`other` Used when your page does not fit into the page types listed above, for example, a "Contact Us" or "About Us" page.</li></ul> </li></ul> <ul><li>If you choose to include this parameter map your data source to `hrental.pagetype.`</li></ul> |

### Jobs

The following table describes destination names and descriptions for Jobs variables.

|Destination Name| Description|
|---| ---|
|`job.id`|  <ul><li>(Required) This parameter is the ID of the job opening being viewed on `searchresults`, `offerdetail`, `conversionintent` and `conversion` page types.</li><li>This ID must match a value in your feed.</li></ul> |
|`job.locid`|  <ul><li>This parameter represents a location ID or name and is used as a secondary matching key in your feed allowing for multiple job\_ids of the same value, but using separate location IDs and should be present on search results, offer detail, conversion intent and conversion page types.</li></ul> |
|`job.totalvalue`|  <ul><li>This parameter should be used on the conversion intent and conversion page types and should contain the total value of the job listings that the user has selected.</li><li>Do not include any currency symbols.</li></ul> |
|`job.pagetype`|  <ul><li>Recommended.</li><li>Indicates the type of page that the tag is on.</li><li>Use one of the following values:  <ul><li>`home`</li><li>`searchresults`</li><li>`offerdetail`</li><li>`conversionintent` or</li><li>`other` Used when your page does not fit into the page types listed above, for example, a "Contact Us" or "About Us" page.</li></ul> </li><li>If you choose to include this parameter map your data source to `job.pagetype.`</li></ul> |

### Local

The following table describes destination names and descriptions for Local variables.

|Destination Name| Description|
|---| ---|
|`local.id`|  <ul><li>(Required) This parameter is the ID of the offer or deal being viewed on search results, offer detail, conversion intent and conversion page types.</li><li>This ID must match a value in your feed.</li></ul> |
|`local.totalvalue`|  <ul><li>This parameter should be used on the conversion intent and conversion page types and should contain the total value of the offer or offers that the user has purchased.</li><li>Do not include any currency symbols.</li></ul> |
|`local.pagetype`|  <ul><li>Recommended.</li><li>Indicates the type of page that the tag is on.</li><li>Use one of the following values:  <ul><li>`home`</li><li>`searchresults`</li><li>`offerdetail`</li><li>`conversionintent`</li><li>`conversion` or</li><li>`other` Used when your page does not fit into the page types listed above, for example, a "Contact Us" or "About Us" page.</li></ul> </li><li>If you choose to include this parameter map your data source to `local.pagetype`.</li></ul> |

### Real estate

The following table describes destination names and descriptions for Real Estate variables.

|Destination Name| Description|
|---| ---|
|`listing.id`|  <ul><li>(Required) This parameter is the ID of the property being viewed on search results, offer detail, conversion intent and conversion page types.</li><li>This ID must match a value in your feed.</li></ul> |
|`listing.totalvalue`|  <ul><li>This parameter should be used on the conversion intent and conversion page types and should contain the total value of the property</li><li>Do not include any currency symbols.</li></ul> |
|`listing.pagetype`|  <ul><li>Recommended.</li><li>Indicates the type of page that the tag is on.</li><li>Use one of the following values:  <ul><li>`home`</li><li>`searchresults`</li><li>`offerdetail`</li><li>`conversionintent`</li><li>`conversion` or</li><li>`other` Used when your page does not fit into the page types listed above, for example, a "Contact Us" or "About Us" page.</li></ul> </li><li>If you choose to include this parameter map your data source to `listing.pagetype`.</li></ul> |

### Travel

The following table describes destination names and descriptions for Travel variables.

|Destination Name| Description|
|---| ---|
|`travel.destid`|  <ul><li>(Required) This parameter is the ID of the travel destination being viewed on search results, conversion intent and conversion page types.</li><li>This ID must match a value in your feed.</li></ul> |
|`travel.originid`|  <ul><li>(Optional) This parameter is the ID of the travel origin location being viewed on search results, conversion intent and conversion page types.</li><li>This value is used as a secondary matching key in your feed and does not need to represent anything, but Google recommends that you use three-letter airport codes or two-letter country codes.</li></ul> |
|`travel.startdate`|  <ul><li>The date when the travel itinerary starts.</li><li>Should be in the `YYYY-MM-DD` format.</li></ul> |
|`travel.enddate`|  <ul><li>The date when the travel itinerary ends.</li><li>Should be in the `YYYY-MM-DD` format.</li></ul> |
|`travel.totalvalue`|  <ul><li>This parameter should be used on the conversion intent and conversion page types and should contain the total value of the travel itinerary.</li><li>Do not include any currency symbols.</li></ul> |
|`travel.pagetype`|  <ul><li>Recommended.</li><li>Indicates the type of page that the tag is on.</li><li>Use one of the following values:  <ul><li>`home`</li><li>`searchresults`</li><li>`offerdetail`</li><li>`conversionintent`</li><li>`conversion`</li><li>`cancel` or</li><li>`other` Used when your page does not fit into the page types listed above, for example, a "Contact Us" or "About Us" page.</li></ul> </li><li>If you choose to include this parameter map your data source to `travel.pagetype`.</li></ul> |

### Phone conversion options

Use phone call conversion tracking to help you see how effectively your ads lead to phone calls from your website. When someone visits your website after clicking one of your ads, website call conversion tracking can help you identify and measure calls from your site. This kind of conversion tracking tracks a call as a conversion when it lasts longer than a minimum length you set

The following table describes destination names and descriptions for Phone Conversion option variables.

|Destination Name| Description|
|---| ---|
|`phone_conversion_number`|  <ul><li>(Required) In the following example, replace "REPLACE WITH VALUE" with your business phone number. </li><li>Ensure that the number matches the number on your page exactly and includes any relevant country codes.</li></ul> |
|`phone_conversion_css_class`|  <ul><li>(Required) Enter a CSS class name.</li><li>All elements of that class will have their contents replaced with a formatted telephone number.</li></ul> |

### Other

The following table describes destination names and descriptions for variables categorized as "Other".

|Destination Name| Description|
|---| ---|
|`dynx.itemid`|  <ul><li>(Required) This parameter is the ID of the product being viewed on search results, offer detail, conversion intent and conversion page types.</li><li>This ID must match a value in your feed.</li></ul> |
|`dynx.itemid2`|  <ul><li>(Optional) This parameter is the secondary ID of the product being viewed on search results, offer detail, conversion intent and conversion page types.</li><li>This ID must match a value in your feed.</li></ul> |
|`dynx.totalvalue`|  <ul><li>This parameter should be used on the conversion intent page type and should contain the total value of the products that the visitor has purchased.</li><li>Do not include any currency symbols.</li></ul> |
|`dynx.pagetype`|  <ul><li>Recommended.</li><li>Indicates the type of page that the tag is on. Use one of the following values:</li> <ul><li>`home`</li><li>`searchresults`</li><li>`offerdetail`</li><li>`conversionintent`</li><li>`conversion`</li><li>`cancel`</li></ul> <ul><li>`other` Used when your page does not fit into the page types listed above, for example, a "Contact Us" or "About Us" page.</li></ul> <li>If you choose to include this parameter map your data source to `dynx.pagetype`.</li></ul> |

### Advanced

The following table describes destination names and descriptions for Advanced variables.

|Destination Name| Description|
|---| ---|
|Recommended Product IDs `custom.ecomm_rec_prodid`|  <ul><li>This parameter may be used to pass product IDs of recommended products on the page.</li></ul> |
|Visitor's Age `custom.a`|  <ul><li>This parameter may be used to pass a visitor's age.</li></ul> |
|Visitor's Gender `custom.g`|  <ul><li>This parameter may be used to pass a visitor's gender.</li></ul> |
|Visitor Has Account `custom.hasaccount`|  <ul><li>This parameter may be used to indicate if the visitor has an account.</li></ul> |
|Customer Quality Score `custom.cqs`|  <ul><li>This parameter can be used to report a visitor's customer quality score.</li></ul> |
|Repeat Purchaser`custom.rp`|  <ul><li>This parameter can be used to identify if the visitor is a repeat purchaser.</li></ul> |
| Visitor Loyalty Score `custom.ly` |  <ul><li>This parameter is used to identify the visitor's loyalty score.</li></ul> |
|Visitor High Spender Score `custom.hs`|  <ul><li>This parameter is used to identify the visitor's high spender score.</li></ul> |
|Custom `custom.myvar`|  <ul><li>This parameter can be used to pass any customized parameters.</li><li>Replace `myvar` with your own parameter name.</li></ul> |

### E-Commerce

This tag automatically pulls in data from the E-Commerce extension to populate the following retail parameters: 

* `ecomm.prodid` from `_cprod`
* `ecomm.category` from `_ccat`
* `ecomm.totalvalue` from `_csubtotal` when `_corder` is present or one of the page types includes `purchase`, `conversion`, `cart`, or `conversionintent`.

The following table describes destination names and descriptions for E-Commerce variables.

|Destination Name| Description|
|---| ---|
|Order ID `_corder`|  <ul><li>Represents the unique identifier assigned to the final order.</li><li>One advantage of using Ecommerce parameters is the tag will automatically use `_csubtotal` for the total value for any business type you configure.</li><li>For example, for the Retail business type, the value of `ecomm.totalvalue` will use `_csubtotal`.</li></ul> |
|Sub Total (`_csubtotal`)|  <ul><li>Represents the sub total amount of the final order.</li><li>The value within `_csubtotal` will automatically use `_csubtotal` for the total value for any business type being reported.</li><li>For example, for the Retail business type, the value of `ecomm.totalvalue` will use `_csubtotal`.</li></ul> |
|List of Product IDs `_cprod`|  <ul><li>Represents the unique identifier of each product in the product array.</li><li>When present, a custom parameter ecomm.prodid will contain the contents of `_cprod`.</li></ul> |
|List of Categories `_ccat`|  <ul><li>Represents the category of each product in the product array.</li><li>When present, a custom parameter ecomm.category will contain the contents of `_ccat`.</li></ul> |
|List of Quantities `_cquan`|  <ul><li>Represents the quantity of each product in the product array.</li><li>When present, a custom parameter ecomm.quantity will contain the contents of `_cquan`.</li></ul> |
|List of Prices `_cprice`|  <ul><li>Represents the product unit price of each product in the product array.</li><li>When present, a custom parameter ecomm.pvalue will contain the contents of `_cprice`.</li></ul> |
|Currency `_ccurrency`|  <ul><li>Represents the currency of the prices in the product array.</li><li>When present, a custom parameter ecomm.currency will contain the contents of `_ccurrency`.</li></ul> |
|List of Discounts `product_discount`|  <ul><li>Represents the product unit discount of each product in the product array.</li><li>When present, a custom parameter ecomm.discount will contain the contents of `_cdisc`.</li></ul> |

## Verifying the tag

You will need the Chrome Web browser to use [Google Tag Assistant](https://support.google.com/tagassistant/answer/2947093?hl=en&ref_topic=6000196). If the browser is already installed on your computer, install the Google Tag Assistant from the [Google Chrome Store](https://chrome.google.com/webstore/detail/tag-assistant-by-google/kejbdjndbnbjgmefkgdddjlbokphdefk). Once successfully installed, follow these steps:

1. Go to your site and open the target page.
1. Click on the assistant icon at the top right corner in your browser.
1. Click **Check this page now**.  
![](https://docs.tealium.com/images/client-side-tags/test-page.png)

<blockquote>
The color indicator on the icon may display red instead of green since you are implementing the tag through Tealium and not the traditional way.
</blockquote>

 Once the Tag Assistant runs, you will be able to see the values being populated. The following sample use case shows testing the homepage. In the example, you will notice the request is 'working' and the data sources are being grabbed. Also note that the `ecomm_pagetype` is populated with a value of `home`, but, `ecomm_value` and `ecomm_prodid` are not populated because the homepage does not contain those values.  
![](https://docs.tealium.com/images/client-side-tags/home-page.png)The following example shows how Tag Assistant looks for Product Detail pages.  
![](https://docs.tealium.com/images/client-side-tags/product-detail.png)

## Vendor documentation

For additional information, see the following vendor documentation:

* [Google Ads Help](https://support.google.com/adwords#topic=3119071)
* [Tagging your site for dynamic retargeting](https://support.google.com/adwords/answer/3103357)
* [About conversion values](https://support.google.com/adwords/answer/3419241?hl=en)
* [Dynamic Remarketing Parameters](https://developers.google.com/adwords-remarketing-tag/parameters)
