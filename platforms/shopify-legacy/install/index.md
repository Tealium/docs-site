---
title: Install
description: This article describes how to customize your Shopify theme to use Tealium with the Tealium Shopify (legacy) integration.
url: https://docs.tealium.com/platforms/shopify-legacy/install/
---
Tealium now provides a Shopify app in the Shopify marketplace that lets you use Tealium iQ Tag Management with your Shopify site. For more information, see [About Tealium Shopify app]().

## How it works

To use Tealium with Shopify, you must customize your Shopify theme to use Tealium code with the Tealium Shopify (legacy) integration. The Tealium code provides a Universal Data Object (UDO) and loads the necessary Tealium assets on each page of your site.

The code snippet for the order status page also appears on the &#34;Thank you&#34; page of the checkout. The code snippet provides the UDO for conversion tracking. Since the order status page may be revisited after the order is placed, it is recommended to configure logic in Tealium iQ Tag Management in order not to track conversions twice.

Only Shopify Plus customers have access to the `checkout.liquid` file, which loads `utag.js` throughout the checkout funnel. This integration does not currently support the checkout funnel. However you may implement your own `checkout.liquid` following the patterns used on other pages.

## Setup Instructions

To customize your Shopify theme for Tealium integration, follow these steps:

1. [Enable Tealium settings](#enable-tealium-settings).
1. [Install utag.js and the on-page data layer](#install-utagjs-and-on-page-data-layer).
1. [Install the script for the order status page](#install-script-for-order-status-page).
1. (For Shopify Plus customers) [Install the script for the checkout process](#install-script-for-checkout-shopify-plus-only). Shopify will deprecate the `checkout.liquid` theme file on August 13, 2024. For details, see [Shopify.dev docs: Upgrade](https://shopify.dev/docs/apps/checkout#upgrade).

### Enable Tealium settings

Copy and paste the following JSON object into the JSON array in the [Config/settings_schema.json](https://help.shopify.com/themes/development/theme-editor/settings-schema) file of your Shopify theme. The JSON object enables the Tealium-specific settings for your theme.

```json
{
  &#34;name&#34;: &#34;Tealium&#34;,
  &#34;settings&#34;: [
    {
      &#34;type&#34;: &#34;text&#34;,
      &#34;id&#34;: &#34;tealium_account&#34;,
      &#34;label&#34;: &#34;Account&#34;,
      &#34;info&#34;: &#34;Name of your acount&#34;
    },
    {
      &#34;type&#34;: &#34;text&#34;,
      &#34;id&#34;: &#34;tealium_profile&#34;,
      &#34;label&#34;: &#34;Profile&#34;,
      &#34;default&#34;: &#34;main&#34;,
      &#34;info&#34;: &#34;Which profile to load your tags from&#34;,
      &#34;placeholder&#34;: &#34;main&#34;
    },
    {
      &#34;type&#34;: &#34;text&#34;,
      &#34;id&#34;: &#34;tealium_environment&#34;,
      &#34;label&#34;: &#34;Environment&#34;,
      &#34;default&#34;: &#34;prod&#34;,
      &#34;info&#34;: &#34;Which environment to load your tags from&#34;,
      &#34;placeholder&#34;: &#34;prod&#34;
    },
    {
      &#34;type&#34;: &#34;checkbox&#34;,
      &#34;id&#34;: &#34;tealium_enabled&#34;,
      &#34;label&#34;: &#34;Enable&#34;,
      &#34;default&#34;: false,
      &#34;info&#34;: &#34;Check to enable Tealium&#34;
    }
  ]
}
```

Edit your Tealium-specific settings in the **General Settings** tab when customizing your theme.

### Install utag.js and on-page data layer

Follow these steps to install `utag.js` and set up an on-page data layer for your Shopify store. This process involves adding specific snippets to your Shopify theme, which are provided in the [Tealium Integration for Shopify GitHub repository](https://github.com/Tealium/integration-shopify). These snippets enable the Universal Data Object (UDO) implementations, necessary for tracking and analytics on different types of pages within your store.

#### Step 1 - Access your theme&#39;s code

1. Log in to your Shopify account.
1. Go to **Online Store &gt; Themes** to view your current theme.
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
      {% include &#39;product_udo&#39; %}
      ```

    * This line should be placed before any existing content in the template file to ensure the data layer is initialized before any other scripts run. The `product.liquid` template should be similar to this after including the `product_udo` snippet:

      ```liquid
      {% include &#39;product_udo&#39; %}

      {% comment %}
        The contents of the product.liquid template can be found in /sections/product-template.liquid
      {% endcomment %}

      {% section &#39;product-template&#39; %}

      &lt;script&gt;
        // Override default values of shop.strings for each template.
        // Alternate product templates can change values of
        // add to cart button, sold out, and unavailable states here.
        theme.productStrings = {
          addToCart: {{ &#39;products.product.add_to_cart&#39; | t | json }},
          soldOut: {{ &#39;products.product.sold_out&#39; | t | json }},
          unavailable: {{ &#39;products.product.unavailable&#39; | t | json }}
        }
      &lt;/script&gt;
      ```

    * Continue this process for each template corresponding to different page types, using the appropriate snippet name in place of `product_udo`. Generally, the names of the snippets and the templates they correspond to are similar, without the `_udo` suffix in the snippet names. For example:
      * For the `index.liquid` template (the homepage), include the `home_udo` snippet.
      * For generic templates like `404.liquid`, use the `page_udo` snippet to ensure a broad coverage.
      For more information, see [Shopify.dev docs: Theme architecture](https://help.shopify.com/themes/development/templates)
1. After adding the `include` statement to a template, click **Save** to apply your changes.
1. To verify your changes, open the developer console in your web browser and inspect `utag.data`.

### Install script for order status page

Unlike other pages, the order status page doesn&#39;t have access to the admin settings, so you must reconfigure your Tealium account information. Follow these steps to define these settings:

1. From your Shopify admin, click **Settings** and then click **Checkout**.
1. In the **Checkout** settings, scroll to **Order status page** near the bottom of the page.
1. In **Additional scripts**, add the following code:

    ```liquid
    &lt;script&gt;
      {
        &#34;product_price&#34;: [
        {% for line_item in checkout.line_items %}
          &#34;{{ line_item.price | money_without_currency }}&#34;{% unless forloop.last %},{% endunless %}
        {% endfor %}
        ],
        &#34;product_name&#34;: [
        {% for line_item in checkout.line_items %}
          &#34;{{ line_item.title }}&#34;{% unless forloop.last %},{% endunless %}
        {% endfor %}
        ],
        &#34;product_sku&#34;: [
        {% for line_item in checkout.line_items %}
          &#34;{{ line_item.sku }}&#34;{% unless forloop.last %},{% endunless %}
        {% endfor %}
        ],

        &#34;page_name&#34;: &#34;{{ page_title }}&#34;,
        &#34;language_code&#34;: &#34;{{ shop.locale }}&#34;,

        {% if customer %}
          &#34;customer_logged_in&#34;: &#34;true&#34;,
          &#34;customer_id&#34;: &#34;{{ customer.id }}&#34;,
          &#34;customer_email&#34;: &#34;{{ customer.email }}&#34;,
          &#34;customer_first_name&#34;: &#34;{{ customer.first_name }}&#34;,
          &#34;customer_last_name&#34;: &#34;{{ customer.last_name }}&#34;,

          {% if customer.default_address %}
            &#34;country_code&#34;: &#34;{{ customer.default_address.country_code }}&#34;,
          {% endif %}

        {% else %}
          &#34;customer_loggedin&#34;: &#34;false&#34;,
        {% endif %}

        {% if cart %}
          &#34;cart_total_items&#34;: &#34;{{ cart.item_count }}&#34;,
          &#34;cart_total_value&#34;: &#34;{{ cart.total_price | money_without_currency }}&#34;,
        {% endif %}

        &#34;page_type&#34;: &#34;order&#34;
      }
    &lt;/script&gt;

    &lt;!-- Loading script asynchronously --&gt;
    &lt;script type=&#34;text/javascript&#34;&gt;
        (function(a,b,c,d){
        a=&#39;//tags.tiqcdn.com/utag/{{ settings.tealium_account }}/{{ settings.tealium_profile }}/{{ settings.tealium_environment }}/utag.js&#39;;
        b=document;c=&#39;script&#39;;d=b.createElement(c);d.src=a;d.type=&#39;text/java&#39;&#43;c;d.async=true;
        a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
        })();
    &lt;/script&gt;
    {% else %}
    &lt;!-- Configure your Tealium account information for the order confirmation page. --&gt;
    {% endif %}
    ```

    For more information, see [Shopify help center: Order status page](https://help.shopify.com/themes/customization/order-status)

1. Set `tealium_enabled` to `true`.
1. Set the `tealium_account`, `tealium_profile`, and `tealium_environment` variables to match what you configured in the settings.

### Install script for checkout (Shopify Plus only)

This step is for Shopify Plus customers who want to integrate `utag.js` throughout the checkout funnel using the `checkout.liquid` file.

#### Accessing `checkout.liquid`

* **Shopify Plus Customers**: You can request access to your `checkout.liquid` file if it&#39;s not already accessible. This file loads `utag.js` during the checkout process. If you haven&#39;t previously modified this file, you&#39;ll need to contact Shopify Support to gain access before you can proceed with the installation.
* **Non-Shopify Plus Customers**: Shopify Support does not grant access to the `checkout.liquid` file for customers without a Shopify Plus account. This limitation means that the `utag.js` script cannot be installed on checkout pages. However, completing the prior steps ensures that `utag.js` is installed on other important pages, such as the shopping cart and order confirmation pages.

#### Installation instructions

1. Open the `checkout_udo.liquid` file.
2. In line 10, replace the placeholders with your Tealium iQ account and profile information.
3. Copy the modified content and paste it in the Shopify checkout liquid file.
4. Save your changes and test to ensure the integration works as expected.

This  checkout code serves as a foundational template. Depending on your Shopify site&#39;s specific requirements and setup, customizations may be necessary for optimal performance.

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