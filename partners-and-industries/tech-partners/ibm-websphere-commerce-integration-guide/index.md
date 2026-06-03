---
title: IBM WebSphere Commerce Integration Guide
description: IBM Websphere Commerce's Tealium Extension is designed to help you integrate Tealium iQ Tag Management within your IBM Websphere solution. Using this extension you can add Tealium's Universal Data Object (UDO) into your site's data layer.
url: https://docs.tealium.com/partners-and-industries/tech-partners/ibm-websphere-commerce-integration-guide/
---
This document is for developers who need to integrate Tealium iQ Tag Management within an IBM Websphere-based e-commerce site. Please note that you should be familiar with the IBM Websphere Commerce product core and its e-commerce functionality.

## Compatibility notes

IBM has certified this version of the Tealium extension and added Tealium as an integration partner. Support for the B2B E-Commerce Engine has not yet been tested.

## Integration

### Websphere extension installation

The Tealium extension is distributed as a packaged file in TGZ format: [tealium-websphere-commerce.tgz](/images/tech-partners/tealium-websphere-commerce.tgz).

To install the extension, unpack the contents of the compressed file into the appropriate locations detailed below. The instructions below use the fictional `AuroraStorefrontAssetStore` project with a store ID of `10152`. Replace these values with your own.

To install the Tealium extension:

1. Place the `TealiumUDO.jsp` file and related `.jspf` files into the `/Stores/WebContent/ AuroraStorefrontAssetStore/Tealium` directory.
2. Place the `tealium_udo_helper_1_2_0a.jar` file (or later version) into the `/Stores/WebContent/WEB-INF/lib/` directory.![](/images/tech-partners/ibmwebsphere1.png)
3. To activate the extension, insert the following entries into the database and restart the Websphere Commerce web server:
```
  insert into storeconf (storeent_id, name, value, optcounter) values (10152, &#39;wc.pgl.jspInclude_Tealium_TealiumUDO&#39;, &#39;/AuroraStorefrontAssetStore/Tealium/TealiumUDO.jsp&#39;, 0);
  insert into storeconf (storeent_id, name, value, optcounter) values (10152, &#39;wc.tealium.account&#39;, &#39;myaccount&#39;, 0);
  insert into storeconf (storeent_id, name, value, optcounter) values (10152, &#39;wc.tealium.profile&#39;, &#39;myprofile&#39;, 0);
  insert into storeconf (storeent_id, name, value, optcounter) values (10152, &#39;wc.tealium.environment&#39;, &#39;prod&#39;, 0);
  ```
4. Set the `env_includeJSPFExtension` variable to `true` in the `/Stores/WebContent/AuroraStoreFrontAssetStore/Common/EnvironmentSetup.jspf` file

### iQ Tag Management setup

To pass data from your Tealium Data Layer to analytics tags, you must identify the data points in your Data Layer for iQ Tag Management, as follows:

1. Log into iQ Tag Management and navigate to the **Data Layer** tab.
1. Click the drop-down next to **Add Data Source**, then click **Add Common
Data Sources**.
1. Under **Provider Bundles**, select **IBM WebSphere Commerce** and click **Import This Bundle**.![](/images/tech-partners/ibmwebsphere2.png)
1. Click **Close**.
1. **Save/Publish** the changes to your iQ Tag Management profile.

### Validation

To validate the implementation, navigate to your site and view the page source. In the page’s source, look for `utag_data` (Tealium’s UDO). You can also see the `Validation.txt` file included in the distribution package for sample values on specific commerce pages.

Use a proxy tool or Chrome developer tools to confirm that the browser is loading the `utag.js` file. After you activate a tag in iQ Tag Management, such as IBM Digital Analytics, you can use Charles Proxy, HTTP Fox, or Chrome Developer Tools to see the data passing to your analytics vendor. ![](/images/tech-partners/ibmwebsphere3.png)

The values for `wc.tealium.account` and `wc.tealium.profile` are the Tealium account and profile associated with the site, respectively.
