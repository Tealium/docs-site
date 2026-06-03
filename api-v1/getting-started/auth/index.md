---
title: Authentication
description: This article describes the authentication methods used in Tealium V1 APIs.
url: https://docs.tealium.com/api-v1/getting-started/auth/
---
 This is an older version of [the current Tealium API](). 

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
curl -i -d username=&#39;{email}&#39; -d password=&#39;{password}&#39; https://api.tealiumiq.com/v1/login

```

Example request:

```bash
curl -i -d username=&#39;user@example.com&#39; -d password=&#39;password123&#39; https://api.tealiumiq.com/v1/login

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
   &#34;utk&#34;: &#34;65489FMSTJGF549870KSH&#34;,
}

```

From this response, you would make note of the following values for all subsequent API calls:

(Sample Values)

* JSESSION = `3513642946826543477`
* utk = `65489FMSTJGF549870KSH`

### Error messages

If the call fails, the API returns a `401 Authentication Failure` error. Here are the error messages you can expect to see:

`{ &lt;br&gt;   &#34;returnCode&#34; : 1401,&lt;br&gt;  &#34;message&#34; : &#34;Authentication Failed&#34;&lt;br&gt;}`

`{ &lt;br&gt;   &#34;returnCode&#34; : 1402,&lt;br&gt;  &#34;message&#34; : &#34;Too many unsuccessful login attempts. Please try again in 10 minutes&#34; &lt;br&gt;}`

`{ &lt;br&gt;   &#34;returnCode&#34; : 1469,&lt;br&gt;  &#34;message&#34; : &#34;Although the user is authenticated, the request is denied due of lack of proper permissions&#34; &lt;br&gt;}`

## Logout

Terminates the current session for the logged-in user.

 This API call is optional because a user is automatically logged out after their session expires.

### Resource URL

POST &lt;https://api.tealiumiq.com/v1/logout&gt;

### Request header

| Header Field Name | Description | Example value |
| --- | --- | --- |
| [Content-type](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields) | Indicates the MIME type of the body of the GET request  | `application/x-www-form-urlencoded` |
| JSESSION cookie | Cookie for sending jsession ID. For example, the unique session identifier. | `JSESSIONID=415072043799098022` |

### Example response

The API returns `status 200 OK` upon successful logout.