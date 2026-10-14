---
title: About Data Layer Enrichment
description: Data Layer Enrichment imports AudienceStream attributes into your Tealium iQ data layer and provides access to visitor profile data through public APIs.
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/about/
---
Data layer enrichment has two components:

* The Tealium iQ configuration imports AudienceStream [attributes]() into your data layer and populates them on your website, where they can be used in load rules, extensions, and tags to create personalized experiences for your visitors.
* The server-side component provides access to visitor profile data through the Data Layer Enrichment API and Profile Definition API.

## Requirements

Data layer enrichment requires the following:

* An active **AudienceStream** profile with visit and visitor attributes defined.
* An active **Tealium Collect tag**.
* `utag.js` version 4.27 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

### Data layer enrichment profile in Tealium iQ

The Tealium iQ configuration links your iQ profile to a corresponding AudienceStream profile. After you configure the data layer enrichment profile in Tealium iQ, a new type of data layer variable called AudienceStream Attribute appears in the list of variables on the Data Layer screen. The visit and visitor attributes from the AudienceStream profile are imported and become available to use just like any other data layer variable.

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-audiencestreamattributes.png)

These attributes are populated with real-time customer data into the Universal Data Object (UDO) using the [Tealium Collect Tag](https://docs.tealium.com/tealium-collect-tag/).

Upon a visitor's first visit to your site, the Tealium Collect tag sends a call to AudienceStream to retrieve the most recent visitor profile attributes. The data is placed in the browser's local storage for future use.

On the second tracking call, the AudienceStream attributes are now in your UDO and affect any load rules, extensions, or tags that are configured with them.


<blockquote>
Because tags load asynchronously, the most recently retrieved set of attributes are available for use on subsequent tracking calls, rather than on the current page's events.
</blockquote>


#### Same origin policy

It's important to note that visitor data is stored in the browser using `localStorage` which adheres to the [same origin policy](https://en.wikipedia.org/wiki/Same-origin_policy) for security purposes. This means that data layer enrichment does not persist across `http` protocols or subdomains.

For example, when going from a page on `www.tealium.com` to a page on `secure.tealium.com`, the data layer enrichment data stored in `localStorage` does not persist to the new subdomain. Therefore, when a user changes subdomains or protocols, a new data layer enrichment call must be made to re-populate `localStorage` and the data may not be available until the subsequent tracking call.

### Server-side data layer enrichment

The server-side component exposes visitor profile data through two public endpoints: 

* The Data Layer Enrichment API, which returns the full visitor profile without filtering.
* The Profile Definition API, which returns badge and audience definitions.

If the server-side component is disabled, both APIs return a `404` response and no visitor data is available through those endpoints.

You can also create a domain allow list to restrict which domains can access visitor profiles using the TAPID cookie. For more information, see [Domain allow list](https://docs.tealium.com/enable-data-layer-enrichment/#domain-allow-list).

## Next steps

* [Enable server-side Data Layer Enrichment](https://docs.tealium.com/enable-data-layer-enrichment/)
* [Configure Data Layer Enrichment in Tealium iQ](https://docs.tealium.com/configure-data-layer-enrichment-iq/)
