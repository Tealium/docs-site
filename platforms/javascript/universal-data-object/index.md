---
title: Universal Data Object (utag_data)
description: Learn about the Universal Data Object (`utag_data`) and the different types of web page data it makes available.
url: https://docs.tealium.com/platforms/javascript/universal-data-object/
---
## Universal Data Object (UDO)

The [data layer]() is the foundation of your Tealium solution and serves as the one true definition of your data across all digital assets and customer interactions. The data layer comprises all of the various [variables]() that are collected across your site and the visitor interactions and events that are tracked.

The data layer is implemented on your website as a JavaScript object called `utag_data` in which you expose data from the page to the Tealium tag. The properties in this object use plain, vendor neutral names that are tailored to your business.

The following is an example declaration of `utag_data`:

```html
&lt;script type=&#34;text/javascript&#34;&gt;
  var utag_data={
      &#34;tealium_event&#34;  : &#34;search&#34;,
      &#34;page_name&#34;      : &#34;Search Results&#34;,
      &#34;search_results&#34; : &#34;42&#34;,
      &#34;search_keyword&#34; : &#34;Tealium shirt&#34;};
&lt;/script&gt;
```


Define and populate the `utag_data` object variable prior to loading the Universal Tag (`utag.js`).

When `utag.js` loads in the page, it looks for the `utag_data` variable and uses the data to automatically trigger a page view tracking call with `utag.view()`. If you have a single page application, or are calling `utag.view()` manually, you might not need `utag_data`. 

[Learn more](/platforms/javascript/page-tracking/) about page tracking options.

### Syntax Guidelines

When implementing the UDO there are certain guidelines to follow, not only to avoid errors or inconsistencies in your implementation but also to conform to JavaScript and Tealium standards.

*   **String Values**  
Use string values for all variables, including boolean and numeric data.
*   **Escape Quotes**    
    Enclose all values in double quotes or single quotes and escape any quotes that might appear in the value itself. For example, `utag_data.page_name = &#39;It\&#39;s All About the Data!&#39;;`.
*   **Boolean Values**   
    For boolean values use `&#34;1&#34;` and `&#34;0&#34;` to represent `true` and `false`. This is the simplest way to represent a boolean using strings.
*   **Amount Values**  
    Use strings for all dollar amounts and exclude all currency symbols and commas. For example, `utag_data.order_total = &#34;1234.00&#34;;` instead of `&#34;$1,234.00&#34;`.  
*   **Array Values**  
    Use array values for all product related variables. The Tealium library, and each vendor tag integration, is designed to use arrays for all product-related data. For example, ID, price, or quantity.   
    `utag_data.product_id = [&#34;P1234&#34;, &#34;P4567&#34;, &#34;P7890&#34;];`
*   **Avoid Extra Code**  
    Do not add extra code to the UDO script block. If any code in the same script block fails, the UDO may not be defined correctly which might lead to unexpected data being passed to your vendor tags.


## Examples

### Standard Page

The following is a _sample_ UDO as it appears on a page. This specific example shows properties that might appear on a &#34;Shopping Cart&#34; page with two products in the cart.

```html
&lt;script type=&#34;text/javascript&#34;&gt;
  var utag_data = {
    &#34;tealium_event&#34;      : &#34;cart_add&#34;,
    &#34;country_code&#34;       : &#34;US&#34;,    
    &#34;currency_code&#34;      : &#34;USD&#34;,    
    &#34;page_name&#34;          : &#34;Cart: View Shopping Bag&#34;,   
    &#34;page_type&#34;          : &#34;cart&#34;,    
    &#34;product_id&#34;         : [&#34;PROD123&#34;, &#34;PROD456&#34;],    
    &#34;product_name&#34;       : [&#34;Red Shoes&#34;, &#34;Black Socks&#34;],
    &#34;product_category&#34;   : [&#34;Footwear&#34;, &#34;Apparel&#34;],    
    &#34;product_quantity&#34;   : [&#34;1&#34;, &#34;2&#34;],    
    &#34;product_unit_price&#34; : [&#34;65.00&#34;, &#34;4.75&#34;],    
    &#34;cart_total_items&#34;   : &#34;3&#34;,    
    &#34;cart_subtotal&#34;      : &#34;74.00&#34;};
&lt;/script&gt;
```

If needed, update the UDO with additional values outside of the declaration block, as long as the data gets set prior to loading `utag.js`. UDO variables set after loading `utag.js` are ignored.  

```html
&lt;script type=&#34;text/javascript&#34;&gt;
  utag_data[&#34;page_name&#34;] = &#34;View Cart&#34;;
&lt;/script&gt;
```

### Page Specific Data

When populating the UDO, only include variables pertinent to the current page type. This reduces clutter in the page code and eliminates confusion about what data is expected. Below is an example of a search page UDO that omits unnecessary items such as product and order data.

```html
&lt;script type=&#34;text/javascript&#34;&gt;
  var utag_data={
      &#34;page_name&#34;      : &#34;Search Results&#34;,
      &#34;page_type&#34;      : &#34;search&#34;,
      &#34;search_results&#34; : &#34;42&#34;,
      &#34;search_keyword&#34; : &#34;tennis shoes&#34;};
&lt;/script&gt;
```


### Product Arrays
Product variables are to be populated as arrays, even when a single product is being set. Below are examples of setting the product ID variable with one product ID (on the Product Detail page) and with three product IDs such as a Shopping Cart page.

```javascript
// Single product. For example, product detail page
utag_data[&#34;product_id&#34;] = [&#34;PROD123&#34;];

// Multiple products. For example, cart page
utag_data[&#34;product_id&#34;] = [&#34;PROD123&#34;, &#34;PROD456&#34;, &#34;PROD789&#34;];
```

### Array Alignment

All product array variables must have the same number of elements to ensure data alignment. In this example, notice that the first element in each array corresponds to the first product. Properties associated with this product (such as ID, price, and quantity) all appear in the first element in each array, while the properties of the second product appear in the second element in each array, and so on.

```javascript
// Product 1:
//   ID    = PROD123
//   Price = 3.00
//   QTY   = 1
//
// Product 2:
//   ID    = PROD456
//   Price = 5.00
//   QTY   = 1
//
utag_data[&#34;product_id&#34;]       = [&#34;PROD123&#34;, &#34;PROD456&#34;];
utag_data[&#34;product_price&#34;]    = [&#34;3.00&#34;, &#34;5.00&#34;];
utag_data[&#34;product_quantity&#34;] = [&#34;1&#34;, &#34;1&#34;];
```
