---
title: About Visitor Privacy API (formerly Visitor Lookup API)
description: The Visitor Privacy API is used to query visitor profile records from the Customer Data Hub in support of General Data Protection Regulation (GDPR) compliance to satisfy the requirement of responding to data subject access requests.
url: https://docs.tealium.com/api/v3/visitor-privacy/about/
---
## How it works

This API lets you retrieve known data about a specific visitor, delete a visitor record, and check the status of a delete request. Visitor lookups are based on a [Visitor ID](https://docs.tealium.com/visitor-id-attribute/) attribute from your account.

### Limits and intended use

The Visitor Privacy API is intended to satisfy regulatory requirements such as GDPR and CCPA and is not designed for high volume usage. We recommend that you have a maximum of one (1) connection open to this API at any given time. Contact your account manager if you estimate that your usage will exceed 1000 API calls per day.

## Rate Limits

The Visitor Privacy API has a default rate limit of 50 requests/second. 

## Authentication


<blockquote>
The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.
</blockquote>


To learn about generating a bearer token from the API key, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).

