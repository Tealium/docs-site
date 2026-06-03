---
title: Tealium Collect Tag Setup Guide
description: The Tealium Collect tag is the primary data collection tag for Tealium EventStream and AudienceStream. This article explains how to add and configure the Tealium Collect tag in your iQ Tag Management profile.
url: https://docs.tealium.com/client-side-tags/tealium-collect-tag/
---
## Requirements

* Contact your account manager to enable this tag for your account.

## How it works

The Tealium Collect tag captures a mix of predefined data and dynamic data from the page. This tag requires no mapping; it automatically sends everything set in `utag.data` or any data passed to a tracking call.

For a full list of collected variables, see . For information about how this data appears in EventDB, see .

To see the incoming data from the Tealium Collect tag, see [Live Events]().

Use the Tealium Collect tag with the following features:

* **Reduce pixel requests with EventStream**  
Use this tag with EventStream and event feeds to transition client-side tags to server-side connectors, such as the [Webhook connector]().
* **AudienceStream**  
Use this tag with AudienceStream to identify and action your visitors.
* **DataAccess**  
The event data coming from this tag can also be made available to DataAccess, where it can be analyzed using Business Intelligence (BI) tools of your choice.
* **Enrich your data layer**  
Use the data enrichment setting to add visit and visitor attributes from AudienceStream to your data layer.  
For more information, see .

## Tag tips

* This tag automatically sends all data in `utag.data` on initial page load or any data object passed to `utag.view()` or `utag.link()`.
* When using proxy tools to inspect network requests, look for the `POST` method (instead of GET).
* Specify a value in the **Tealium Profile** field only when **Tealium Collect Endpoint** field is blank and your server-side data collection profile is something other than the current profile.

## Best practices

Apply the following best practices in your implementation:

* To prioritize third-party client-side tags, position the Tealium Collect tag last in your list of tags to allow them to run first.
* Do not add more than one instance of the Tealium Collect tag in your profile.
* Use the latest version of the uTag Loader template. For more information, see .

## Tag configuration

First, go to the tag marketplace and add the Tealium Collect tag. For more information, see [Manage tags]().

After adding the tag, configure the following settings:

* **Title**
  * Enter a title for this tag.
  * Default: `Tealium Collect`.
* **Tealium Collect Endpoint** (Optional)
  * Only for use with custom data collection endpoints.
  * Custom URLs entered into this field automatically default to HTTPS unless otherwise specified.
  * Default: Not set.
* **Data Layer Enrichment Frequency**  
  * Enables AudienceStream data layer enrichment.
  * Choose the frequency for enriching your data layer with AudienceStream data.  
    * **None**: (default) Enrichment does not occur.
    * **Infrequent**: (Recommended) enrichment occurs once per session.
    * **Frequent**: Enrichment occurs on every page load.
* **Tealium Collect Profile** (Optional)  
  * Use to override the existing data collection endpoint, such as the AudienceStream profile that receives data from your site.
  * Specify a value in this field only when the **Tealium Collect Endpoint** field is blank and your data collection profile for AudienceStream is different from the current profile.
  * Default: Not set.
* **Tealium Data Source Key**  
  * (Optional) The unique identifier of the data source you are tracking through the Customer Data Hub.
  * Default: Not set.
* **Tealium Collection Region**
  * The geographic location of the data collection servers.
  * Default: Global (Recommended).
  * If you are not sure what to choose, contact your Account Manager.
* **Sample Size** (Optional)  
  * Default: 100% (Recommended).
  * Use this option during a trial on high volume sites to limit data collection to a small percentage of visitors.
* **Use SendBeacon**
  * Set to `true` to use `navigator.sendBeacon()` to send tracking calls.
  * Set to `false` to use the legacy browser method `XMLHttpRequest` to send tracking calls.
  * SendBeacon is intended for small amounts of data and has a data size limit of 64Kb in most browsers. For more information, see [Navigator:sendBeacon() method](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon).
  * Default: `true`.
* **Use HTTP API Endpoint**
  * Set to true to use the [HTTP API endpoint]() instead of the Tealium Collect endpoint.
  * Default: `false`.
* **Visitor Service Override**
  * Specifies the domain used to retrieve visitor profile data from Tealium AudienceStream for data layer enrichment.
  * Enter a custom domain to override the default value.
  * This value is usually set to a first-party domain, such as `visitor-service.yourdomain.com`.
* **Tealium Cookie Domain** (Optional)
  * The domain used to set the Tealium anonymous ID (TAPID cookie).
  * Enter a custom domain to override the default value.
  * This value is usually set to a first-party domain, such as `.yourdomain.com`.
  * This option only applies if the [first-party domains feature]() is enabled and the Tealium Collect tag is on that first-party domain.
* **Tealium Cookie Expiry** (Optional)
  * The expiration time of the TAPID cookie in seconds.
* Filter data sent to the Tealium Collect endpoint using the following settings:
  * **Send UDO Variables**: The default is `true`.
  * **Send Cookie Values**: The default is `true`.
  * **Send Meta Values**: The default is `true`.
  * **Send QP Values**: The default is `true`.
  * **Send Session Storage Variables**: The default is `false`.
  * **Send LocalStorage Variables**: The default is `false`.

## Advanced

For first-party CNAME of the Tealium visitor service endpoint used for data layer enrichment, use a JavaScript Code extension scoped to the Tealium Collect tag to override the URL with the following code:

```js
u.visitor_service_override = &#34;https://visitor-service.example.co.uk&#34;;
```

## Load rules

The best practice is to use the **All Pages and Events** load rule. Loading this tag on all pages ensures that all events are tracked server-side, which allows for full activation of both event and audience data. Using custom load rules on this tag limits the data that can be activated server-side and is not recommended.

### Working with trace

If you use a more restrictive load rule and you&#39;ve noticed that you can&#39;t end a session in the trace tool, a custom load rule is needed to allow the special event triggered by trace.

Create the following load rule and assign it to the Tealium Collect tag.

```
ut.event equals (ignore case) kill_visitor_session
```

![](/images/client-side-tags/tealium-collect-load-rule-for-trace.png)

## Implementing with mobile

For deployments using [Tealium for Android]() or [Tealium for iOS](), note the following:

* The default [mobile publish settings]() enable the native mobile Tealium Collect service by default.  
Learn more about the [native Collect module for mobile]().
* When using the [Tealium Collect tag with the Tag Management module for mobile](), ensure that the **Tealium Collect** option in the [mobile publish settings]() is off to avoid duplicate tracking.

## Cookies

The Tealium Collect tag creates the following cookies:

* `utag_main_v_id`: a unique, partially random identifier to ensure compliance with data privacy and consent rules. The Collect tag creates this cookie in `utag.js` version 4.50 and later if the [`always_set_v_id` utag setting]() is set to `true`. Otherwise, the Collect tag creates the cookie under the following conditions:
    * The `suppress_v_id` Collect setting is set to `false` or not set.
    * The cookie&#39;s value is not already set.  
    For more information about this cookie, see [`utag.js` Release Notes version 4.50]().
* `utag_main_dc_group`: a random number to use with the **Sample Size** setting.
* `utag_main_dc_region`: the AudienceStream region where the visit session is stored. This cookie is used for determining the endpoints for [data layer enrichment]().

### Legacy cookies

For compatibility reasons, the Tealium Collect tag creates the following legacy cookies:

* `utag_main_dc_visit`: The number of sessions for which the Tealium Collect tag has fired.
* `utag_main_dc_event`: The number of events for which the Tealium Collect tag has fired.

For more information about these cookies, see [Data Layer: Cookies]().