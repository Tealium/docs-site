---
title: Dun & Bradstreet Web Visitor ID Tag Setup Guide
description: This article describes how to set up the Dun & Bradstreet Web Visitor ID tag.
url: https://docs.tealium.com/client-side-tags/dun-amp-bradstreet-web-visitor-id-tag/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## Tag Tips

* Use mapping to dynamically override standard configuration values.
* Use the JavaScript Code extension to set returned data.  
Example:  
```javascript
window.tealium_dnbwvid = function(dnb_Data)
{
 // Set data here, ex: visitor_duns = dnb_Data.duns;
}
```

* To make Dun &amp; Bradstreet data available as server-side attributes (once per session):

  * Set **Send to Tealium (server-side)** to `true`
  * If left blank, Tealium Account and Tealium Profile will be automatically populated with your current account and profile.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the D&amp;B Web Visitor ID tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **API Key**
  * Your API key supplied by Dun &amp; Bradstreet.
  * Example: `//API_KEY_HERE.d41.co/sync/`

* **Data Key**
  * API Key supplied in the getData call.
  * Leave blank to use the API Key.
  * Example: `dnbvid.getData(&#39;DATA_KEY_HERE&#39;,&#39;json&#39;,&#39;T&#39;... )`

* **Send to Tealium (server-side)**
* **Tealium Account**
  * (Optional) Override the `tealium_account` used for server-side requests.

* **Tealium Profile**
  * (Optional) Override the `tealium_profile` used for server-side requests.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`api_key`|  &lt;ul&gt;&lt;li&gt;Your API key supplied by Dun &amp; Bradstreet.&lt;/li&gt;&lt;li&gt;Example: `//API_KEY_HERE.d41.co/sync/`&lt;/li&gt;&lt;/ul&gt; |
|`data_key`|  &lt;ul&gt;&lt;li&gt;API Key supplied in the getData call.&lt;/li&gt;&lt;li&gt;Leave blank to use the API Key.&lt;/li&gt;&lt;li&gt;Example: `dnbvid.getData(&#39;DATA_KEY_HERE&#39;,&#39;json&#39;,&#39;T&#39;... )`&lt;/li&gt;&lt;/ul&gt; |
|`send_to_tealium`|  &lt;ul&gt;&lt;li&gt;Send to Tealium&lt;/li&gt;&lt;li&gt;Data received from Dun &amp; Bradstreet is made available to Tealium server-side.&lt;/li&gt;&lt;/ul&gt; |
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;(Optional) Tealium Account&lt;/li&gt;&lt;li&gt;Override the `tealium_account` used for server-side requests.&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;(Optional) Tealium Profile&lt;/li&gt;&lt;li&gt;Override the `tealium_profile` used for server-side requests.&lt;/li&gt;&lt;/ul&gt; |
