---
title: Retail data layer specification
description: This article provides the data layer definition for retail.
url: https://docs.tealium.com/platforms/getting-started-web/data-layer/definitions/retail/
---## Data layer attributes


|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`brand_name`| Name of the brand for brand specific pages| `Ralph Lauren`| String|
|`browse_refine_type`| Array of browse refinement types| `[&#34;Size&#34;, &#34;Color&#34;]`| Array|
|`browse_refine_value`| Array browse refinement values| `[&#34;XL&#34;, &#34;Red&#34;]`| Array|
|`cart_product_id`| On `cart_add` event, an array of all product ID&#39;s currently in the cart| `[&#34;PROD123&#34;, &#34;PROD456&#34;]` | Array|
|`cart_product_price`| On `cart_add` event, an array of all product prices currently in the cart| `[&#34;12.99&#34;, &#34;25.99&#34;]`| Array|
|`cart_product_quantity`| On `cart_add` event, an array of all product quantities currently in the cart| [`&#34;2&#34;, &#34;2&#34;]`| Array|
|`cart_product_sku`| On `cart_add` event, an array of all product SKUs currently in the cart| `[&#34;PR-RED-1234&#34;, &#34;PR-BLK-6789&#34;]` | Array|
|`cart_total_items`| Total number of all items in the cart| `4`| String|
|`cart_total_value`| Total value for all items in the cart as a string with only digits and decimal| `77.96`| String|
|`category_id`| A unique ID for the category being viewed| `243`| String|
|`category_name`| A user-friendly name for the category being viewed | `Shoes: Boots`| String|
|`country_code`| Country Code | `us`| String|
|`customer_city`| Contains the customer&#39;s city of residence| `San Diego`| String|
|`customer_country`| Contains the customer&#39;s country of residence| `United States`| String|
|`customer_email`| Contains the customer&#39;s email address| `user@example.com`| String|
|`customer_first_name`| The first name of the customer| `John`| String|
|`customer_id`| Contains the unique customer ID| `8237572`| String|
|`customer_last_name`| The last name of the customer| `Smith`| String|
|`customer_postal_code`| Contains the customer&#39;s postal code| `92101`| String|
|`customer_state`| Contains the customer&#39;s state of residence| `CA`| String|
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
|`product_brand`| An array of product brands| `[&#34;Ralph Lauren&#34;, &#34;Lucky&#34;]`| Array|
|`product_category`| An array of product categories| `[&#34;Shirts&#34;, &#34;Pants&#34;]`| Array|
|`product_discount_amount`| An array of product discount amounts, usually as a result of product-level coupons as strings with only digits and decimal| `[&#34;2.98&#34;, &#34;0.00&#34;]`| Array|
|`product_id`| An array of product IDs| `[&#34;PROD123&#34;, &#34;PROD456&#34;]`| Array|
|`product_image_url`| An array of URLs to the main product image| `[&#34;//domain.com/123.gif&#34;, &#34;//domain.com/456.gif&#34;]` | Array|
|`product_name`| An array of product names| `[&#34;Product One&#34;, &#34;Expensive Product Two&#34;]` | Array|
|`product_on_page`| An array of product IDs of other products that are displayed on the page| `[&#34;PROD123&#34;, &#34;PROD456&#34;]`| Array|
|`product_original_price`| An array of original suggested retail product prices, omitting commas and symbols| `[&#34;29.99&#34;, &#34;1015.00&#34;]`| Array|
|`product_price`| An array of product selling prices, omitting commas and symbols| `[&#34;12.99&#34;, &#34;1010.98&#34;]`| Array|
|`product_promo_code`| An array of promo/coupon codes applied to specific products| `[&#34;SHIRT10OFF&#34;,&#34;PROMO10&#34;]`| Array|
|`product_quantity`| An array of quantities for each product| `[&#34;2&#34;,&#34;2&#34;]`| Array|
|`product_sku`| An array of product SKUs| `[&#34;PR-RED-1234&#34;, &#34;PR-BLK-6789&#34;]` | Array|
|`product_subcategory`| An array of product sub-categories| `[&#34;T-Shirts&#34;, &#34;Dress Pants&#34;]`| Array|
|`product_url`| An array of URLs to the individual product page| `[&#34;//domain.com/123.html&#34;, &#34;//domain.com/456/html&#34;]` | Array|
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
    &#34;cart_total_items&#34; : &#34;4&#34;,
    &#34;cart_total_value&#34; : &#34;77.96&#34;,
    &#34;country_code&#34;     : &#34;us&#34;,
    &#34;language_code&#34;    : &#34;en&#34;,
    &#34;page_name&#34;        : &#34;Homepage&#34;,
    &#34;page_type&#34;        : &#34;home&#34;,
    &#34;site_section&#34;     : &#34;Clothing&#34;,
    &#34;tealium_event&#34;    : &#34;page_view&#34;
}
```

### Section Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `page_view`| A parent-category or top-level section page.| `http://www.example.com/top-level/`|

Sample:  
```javascript
{
    &#34;brand_name&#34;        : &#34;Ralph Lauren&#34;,
    &#34;cart_total_items&#34;  : &#34;4&#34;,
    &#34;cart_total_value&#34;  : &#34;77.96&#34;,
    &#34;category_id&#34;       : &#34;243&#34;,
    &#34;category_name&#34;     : &#34;Shoes: Boots&#34;,
    &#34;country_code&#34;      : &#34;us&#34;,
    &#34;language_code&#34;     : &#34;en&#34;,
    &#34;page_name&#34;         : &#34;Homepage&#34;,
    &#34;page_type&#34;         : &#34;section&#34;,
    &#34;product_on_page&#34;   : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;site_section&#34;      : &#34;Clothing&#34;,
    &#34;tealium_event&#34;     : &#34;page_view&#34;
}
```

### Category Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `category_view`| A category page, usually displaying a list of products.| `http://www.example.com/top-level/sub-level/`|

Sample:  
```javascript
{
    &#34;brand_name&#34;           : &#34;Ralph Lauren&#34;,
    &#34;browse_refine_type&#34;   : [&#34;Size&#34;, &#34;Color&#34;],
    &#34;browse_refine_value&#34;  : [&#34;XL&#34;, &#34;Red&#34;],
    &#34;cart_total_items&#34;     : &#34;4&#34;,
    &#34;cart_total_value&#34;     : &#34;77.96&#34;,
    &#34;category_id&#34;          : &#34;243&#34;,
    &#34;category_name&#34;        : &#34;Shoes: Boots&#34;,
    &#34;country_code&#34;         : &#34;us&#34;,
    &#34;language_code&#34;        : &#34;en&#34;,
    &#34;page_name&#34;            : &#34;Homepage&#34;,
    &#34;page_type&#34;            : &#34;category&#34;,
    &#34;product_on_page&#34;      : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;site_section&#34;         : &#34;Clothing&#34;,
    &#34;tealium_event&#34;        : &#34;category_view&#34;
}
```

### Product Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `product_view`| A product detail page.| `http://www.example.com/top-level/sub-level/product.html`|

Sample:  
```javascript
{
    &#34;cart_total_items&#34;        : &#34;4&#34;,
    &#34;cart_total_value&#34;        : &#34;77.96&#34;,
    &#34;category_id&#34;             : &#34;243&#34;,
    &#34;category_name&#34;           : &#34;Shoes: Boots&#34;,
    &#34;country_code&#34;            : &#34;us&#34;,
    &#34;language_code&#34;           : &#34;en&#34;,
    &#34;page_name&#34;               : &#34;Homepage&#34;,
    &#34;page_type&#34;               : &#34;product&#34;,
    &#34;product_brand&#34;           : [&#34;Ralph Lauren&#34;, &#34;Lucky&#34;],
    &#34;product_category&#34;        : [&#34;Shirts&#34;, &#34;Pants&#34;],
    &#34;product_id&#34;              : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;product_image_url&#34;       : [&#34;//domain.com/path/image.gif&#34;],
    &#34;product_name&#34;            : [&#34;Product One&#34;, &#34;Fancy Product Two&#34;],
    &#34;product_on_page&#34;         : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;product_original_price&#34;  : [&#34;29.99&#34;, &#34;1015.00&#34;],
    &#34;product_price&#34;           : [&#34;12.99&#34;, &#34;1010.98&#34;],
    &#34;product_sku&#34;             : [&#34;PR-RED-1234&#34;, &#34;PR-BLK-6789&#34;],
    &#34;product_subcategory&#34;     : [&#34;T-Shirts&#34;, &#34;Dress Pants&#34;],
    &#34;product_url&#34;             : [&#34;//domain.com/cat/prod/prod123.html&#34;],
    &#34;site_section&#34;            : &#34;Clothing&#34;,
    &#34;tealium_event&#34;           : &#34;product_view&#34;
}
```

### Search Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `search`| A search results page.| `http://www.example.com/search?query=term`|

Sample:  
```javascript
{
    &#34;browse_refine_type&#34;   : [&#34;Size&#34;, &#34;Color&#34;],
    &#34;browse_refine_value&#34;  : [&#34;XL&#34;, &#34;Red&#34;],
    &#34;cart_total_items&#34;     : &#34;4&#34;,
    &#34;cart_total_value&#34;     : &#34;77.96&#34;,
    &#34;country_code&#34;         : &#34;us&#34;,
    &#34;language_code&#34;        : &#34;en&#34;,
    &#34;page_name&#34;            : &#34;Homepage&#34;,
    &#34;page_type&#34;            : &#34;search&#34;,
    &#34;product_on_page&#34;      : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;search_keyword&#34;       : &#34;cargo&#34;,
    &#34;search_results&#34;       : &#34;42&#34;,
    &#34;site_section&#34;         : &#34;Clothing&#34;,
    &#34;tealium_event&#34;        : &#34;search&#34;
}
```

### Cart Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `cart_view`| The shopping cart page, displaying product contents of cart.| `http://www.example.com/cart`|

Sample:  
```javascript
{
    &#34;cart_total_items&#34;         : &#34;2&#34;,
    &#34;cart_total_value&#34;         : &#34;2524.00&#34;,
    &#34;country_code&#34;             : &#34;us&#34;,
    &#34;language_code&#34;            : &#34;en&#34;,
    &#34;page_name&#34;                : &#34;Shopping Bag&#34;,
    &#34;page_type&#34;                : &#34;cart&#34;,
    &#34;product_brand&#34;            : [&#34;Ralph Lauren&#34;, &#34;Lucky&#34;],
    &#34;product_category&#34;         : [&#34;Shirts&#34;, &#34;Pants&#34;],
    &#34;product_discount_amount&#34;  : [&#34;2.98&#34;, &#34;0.00&#34;],
    &#34;product_id&#34;               : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;product_image_url&#34;        : [&#34;//domain.com/path/image123.gif&#34;,
                                  &#34;//domain.com/path/image456.gif&#34;],
    &#34;product_name&#34;             : [&#34;Product One&#34;, &#34;Fancy Product Two&#34;],
    &#34;product_price&#34;            : [&#34;12.00&#34;, &#34;1250.00&#34;],
    &#34;product_promo_code&#34;       : [&#34;SHIRT10OFF&#34;,&#34;&#34;],
    &#34;product_quantity&#34;         : [&#34;2&#34;,&#34;2&#34;],
    &#34;product_sku&#34;              : [&#34;PR-RED-1234&#34;, &#34;PR-BLK-6789&#34;],
    &#34;product_subcategory&#34;      : [&#34;T-Shirts&#34;, &#34;Dress Pants&#34;],
    &#34;product_url&#34;              : [&#34;//domain.com/cat/prod/prod123.html&#34;,
                                  &#34;//domain.com/cat/prod/prod456.html&#34;],
    &#34;tealium_event&#34;            : &#34;cart_view&#34;
}
```

### Checkout Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `checkout`| The checkout pages, usually the shipping, payment, and billing info pages.| `http://www.example.com/checkout/billing/shipping`|

Sample:  
```javascript
{
    &#34;cart_total_items&#34;  : &#34;2&#34;,
    &#34;cart_total_value&#34;  : &#34;2524.00&#34;,
    &#34;country_code&#34;      : &#34;us&#34;,
    &#34;language_code&#34;     : &#34;en&#34;,
    &#34;page_name&#34;         : &#34;Checkout : Payment&#34;,
    &#34;page_type&#34;         : &#34;checkout&#34;,
    &#34;tealium_event&#34;     : &#34;checkout&#34;
}
```

### Order Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `purchase`| The order confirmation (&#34;Thank you&#34;) page.| `http://www.example.com/checkout/success/order.html`|

Sample:  
```javascript
{
    &#34;cart_total_items&#34;         : &#34;2&#34;,
    &#34;cart_total_value&#34;         : &#34;2524.00&#34;,
    &#34;country_code&#34;             : &#34;us&#34;,
    &#34;customer_city&#34;            : &#34;San Diego&#34;,
    &#34;customer_country&#34;         : &#34;United States&#34;,
    &#34;customer_email&#34;           : &#34;john.smith@example.com&#34;,
    &#34;customer_first_name&#34;      : &#34;John&#34;,
    &#34;customer_id&#34;              : &#34;8237572&#34;,
    &#34;customer_last_name&#34;       : &#34;Smith&#34;,
    &#34;customer_postal_code&#34;     : &#34;92101&#34;,
    &#34;customer_state&#34;           : &#34;CA&#34;,
    &#34;language_code&#34;            : &#34;en&#34;,
    &#34;order_currency_code&#34;      : &#34;USD&#34;,
    &#34;order_discount_amount&#34;    : &#34;10.00&#34;,
    &#34;order_id&#34;                 : &#34;ORD123456&#34;,
    &#34;order_payment_type&#34;       : &#34;paypal&#34;,
    &#34;order_promo_code&#34;         : &#34;SPRFREE,PROMO10&#34;,
    &#34;order_shipping_amount&#34;    : &#34;6.99&#34;,
    &#34;order_shipping_type&#34;      : &#34;UPS&#34;,
    &#34;order_store&#34;              : &#34;mobile web&#34;,
    &#34;order_subtotal&#34;           : &#34;2524.00&#34;,
    &#34;order_tax_amount&#34;         : &#34;25.00&#34;,
    &#34;order_total&#34;              : &#34;2549.00&#34;,
    &#34;page_name&#34;                : &#34;Order Confirmation - Thank You&#34;,
    &#34;page_type&#34;                : &#34;order&#34;,
    &#34;product_brand&#34;            : [&#34;Ralph Lauren&#34;, &#34;Lucky&#34;],
    &#34;product_category&#34;         : [&#34;Shirts&#34;, &#34;Pants&#34;],
    &#34;product_discount_amount&#34;  : [&#34;5.00&#34;, &#34;0.00&#34;],
    &#34;product_id&#34;               : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;product_image_url&#34;        : [&#34;//domain.com/path/image123.gif&#34;,
                                  &#34;//domain.com/path/image456.gif&#34;],
    &#34;product_name&#34;             : [&#34;Product One&#34;, &#34;Fanct Product Two&#34;],
    &#34;product_price&#34;            : [&#34;12.00&#34;, &#34;1250.00&#34;],
    &#34;product_promo_code&#34;       : [&#34;SHIRT10OFF&#34;,&#34;&#34;],
    &#34;product_quantity&#34;         : [&#34;2&#34;,&#34;2&#34;],
    &#34;product_sku&#34;              : [&#34;PR-RED-1234&#34;, &#34;PR-BLK-6789&#34;],
    &#34;product_subcategory&#34;      : [&#34;T-Shirts&#34;, &#34;Dress Pants&#34;],
    &#34;product_url&#34;              : [&#34;//domain.com/cat/prod/prod123.html&#34;,
                                  &#34;//domain.com/cat/prod/prod456.html&#34;],
    &#34;tealium_event&#34;            : &#34;purchase&#34;
}
```

### Account Page

|Event Name|Description| Sample URL|
|---| ---| ---|
| `page_view`| User account profile pages.| `http://www.example.com/account/profile`|

Sample:  
```javascript
{
    &#34;cart_total_items&#34;      : &#34;4&#34;,
    &#34;cart_total_value&#34;      : &#34;77.96&#34;,
    &#34;country_code&#34;          : &#34;us&#34;,
    &#34;customer_city&#34;         : &#34;San Diego&#34;,
    &#34;customer_country&#34;      : &#34;United States&#34;,
    &#34;customer_email&#34;        : &#34;johnsmith@example.com&#34;,
    &#34;customer_first_name&#34;   : &#34;John&#34;,
    &#34;customer_id&#34;           : &#34;8237572&#34;,
    &#34;customer_last_name&#34;    : &#34;Smith&#34;,
    &#34;customer_postal_code&#34;  : &#34;92101&#34;,
    &#34;customer_state&#34;        : &#34;CA&#34;,
    &#34;language_code&#34;         : &#34;en&#34;,
    &#34;page_name&#34;             : &#34;Homepage&#34;,
    &#34;page_type&#34;             : &#34;account&#34;,
    &#34;tealium_event&#34;         : &#34;page_view&#34;
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
    &#34;cart_product_id&#34;          : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;cart_product_price&#34;       : [&#34;12.00&#34;, &#34;25.99&#34;],
    &#34;cart_product_quantity&#34;    : [&#34;2&#34;, &#34;2&#34;],
    &#34;cart_product_sku&#34;         : [&#34;PR-RED-123&#34;, &#34;PR-BLK-456&#34;],
    &#34;product_category&#34;         : [&#34;Shirts&#34;],
    &#34;product_id&#34;               : [&#34;PROD678&#34;],
    &#34;product_image_url&#34;        : [&#34;//domain.com/path/image.gif&#34;],
    &#34;product_name&#34;             : [&#34;Product Three&#34;],
    &#34;product_price&#34;            : [&#34;18.00&#34;],
    &#34;product_quantity&#34;         : [&#34;2&#34;],
    &#34;product_sku&#34;              : [&#34;PR-BLU-678&#34;],
    &#34;product_subcategory&#34;      : [&#34;T-Shirts&#34;],
    &#34;tealium_event&#34;            : &#34;cart_add&#34;
}
```
### Remove from Cart

|Event Name|Description|
|---| ---|
| `cart_remove`| Remove from cart action.|

Sample:  
```javascript
{
    &#34;cart_product_id&#34;          : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;cart_product_price&#34;       : [&#34;12.00&#34;, &#34;25.99&#34;],
    &#34;cart_product_quantity&#34;    : [&#34;2&#34;, &#34;2&#34;],
    &#34;cart_product_sku&#34;         : [&#34;PR-RED-123&#34;, &#34;PR-BLK-456&#34;],
    &#34;product_category&#34;         : [&#34;Shirts&#34;],
    &#34;product_id&#34;               : [&#34;PROD456&#34;],
    &#34;product_image_url&#34;        : [&#34;//domain.com/path/image.gif&#34;],
    &#34;product_name&#34;             : [&#34;Product Two&#34;],
    &#34;product_price&#34;            : [&#34;12.00&#34;],
    &#34;product_quantity&#34;         : [&#34;2&#34;],
    &#34;product_sku&#34;              : [&#34;PR-BLK-456&#34;],
    &#34;product_subcategory&#34;      : [&#34;T-Shirts&#34;],
    &#34;tealium_event&#34;            : &#34;cart_remove&#34;
}
```

### User Registration

|Event Name|Description|
|---| ---|
| `user_register`| Upon successful user registration.|

Sample:  
```javascript
{
    &#34;customer_city&#34;         : &#34;San Diego&#34;,
    &#34;customer_country&#34;      : &#34;United States&#34;,
    &#34;customer_email&#34;        : &#34;john.smith@example.com&#34;,
    &#34;customer_first_name&#34;   : &#34;John&#34;,
    &#34;customer_id&#34;           : &#34;8237572&#34;,
    &#34;customer_last_name&#34;    : &#34;Smith&#34;,
    &#34;customer_postal_code&#34;  : &#34;92101&#34;,
    &#34;customer_state&#34;        : &#34;CA&#34;,
    &#34;tealium_event&#34;         : &#34;user_register&#34;
}
```

### User Update

|Event Name|Description|
|---|---|
| `user_update`| Upon successful update of user profile information.|

Sample:  
```javascript
{
    &#34;customer_city&#34;         : &#34;San Diego&#34;,
    &#34;customer_country&#34;      : &#34;United States&#34;,
    &#34;customer_email&#34;        : &#34;john.smith@example.com&#34;,
    &#34;customer_first_name&#34;   : &#34;John&#34;,
    &#34;customer_id&#34;           : &#34;8237572&#34;,
    &#34;customer_last_name&#34;    : &#34;Smith&#34;,
    &#34;customer_postal_code&#34;  : &#34;92101&#34;,
    &#34;customer_state&#34;        : &#34;CA&#34;,
    &#34;tealium_event&#34;         : &#34;user_update&#34;
}
```

### Email Signup

|Event Name|Description|
|---|---|
| `email_signup`| Upon successful signup for email newsletter.|


Sample:  
```javascript
{
    &#34;customer_email&#34;  : &#34;john.smith@example.com&#34;,
    &#34;tealium_event&#34;   : &#34;email_signup&#34;
}
```
### Custom Click

|Event Name|Description|
|---|---|
| `custom_click`| Tracking of specific click interactions with the page.|


Sample:  
```javascript
{
    &#34;link_category&#34;  : &#34;Header&#34;,
    &#34;link_name&#34;      : &#34;Login&#34;,
    &#34;tealium_event&#34;  : &#34;custom_click&#34;
}
```
