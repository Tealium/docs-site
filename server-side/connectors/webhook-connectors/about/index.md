---
title: About webhook connectors
description: Connect the webhook connector to an HTTP API endpoint to send event or visitor data directly to your service, either by posting the full JSON payload or mapping individual attributes to request fields.
url: https://docs.tealium.com/server-side/connectors/webhook-connectors/about/
---
## Requirements

* Tealium account enabled for EventStream (for event data)
* Tealium account enabled for AudienceStream (for visitor data)

## How it works

The webhook connector sends event or visitor data to your vendor through HTTP requests. All aspects of the HTTP request can be configured to create the exact request needed by your vendor.

## Authentication

The following authentication methods are supported for HTTP-based webhook connectors:

* **BasicAuth**: Authenticate webhook requests using a username and password sent with the request.
* **OAuth2 3-Legged**: Authenticate webhook requests through a user-consent flow that issues access tokens on the user&#39;s behalf. Requires the user to log in to the service to obtain an access token.
* **OAuth2 2-Legged**: Authenticate webhook requests using server-to-server access tokens without any user involvement.
* **JWT**: Authenticate webhook requests with a JSON web token.

Webhook OAuth2 is used for services that explicitly require OAuth 2.0 authentication.

For more information, see .

To use a webhook to send data to a JDBC-compatible database, see [Webhook JDBC]().

## Actions

| Action Name    | Description    | Webhook (BasicAuth) | Webhook OAuth2 |
|:--------|:--------|:------|:-----|
| Send Event Data via HTTP Request  | Sends the entire event object, either as a URL-encoded JSON string or a JSON payload.     | ✓      | ✓     |
| Send Visitor Data via HTTP Request | Sends the entire visitor profile object, either as a URL-encoded JSON string or a JSON payload. | ✓    | ✓      |
| Send Customized Data via HTTP Request (Advanced)    | Sends individual event/visitor attributes specified with mappings          | ✓      | ✓       |
| Send Batched Data via HTTP Request  | Sends the entire event object, either as a URL-encoded JSON string or a JSON payload.     | ✓      | ✓     |
| Send Batched Customized Data via HTTP Request (Advanced) | Sends batched event/visitor attributes specified with mappings.    | ✓      | ✓          |

For more information, see .

## HTTP response cookies

While cookie-based session management is common in web browsers, it is generally discouraged in server-to-server environments that communicate with stateless APIs. For that reason, the webhook connector does not track cookie-based sessions and effectively ignores `Set-Cookie` header values in HTTP responses.