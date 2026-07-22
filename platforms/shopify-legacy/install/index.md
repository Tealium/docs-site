---
title: Install
description: This article describes how to customize your Shopify theme to use Tealium with the Tealium Shopify (legacy) integration.
url: https://docs.tealium.com/platforms/shopify-legacy/install/
---

<blockquote>
Tealium now provides a Shopify app in the Shopify marketplace that lets you use Tealium iQ Tag Management with your Shopify site. For more information, see [About Tealium Shopify app]().
</blockquote>


## How it works

To use Tealium with Shopify, you must customize your Shopify theme to use Tealium code with the Tealium Shopify (legacy) integration. The Tealium code provides a Universal Data Object (UDO) and loads the necessary Tealium assets on each page of your site.

The code snippet for the order status page also appears on the "Thank you" page of the checkout. The code snippet provides the UDO for conversion tracking. Since the order status page may be revisited after the order is placed, it is recommended to configure logic in Tealium iQ Tag Management in order not to track conversions twice.

Only Shopify Plus customers have access to the `checkout.liquid` file, which loads `utag.js` throughout the checkout funnel. This integration does not currently support the checkout funnel. However you may implement your own `checkout.liquid` following the patterns used on other pages.

## Setup Instructions

To customize your Shopify theme for Tealium integration, follow these steps:

1. [Enable Tealium settings](#enable-tealium-settings).
1. [Install utag.js and the on-page data layer](#install-utagjs-and-on-page-data-layer).
1. [Install the script for the order status page](#install-script-for-order-status-page).
1. (For Shopify Plus customers) [Install the script for the checkout process](#install-script-for-checkout-shopify-plus-only). 
<blockquote>
Shopify will deprecate the `checkout.liquid` theme file on August 13, 2024. For details, see [Shopify.dev docs: Upgrade](https://shopify.dev/docs/apps/checkout#upgrade).
</blockquote>


### Enable Tealium settings

Copy and paste the following JSON object into the JSON array in the [Config/settings_schema.json](https://help.shopify.com/themes/development/theme-editor/settings-schema) file of your Shopify theme. The JSON object enables the Tealium-specific settings for your theme.

```json
{
  "name": "Tealium",
  "settings": [
    {
      "type": "text",
      "id": "tealium_account",
      "label": "Account",
      "info": "Name of your acount"
    },
    {
      "type": "text",
      "id": "tealium_profile",
      "label": "Profile",
      "default": "main",
      "info": "Which profile to load your tags from",
      "placeholder": "main"
    },
    {
      "type": "text",
      "id": "tealium_environment",
      "label": "Environment",
      "default": "prod",
      "info": "Which environment to load your tags from",
      "placeholder": "prod"
    },
    {
      "type": "checkbox",
      "id": "tealium_enabled",
      "label": "Enable",
      "default": false,
      "info": "Check to enable Tealium"
    }
  ]
}
```

Edit your Tealium-specific settings in the **General Settings** tab when customizing your theme.

### Install utag.js and on-page data layer

Follow these steps to install `utag.js` and set up an on-page data layer for your Shopify store. This process involves adding specific snippets to your Shopify theme, which are provided in the [Tealium Integration for Shopify GitHub repository](https://github.com/Tealium/integration-shopify). These snippets enable the Universal Data Object (UDO) implementations, necessary for tracking and analytics on different types of pages within your store.

#### Step 1 - Access your theme's code

1. Log in to your Shopify account.
1. Go to **Online Store > Themes** to view your current theme.
1. Find the theme you want to edit, click on the **Actions** drop-down menu, and select **Edit code**. Alternatively, you can access the code editor directly by clicking the **Customize** button for your theme.

#### Step 2 - Add the UDO implementation snippets

1. Access the [Tealium Integration for Shopify GitHub repository](https://github.com/Tealium/integration-shopify) to download the necessary code snippets for UDO implementations across various page types.
1. In the Shopify theme code editor, click the **Snippets** folder to expand it.
1. Drag and drop the appropriate snippets from the GitHub repository into the **Snippets** folder in your Shopify theme editor. For more information, see [Shopify.dev docs: Theme snippets](https://help.shopify.com/themes/development/templates#snippets).

#### Step 3 - Reference the snippets in your templates

1. After adding the snippets, click the **Templates** folder to expand it.
1. For each template that corresponds to a page type (such as product, home, about us), insert a reference to the relevant UDO snippet at the beginning of the template file. These references ensure the data layer is initialized correctly for each page type.
  
    For example, to integrate the data layer on a product page, edit the `product.liquid` template as follows:
    * At the beginning of the `product.liquid` file, add the following line to include the `product_udo` snippet, previously added to the **Snippets** folder:

      ```liquid
      {% include 'product_udo' %}
      ```

    * This line should be placed before any existing content in the template file to ensure the data layer is initialized before any other scripts run. The `product.liquid` template should be similar to this after including the `product_udo` snippet:

      ```liquid
      {% include 'product_udo' %}

      {% comment %}
        The contents of the product.liquid template can be found in /sections/product-template.liquid
      {% endcomment %}

      {% section 'product-template' %}

      <script>
        // Override default values of shop.strings for each template.
        // Alternate product templates can change values of
        // add to cart button, sold out, and unavailable states here.
        theme.productStrings = {
          addToCart: {{ 'products.product.add_to_cart' | t | json }},
          soldOut: {{ 'products.product.sold_out' | t | json }},
          unavailable: {{ 'products.product.unavailable' | t | json }}
        }
      </script>
      ```

    * Continue this process for each template corresponding to different page types, using the appropriate snippet name in place of `product_udo`. Generally, the names of the snippets and the templates they correspond to are similar, without the `_udo` suffix in the snippet names. For example:
      * For the `index.liquid` template (the homepage), include the `home_udo` snippet.
      * For generic templates like `404.liquid`, use the `page_udo` snippet to ensure a broad coverage.
      For more information, see [Shopify.dev docs: Theme architecture](https://help.shopify.com/themes/development/templates)
1. After adding the `include` statement to a template, click **Save** to apply your changes.
1. To verify your changes, open the developer console in your web browser and inspect `utag.data`.

### Install script for order status page

Unlike other pages, the order status page doesn't have access to the admin settings, so you must reconfigure your Tealium account information. Follow these steps to define these settings:

1. From your Shopify admin, click **Settings** and then click **Checkout**.
1. In the **Checkout** settings, scroll to **Order status page** near the bottom of the page.
1. In **Additional scripts**, add the following code:

    ```liquid
    <script>
      {
        "product_price": [
        {% for line_item in checkout.line_items %}
          "{{ line_item.price | money_without_currency }}"{% unless forloop.last %},{% endunless %}
        {% endfor %}
        ],
        "product_name": [
        {% for line_item in checkout.line_items %}
          "{{ line_item.title }}"{% unless forloop.last %},{% endunless %}
        {% endfor %}
        ],
        "product_sku": [
        {% for line_item in checkout.line_items %}
          "{{ line_item.sku }}"{% unless forloop.last %},{% endunless %}
        {% endfor %}
        ],

        "page_name": "{{ page_title }}",
        "language_code": "{{ shop.locale }}",

        {% if customer %}
          "customer_logged_in": "true",
          "customer_id": "{{ customer.id }}",
          "customer_email": "{{ customer.email }}",
          "customer_first_name": "{{ customer.first_name }}",
          "customer_last_name": "{{ customer.last_name }}",

          {% if customer.default_address %}
            "country_code": "{{ customer.default_address.country_code }}",
          {% endif %}

        {% else %}
          "customer_loggedin": "false",
        {% endif %}

        {% if cart %}
          "cart_total_items": "{{ cart.item_count }}",
          "cart_total_value": "{{ cart.total_price | money_without_currency }}",
        {% endif %}

        "page_type": "order"
      }
    </script>

    <!-- Loading script asynchronously -->
    <script type="text/javascript">
        (function(a,b,c,d){
        a='//tags.tiqcdn.com/utag/{{ settings.tealium_account }}/{{ settings.tealium_profile }}/{{ settings.tealium_environment }}/utag.js';
        b=document;c='script';d=b.createElement(c);d.src=a;d.type='text/java'+c;d.async=true;
        a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
        })();
    </script>
    {% else %}
    <!-- Configure your Tealium account information for the order confirmation page. -->
    {% endif %}
    ```

    For more information, see [Shopify help center: Order status page](https://help.shopify.com/themes/customization/order-status)

1. Set `tealium_enabled` to `true`.
1. Set the `tealium_account`, `tealium_profile`, and `tealium_environment` variables to match what you configured in the settings.

### Install script for checkout (Shopify Plus only)

This step is for Shopify Plus customers who want to integrate `utag.js` throughout the checkout funnel using the `checkout.liquid` file.

#### Accessing `checkout.liquid`

* **Shopify Plus Customers**: You can request access to your `checkout.liquid` file if it's not already accessible. This file loads `utag.js` during the checkout process. If you haven't previously modified this file, you'll need to contact Shopify Support to gain access before you can proceed with the installation.
* **Non-Shopify Plus Customers**: Shopify Support does not grant access to the `checkout.liquid` file for customers without a Shopify Plus account. This limitation means that the `utag.js` script cannot be installed on checkout pages. However, completing the prior steps ensures that `utag.js` is installed on other important pages, such as the shopping cart and order confirmation pages.

#### Installation instructions

1. Open the `checkout_udo.liquid` file.
2. In line 10, replace the placeholders with your Tealium iQ account and profile information.
3. Copy the modified content and paste it in the Shopify checkout liquid file.
4. Save your changes and test to ensure the integration works as expected.


<blockquote>
This  checkout code serves as a foundational template. Depending on your Shopify site's specific requirements and setup, customizations may be necessary for optimal performance.
</blockquote>


## Release Notes

#### 1.0.2

* Updated `README` to more clearly reflect the capabilities of the integration.
* Updated `order_status` snippet to include more data and better variable names.
* Renamed checkout.liquid to `order_status.liquid` to better reflect its functionality.

#### 1.0.1

* Fixed misspelled variable name in the global_udo_vars snippet. `customer_loggedin` was replaced with `customer_logged_in`.

#### 1.0.0 Initial Release

* All snippets and configuration required to customize a Shopify theme to integrate Tealium.
* Instructions for customizing a theme.

## License

Use of this software is subject to the terms and conditions of the license agreement contained in the file titled [LICENSE.txt](https://github.com/Tealium/integration-shopify/blob/master/LICENSE.txt). Please read the license before downloading or using any of the files contained in this repository. By downloading or using any of these files, you are agreeing to be bound by and comply with the license agreement.