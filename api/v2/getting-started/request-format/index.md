---
title: Tealium API request format
description: This article describes the request format for Tealium APIs.
url: https://docs.tealium.com/api/v2/getting-started/request-format/
---
The [previous v1 API]() is still available, but will eventually be deprecated.

## Root URL

Each API has its own endpoint and supported parameters. The root URL for all API requests is:

```
https://api.tealiumiq.com/v2
```

An API endpoint is documented with a specific HTTP method and path, for example:

```
GET /revisions
```

Some endpoints show placeholder variables ( `{variable}`) to indicate values that you supply. Most endpoints require the name of the your iQ Tag Management (TiQ) account and profile in the path of the call.

Example API endpoint path for TiQ revisions:

```
https://api.tealiumiq.com/v2/accounts/{account}/{profile}/revisions
```

## Request and response format

The API supports JavaScript Object Notation (JSON). API requests that use JSON require the following header setting:

```
Content-Type: application/json
```

Most responses are in JSON format. Documentation for each endpoint contains example cURL calls and responses.
