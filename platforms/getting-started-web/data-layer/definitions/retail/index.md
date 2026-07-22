---
title: Retail data layer specification
description: This article provides the data layer definition for retail.
url: https://docs.tealium.com/platforms/getting-started-web/data-layer/definitions/retail/
---## Data layer attributes


|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`brand_name`| Name of the brand for brand specific pages| `Ralph Lauren`| String|
|`browse_refine_type`| Array of browse refinement types| `["Size", "Color"]`| Array|
|`browse_refine_value`| Array browse refinement values| `["XL", "Red"]`| Array|
|`cart_product_id`| On `cart_add` event, an array of all product ID's currently in the cart| `["PROD123", "PROD456"]` | Array|
|`cart_product_price`| On `cart_add` event, an array of all product prices currently in the cart| `["12.99", "25.99"]`| Array|
|`cart_product_quantity`| On `cart_add` event, an array of all product quantities currently in the cart| [`"2", "2"]`| Array|
|`cart_product_sku`| On `cart_add` event, an array of all product SKUs currently in the cart| `["PR-RED-1234", "PR-BLK-6789"]` | Array|
|`cart_total_items`| Total number of all items in the cart| `4`| String|
|`cart_total_value`| Total value for all items in the cart as a string with only digits and decimal| `77.96`| String|
|`category_id`| A unique ID for the category being viewed| `243`| String|
|`category_name`| A user-friendly name for the category being viewed | `Shoes: Boots`| String|
|`country_code`| Country Code | `us`| String|
|`customer_city`| Contains the customer's city of residence| `San Diego`| String|
|`customer_country`| Contains the customer's country of residence| `United States`| String|
|`customer_email`| Contains the customer's email address| `user@example.com`| String|
|`customer_first_name`| The first name of the customer| `John`| String|
|`customer_id`| Contains the unique customer ID| `8237572`| String|
|`customer_last_name`| The last name of the customer| `Smith`| String|
|`customer_postal_code`| Contains the customer's postal code| `92101`| String|
|`customer_state`| Contains the customer's state of residence| `CA`| String|
|`event_name`| Tealium variable to identify unique events| `cart_add`| String|
|`language_code`| Language code| `en`| String|
|`link_category`| During click tracking events, the category of the element clicked| `Header`| String|
|`link_name`| During click tracking events, the name of the element clicked| `Login`| String|
|`order_currency_code`| Currency code for the site| `USD`| String|
|`order_discount_amount`| Contains the order-level discount amount| `10.00`| String|
|`order_id`| Unique ID for an order, should only be populated on Order Confirmation page| `ORD123456`| String|
|`order_merchandise_total`| Contains price of all items not including any product or order level discounts, tax, or shipping as a string with only digits and decimal| `55.98`| String|
|`order_payment_type`| Contains the type of payment| `Paypal`| String|
|`order_promo_code`| String list of comma separated promotion codes| `PROMO10`| String|
|`order_shipping_amount`| Contains the total value for shipping as a string with only digits and decimal| `6.99`| String|
|`order_shipping_type`| Contains the type of shipping| `UPS`| String|
|`order_store`| Identifier of store type | `mobile web`| String|
|`order_subtotal`| Contains price of all items including any product or order level discounts, but excluding tax and shipping as a string with only digits and decimal| `45.98`| String|
|`order_tax_amount`| Total tax amount for this order as a string with only digits and decimal| `2.50`| String|
|`order_total`| Total Amount of the Order including tax and shipping but less all discounts as a string with only digits and decimal| `54.47`| String|
|`order_type`| The type of conversion that just took place or user that is on the site| `email`| String|
|`page_name`| Tealium variable to identify the page name| `Homepage`| String|
|`page_type`| Type of page| `product`| String|
|`product_brand`| An array of product brands| `["Ralph Lauren", "Lucky"]`| Array|
|`product_category`| An array of product categories| `["Shirts", "Pants"]`| Array|
|`product_discount_amount`| An array of product discount amounts, usually as a result of product-level coupons as strings with only digits and decimal| `["2.98", "0.00"]`| Array|
|`product_id`| An array of product IDs| `["PROD123", "PROD456"]`| Array|
|`product_image_url`| An array of URLs to the main product image| `["//domain.com/123.gif", "//domain.com/456.gif"]` | Array|
|`product_name`| An array of product names| `["Product One", "Expensive Product Two"]` | Array|
|`product_on_page`| An array of product IDs of other products that are displayed on the page| `["PROD123", "PROD456"]`| Array|
|`product_original_price`| An array of original suggested retail product prices, omitting commas and symbols| `["29.99", "1015.00"]`| Array|
|`product_price`| An array of product selling prices, omitting commas and symbols| `["12.99", "1010.98"]`| Array|
|`product_promo_code`| An array of promo/coupon codes applied to specific products| `["SHIRT10OFF","PROMO10"]`| Array|
|`product_quantity`| An array of quantities for each product| `["2","2"]`| Array|
|`product_sku`| An array of product SKUs| `["PR-RED-1234", "PR-BLK-6789"]` | Array|
|`product_subcategory`| An array of product sub-categories| `["T-Shirts", "Dress Pants"]`| Array|
|`product_url`| An array of URLs to the individual product page| `["//domain.com/123.html", "//domain.com/456/html"]` | Array|
|`search_keyword`| Value of search text entered by user| `cargo`| String|
|`search_results`| Number of results returned by search| `42`| String|
|`site_section`| The high-level sections of your site| `Clothing`| String|

## Tracked pages

### Home Page


|Event Name|Description| Sample URL|
|---| ---| ---|
| `page_view`| The home page.|`http://www.example.com/`|

Sample:  
```javascript
{
    "cart_total_items" : "4",
    "cart_total_value" : "77.96",
    "country_code"     : "us",
    "language_code"    : "en",
    "page_name"        : "Homepage",
    "page_type"        : "home",
    "site_section"     : "Clothing",
    "tealium_event"    : "page_view"
}
```

### Section Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `page_view`| A parent-category or top-level section page.| `http://www.example.com/top-level/`|

Sample:  
```javascript
{
    "brand_name"        : "Ralph Lauren",
    "cart_total_items"  : "4",
    "cart_total_value"  : "77.96",
    "category_id"       : "243",
    "category_name"     : "Shoes: Boots",
    "country_code"      : "us",
    "language_code"     : "en",
    "page_name"         : "Homepage",
    "page_type"         : "section",
    "product_on_page"   : ["PROD123", "PROD456"],
    "site_section"      : "Clothing",
    "tealium_event"     : "page_view"
}
```

### Category Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `category_view`| A category page, usually displaying a list of products.| `http://www.example.com/top-level/sub-level/`|

Sample:  
```javascript
{
    "brand_name"           : "Ralph Lauren",
    "browse_refine_type"   : ["Size", "Color"],
    "browse_refine_value"  : ["XL", "Red"],
    "cart_total_items"     : "4",
    "cart_total_value"     : "77.96",
    "category_id"          : "243",
    "category_name"        : "Shoes: Boots",
    "country_code"         : "us",
    "language_code"        : "en",
    "page_name"            : "Homepage",
    "page_type"            : "category",
    "product_on_page"      : ["PROD123", "PROD456"],
    "site_section"         : "Clothing",
    "tealium_event"        : "category_view"
}
```

### Product Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `product_view`| A product detail page.| `http://www.example.com/top-level/sub-level/product.html`|

Sample:  
```javascript
{
    "cart_total_items"        : "4",
    "cart_total_value"        : "77.96",
    "category_id"             : "243",
    "category_name"           : "Shoes: Boots",
    "country_code"            : "us",
    "language_code"           : "en",
    "page_name"               : "Homepage",
    "page_type"               : "product",
    "product_brand"           : ["Ralph Lauren", "Lucky"],
    "product_category"        : ["Shirts", "Pants"],
    "product_id"              : ["PROD123", "PROD456"],
    "product_image_url"       : ["//domain.com/path/image.gif"],
    "product_name"            : ["Product One", "Fancy Product Two"],
    "product_on_page"         : ["PROD123", "PROD456"],
    "product_original_price"  : ["29.99", "1015.00"],
    "product_price"           : ["12.99", "1010.98"],
    "product_sku"             : ["PR-RED-1234", "PR-BLK-6789"],
    "product_subcategory"     : ["T-Shirts", "Dress Pants"],
    "product_url"             : ["//domain.com/cat/prod/prod123.html"],
    "site_section"            : "Clothing",
    "tealium_event"           : "product_view"
}
```

### Search Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `search`| A search results page.| `http://www.example.com/search?query=term`|

Sample:  
```javascript
{
    "browse_refine_type"   : ["Size", "Color"],
    "browse_refine_value"  : ["XL", "Red"],
    "cart_total_items"     : "4",
    "cart_total_value"     : "77.96",
    "country_code"         : "us",
    "language_code"        : "en",
    "page_name"            : "Homepage",
    "page_type"            : "search",
    "product_on_page"      : ["PROD123", "PROD456"],
    "search_keyword"       : "cargo",
    "search_results"       : "42",
    "site_section"         : "Clothing",
    "tealium_event"        : "search"
}
```

### Cart Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `cart_view`| The shopping cart page, displaying product contents of cart.| `http://www.example.com/cart`|

Sample:  
```javascript
{
    "cart_total_items"         : "2",
    "cart_total_value"         : "2524.00",
    "country_code"             : "us",
    "language_code"            : "en",
    "page_name"                : "Shopping Bag",
    "page_type"                : "cart",
    "product_brand"            : ["Ralph Lauren", "Lucky"],
    "product_category"         : ["Shirts", "Pants"],
    "product_discount_amount"  : ["2.98", "0.00"],
    "product_id"               : ["PROD123", "PROD456"],
    "product_image_url"        : ["//domain.com/path/image123.gif",
                                  "//domain.com/path/image456.gif"],
    "product_name"             : ["Product One", "Fancy Product Two"],
    "product_price"            : ["12.00", "1250.00"],
    "product_promo_code"       : ["SHIRT10OFF",""],
    "product_quantity"         : ["2","2"],
    "product_sku"              : ["PR-RED-1234", "PR-BLK-6789"],
    "product_subcategory"      : ["T-Shirts", "Dress Pants"],
    "product_url"              : ["//domain.com/cat/prod/prod123.html",
                                  "//domain.com/cat/prod/prod456.html"],
    "tealium_event"            : "cart_view"
}
```

### Checkout Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `checkout`| The checkout pages, usually the shipping, payment, and billing info pages.| `http://www.example.com/checkout/billing/shipping`|

Sample:  
```javascript
{
    "cart_total_items"  : "2",
    "cart_total_value"  : "2524.00",
    "country_code"      : "us",
    "language_code"     : "en",
    "page_name"         : "Checkout : Payment",
    "page_type"         : "checkout",
    "tealium_event"     : "checkout"
}
```

### Order Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `purchase`| The order confirmation ("Thank you") page.| `http://www.example.com/checkout/success/order.html`|

Sample:  
```javascript
{
    "cart_total_items"         : "2",
    "cart_total_value"         : "2524.00",
    "country_code"             : "us",
    "customer_city"            : "San Diego",
    "customer_country"         : "United States",
    "customer_email"           : "john.smith@example.com",
    "customer_first_name"      : "John",
    "customer_id"              : "8237572",
    "customer_last_name"       : "Smith",
    "customer_postal_code"     : "92101",
    "customer_state"           : "CA",
    "language_code"            : "en",
    "order_currency_code"      : "USD",
    "order_discount_amount"    : "10.00",
    "order_id"                 : "ORD123456",
    "order_payment_type"       : "paypal",
    "order_promo_code"         : "SPRFREE,PROMO10",
    "order_shipping_amount"    : "6.99",
    "order_shipping_type"      : "UPS",
    "order_store"              : "mobile web",
    "order_subtotal"           : "2524.00",
    "order_tax_amount"         : "25.00",
    "order_total"              : "2549.00",
    "page_name"                : "Order Confirmation - Thank You",
    "page_type"                : "order",
    "product_brand"            : ["Ralph Lauren", "Lucky"],
    "product_category"         : ["Shirts", "Pants"],
    "product_discount_amount"  : ["5.00", "0.00"],
    "product_id"               : ["PROD123", "PROD456"],
    "product_image_url"        : ["//domain.com/path/image123.gif",
                                  "//domain.com/path/image456.gif"],
    "product_name"             : ["Product One", "Fanct Product Two"],
    "product_price"            : ["12.00", "1250.00"],
    "product_promo_code"       : ["SHIRT10OFF",""],
    "product_quantity"         : ["2","2"],
    "product_sku"              : ["PR-RED-1234", "PR-BLK-6789"],
    "product_subcategory"      : ["T-Shirts", "Dress Pants"],
    "product_url"              : ["//domain.com/cat/prod/prod123.html",
                                  "//domain.com/cat/prod/prod456.html"],
    "tealium_event"            : "purchase"
}
```

### Account Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `page_view`| User account profile pages.| `http://www.example.com/account/profile`|

Sample:  
```javascript
{
    "cart_total_items"      : "4",
    "cart_total_value"      : "77.96",
    "country_code"          : "us",
    "customer_city"         : "San Diego",
    "customer_country"      : "United States",
    "customer_email"        : "johnsmith@example.com",
    "customer_first_name"   : "John",
    "customer_id"           : "8237572",
    "customer_last_name"    : "Smith",
    "customer_postal_code"  : "92101",
    "customer_state"        : "CA",
    "language_code"         : "en",
    "page_name"             : "Homepage",
    "page_type"             : "account",
    "tealium_event"         : "page_view"
}
```

## Tracked events

### Add to Cart

|Event Name|Description|
|---| ---|
| `cart_add`| Add to cart action.|

Sample:  
```javascript
{
    "cart_product_id"          : ["PROD123", "PROD456"],
    "cart_product_price"       : ["12.00", "25.99"],
    "cart_product_quantity"    : ["2", "2"],
    "cart_product_sku"         : ["PR-RED-123", "PR-BLK-456"],
    "product_category"         : ["Shirts"],
    "product_id"               : ["PROD678"],
    "product_image_url"        : ["//domain.com/path/image.gif"],
    "product_name"             : ["Product Three"],
    "product_price"            : ["18.00"],
    "product_quantity"         : ["2"],
    "product_sku"              : ["PR-BLU-678"],
    "product_subcategory"      : ["T-Shirts"],
    "tealium_event"            : "cart_add"
}
```
### Remove from Cart

|Event Name|Description|
|---| ---|
| `cart_remove`| Remove from cart action.|

Sample:  
```javascript
{
    "cart_product_id"          : ["PROD123", "PROD456"],
    "cart_product_price"       : ["12.00", "25.99"],
    "cart_product_quantity"    : ["2", "2"],
    "cart_product_sku"         : ["PR-RED-123", "PR-BLK-456"],
    "product_category"         : ["Shirts"],
    "product_id"               : ["PROD456"],
    "product_image_url"        : ["//domain.com/path/image.gif"],
    "product_name"             : ["Product Two"],
    "product_price"            : ["12.00"],
    "product_quantity"         : ["2"],
    "product_sku"              : ["PR-BLK-456"],
    "product_subcategory"      : ["T-Shirts"],
    "tealium_event"            : "cart_remove"
}
```

### User Registration

|Event Name|Description|
|---| ---|
| `user_register`| Upon successful user registration.|

Sample:  
```javascript
{
    "customer_city"         : "San Diego",
    "customer_country"      : "United States",
    "customer_email"        : "john.smith@example.com",
    "customer_first_name"   : "John",
    "customer_id"           : "8237572",
    "customer_last_name"    : "Smith",
    "customer_postal_code"  : "92101",
    "customer_state"        : "CA",
    "tealium_event"         : "user_register"
}
```

### User Update

|Event Name|Description|
|---|---|
| `user_update`| Upon successful update of user profile information.|

Sample:  
```javascript
{
    "customer_city"         : "San Diego",
    "customer_country"      : "United States",
    "customer_email"        : "john.smith@example.com",
    "customer_first_name"   : "John",
    "customer_id"           : "8237572",
    "customer_last_name"    : "Smith",
    "customer_postal_code"  : "92101",
    "customer_state"        : "CA",
    "tealium_event"         : "user_update"
}
```

### Email Signup

|Event Name|Description|
|---|---|
| `email_signup`| Upon successful signup for email newsletter.|


Sample:  
```javascript
{
    "customer_email"  : "john.smith@example.com",
    "tealium_event"   : "email_signup"
}
```
### Custom Click

|Event Name|Description|
|---|---|
| `custom_click`| Tracking of specific click interactions with the page.|


Sample:  
```javascript
{
    "link_category"  : "Header",
    "link_name"      : "Login",
    "tealium_event"  : "custom_click"
}
```
