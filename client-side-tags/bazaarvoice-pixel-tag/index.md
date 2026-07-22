---
title: BazaarVoice Pixel Tag Setup Guide
description: Bazaarvoice is a network that connects brands and retailers to the authentic voices of people where they shop.
url: https://docs.tealium.com/client-side-tags/bazaarvoice-pixel-tag/
---
## Tag Configuration

First, go to the tag marketplace and add the Bazaarvoice Pixel tag to your profile (See [Add a tag](https://docs.tealium.com/manage-tags/#add-a-tag)).

After adding the tag, configure the below settings:

* Client Name: The client name provided by Bazaarvoice
* Site ID: The Site ID is found in the Conversations configuration hub in the Bazaarvoice workbench under deployment zone. Default `main_site`
* Environment: The deployment environment where you want to implement the BV Pixel. Choose from production or staging
* Locale: The locale used by the BV Pixel implementation. Default `en_US`

## Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

Recommended load rule: All Pages

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The destination variables for the Bazaarvoice Pixel tag are built into its **Data Mapping** tab. Available categories are:

### Standard

| **Destination Name**      | **Description**                                                                               |
|:--------------------------|:----------------------------------------------------------------------------------------------|
| Client Name               | Use to dynamically set or override the configuration value                                    |
| Site ID                   | Use to dynamically set or override the configuration value                                    |
| Environment               | Use to dynamically set or override the configuration value                                    |
| Locale                    | Use to dynamically set or override the configuration value                                    |
| RatingsAndReviews Present | Set to `true` to send the current data with `bvProduct` value equal to `RatingsAndReviews`    |
| AskAndAnswer Present      | Set to `true` to send the current data with `bvProduct` value equal to `AskAndAnswer Present` |
| Curations Present         | Set to `true` to send the current data with `bvProduct` value equal to `Curations Present`    |

### E-Commerce

Since the Bazaarvoice Pixel tag is e-commerce enabled, it will automatically use the default E-Commerce Extension mappings. Manually mapping in this category is generally not needed unless:

* You want to override any extension mappings
* An e-commerce variable you want is not offered in the extension

| **Destination Name**                            | **Description**                                                                                      |
|:------------------------------------------------|:-----------------------------------------------------------------------------------------------------|
| Order Delivery Date (`order_delivery_date`)     | The expected delivery date for this order                                                            |
| Order Label (`label`)                           | The label associated with this conversion                                                            |
| Order Deployment Zone (`order_deployment_zone`) | The deployment zone for this order                                                                   |
| Order ID (`order_id`)                           | Unique identifier for this order. Use this to override the default e-commerce value `_corder`        |
| Order Total (`order_total`)                     | The total revenue for this order. Use this to override the default e-commerce value `_ctotal`        |
| Order Shipping Amount (`order_shipping`)        | Shipping applied to the order. Use this to override the default e-commerce value `_cship`            |
| Order Tax Amount (`order_tax`)                  | The tax applied to the order. Use this to override the default e-commerce value `_ctax`              |
| Order Currency (`order_currency`)               | Use this to override the default e-commerce value `_ccurrency`                                       |
| Customer City (`customer_city`)                 | Use this to override the default e-commerce value `_ccity`                                           |
| Customer State (`customer_state`)               | Use this to override the default e-commerce value `_cstate`                                          |
| Customer Country (`customer_country`)           | Use this to override the default e-commerce value `_ccountry`                                        |
| List of Names (`product_name`)                  | Use this to override the default e-commerce value `_cprodname`                                       |
| List of SKUs (`product_sku`)                    | The product SKU for each line item. Use this to override the default e-commerce value `_csku`        |
| List of Categories (`product_category`)         | The product category for each line item. Use this to override the default e-commerce value `_ccat`   |
| List of Quantities (`product_quantity`)         | Quantity of product for each line item. Use this to override the default e-commerce value `_cquan`   |
| List of Prices (`product_unit_price`)           | The price of each item at point of sale. Use this to override the default e-commerce value `_cprice` |
| List of Image URLs (`product_img_url`)          | The image URL of each line item.                                                                     |

### Conversion

| **Destination Name** | **Description**                                                           |
|:---------------------|:--------------------------------------------------------------------------|
| Type                 | The type of this conversion, for example, `Download`, `Compare`, `Coupon` |
| Label                | The label associated with this conversion                                 |
| Value                | A value associated with this conversion. Do not send PII data.            |

### E-Commerce and Conversion PII

| **Destination Name**    | **Description**                                                                            |
|:------------------------|:-------------------------------------------------------------------------------------------|
| Email                   | The email address for the user associated with the transaction or conversion               |
| Locale                  | The local for the user associated with the transaction or conversion. For example, `en_US` |
| Nickname                | The nickname for the user associated with the transaction or conversion                    |
| Customer/User ID        | Use this to override the default e-commerce value `_ccustid`                               |
| Order Shipping Date     | Defines specific date to send a post-interaction email for this order                      |
| Order Shipping Delay    | Defines the number of days after purchase to send a post-interaction email for this order  |
| List of Shipping Dates  | The shipping date for each line item                                                       |
| List of Shipping Delays | The shipping delay for each line item                                                      |

### Events

Map to these destinations for triggering specific events on a page. To trigger an event:

1. Select an event from the dropdown list. You may choose from the predefined list or create a Custom event. For a Custom event, enter a name with which to identify it.
1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the **+** button and repeat steps 1 and 2.
1. Click **Apply**.

The event triggers when the supplied value is found in the data layer.

| **Destination Name**                        | **Description**                                                                         |
|:--------------------------------------------|:----------------------------------------------------------------------------------------|
| Pageview (`trackPageView`)                  | Track a view of a page                                                                  |
| Impression (`trackImpression`)              | Track the presence of consumer generated content on a page                              |
| CGC In View (`trackInView`)                 | Track that consumer generated content is visible on a page                              |
| CGC Viewed (`trackViewedCGC`)               | Track that consumer generated content is visible on a page for a set amount of time     |
| Non-commerce Conversion (`trackConversion`) | Track when a non-commerce user event has occurred                                       |
| eCommerce Transaction (`trackTransaction`)  | Track when a e-commerce user event has occurred                                         |
| Helpfulness Vote (`helpfulness\`)            | Track when a user event indicating a helpfulness vote has occurred                      |
| Profile (`profile`)                         | Track when a user event indicating a profile view has occurred                          |
| Report (`report`)                           | Track when a user event for clicking a report button                                    |
| Read More (`read_more`)                     | Track when a user event for clicking a read more button                                 |
| Filter (`filter`)                           | Track when a user event for filtering content has occurred                              |
| Link (`link`)                               | Track when a user has clicked a link                                                    |
| Paginate (`paginate`)                       | Track when a user event for requesting content from a different page occurs             |
| Ask (`ask`)                                 | Track when a user event for asking a question occurs                                    |
| Statistics (`statistics`)                   | Track when a user event for viewing a histogram has occurred                            |
| Write (`write`)                             | Track when a user event indicating interaction with a contribution control has occurred |
| Sort (`sort`)                               | Track when a user event for rearranging the order of content has occurred               |
| Search (`search`)                           | Track when a user event for searching consumer-generated content has occurred           |
| Submission (`submit`)                       | Track when a user event for submitting consumer-generated content has occurred          |
| Custom                                      | Send a custom event type                                                                |

### Event Parameters

Map to these destinations if you want to pass additional data with the Event(s) you mapped earlier.

Note: Parameters are only used with pre-defined Events. See Custom Event Data to learn how to pass a Parameter with a Custom event.

To pass a Parameter with a pre-defined Event:

1. **Event** - Select a BazaarVoice event from the drop-down list.
1. **Parameter** - Select a BazaarVoice Parameter from the dropdown list.
1. For a Custom parameter, enter a name with which to identify it.
1. Click **+Add**.

| **Destination Name**                       | **Description**                                                                                                         |
|:-------------------------------------------|:------------------------------------------------------------------------------------------------------------------------|
| Content Container ID (`containerId`)       | ID of the HTML element containing the consumer-generated content                                                        |
| Page Type (`type`)                         | For view events - the type of page currently being viewed. For Feature events - defaults to `Used` if there is no value |
| Product ID (`productId`)                   | ID of the currently viewed product                                                                                      |
| Category ID (`categoryId`)                 | ID of the currently viewed product or page's category                                                                   |
| Root Category ID (`rootCategoryId`)        | ID of the top level category of the currently viewed product or page's category                                         |
| Brand Name (`brand`)                       | Name of the brand of the currently viewed product or page                                                               |
| HTML Control Name (`name`)                 | Used to describe the purpose of the HTML control                                                                        |
| Number of Reviews (`numReviews`)           | The total number of reviews on the current page                                                                         |
| Number of Questions (`numQuestions`)       | The total number of question on the current page                                                                        |
| Number of Answers (`numAnswers`)           | The total number of answers on the current page                                                                         |
| Average Rating (`avgRating`)               | The average overall rating for the product on the current page                                                          |
| Percent Recommended (`percentRecommended`) | The number of recommendations divided by the total review count                                                         |
| Metadata Detail1 (`detail1`)               | This value aims at capturing secondary metadata about the Feature Used active event                                     |
| Metadata Detail2 (`detail2`)               | When applicable, this attribute should capture additional metadata about the HTML control                               |
| Minimum Pixels (`minPixels`)               | Minimum number of pixels the consumer-generated content container must be view for the analytics event to execute       |
| Minimum Time (`minTime`)                   | Minimum amount of time, in milliseconds, that a portion (minPixels) of the element be continuously on screen            |
| Custom                                     | A custom variable                                                                                                       |

### Custom Event Data

Map to these destinations if you want to pass a custom parameter with a custom Event that you mapped in the Events tab.

To map a Custom Event Data variable:

1. **Event Action** - Enter the name of the Custom Event exactly as specified in the Events tab.
1. **Parameter** - Enter the name of the Parameter you want to send.
1. Click **+Add**.

## Vendor Documentation

* [Implement Collection BV Pixel](https://knowledge.bazaarvoice.com/wp-content/conversations/en_US/Collect/bvpixel.html)
* [Conversations API BV Pixel](https://developer.bazaarvoice.com/conversations-api/tutorials/bv-pixel)
