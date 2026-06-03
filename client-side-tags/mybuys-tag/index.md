---
title: MyBuys Tag Setup Guide
description: This article describes how to configure the MyBuys tag in your iQ Tag Management (TiQ) account.
url: https://docs.tealium.com/client-side-tags/mybuys-tag/
---
## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

After adding the tag, configure the below settings:

* **Client ID:** Your MyBuys Client ID.
* **Div ID:** The ID attribute of the DOM element on the page where the recommendations should appear.
* **MySite Recommendation Zone:** The numeric zone number.
* **Global CSS Path:** The default URL to the global MyBuys CSS (if used).
* **Client CSS Path:** The URL to the client-specific CSS (if used).

## Load Rules

[Load Rules]()determine when and where to load an instance of this tag on your site.

Recommended Load Rule: All Pages.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]()to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The following tables explain the different page types and events that MyBuys tracks and how the corresponding data is mapped within Tealium iQ. Your Universal Data Object should already contain the `page_type` and `event_name` variables.

### Page Types

| MyBuys Page Type           | Tealium Page Type (`page_type`) | Required/optional |
|:---------------------------|:--------------------------------|:------------------|
| Home                       | `home`                          | Required          |
| High Level Category        | `section`                       | Required          |
| Leaf Level Category        | `category`                      | Required          |
| Product Detail             | `product`                       | Required          |
| Search Results             | `search`                        | Required          |
| Add to Cart                | `cart_add` (`event_name`)       | Required          |
| Shopping Cart and Checkout | `cart`, `checkout`              | Required          |
| Order Confirmation         | `receipt`                       | Required          |
| Sale                       | `sale`                          | Optional          |
| New Arrivals               | `new_arrivals`                  | Optional          |
| Brand Home                 | `brand_home`                    | Optional          |
| Brand                      | `brand`                         | Optional          |
| Landing Page               | `landing`                       | Optional          |
| My Page                    | `account`                       | Optional          |
| Product Ratings            | `product_ratings`               | Optional          |
| Email Newsletter Signup    | `email_signup` (`event_name`)   | Optional          |

The name of the `page_type` variable might vary for your implementation. The mapping toolbox makes it easy to connect the Tealium page types to the MyBuys page types. When you map the `page_type` variable, click on the &#34;Page Types&#34; tab, then enter the values populated in the Tealium UDO and select the corresponding MyBuys page from the drop-down menu.

The same type of mapping can be used to track events using the `event_name` variable.

### E-Commerce

Map to these destinations for sending ecommerce–specific Data Layer variables. We typically recommend using Tealium&#39;s [E-Commerce Extension]() for this purpose. Why? When it is properly configured, the Extension automatically maps your variables to the appropriate destinations for all E-Commerce enabled Tags in your profile. That way you don&#39;t have to map those variables over and over for every one of your Tag. If you, however, decide to override any Extension variable, or otherwise your variables are not available to the Extension, you must manually map a data source to its destination using the toolbox.

## Variables By Page Type

These MyBuys page types have the following variables associated with them. If these variables are mapped in the [E-Commerce Extension]() then their values will be passed automatically to the MyBuys tag. Otherwise they will need to be mapped explicitly in the tag configuration. Please note that Tealium variable names may vary.

### High Level Category

| MyBuys Variable      | Tealium Variable          | Mapping |
|:---------------------|:--------------------------|:--------|
| categoryId           | `category_id`               | Mapped  |
| addItemPresentOnPage | `product_on_page` (Array) | Mapped  |

### Leaf Level Category

| MyBuys Variable      | Tealium Variable          | Mapping |
|:---------------------|:--------------------------|:--------|
| categoryId           | `category_id`               | Mapped  |
| addItemPresentOnPage | `product_on_page` (Array) | Mapped  |

### Brand Page (Optional)

| MyBuys Variable      | Tealium Variable          | Mapping |
|:---------------------|:--------------------------|:--------|
| brandname            | `brand_name`                | Mapped  |
| addItemPresentOnPage | `product_on_page` (Array) | Mapped  |

### Product Detail Page

| MyBuys Variable      | Tealium Variable          | Mapping    |
|:---------------------|:--------------------------|:-----------|
| addItemPresentOnPage | `product_on_page` (Array) | Mapped     |
| productId            | `product_id` (Array)      | E-Commerce |

### Product Ratings Page

| MyBuys Variable | Tealium Variable     | Mapping    |
|:----------------|:---------------------|:-----------|
| productId       | `product_id` (Array) | E-Commerce |

### Search Results Page

| MyBuys Variable      | Tealium Variable          | Mapping |
|:---------------------|:--------------------------|:--------|
| addItemPresentOnPage | `product_on_page` (Array) | Mapped  |

### Add to Cart Page/Event

| MyBuys Variable        | Tealium Variable                                                          | Mapping             |
|:-----------------------|:--------------------------------------------------------------------------|:--------------------|
| email                  | `customer_email` (defaults to `customer_id`)                              | Mapped (E-Commerce) |
| amount                 | `cart_total_value`                                                        | Mapped              |
| optin                  | `customer_optin`                                                          | Mapped              |
| addCartItemQtySubtotal | `cart_product_id`, `cart_product_quantity`, `cart_product_price` (Arrays) | Mapped              |

### Shopping Cart Page

| MyBuys Variable        | Tealium Variable                                           | Mapping             |
|:-----------------------|:-----------------------------------------------------------|:--------------------|
| email                  | `customer_email` (defaults to `customer_id`)               | Mapped (E-Commerce) |
| amount                 | `cart_total_value`                                         | Mapped              |
| optin                  | `customer_optin`                                           | Mapped              |
| addCartItemQtySubtotal | `product_id`, `product_quantity`, `product_price` (Arrays) | E-Commerce          |

### Order Confirmation Page

| MyBuys Variable        | Tealium Variable                                           | Mapping             |
|:-----------------------|:-----------------------------------------------------------|:--------------------|
| email                  | `customer_email` (defaults to `customer_id`)               | Mapped (E-Commerce) |
| orderId                | `order_id`                                                 | E-Commerce          |
| amount                 | `order_subtotal`                                           | E-Commerce          |
| optin                  | `customer_optin`                                           | Mapped              |
| addCartItemQtySubtotal | `product_id`, `product_quantity`, `product_price` (Arrays) | E-Commerce          |

### Email Signup Page/Event

| MyBuys Variable | Tealium Variable                             | Mapping             |
|:----------------|:---------------------------------------------|:--------------------|
| email           | `customer_email` (defaults to `customer_id`) | Mapped (E-Commerce) |
| gender          | `customer_gender`                            | Mapped              |
| zipcode         | `customer_postal_code`                       | E-Commerce          |

Sample MyBuys Variable Mapping in Tealium iQ:

![](/images/client-side-tags/tealium-mybuys-mapped-sources.jpg)

### MySite Recommendation Zones

MySite Recommendation Zones can be configured by specifying two settings: the DIV ID and the zone number. The DIV ID should reference the `id` attribute of an HTML tag in the page where the recommendations should appear. The zone number will match the numeric zone created for your MyBuys recommendations. It is recommended to have these HTML elements hard-coded onto the page to ensure proper placement.

Example:

```html
&lt;body&gt;
...
&lt;div id=&#34;mybuys1&#34;&gt;&lt;/div&gt;
...
&lt;/body&gt;
```

To configure multiple zones per page, additional mappings are required for the `divs` and `zones` variables. The values of these variables should be arrays containing a list of DIV ID&#39;s and the matching zone numbers.

In this example, `mb_divs` and `mb_zones` have been defined as new variables and are set as arrays of their respective values using a [Set Data Values extension](). The arrays can be populated using the **JS Code** assignment option. Zones can be configured on a page-by-page basis by creating multiple extensions, each with a condition.

Example extension setting multiple zones on the product detail page:

![](/images/client-side-tags/tealium-mybuys-multiple-zones.jpg)

Result:

```
// On the product page (when page_type equals &#34;product&#34;)
b.mb_divs = [&#34;mybuys1&#34;, &#34;mybuys2&#34;, &#34;mybuys3&#34;]
b.mb_zones = [&#34;1&#34;, &#34;2&#34;, &#34;3&#34;]
```

## Verifying the Tag

The MyBuys tag should behave identically inside of Tealium as it would outside of Tealium. The easiest way to verify that the MyBuys tag is working is to inspect the network traffic as the page loads. As Tealium loads and fires the MyBuys tag there will be several requests to the MyBuys servers to fetch the CSS files, the JavaScript code files, and ultimately the final pixel call containing the dynamic attributes.