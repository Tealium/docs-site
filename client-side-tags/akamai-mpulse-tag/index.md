---
title: Akamai mPulse Tag Setup Guide
description: This article describes how to set up the Akamai mPulse tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/akamai-mpulse-tag/
---
Real time performance monitoring tools provide the capabilities needed for detailed performance and advanced error analysis and the ability to correlate the results directly to business metrics, such as conversions, page views, and revenue.

You can easily add, implement, and manage the Akamai mPulse JavaScript tag through Tealium iQ. You can then create load rules to determine when and where to trigger this vendor and use the mapping feature to control which data points are shared with Akamai.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **API Key**: The API key supplied by Akamai. This key is the unique identifier for your data.

### Advanced settings

These settings are not required for most tags, but are needed for Akamai.

  * Set **Tag Timing** to **Prioritized**.  
Determines the timing of the tag firing. Prioritized tags fire immediately as `utag.js` loads.
  * Set **Synchronous Load Type** to **No**.  
If set to **Yes**, the tag will not fire.

## Load rules

Use the following steps to apply load rules:

1. Click **Next** to advance to the Load Rules tab.
1. From Load Rules, apply the **Load on All Pages and Events** rule.  
This step is required to enable the tag to be bundled when configuring the Publish settings in the following steps.
1. Click **Finish**.
1. Click **Save** in the upper right corner but do not publish.

### Configure and publish settings to optimize performance

Use the following steps to configure and publish settings that will optimize tag performance:

1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
There are many Publish Settings options described on the Tealium support site. For Akamai mPulse, activate the following two optional settings for Akamai to improve tag performance.

1. From the **Publish Configurations** dialog, click the **General Publishing** tab.
1. Scroll down to **Performance Optimization** and set the **Minify Tag Templates** and **Bundle Tags Loaded on All Pages** toggles to **ON**.
    * Setting the **Performance Optimization** option to **On** ensures that any tags that load on the All Pages load rule are included inline in your `utag.js `file instead of in a separate, numbered file. Although your `utag.js` file will be larger, it will remove one http request (server call) as the page loads.
    * Setting the **Minify Tag Templates** option to **On** applies &#34;minification&#34; to the generated JavaScript, which removes unnecessary whitespace so that the file size downloaded is smaller.

1. Click **Apply** to close the **Publish Settings** dialog.  

### Publishing and testing

As a final step, publish and test your new tag as follows:

1. In the **Save/Publish dialog**, do not select the **Overwrite current version** checkbox. Using **Save As** saves your change as a new version, which enables you to roll back your changes if needed.After the updated `utag.js` is loaded to the CDN, Akamai tag will appear in the browser.
1. Use a tag monitor, such as Ghostery, to test that the tag is performing as expected, such as Ghostery. You can use your browser&#39;s network monitoring tool. You will know that the tag is firing correctly if you see the following request: ![](/images/client-side-tags/no-title-1727i9db56b2bbbbe8690.png)
1. Monitor the request at `http://c.go-mpulse.net/boomerang`.

The key displayed will match the API key you entered when you configured the Akamai mPulse tag.
