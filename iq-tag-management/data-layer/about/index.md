---
title: About the data layer
description: Learn the basics of the data layer for Tealium iQ Tag Management.
url: https://docs.tealium.com/iq-tag-management/data-layer/about/
---
## What is the data layer?

![](/images/iq-tag-management/data-layer-stack.png)

The data layer is the foundation of tag management. In the data layer, you define attributes of your website, such as the site language or page name. The data layer is also where you define important user behaviors you want to track, such as purchases and logins. When implementing tag management, defining the attributes of your data layer is the first step.

## How it works

Tags need data from your website or application. We recommend a Universal Data Object (UDO) to centralize your data. The UDO is the JavaScript object that represents the data layer on your site. This UDO can be supplemented by querystring parameters, first-party cookies, JavaScript variables, and metadata elements. These variables form your data layer.

Before adding your first data layer variable, let&#39;s review how it works:

*   **JavaScript object**  
Most variables created in the data layer are also added to your page code in a JavaScript object named `utag_data`, also known as the **Universal Data Object (UDO)**.
*   **Consistent names**  
The data layer variable names defined in Tealium iQ Tag Management must match the names of the variables populated in your page code. For example, a data layer variable named `page_name` in Tealium iQ is populated in your page code as:  
      ```js
      utag_data = { &#34;page_name&#34; : &#34;My Home Page&#34; };
      ```
*   **User-friendly variable names**  
Data layer variables have user-friendly names that are vendor-neutral and easy to understand across all of your business units, for example `order_id` instead of `oid`.
*   **Additional page data**  
In addition to the variables you define, the data layer also makes use of the following data from your web pages: 
    * Meta data tags
    * URL components
    * Query string parameters
    * Cookies
    * Local and session storage
    * Other global JavaScript variables
