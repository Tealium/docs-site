---
title: Tealium V3 API request format
description: This article provides information about the Tealium v3 API request format.
url: https://docs.tealium.com/api/v3/getting-started/request-format/
---## Root URL

Each API has its own endpoint and supported parameters. The root URL for all API requests is:

```none
https://platform.tealiumapis.com/v3
```

An API endpoint is documented with a specific HTTP method and path, for example:

```none
GET /visitor
```

Some endpoints show placeholder variables (`{variable}`) to indicate values that you supply. Most endpoints require the name of the your Tealium account and profile in the path of the call.

Example API endpoint path for Visitor Profile API:

```none
https://platform.tealiumapis.com/v3/customer/visitor/accounts/{account}/profiles/{profile}
```

## Request and response format

The API supports JavaScript Object Notation (JSON). API requests that use JSON require the following header setting:

```none
Content-Type: application/json
```

Most responses are in JSON format. Documentation for each endpoint contains example cURL calls and responses.

## Rate Limits

Tealium API endpoints serve different purposes and can vary in their rate limits. Check the specific API endpoint documentation for rate limit information. If you exceed the stated rate limit for any API endpoint, you can expect the HTTP `429 Too Many Requests` response code.


<blockquote>
If your business needs require higher limits, contact your Tealium account manager.
</blockquote>


