---
title: Usage examples
description: This article provides examples of HTTP requests.
url: https://docs.tealium.com/server-side/connectors/webhook-connectors/usage-examples/
---
A simple JSON object is used in these examples for the purpose of clarity. The actual data sent is a full event or visitor object. We also include a single URL parameter of `param1` receiving a value of `value1` to demonstrate how additional parameters are sent.

### Send event/visitor - GET method

When using the GET method with the Send Event Data or Send Visitor Data actions, the data is sent as a single query string parameter named `data` . The value is a URL-encoded JSON string of the event/visitor data object. Any URL parameters configured are appended as additional query string parameters.

In this example the data is:

```json
{
    "foo" : "bar"
}
```

The resulting URL-encoded JSON string is:

`%7B%22foo%22%3A%22bar%22%7D`

You can see that this appears in the final GET request as the following query string parameter:

`data=%7B%22foo%22%3A%22bar%22%7D`

```
GET /webhook-service?data=%7B%22foo%22%3A%22bar%22%7D&param1=value1

VERSION: HTTP/1.1
CONNECTION: close
ACCEPT-ENCODING: gzip
X-HEADER-KEY: header_value
COOKIE: cookie_key=cookie_valie,__cfduid=d63c6b0e0a23195e9a7142f314360b4e11502122913
USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
```

### Send event/visitor - POST method

The following are sample POST requests for the **`application/json`** and `application/x-www-form-urlencoded`content types.

##### **Content-Type: application/json**

The body data is sent as a JSON payload.

```
POST /webhook-service?param1=value1

VERSION: HTTP/1.1
CONNECTION: close
ACCEPT-ENCODING: gzip
X-HEADER-KEY: header_value
COOKIE: cookie_key=cookie_valie
CONTENT-TYPE: application/json; charset=UTF-8
USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
CONTENT-LENGTH: 13

{
    "foo": "bar"
}

```

##### **Content-Type: application/x-form-urlencoded**

The body data is sent as a URL-encoded JSON string using the form-data field named `data`.

```
POST /webhook-service?param1=value1

VERSION: HTTP/1.1
CONNECTION: close
ACCEPT-ENCODING: gzip
X-HEADER-KEY: header_value
COOKIE: cookie_key=cookie_valie,__cfduid=d63c6b0e0a23195e9a7142f314360b4e11502122913
CONTENT-TYPE: application/x-www-form-urlencoded; charset=UTF-8
USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
CONTENT-LENGTH: 32

data=%7B%22foo%22%3A%22bar%22%7D
```

