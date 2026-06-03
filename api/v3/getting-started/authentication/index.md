---
title: Tealium V3 API Authentication
description: This article provides authentication information for Tealium v3 APIs.
url: https://docs.tealium.com/api/v3/getting-started/authentication/
---
## Authentication

Authentication (login) requires an API key from Tealium iQ Tag Management. To learn more about Tealium API keys, see [Managing and Generating API Keys]().

The authentication call has two parameters: username and the API key. The API key is used in place of a password to log into the API. After a successful login to the API, the authentication call returns a JWT, referred to as a bearer token. The bearer token, which is valid for 30 minutes, is the value that must be used to authenticate subsequent API calls.

Do not generate a new bearer token for every call. Use the token until it expires. Each token expires within 30 minutes. Failure to use the token in this manner will result in authentication call throttling at Tealium&#39;s discretion.

### Region-specific host

The authentication response contains a token and host value.

```json
{
  &#34;token&#34;:&#34;eyJ0[...]kqkpj8vE&#34;
  &#34;host&#34;: &#34;us-east-1-platform.tealiumapis.com&#34;
}
```

The host value must be used in subsequent API calls that are region-specific. For example, the visitor API endpoint would be:

```none
https://us-east-1-platform.tealiumapis.com/v3/visitor/accounts/{account}/profiles/{profile}
```

### cURL request

The following cURL request shows the variables required for the API key exchange for a JWT token. The URL, username, and API key are encoded.

```bash
curl -X POST \
https://platform.tealiumapis.com/v3/auth/accounts/{account}/profiles/{profile} \
-H &#39;Content-Type: application/x-www-form-urlencoded&#39; \
--data-urlencode &#39;username={email}&#39; \
--data-urlencode &#39;key={api_key}&#39;
```

#### Example request

```bash
curl -X POST \
https://platform.tealiumapis.com/v3/auth/accounts/{account}/profiles/{profile} \
-H &#39;Content-Type: application/x-www-form-urlencoded&#39; \
--data-urlencode &#39;username=tealium.user@yourdomain.com&#39; \
--data-urlencode &#39;key=7O4Pjn8tuc0%5B3Nc2)%7DyXJW8EaCuDRA1U8Jn%23p)qc*O94(*ubIeEUz%25%5D%242~)WKlLB&#39;
```

#### Example Response

```bash
* Trying 10.220.2.176...
* Connected to platform.tealiumapis.com (10.220.2.176) port 443 (#0)
* TLS 1.2 connection using TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
* Server certificate: *.tealiumiq.com
* Server certificate: DigiCert SHA2 Secure Server CA
* Server certificate: DigiCert Global Root CA
&gt; POST /v3/auth/accounts/{account}/profiles/{profile} HTTP/1.1
&gt; Host: platform.tealiumapis.com
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
* Connection #0 to host platform.tealiumapis.com left intact
{
  &#34;token&#34;:&#34;eyJ0[...]kqkpj8vE&#34;
  &#34;host&#34;: &#34;us-east-1-platform.tealiumapis.com&#34;
}

```
