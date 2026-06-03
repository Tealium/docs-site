---
title: Data layer best practices
description: This article reviews our best practices for implementing and managing your data layer.
url: https://docs.tealium.com/iq-tag-management/data-layer/best-practices/
---

## Code placement

In the page code, the data layer object (`utag_data`) must be declared _before_ the reference to the Universal Tag (`utag.js`). This ensures that the Universal Tag has all the data layer variables needed to evaluate load rules, extensions, and tags. An example of the recommended code placement can be accessed from the Code Center.

To learn more, see [installing the Universal Tag (utag.js)](/platforms/javascript/install/#universal-tag-utag-js).

## Naming conventions

The goal of the data layer is to provide a set of variables that are vendor-neutral and easy to understand. The following best practices apply:

* **Use lowercase, underscore-separated variable names.**  
Examples: `site_section`, `product_unit_price`, `login_status`.
* **Avoid vendor specific naming.**  
Avoid `eVar1`, `pv_a3`, or `oid`.
* **Use meaningful variable descriptions.**  
Sometimes even a properly named variable still needs additional clarification. A good variable description includes details about when and where a variable is set, which vendor is using the variable, and possible values to expect in the variable. Examples:
    * Login status `anonymous` or `authenticated`, used for `eVar1` in Adobe Analytics.
    * Order subtotal does not include tax or shipping, exclude commas and currency symbols.
* **Avoid pluralized variable names.**  
Variables that contain multiple values, such as the product array variables, should use the singular form of the name. Examples:
    * `product_category` instead of `product_categories`
    * `product_id` instead of `product_ids`
* **Prefix boolean variable names with `is_.` or `has_.`**  
This lets you quickly identify variables that contain a value of `1` or `0`. Examples: `is_registered`, `is_first_time_visitor`, `is_logged_in`

**Pros**

- Creates a consistent naming convention.
- Easier for new users to understand what is available in your data layer and how each variable is used.
- Tealium Support is familiar with this convention.

**Cons**

- Additional effort to transition vendor-specific variables to vendor-neutral naming convention.

## String variables

Use string values for all non-product variables. Boolean and numeric variables should be passed as strings.

For boolean values, use `1` and `0` instead of `true` and `false`. This approach is more stable and reduces confusion about the expected values in these variables.

Examples:

| | Boolean| Integer|
|---| ---| ---|
|Correct|  `is_registered : &#34;1&#34;` |  `order_total : &#34;1234.56&#34;` |
|Incorrect|  `is_registered : true` |  `order_total : 1234.56` |

**Pros**

- Tag templates expect strings and arrays.
- Minimizes testing effort during and after implementation.

**Cons**

- None.

## Array variables

Set product variables (price, quantity, ID, etc.) as arrays. The Universal Tag (`utag.js`) is designed to use arrays for all product variables. While it is possible to set product values in a comma-separated string, this approach is more prone to errors.

Array (Recommended):

```javascript
product_id : [&#34;prodID1&#34;,&#34;prodID2&#34;,&#34;prodID3&#34;]
```

String:

```javascript
product_id : &#34;prodID1,prodID2,prodID3&#34;
```

**Pros**

- Same format expected by vendor tag templates.
- Improves readability of the data layer.

**Cons**

- None.

## Page types

All pages of your site should include a variable called `page_type`. This is used to determine the type of page the user is viewing. The suggested values include, but are not limited to:

| Page |  Value |
|:---|:---|
| Home Page | `home` |
| Category / Product List |  `category` |
| Product Detail |  `product` |
| Search Results |  `search` |
| Cart / Basket |  `cart` |
| Checkout Flow (User Info, Billing Address, Shipping Address) |  `checkout` |
| Order Confirmation / Thank You |  `order` |

**Pros**

- Gives a clear understanding of what kind of page the user is viewing.
- Many vendor tags utilize a page type to function properly.

**Cons**

- Initial development effort to add `page_type` variable to the Universal Data Object.

## Third-party data layer objects

You might already have a data layer object implemented on your site, such as the W3C Data Object or your own custom object. We recommend that these objects be converted to the UDO `utag_data` format using one of the available [data layer converters]().

**Pros**

- Better compatibility with built-in functionality, such as load rules, data mappings, and Web Companion.
- Reduces support costs to investigate issues with your custom object.

**Cons**

- Additional effort to implement.

