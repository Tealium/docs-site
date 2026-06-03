---
title: Google Ads Remarketing Tag Setup Guide
description: This article describes setting up the Google Ads Remarketing tag in Tealium iQ Tag Management and how to use the Chrome Google Tag Assistant extension to check if custom parameters are being captured.
url: https://docs.tealium.com/client-side-tags/google-ads-remarketing-tag/
---
## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

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

Optionally, set all of the above settings in the Data Mappings toolbox.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

### Standard

Map to these destinations for dynamically sending (or overriding) the values under tag settings.

The following table describes destination names and descriptions for Standard variables.

|Destination Name| Description|
|---| ---|
| Conversion ID `google_conversion_id` |  &lt;ul&gt;&lt;li&gt;Value of the `google_conversion_id` parameter.&lt;/li&gt;&lt;/ul&gt; |
|Conversion Label|  &lt;ul&gt;&lt;li&gt;Set a default label here and use mapping to dynamically override this value.&lt;/li&gt;&lt;li&gt;Use a comma-separated list to send data for multiple labels.&lt;/li&gt;&lt;li&gt;This list can use a matching number of Conversion Labels as Conversion IDs or use a single label for all Conversion IDs.&lt;/li&gt;&lt;/ul&gt; |
|Conversion Value (value)|  &lt;ul&gt;&lt;li&gt;Set a default value here or leave this blank to use the Subtotal value from the E-Commerce extension.&lt;/li&gt;&lt;li&gt;Use mapping to dynamically override this value and the E-Commerce extension value.&lt;/li&gt;&lt;li&gt;When you use conversion tracking, you can assign the same value to all conversion actions of a certain type (a static value) or let a conversion action have different values (dynamic, representing transaction-specific values).&lt;/li&gt;&lt;li&gt;If you assign values to your conversions, you will be able to distinguish the total value driven by your advertising across different conversions and be able to identify and focus on high-value conversions.&lt;/li&gt;&lt;li&gt;If you leave this field empty, the tag will auto-fill using the E-commerce value for subtotal ( `_csubtotal`).&lt;/li&gt;&lt;/ul&gt; |
|Global Object|  &lt;ul&gt;&lt;li&gt;The name of the Global Object used for the event queue.&lt;/li&gt;&lt;li&gt;If not specified, &#34;gtag&#34; is used.&lt;/li&gt;&lt;li&gt;Not required for most implementations.&lt;/li&gt;&lt;/ul&gt; |
|Data Layer Name|  &lt;ul&gt;&lt;li&gt;By default, the data layer initiated and referenced by the global site tag is named **dataLayer**.&lt;/li&gt;&lt;li&gt;Rename the data layer only if your project requires a separate name.&lt;/li&gt;&lt;/ul&gt; |
|Enable Remarketing|  &lt;ul&gt;&lt;li&gt;Values are **On** or **Off**.&lt;/li&gt;&lt;li&gt;Default value is **Off**.&lt;/li&gt;&lt;li&gt;When Remarketing is enabled, this tag will automatically pull in data from the E-Commerce Extension to populate the Google Ads &#34;Retail&#34; parameters (prefix `ecomm_`).&lt;/li&gt;&lt;li&gt;Mapping directly to the &#34;Retail&#34; tab in the toolbox will override the data pulled in through the E-Commerce Extension.&lt;/li&gt;&lt;/ul&gt; |
| Page Type `pagetype` |  &lt;ul&gt;&lt;li&gt;Type of page where you are tracking conversions.&lt;/li&gt;&lt;li&gt;Select a default page type here and use mapping to dynamically override this value.&lt;/li&gt;&lt;/ul&gt; |
|Cross-Tracking Domains|  &lt;ul&gt;&lt;li&gt;A comma-separated list of domains to use with Cross-Domain Tracking (setAllowLinker).&lt;/li&gt;&lt;li&gt;Should be the top level domain, such as &#34;tealiumiq.com&#34;.&lt;/li&gt;&lt;/ul&gt; |
|Custom|  &lt;ul&gt;&lt;li&gt;You may define customized parameters not predefined by Google Ads.&lt;/li&gt;&lt;li&gt;See &#34;Advanced&#34; below for more information.&lt;/li&gt;&lt;/ul&gt; |

### Retail

We recommend setting up the [E-Commerce Extension]() for this tag since it will automatically send the necessary product and order details to the appropriate Ads parameters. You also have the option to override the Extension variables with a mapping.

The following table describes destination names and descriptions for Retail variables.

|Destination Name| Description|
|---| ---|
|`ecomm.prodid`|  &lt;ul&gt;&lt;li&gt;(Required) This is the product ID of the product or products displayed on the current page - the IDs used here should match the IDs in your feed.&lt;/li&gt;&lt;li&gt;When using the E-commerce extension, mapping this parameter overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`ecomm.totalvalue`|  &lt;ul&gt;&lt;li&gt;This parameter should be used on product, cart and purchase page types and should contain the value of a single product on product pages, or the total sum of the values of one or more products on the cart and purchase pages.&lt;/li&gt;&lt;/ul&gt; |
|`ecomm.category`|  &lt;ul&gt;&lt;li&gt;This parameter contains the category of the currently viewed product or category pages.&lt;/li&gt;&lt;li&gt;When using the E-commerce extension, this parameter overrides `_ccat`.&lt;/li&gt;&lt;/ul&gt; |
|`ecomm.pagetype`|  &lt;ul&gt;&lt;li&gt;Recommended.&lt;/li&gt;&lt;li&gt;Indicates the type of page that the tag is on.&lt;/li&gt;&lt;li&gt;Use one of the following values:&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`category`&lt;/li&gt;&lt;li&gt;`product`&lt;/li&gt;&lt;li&gt;`cart`&lt;/li&gt;&lt;li&gt;`purchase`&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;`other` Used when your page does not fit into the page types listed above, for example, a &#34;Contact Us&#34; or &#34;About Us&#34; page.&lt;/li&gt;&lt;/ul&gt; &lt;li&gt;If you choose to include this parameter, map your data source to `ecomm.pagetype`.&lt;/li&gt;&lt;/ul&gt; |
|`ecomm.value`|  &lt;ul&gt;&lt;li&gt;Deprecated.&lt;/li&gt;&lt;li&gt;This parameter is no longer used by Google Ads for this Remarketing tag.&lt;/li&gt;&lt;/ul&gt; |
|`ecomm.quantity`|  &lt;ul&gt;&lt;li&gt;Deprecated.&lt;/li&gt;&lt;li&gt;This parameter is no longer used by Google Ads for this Remarketing tag.&lt;/li&gt;&lt;/ul&gt; |
|`Custom`|  &lt;ul&gt;&lt;li&gt;You may define customized parameters not predefined by Google Ads.&lt;/li&gt;&lt;li&gt;See &#34;Advanced&#34; below for more information.&lt;/li&gt;&lt;/ul&gt; |

### Education

The following table describes destination names and descriptions for Education variables.

|Destination Name| Description|
|---| ---|
|`edu.pid`|  &lt;ul&gt;&lt;li&gt;(Required) This parameter is the ID of the program that the visitor is currently viewing on either the program or lead page types.&lt;/li&gt;&lt;li&gt;This ID must match a value in the &#34;Education Program&#34; in your feed.&lt;/li&gt;&lt;/ul&gt; |
|`edu.plocid`|  &lt;ul&gt;&lt;li&gt;This parameter is the ID for the location of the program that the user is currently viewing on either the program or lead page types.&lt;/li&gt;&lt;li&gt;This ID must match a value in the &#34;Location ID&#34; in your feed.&lt;/li&gt;&lt;/ul&gt; |
|`edu.pagetype`|  &lt;ul&gt;&lt;li&gt;Recommended.&lt;/li&gt;&lt;li&gt;Indicates the type of page that the tag is on.&lt;/li&gt;&lt;li&gt;Use one of the following values:&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`program`&lt;/li&gt;&lt;li&gt;`lead`&lt;/li&gt;&lt;li&gt;`complete` or&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;`other` Used when your page does not fit into the page types listed above, for example, a &#34;Contact Us&#34; or &#34;About Us&#34; page.&lt;/li&gt;&lt;/ul&gt; &lt;li&gt;If you choose to include this parameter map your data source to `edu.pagetype`.&lt;/li&gt;&lt;/ul&gt; |

### Flights

The following table describes destination names and descriptions for Flights variables.

|Destination Name| Description|
|---| ---|
|`flight.originid`|  &lt;ul&gt;&lt;li&gt;This parameter is the origin of the flight itinerary being viewed on search results, cart and purchase page types.&lt;/li&gt;&lt;li&gt;This ID must match a value in your feed though Google recommends you use three-letter airport codes.&lt;/li&gt;&lt;/ul&gt; |
|`flight.destid`|  &lt;ul&gt;&lt;li&gt;(Required) This parameter is the destination of the flight itinerary being viewed on search results, cart and purchase page types.&lt;/li&gt;&lt;li&gt;This ID must match a value in your feed though Google recommends you use three-letter airport codes.&lt;/li&gt;&lt;/ul&gt; |
|`flight.totalvalue`|  &lt;ul&gt;&lt;li&gt;This parameter should be used on the cart and purchase page type and should contain the total value of the flight itinerary.&lt;/li&gt;&lt;li&gt;Do not include any currency symbols.&lt;/li&gt;&lt;/ul&gt; |
|`flight.startdate`|  &lt;ul&gt;&lt;li&gt;The date when the flight itinerary starts.&lt;/li&gt;&lt;li&gt;Should be in the `YYYY-MM-DD` format.&lt;/li&gt;&lt;/ul&gt; |
|`flight.enddate`|  &lt;ul&gt;&lt;li&gt;The date when the flight itinerary ends.&lt;/li&gt;&lt;li&gt;Should be in the `YYYY-MM-DD` format.&lt;/li&gt;&lt;/ul&gt; |
|`flight.pagetype`|  &lt;ul&gt;&lt;li&gt;Recommended.&lt;/li&gt;&lt;li&gt;Indicates the type of page that the tag is on.&lt;/li&gt;&lt;li&gt;Use one of the following values:  &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`cart`&lt;/li&gt;&lt;li&gt;`purchase`&lt;/li&gt;&lt;li&gt;`cancel` or&lt;/li&gt;&lt;li&gt;`other` Used when your page does not fit into the page types listed above, for example, a &#34;Contact Us&#34; or &#34;About Us&#34; page.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;If you choose to include this parameter map your data source to `flight.pagetype`.&lt;/li&gt;&lt;/ul&gt; |

### Hotels and rental

The following table describes destination names and descriptions for Hotels and Rental variables.

|Destination Name| Description|
|---| ---|
|`hrental.id`|  &lt;ul&gt;&lt;li&gt;(Required) This parameter is the ID of the hotel or rental property that the visitor is currently viewing on the property page type.&lt;/li&gt;&lt;li&gt;This ID must match a value in your feed.&lt;/li&gt;&lt;/ul&gt; |
|`hrental.startdate`|  &lt;ul&gt;&lt;li&gt;The date when the booking is to begin.&lt;/li&gt;&lt;li&gt;Should be in the `YYYY-MM-DD` format.&lt;/li&gt;&lt;/ul&gt; |
|`hrental.enddate`|  &lt;ul&gt;&lt;li&gt;The date when the booking is to end.&lt;/li&gt;&lt;li&gt;Should be in the `YYYY-MM-DD` format.&lt;/li&gt;&lt;/ul&gt; |
|`hrental.totalvalue`|  &lt;ul&gt;&lt;li&gt;This parameter should be used on the conversion intent and conversion page types and should contain the total sum of the values of all properties in the visitor&#39;s cart.&lt;/li&gt;&lt;li&gt;Do not include any currency symbols.&lt;/li&gt;&lt;/ul&gt; |
|`hrental.pagetype`|  &lt;ul&gt;&lt;li&gt;Recommended.&lt;/li&gt;&lt;li&gt;Indicates the type of page that the tag is on.&lt;/li&gt;&lt;li&gt;Use one of the following values:  &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent`&lt;/li&gt;&lt;li&gt;`conversion` or&lt;/li&gt;&lt;li&gt;`other` Used when your page does not fit into the page types listed above, for example, a &#34;Contact Us&#34; or &#34;About Us&#34; page.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;If you choose to include this parameter map your data source to `hrental.pagetype.`&lt;/li&gt;&lt;/ul&gt; |

### Jobs

The following table describes destination names and descriptions for Jobs variables.

|Destination Name| Description|
|---| ---|
|`job.id`|  &lt;ul&gt;&lt;li&gt;(Required) This parameter is the ID of the job opening being viewed on `searchresults`, `offerdetail`, `conversionintent` and `conversion` page types.&lt;/li&gt;&lt;li&gt;This ID must match a value in your feed.&lt;/li&gt;&lt;/ul&gt; |
|`job.locid`|  &lt;ul&gt;&lt;li&gt;This parameter represents a location ID or name and is used as a secondary matching key in your feed allowing for multiple job\_ids of the same value, but using separate location IDs and should be present on search results, offer detail, conversion intent and conversion page types.&lt;/li&gt;&lt;/ul&gt; |
|`job.totalvalue`|  &lt;ul&gt;&lt;li&gt;This parameter should be used on the conversion intent and conversion page types and should contain the total value of the job listings that the user has selected.&lt;/li&gt;&lt;li&gt;Do not include any currency symbols.&lt;/li&gt;&lt;/ul&gt; |
|`job.pagetype`|  &lt;ul&gt;&lt;li&gt;Recommended.&lt;/li&gt;&lt;li&gt;Indicates the type of page that the tag is on.&lt;/li&gt;&lt;li&gt;Use one of the following values:  &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent` or&lt;/li&gt;&lt;li&gt;`other` Used when your page does not fit into the page types listed above, for example, a &#34;Contact Us&#34; or &#34;About Us&#34; page.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;If you choose to include this parameter map your data source to `job.pagetype.`&lt;/li&gt;&lt;/ul&gt; |

### Local

The following table describes destination names and descriptions for Local variables.

|Destination Name| Description|
|---| ---|
|`local.id`|  &lt;ul&gt;&lt;li&gt;(Required) This parameter is the ID of the offer or deal being viewed on search results, offer detail, conversion intent and conversion page types.&lt;/li&gt;&lt;li&gt;This ID must match a value in your feed.&lt;/li&gt;&lt;/ul&gt; |
|`local.totalvalue`|  &lt;ul&gt;&lt;li&gt;This parameter should be used on the conversion intent and conversion page types and should contain the total value of the offer or offers that the user has purchased.&lt;/li&gt;&lt;li&gt;Do not include any currency symbols.&lt;/li&gt;&lt;/ul&gt; |
|`local.pagetype`|  &lt;ul&gt;&lt;li&gt;Recommended.&lt;/li&gt;&lt;li&gt;Indicates the type of page that the tag is on.&lt;/li&gt;&lt;li&gt;Use one of the following values:  &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent`&lt;/li&gt;&lt;li&gt;`conversion` or&lt;/li&gt;&lt;li&gt;`other` Used when your page does not fit into the page types listed above, for example, a &#34;Contact Us&#34; or &#34;About Us&#34; page.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;If you choose to include this parameter map your data source to `local.pagetype`.&lt;/li&gt;&lt;/ul&gt; |

### Real estate

The following table describes destination names and descriptions for Real Estate variables.

|Destination Name| Description|
|---| ---|
|`listing.id`|  &lt;ul&gt;&lt;li&gt;(Required) This parameter is the ID of the property being viewed on search results, offer detail, conversion intent and conversion page types.&lt;/li&gt;&lt;li&gt;This ID must match a value in your feed.&lt;/li&gt;&lt;/ul&gt; |
|`listing.totalvalue`|  &lt;ul&gt;&lt;li&gt;This parameter should be used on the conversion intent and conversion page types and should contain the total value of the property&lt;/li&gt;&lt;li&gt;Do not include any currency symbols.&lt;/li&gt;&lt;/ul&gt; |
|`listing.pagetype`|  &lt;ul&gt;&lt;li&gt;Recommended.&lt;/li&gt;&lt;li&gt;Indicates the type of page that the tag is on.&lt;/li&gt;&lt;li&gt;Use one of the following values:  &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent`&lt;/li&gt;&lt;li&gt;`conversion` or&lt;/li&gt;&lt;li&gt;`other` Used when your page does not fit into the page types listed above, for example, a &#34;Contact Us&#34; or &#34;About Us&#34; page.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;If you choose to include this parameter map your data source to `listing.pagetype`.&lt;/li&gt;&lt;/ul&gt; |

### Travel

The following table describes destination names and descriptions for Travel variables.

|Destination Name| Description|
|---| ---|
|`travel.destid`|  &lt;ul&gt;&lt;li&gt;(Required) This parameter is the ID of the travel destination being viewed on search results, conversion intent and conversion page types.&lt;/li&gt;&lt;li&gt;This ID must match a value in your feed.&lt;/li&gt;&lt;/ul&gt; |
|`travel.originid`|  &lt;ul&gt;&lt;li&gt;(Optional) This parameter is the ID of the travel origin location being viewed on search results, conversion intent and conversion page types.&lt;/li&gt;&lt;li&gt;This value is used as a secondary matching key in your feed and does not need to represent anything, but Google recommends that you use three-letter airport codes or two-letter country codes.&lt;/li&gt;&lt;/ul&gt; |
|`travel.startdate`|  &lt;ul&gt;&lt;li&gt;The date when the travel itinerary starts.&lt;/li&gt;&lt;li&gt;Should be in the `YYYY-MM-DD` format.&lt;/li&gt;&lt;/ul&gt; |
|`travel.enddate`|  &lt;ul&gt;&lt;li&gt;The date when the travel itinerary ends.&lt;/li&gt;&lt;li&gt;Should be in the `YYYY-MM-DD` format.&lt;/li&gt;&lt;/ul&gt; |
|`travel.totalvalue`|  &lt;ul&gt;&lt;li&gt;This parameter should be used on the conversion intent and conversion page types and should contain the total value of the travel itinerary.&lt;/li&gt;&lt;li&gt;Do not include any currency symbols.&lt;/li&gt;&lt;/ul&gt; |
|`travel.pagetype`|  &lt;ul&gt;&lt;li&gt;Recommended.&lt;/li&gt;&lt;li&gt;Indicates the type of page that the tag is on.&lt;/li&gt;&lt;li&gt;Use one of the following values:  &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent`&lt;/li&gt;&lt;li&gt;`conversion`&lt;/li&gt;&lt;li&gt;`cancel` or&lt;/li&gt;&lt;li&gt;`other` Used when your page does not fit into the page types listed above, for example, a &#34;Contact Us&#34; or &#34;About Us&#34; page.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;If you choose to include this parameter map your data source to `travel.pagetype`.&lt;/li&gt;&lt;/ul&gt; |

### Phone conversion options

Use phone call conversion tracking to help you see how effectively your ads lead to phone calls from your website. When someone visits your website after clicking one of your ads, website call conversion tracking can help you identify and measure calls from your site. This kind of conversion tracking tracks a call as a conversion when it lasts longer than a minimum length you set

The following table describes destination names and descriptions for Phone Conversion option variables.

|Destination Name| Description|
|---| ---|
|`phone_conversion_number`|  &lt;ul&gt;&lt;li&gt;(Required) In the following example, replace &#34;REPLACE WITH VALUE&#34; with your business phone number. &lt;/li&gt;&lt;li&gt;Ensure that the number matches the number on your page exactly and includes any relevant country codes.&lt;/li&gt;&lt;/ul&gt; |
|`phone_conversion_css_class`|  &lt;ul&gt;&lt;li&gt;(Required) Enter a CSS class name.&lt;/li&gt;&lt;li&gt;All elements of that class will have their contents replaced with a formatted telephone number.&lt;/li&gt;&lt;/ul&gt; |

### Other

The following table describes destination names and descriptions for variables categorized as &#34;Other&#34;.

|Destination Name| Description|
|---| ---|
|`dynx.itemid`|  &lt;ul&gt;&lt;li&gt;(Required) This parameter is the ID of the product being viewed on search results, offer detail, conversion intent and conversion page types.&lt;/li&gt;&lt;li&gt;This ID must match a value in your feed.&lt;/li&gt;&lt;/ul&gt; |
|`dynx.itemid2`|  &lt;ul&gt;&lt;li&gt;(Optional) This parameter is the secondary ID of the product being viewed on search results, offer detail, conversion intent and conversion page types.&lt;/li&gt;&lt;li&gt;This ID must match a value in your feed.&lt;/li&gt;&lt;/ul&gt; |
|`dynx.totalvalue`|  &lt;ul&gt;&lt;li&gt;This parameter should be used on the conversion intent page type and should contain the total value of the products that the visitor has purchased.&lt;/li&gt;&lt;li&gt;Do not include any currency symbols.&lt;/li&gt;&lt;/ul&gt; |
|`dynx.pagetype`|  &lt;ul&gt;&lt;li&gt;Recommended.&lt;/li&gt;&lt;li&gt;Indicates the type of page that the tag is on. Use one of the following values:&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent`&lt;/li&gt;&lt;li&gt;`conversion`&lt;/li&gt;&lt;li&gt;`cancel`&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;`other` Used when your page does not fit into the page types listed above, for example, a &#34;Contact Us&#34; or &#34;About Us&#34; page.&lt;/li&gt;&lt;/ul&gt; &lt;li&gt;If you choose to include this parameter map your data source to `dynx.pagetype`.&lt;/li&gt;&lt;/ul&gt; |

### Advanced

The following table describes destination names and descriptions for Advanced variables.

|Destination Name| Description|
|---| ---|
|Recommended Product IDs `custom.ecomm_rec_prodid`|  &lt;ul&gt;&lt;li&gt;This parameter may be used to pass product IDs of recommended products on the page.&lt;/li&gt;&lt;/ul&gt; |
|Visitor&#39;s Age `custom.a`|  &lt;ul&gt;&lt;li&gt;This parameter may be used to pass a visitor&#39;s age.&lt;/li&gt;&lt;/ul&gt; |
|Visitor&#39;s Gender `custom.g`|  &lt;ul&gt;&lt;li&gt;This parameter may be used to pass a visitor&#39;s gender.&lt;/li&gt;&lt;/ul&gt; |
|Visitor Has Account `custom.hasaccount`|  &lt;ul&gt;&lt;li&gt;This parameter may be used to indicate if the visitor has an account.&lt;/li&gt;&lt;/ul&gt; |
|Customer Quality Score `custom.cqs`|  &lt;ul&gt;&lt;li&gt;This parameter can be used to report a visitor&#39;s customer quality score.&lt;/li&gt;&lt;/ul&gt; |
|Repeat Purchaser`custom.rp`|  &lt;ul&gt;&lt;li&gt;This parameter can be used to identify if the visitor is a repeat purchaser.&lt;/li&gt;&lt;/ul&gt; |
| Visitor Loyalty Score `custom.ly` |  &lt;ul&gt;&lt;li&gt;This parameter is used to identify the visitor&#39;s loyalty score.&lt;/li&gt;&lt;/ul&gt; |
|Visitor High Spender Score `custom.hs`|  &lt;ul&gt;&lt;li&gt;This parameter is used to identify the visitor&#39;s high spender score.&lt;/li&gt;&lt;/ul&gt; |
|Custom `custom.myvar`|  &lt;ul&gt;&lt;li&gt;This parameter can be used to pass any customized parameters.&lt;/li&gt;&lt;li&gt;Replace `myvar` with your own parameter name.&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

This tag automatically pulls in data from the E-Commerce extension to populate the following retail parameters: 

* `ecomm.prodid` from `_cprod`
* `ecomm.category` from `_ccat`
* `ecomm.totalvalue` from `_csubtotal` when `_corder` is present or one of the page types includes `purchase`, `conversion`, `cart`, or `conversionintent`.

The following table describes destination names and descriptions for E-Commerce variables.

|Destination Name| Description|
|---| ---|
|Order ID `_corder`|  &lt;ul&gt;&lt;li&gt;Represents the unique identifier assigned to the final order.&lt;/li&gt;&lt;li&gt;One advantage of using Ecommerce parameters is the tag will automatically use `_csubtotal` for the total value for any business type you configure.&lt;/li&gt;&lt;li&gt;For example, for the Retail business type, the value of `ecomm.totalvalue` will use `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|Sub Total (`_csubtotal`)|  &lt;ul&gt;&lt;li&gt;Represents the sub total amount of the final order.&lt;/li&gt;&lt;li&gt;The value within `_csubtotal` will automatically use `_csubtotal` for the total value for any business type being reported.&lt;/li&gt;&lt;li&gt;For example, for the Retail business type, the value of `ecomm.totalvalue` will use `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|List of Product IDs `_cprod`|  &lt;ul&gt;&lt;li&gt;Represents the unique identifier of each product in the product array.&lt;/li&gt;&lt;li&gt;When present, a custom parameter ecomm.prodid will contain the contents of `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|List of Categories `_ccat`|  &lt;ul&gt;&lt;li&gt;Represents the category of each product in the product array.&lt;/li&gt;&lt;li&gt;When present, a custom parameter ecomm.category will contain the contents of `_ccat`.&lt;/li&gt;&lt;/ul&gt; |
|List of Quantities `_cquan`|  &lt;ul&gt;&lt;li&gt;Represents the quantity of each product in the product array.&lt;/li&gt;&lt;li&gt;When present, a custom parameter ecomm.quantity will contain the contents of `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|List of Prices `_cprice`|  &lt;ul&gt;&lt;li&gt;Represents the product unit price of each product in the product array.&lt;/li&gt;&lt;li&gt;When present, a custom parameter ecomm.pvalue will contain the contents of `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
|Currency `_ccurrency`|  &lt;ul&gt;&lt;li&gt;Represents the currency of the prices in the product array.&lt;/li&gt;&lt;li&gt;When present, a custom parameter ecomm.currency will contain the contents of `_ccurrency`.&lt;/li&gt;&lt;/ul&gt; |
|List of Discounts `product_discount`|  &lt;ul&gt;&lt;li&gt;Represents the product unit discount of each product in the product array.&lt;/li&gt;&lt;li&gt;When present, a custom parameter ecomm.discount will contain the contents of `_cdisc`.&lt;/li&gt;&lt;/ul&gt; |

## Verifying the tag

You will need the Chrome Web browser to use [Google Tag Assistant](https://support.google.com/tagassistant/answer/2947093?hl=en&amp;ref_topic=6000196). If the browser is already installed on your computer, install the Google Tag Assistant from the [Google Chrome Store](https://chrome.google.com/webstore/detail/tag-assistant-by-google/kejbdjndbnbjgmefkgdddjlbokphdefk). Once successfully installed, follow these steps:

1. Go to your site and open the target page.
1. Click on the assistant icon at the top right corner in your browser.
1. Click **Check this page now**.  
![](/images/client-side-tags/test-page.png)
The color indicator on the icon may display red instead of green since you are implementing the tag through Tealium and not the traditional way.
 Once the Tag Assistant runs, you will be able to see the values being populated. The following sample use case shows testing the homepage. In the example, you will notice the request is &#39;working&#39; and the data sources are being grabbed. Also note that the `ecomm_pagetype` is populated with a value of `home`, but, `ecomm_value` and `ecomm_prodid` are not populated because the homepage does not contain those values.  
![](/images/client-side-tags/home-page.png)The following example shows how Tag Assistant looks for Product Detail pages.  
![](/images/client-side-tags/product-detail.png)

## Vendor documentation

For additional information, see the following vendor documentation:

* [Google Ads Help](https://support.google.com/adwords#topic=3119071)
* [Tagging your site for dynamic retargeting](https://support.google.com/adwords/answer/3103357)
* [About conversion values](https://support.google.com/adwords/answer/3419241?hl=en)
* [Dynamic Remarketing Parameters](https://developers.google.com/adwords-remarketing-tag/parameters)
