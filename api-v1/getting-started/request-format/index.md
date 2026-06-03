---
title: Request format
description: This article describes the request format for Tealium APIs.
url: https://docs.tealium.com/api-v1/getting-started/request-format/
---

This is an older version of [the current Tealium API]().


## Root URL

Each API will have its own endpoint and supported parameters. The root URL for all API requests is:

```
https://api.tealiumiq.com/v1
```

An API endpoint will be documented with its specific HTTP method and the path, for example:

```
GET /revisions
```

Endpoints that use placeholder values will use curly braces like this:`{value}`. These will be replaced with values specific to your API calls. Most endpoints require the name of the iQ account and profile on which to perform the call in the path.

A full API endpoint might look like this:

```
https://api.tealiumiq.com/v1/accounts/{account}/{profile}/revisions
```


## Request and response format

The API supports JSON which means most calls must have the proper header set to: `Content-Type: application/json` . Most responses will also be in the form of JSON. The documentation for each endpoint will have example curl calls and responses.


