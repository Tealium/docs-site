---
title: Authentication
description: This article describes the authentication methods used in Tealium V1 APIs.
url: https://docs.tealium.com/api-v1/getting-started/auth/
---

<blockquote>
This is an older version of [the current Tealium API](https://docs.tealium.com/api-authentication/).
</blockquote>


The API can only be used by users with a valid Tealium account. The API supports authentication using an email address and password to verify user identity. Prior to accessing any of the API endpoints, you must authenticate to start a session. All subsequent calls use a session cookie and [CSRF token](https://en.wikipedia.org/wiki/Cross-site_request_forgery) for security purposes.

## Login

Upon a successful login you are granted two items:

* A cookie named `JSESSIONID`.
* A token named `utk`.

These values are then used to authenticate all subsequent API calls.

### Resource URL

`POST /v1/login`

cURL request:

```bash
curl -i -d username='{email}' -d password='{password}' https://api.tealiumiq.com/v1/login

```

Example request:

```bash
curl -i -d username='user@example.com' -d password='password123' https://api.tealiumiq.com/v1/login

```

Example response:

```bash
HTTP/1.1 200 OK

Cache-Control: no-cache,no-store,must-revalidate
Content-Type: application/json
Date: Mon, 31 Oct 2016 20:39:29 GMT
Expires: 0
Pragma: no-cache
Set-Cookie: JSESSIONID=3513642946826543477; Path=/urest_service; Secure; HttpOnly
Set-Cookie: rememberMe=deleteMe; Path=/urest_service; Max-Age=0; Expires=Sun, 30-Oct-2016 20:39:29 GMT
X-NodeId: i-6c3ba529
X-Version: 0.0.528
X-XSS-Protection: 1;mode=block
Content-Length: 60
Connection: keep-alive

{
   "utk": "65489FMSTJGF549870KSH",
}

```

From this response, you would make note of the following values for all subsequent API calls:

(Sample Values)

* JSESSION = `3513642946826543477`
* utk = `65489FMSTJGF549870KSH`

### Error messages

If the call fails, the API returns a `401 Authentication Failure` error. Here are the error messages you can expect to see:

`{ <br>   "returnCode" : 1401,<br>  "message" : "Authentication Failed"<br>}`

`{ <br>   "returnCode" : 1402,<br>  "message" : "Too many unsuccessful login attempts. Please try again in 10 minutes" <br>}`

`{ <br>   "returnCode" : 1469,<br>  "message" : "Although the user is authenticated, the request is denied due of lack of proper permissions" <br>}`

## Logout

Terminates the current session for the logged-in user.


<blockquote>
This API call is optional because a user is automatically logged out after their session expires.
</blockquote>


### Resource URL

POST <https://api.tealiumiq.com/v1/logout>

### Request header

| Header Field Name | Description | Example value |
| --- | --- | --- |
| [Content-type](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields) | Indicates the MIME type of the body of the GET request  | `application/x-www-form-urlencoded` |
| JSESSION cookie | Cookie for sending jsession ID. For example, the unique session identifier. | `JSESSIONID=415072043799098022` |

### Example response

The API returns `status 200 OK` upon successful logout.