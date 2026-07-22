---
title: About Data Layer Enrichment
description: Data Layer Enrichment makes AudienceStream visit and visitor attributes available in your Tealium iQ configuration and populates that data in your data layer.
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/about/
---
Data Layer Enrichment imports your AudienceStream [attributes]() into your Tealium iQ account and makes them available as part of your data layer. The visitor data collected in AudienceStream is populated in the data layer on your website. Those attributes can then be used in load rules, extensions, and tags in your iQ account to create personalized experiences for your visitors.

## Requirements

Data Layer Enrichment requires the following:

* An active **AudienceStream** profile with visit and visitor attributes defined.
* An active **Tealium Collect tag**.
* `utag.js` version 4.27 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

Data Layer Enrichment is a profile-level setting in iQ that links to a corresponding AudienceStream profile. After Data Layer Enrichment is enabled, a new type of data layer variable called AudienceStream Attribute appears in the list of variables on the Data Layer screen. The visit and visitor attributes from the AudienceStream profile are imported and become available to use just like any other data layer variable.

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-audiencestreamattributes.png)

These attributes are populated with real-time customer data into the Universal Data Object (UDO) using the [Tealium Collect Tag](https://docs.tealium.com/tealium-collect-tag/).

Upon a visitor's first visit to your site, the Tealium Collect tag sends a call to AudienceStream to retrieve the most recent visitor profile attributes. The data is placed in the browser's local storage for future use.

On the second tracking call, the AudienceStream attributes are now in your UDO and affect any load rules, extensions, or tags that are configured with them.


<blockquote>
Because tags load asynchronously, the most recently retrieved set of attributes are available for use on subsequent tracking calls, rather than on the current page's events.
</blockquote>


### Same origin policy

It's important to note that visitor data is stored in the browser using `localStorage` which adheres to the [same origin policy](https://en.wikipedia.org/wiki/Same-origin_policy) for security purposes. This means that data layer enrichment does not persist across `http` protocols or subdomains.

For example, when going from a page on `www.tealium.com` to a page on `secure.tealium.com`, the data layer enrichment data stored in `localStorage` does not persist to the new subdomain. Therefore, when a user changes subdomains or protocols, a new data layer enrichment call must be made to re-populate `localStorage` and the data may not be available until the subsequent tracking call.

### Domain allow list

By default, Data Layer Enrichment will look up the visitor profile based on the TAPID cookie, if present, regardless of the domain the request came from. 

Creating an allow list prevents non-trusted domains from accessing visitor profiles based on the TAPID cookie. 

Data Layer Enrichment retrieves the visitor ID depending on the request domain and allow list you set up:

* **Domains match**  
If the referrer matches a domain in the allow list, Data Layer Enrichment uses the visitor ID in the third-party TAPID cookie, if present. Otherwise the visitor ID from the URL path is used.
* **Domains do not match**  
If the referrer does not match a domain in the allow list, Data Layer Enrichment ignores the TAPID cookie and uses the visitor ID in the URL path.

#### Subdomains

When you add a domain to the allow list, all of its subdomains are automatically included. For example, if you allow `example.com`, any subdomain that matches `*.example.com` is included.

```
http://example.com
https://mobile.example.com/xyz/index.html
http://app.mobile.example.com
```

#### Create an allow list

To limit requests from only specific, trusted domains, create an allow list in your profile.

1. Go to **Admin menu > Data Layer Enrichment**.
1. Enter the comma-separated list of domains you trust. You can add a maximum of 250 domains per profile. Do not include the `http` or `https` protocol before the domain (for example, `example.com`).
1. Click **Save**.
1. Save and publish your changes.