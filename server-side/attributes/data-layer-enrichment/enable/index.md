---
title: Enable server-side Data Layer Enrichment
description: Enable or disable server-side Data Layer Enrichment to control access to the Data Layer Enrichment API and Profile Definition API.
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/enable/
---
## How it works

Data layer enrichment provides access to visitor data through two public, unauthenticated APIs:

* The [Data Layer Enrichment API](https://docs.tealium.com/get-data-layer-enrichment-api/), which returns the full visitor profile without filtering.
* The [Profile Definition API](https://docs.tealium.com/get-profile-definition-api/), which returns badge and audience definitions for your profile.

This setting is separate from the [Data Layer Enrichment configuration in Tealium iQ](https://docs.tealium.com/configure-data-layer-enrichment-iq/). The Tealium iQ configuration determines which AudienceStream profile provides attributes to the data layer. It does not control access to the Data Layer Enrichment APIs.

When data layer enrichment is enabled, both APIs are available and return data for valid requests.

When data layer enrichment is disabled, both APIs return a `404` response. Integrations that rely on these APIs stop receiving data. The Tealium Collect tag also uses this endpoint to retrieve visitor attributes, so disabling data layer enrichment also stops client-side attribute sync in Tealium iQ.

Data layer enrichment is enabled by default on existing profiles and disabled by default on new profiles. If you are setting up data layer enrichment on a new profile, enable this setting before using the APIs.

## Enable or disable data layer enrichment

1. In the admin menu, click **Data Layer Enrichment**.
1. Enable or disable **Data Layer Enrichment**.
1. Click **Save**.
1. Save and publish your changes.

## Domain allow list

By default, data layer enrichment looks up the visitor profile based on the TAPID cookie, if present, regardless of the domain the request came from.

Creating an allow list prevents non-trusted domains from accessing visitor profiles based on the TAPID cookie.

Data layer enrichment retrieves the visitor ID depending on the request domain and allow list you set up:

* **Domains match**  
If the referrer matches a domain in the allow list, data layer enrichment uses the visitor ID in the third-party TAPID cookie, if present. Otherwise the visitor ID from the URL path is used.
* **Domains do not match**  
If the referrer does not match a domain in the allow list, data layer enrichment ignores the TAPID cookie and uses the visitor ID in the URL path.

### Subdomains

When you add a domain to the allow list, all of its subdomains are automatically included. For example, if you allow `example.com`, any subdomain that matches `*.example.com` is included.

```
http://example.com
https://mobile.example.com/xyz/index.html
http://app.mobile.example.com
```

### Create an allow list

To limit requests from only specific, trusted domains, create an allow list in your profile.

1. Go to **Admin menu > Data Layer Enrichment**.
1. Enter the comma-separated list of domains you trust. You can add a maximum of 250 domains per profile. Do not include the `http` or `https` protocol before the domain (for example, `example.com`).
1. Click **Save**.
1. Save and publish your changes.

## When to disable data layer enrichment

Disable data layer enrichment in the following cases:

* To limit exposure of visitor data for privacy or compliance reasons.
* To restrict access by external systems or vendors.
* To reduce the number of systems that can access visitor profile data.

## Use authenticated access

The data layer enrichment APIs are public and unauthenticated.

If you require authenticated access to visitor data, use the Context API. For more information, see [About Context API](https://docs.tealium.com/about-context-api/).
