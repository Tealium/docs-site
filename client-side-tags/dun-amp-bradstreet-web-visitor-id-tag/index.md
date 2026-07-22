---
title: Dun & Bradstreet Web Visitor ID Tag Setup Guide
description: This article describes how to set up the Dun & Bradstreet Web Visitor ID tag.
url: https://docs.tealium.com/client-side-tags/dun-amp-bradstreet-web-visitor-id-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


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

* To make Dun & Bradstreet data available as server-side attributes (once per session):

  * Set **Send to Tealium (server-side)** to `true`
  * If left blank, Tealium Account and Tealium Profile will be automatically populated with your current account and profile.

## Tag Configuration

First, go to Tealium's tag marketplace and add the D&B Web Visitor ID tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **API Key**
  * Your API key supplied by Dun & Bradstreet.
  * Example: `//API_KEY_HERE.d41.co/sync/`

* **Data Key**
  * API Key supplied in the getData call.
  * Leave blank to use the API Key.
  * Example: `dnbvid.getData('DATA_KEY_HERE','json','T'... )`

* **Send to Tealium (server-side)**
* **Tealium Account**
  * (Optional) Override the `tealium_account` used for server-side requests.

* **Tealium Profile**
  * (Optional) Override the `tealium_profile` used for server-side requests.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`api_key`|  <ul><li>Your API key supplied by Dun & Bradstreet.</li><li>Example: `//API_KEY_HERE.d41.co/sync/`</li></ul> |
|`data_key`|  <ul><li>API Key supplied in the getData call.</li><li>Leave blank to use the API Key.</li><li>Example: `dnbvid.getData('DATA_KEY_HERE','json','T'... )`</li></ul> |
|`send_to_tealium`|  <ul><li>Send to Tealium</li><li>Data received from Dun & Bradstreet is made available to Tealium server-side.</li></ul> |
|`tealium_account`|  <ul><li>(Optional) Tealium Account</li><li>Override the `tealium_account` used for server-side requests.</li></ul> |
|`tealium_profile`|  <ul><li>(Optional) Tealium Profile</li><li>Override the `tealium_profile` used for server-side requests.</li></ul> |
