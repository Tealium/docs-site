---
title: About Visitor Profile API
description: The Visitor Profile API is used to query visitor profile records from the Customer Data Hub.
url: https://docs.tealium.com/api/v3/visitor-profile/about/
---
## Requirements

This feature requires the following:

* Server-side reader, editor, or publisher legacy permissions, or
* Minimum **View** Visitor Lookup platform permissions

## How it works

This API lets you retrieve known data about a specific visitor to improve personalization for first time visitors to your website. Visitor lookups are based on a [Visitor ID](https://docs.tealium.com/visitor-id-attribute/) attribute from your account.

## Rate Limits

The Visitor Profile API has a default rate limit of 50 requests/second. If you need a higher rate limit, contact your Tealium account manager with your projected usage.

## Authentication


<blockquote>
The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.
</blockquote>


To learn about generating a bearer token from the API key, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).
