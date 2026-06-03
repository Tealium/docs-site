---
title: Tags
description: Learn how to integrate your browser-based tag with Tealium iQ Tag Management.
url: https://docs.tealium.com/partners-and-industries/partner-with-us/tags/
---


Do you want your JavaScript tag offered in the Tealium tag marketplace? Do you want your users to seamlessly add your tag to their site without a lengthy release cycle? If so, this guide explains how tags work and the additional benefits of having an official integration with Tealium iQ Tag Management.

## How Tags Work

A tag in the tag marketplace provides a complete integration of the capabilities of your tag. This means that every option and tracked event expected by your tag is combined into a single configurable instance of the tag in a Tealium user&#39;s account.

### Configuration

The inner workings of your tag are hidden from most users so that they can focus on the point-and-click setup options. However, the code that runs your tag is available to Tealium users that are comfortable working with JavaScript.

A tag is managed in three parts:

* **Settings**   
Tag settings are set once per instance of the tag and usually do not vary from page to page.
[Learn more about tag settings]().
* **Load Rule**  
The load rule determines when the tag should load on a page or event. Load rule conditions are based on data layer values.
[Learn more about load rules]().
* **Data Mappings**  
Data mappings determine which dynamic values the tag needs from the data layer and the corresponding variable name used by the vendor. Mappings also determine how to track in-page events.
[Learn more about data mappings](/iq-tag-management/data-mappings/manage/).

### Loading in the Browser

Vendor tags are loaded by the Tealium Universal Tag (utag.js), a wrapper tag that contains the configuration logic from the iQ Tag Management account. Subsequent vendor tags are loaded using asynchronous JavaScript and run identically to how they run outside of a tag manager.

As a vendor, you can expect to see your same tag library or image pixel in the DOM of the page. At Tealium, we make every effort to load your tag exactly to your specifications. In rare cases where we must alter the code, we will ensure that the final tracking beacon matches your requirements.

Tealium can also load synchronous JavaScript to support A/B and multi-variate testing vendors.

### E-Commerce Values

For e-commerce tags that collect product and order data, Tealium offers a convenience feature, called the E-Commerce Extension, to ensure that all standard e-commerce data is automatically integrated with your tag. When the E-Commerce extension is configured in an account, it acts as a global data mapping to every tag that requires those values. This helps to minimize the amount of work needed to set up a tag of this type.

[Learn more about the E-Commerce Extension]().

## Tag Types

In addition to implementing your tag solution, Tealium can offer additional integration options depending on your system capabilities.

### Standard

Nearly all tags follow the same convention: load a JavaScript file, initialize the code, collect dynamic data from the page, trigger the tag. This standard framework can vary from the simplest image pixel with static parameters to a complicated JavaScript library that runs different code for each page type and collects dynamic data from the page.

### Cookie Match

The purpose of a cookie match tag is to use special requests to synchronize visitor identifiers between Tealium and your system. This lets you share your system&#39;s unique visitor ID with Tealium&#39;s server-side platform and receive Tealium&#39;s visitor ID in return. This type of integration is used _in addition to your standard tag_.

#### Example

The following example demonstrates a cookie match request:

```http
GET https://sync.example-dsp.net/get-userId?
tealium_visitor_id=abxyz0909&amp;
tealium_account=my_account&amp;
tealium_profile=main&amp;
tealium_datasource=abc123 
```

This request originates in the browser and sends the Tealium visitor ID to your system. The result is a forwarding request containing your system&#39;s visitor ID and Tealium&#39;s visitor ID back to Tealium. This indicates that Tealium is hosting the match table, which is preferred. The final request to Tealium includes all of the provided Tealium variables and the vendor matched ID.

The following is an example redirect back to Tealium:

```http
GET https://collect.tealiumiq.com/vdata?
dsp_uid=4595-23423442&amp;
tealium_visitor_id=abxyz0909&amp;
tealium_account=my_account&amp;
tealium_profile=main&amp;
tealium_datasource=abc123
```

The following cookie match example passes the redirect request as a URL parameter, if the DSP&#39;s endpoint accepts it:

```http
GET https://sync.example-dsp.net/get-userId?
redirect=https://collect.tealiumiq.com/vdata?dsp_uid=$UID&amp;tealium_visitor_id=abxyz0909&amp;tealium_account=egbrand&amp;tealium_profile=main&amp;tealium_datasource=abc123
```

### Server-Side Enabled

Server-side enabled tags have the added ability to send events directly to Tealium EventStream and AudienceStream. For example, a user experience vendor inferring user sentiment by tracking mouse movements could trigger specific events directly to Tealium Collect. This type of integration _is included with your standard tag_.

The following example function sends data to the Tealium event endpoint:  
```javascript
window.tealium.sendEvent = function(event_data) {
    //Send Event to CDH event endpoint
    event_data[&#39;tealium_event&#39;] = &#34;EVENT_NAME&#34;;
    event_data[&#39;tealium_account&#39;] = b.tealium_account; // required
    event_data[&#39;tealium_profile&#39;] = b.tealium_profile; // required
    event_data[&#39;tealium_visitor_id&#39;] = b.tealium_visitor_id; // required
    event_data[&#39;tealium_trace_id&#39;] = b[&#34;cp.trace_id&#34;]; // optional
    event_data[&#39;tealium_datasource&#39;] = &#39;DATASOURCE_KEY&#39;; // optional

    var data = new FormData();
    data.append(&#34;data&#34;, JSON.stringify(event_data));

    if (window.utag &amp;&amp; utag.data &amp;&amp; utag.data.tealium_account) {
        var xhr = new XMLHttpRequest();
        xhr.open(&#34;POST&#34;, &#34;https://collect.tealiumiq.com/event?&#34;);
        xhr.send(data);
        }
    return true;
};
```

## Become a Partner

[Contact us](https://tealium.com/tealium-partner-network/) to integrate your technology.
