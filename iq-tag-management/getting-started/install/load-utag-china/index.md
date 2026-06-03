---
title: Load the universal tag from a Chinese network
description: This article describes how to improve performance when loading the universal tag from Chinese networks.
url: https://docs.tealium.com/iq-tag-management/getting-started/install/load-utag-china/
---
Use tags.tiqcdn.cn to expedite content delivery inside mainland China, as well as elsewhere in the world. The domain `tags.tiqcdn.cn` is delivered by Akamai through the closest node to the user, which can be inside or outside the network security.

## Considerations

* **Choose one of the following methods for loading the universal tag**:
    * **Update the code for your website**: If you can modify the source code for your site and a large amount of traffic is from China, we recommend that you use `tags.tiqcdn.cn` in the code you add to your website.
    * **Use the China CDN Deployment Extension**: If you cannot modify the source code for your site or a small amount of traffic is from China, use the [China CDN Deployment Extension]().  Only use one method. Do not use both. 
* **Use a unique profile**  
Use a unique profile for each of your websites. Using multiple profiles lets you tag each website and customize the delivery of all Tealium-based content for that website.
* **tags.tiqcdn.cn**  
`tags.tiqcdn.cn` is available from Akamai through the closest node to the user. This means you can use a `.cn` domain for users outside the China firewall with no impact on performance for those users.

* **Internet Content Provider (ICP) license**  
For all web content to be delivered in mainland China, your website requires a valid ICP license.

## Update the code for your website

To update the code on your website:

1. Create a profile for the `.cn` domain. For more information, see [Manage Profiles]().
    * Consider using [profile libraries]() to share configurations between profiles to make setting up the new dedicated `.cn`  domain profile easier.
2. Update the publishing URLs in **Publish Configuration** to specify the `.cn` CDN path. For example:  
    ```bash
    https://tags.tiqcdn.cn/utag/ACCOUNT/PROFILE/dev/
    https://tags.tiqcdn.cn/utag/ACCOUNT/PROFILE/qa/
    https://tags.tiqcdn.cn/utag/ACCOUNT/PROFILE/prod/
    ```
    For more information, see [Publish Configuration]().
3. Add the following JavaScript, which uses `tags.tiqcdn.cn`, to the HTML source.
    ```javascript
    &lt;script type=&#34;text/javascript&#34;&gt;
      (function(a,b,c,d){
        a=&#39;https://tags.tiqcdn.cn/utag/ACCOUNT/PROFILE/prod/utag.js&#39;;
        b=document;c=&#39;script&#39;;d=b.createElement(c);d.src=a;d.type=&#39;text/java&#39;&#43;c;d.async=true;
        a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
      })();
    &lt;/script&gt;
    ```

## Use the China CDN Deployment Extension

Create and configure a China CDN Deployment Extension to determine the user&#39;s location and serve `utag.js` from the appropriate CDN. For more information on creating an extension, see [China CDN Deployment Extension]().
