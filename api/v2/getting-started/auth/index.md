---
title: Authentication
description: This article describes the authentication methods used in Tealium V2 APIs.
url: https://docs.tealium.com/api/v2/getting-started/auth/
---
This article provides information needed to begin using the Tealium v2 API. The [previous v1 API]() is still available, but will eventually be deprecated.

## Authentication

Authentication (login) requires an API key from Tealium iQ Tag Management. Learn more about [Managing and Generating API Keys]().

The authentication call has two parameters: username and the API key. The API key is used in place of a password to log in to the API. After a successful login to the API, the authentication call returns a JWT, referred to as a bearer token. The bearer token, which is valid for 30 minutes, is the value that must be used to authenticate subsequent API calls.

Do not generate a new bearer token for every call. Use the token until it expires. Failure to use the token in this manner will result in auth call throttling at Tealium&#39;s discretion.

## cURL request

The following cURL request shows the variables required for the API key exchange for a JWT token. The URL, username, and API key are encoded.

```bash
curl -X POST \
https://api.tealiumiq.com/v2/auth \
-H &#39;Content-Type: application/x-www-form-urlencoded&#39; \
--data-urlencode &#39;username={email}&#39; \
--data-urlencode &#39;key={api_key}&#39;
```

## Example request

```bash
curl -X POST \
https://api.tealiumiq.com/v2/auth \
-H &#39;Content-Type: application/x-www-form-urlencoded&#39; \
--data-urlencode &#39;username=tealium.user@yourdomain.com&#39; \
--data-urlencode &#39;key=7O4Pjn8tuc0%5B3Nc2)%7DyXJW8EaCuDRA1U8Jn%23p)qc*O94(*ubIeEUz%25%5D%242~)WKlLB&#39;
```

## Example response

```bash
* Trying 192.0.2.0...
* Connected to api.tealiumiq.com (192.0.2.0) port 443 (#0)
* TLS 1.2 connection using TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
* Server certificate: *.tealiumiq.com
* Server certificate: DigiCert SHA2 Secure Server CA
* Server certificate: DigiCert Global Root CA
&gt; POST /v2/auth HTTP/1.1
&gt; Host: qa20-api.tealiumiq.com
&gt; User-Agent: curl/7.43.0
&gt; Accept: */*
&gt; cache-control: no-cache
&gt; content-type: application/x-www-form-urlencoded
&gt; Content-Length: 127
&gt;
* upload completely sent off: 127 out of 127 bytes
&lt; HTTP/1.1 200 OK
&lt; Date: Wed, 14 Feb 2018 19:04:22 GMT
&lt; Content-Type: application/json
&lt; Content-Length: 893
&lt; Connection: keep-alive
&lt; Cache-Control: no-cache,no-store,must-revalidate
&lt; Pragma: no-cache
&lt; Expires: 0
&lt; X-XSS-Protection: 1;mode=block
&lt; X-NodeId: i-0afb3e9b53ba15930
&lt; X-Version: 1.0.130-SNAPSHOT
&lt; Set-Cookie: rememberMe=deleteMe; Path=/urest_service; Max-Age=0; Expires=Tue, 13-Feb-2018 19:10:41 GMT
&lt;
* Connection #0 to host api.tealiumiq.com left intact
{&#34;token&#34;:&#34;eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUxMiJ9.eyJzdWIiOiJtYXJjLmhpcG9saXRvQHRlYWxpdW0uY29tIiwibmJmIjoxNTE4NjM1NDQxLCJpc3MiOiJodHRwczovL2FwaS50ZWFsaXVtaXEuY29tIiwiZXhwIjoxNTE4NjM3MjQxLCJpYXQiOjE1MTg2MzU0NDF9.EPM_hfocfiF4SJnW0gBrGb9BuYIxsyoRdIWeuMTDLEBroVixmkFnPRC3G9zfn1hEpGfOGL6OKSHPIm5GwJQCNyIX7cE8umheIyTk8xxOuCAKjTOCip_6-AaFBcj6nLxgyez4OgxLral1XmZxyb9mP-vrKeDDQUf4ygdhgeDYoqnfQtIZ8TA68Pcx3H7BLgd0MJjTh7S74-9bWX95PkDDizTg0ia1dIbHsMXsB1ZA6gS-WPrCuy0CNA0IvJo0XuFNoOF2mazREYvG-Yp0-EzlMTa3W_EoI_93F9RbG-soUrLdV5IKav4TjwWfvyOZTx4Tb_Je9NgJ_EfeWW_E84pSAtCo7QX2yXZ3MYROkNnRdsQG4XhaFUbXwJnUghl65MHyjQxINDtbB5vujk04ctnuQvSO-sZslQxXGJm1sBiY3eFa5U4-L0V4MCJ3s9h_RbRyPt07CD4YX85kRJ5mj8x6nFHDE2iwrpSnNlQ_3KctqlJHSNdYhWzSnLpfz5qKq_Uv6XA88lUoRMiCC-Hy2uZe_vrqA0p_-BbrXPvw8olhd0SGD36D982bxKkcJR84ACUPU36FSBRWs_HRWEyjTwWR33oRv3vEIpzlUvp7TEGiD7A5ucNvLUT1yV_8YdsNLEevFg7WWjXkKnYDprq1QikO6KV1drWfrJnLldJ4ziTtK20&#34;}

```