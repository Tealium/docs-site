---
title: Developer Portal authentication
description: This article describes how to authenticate API requests to Tealium APIs using OAuth2 client credentials and bearer tokens.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-authentication/
---
All Tealium API access requires a bearer token. The Developer Portal uses the OAuth2 Client Credentials grant, which is designed for server-to-server communication where no end-user interaction is required.

The authentication flow works as follows:

1. Your application sends its client ID and client secret to the token endpoint.
1. The token endpoint validates the credentials and returns a JWT access token.
1. Your application includes the token in the `Authorization` header of every API request.
1. The API gateway validates the token and checks that the requested operation matches the token's scopes.

Client credentials are for backend services only. Never use them in browser or mobile clients.

## Before you begin

You need a client ID and client secret from an application registered in the Developer Portal. For instructions on creating an application, see [Applications](https://docs.tealium.com/dev-portal-applications/).

The Developer Portal displays the client secret only once when you create the application. If you did not save it, rotate the secret in the Developer Portal to generate a new one before authenticating.

## Request an access token


<blockquote>
You can generate a bearer token without writing any code by clicking **Generate Token** on the application detail page or from the API reference screen. For more information, see [Generate a bearer token from the API reference](https://docs.tealium.com/dev-portal-api-reference/#generate-a-bearer-token-from-the-api-reference).
</blockquote>


Tealium APIs use OAuth 2.0 Client Credentials with compound scopes. The scope format is:

```none
{account}:{profile}:{apiFamily}:{apiVersion}:{resource}:{action}
```

| Segment | Description |
| --- | --- |
| `account` | Your Tealium account name, for example, `tealium-corp`. |
| `profile` | A specific profile, for example, `main`, or `*` for all profiles in the account. |
| `apiFamily` | The API the scope authorizes, for example, `cdp-api`. Taken from the API you subscribed to. |
| `apiVersion` | The version of that API, for example, `2026-07`, or `*` for all versions. Note there is no `v` prefix here, unlike the URL path. |
| `resource` | The API resource, for example, `labels` or `audiences`. |
| `action` | `read` for GET requests, `write` for POST, PUT, and DELETE requests, `manage` for administrative operations. |

Request the scope exactly as it was granted. If your application was granted access to all profiles in an account (using `*`), you must request the wildcard form. A wildcard token authorizes requests against any profile in that account. The portal shows the exact scope strings for your subscription in the **Get Bearer Token** drawer, so you do not need to compose them by hand.

If your subscription grants access to all profiles in an account, request using the `*` wildcard:

```bash
curl -X POST \
https://api.tealiumapis.com/oauth/token \
-u '{client_id}:{client_secret}' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials' \
-d 'scope=tealium-corp:*:cdp-api:2026-07:labels:read'
```

If your subscription grants access to a specific profile, request that profile:

```bash
curl -X POST \
https://api.tealiumapis.com/oauth/token \
-u '{client_id}:{client_secret}' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials' \
-d 'scope=tealium-corp:main:cdp-api:2026-07:labels:read'
```

To request multiple scopes, separate them with a space:

```bash
-d 'scope=tealium-corp:*:cdp-api:2026-07:labels:read tealium-corp:*:cdp-api:2026-07:audiences:write'
```


<blockquote>
Your token contains only the scopes you explicitly request. Even if your application has multiple scopes granted, specify only what you need for each operation. Cache the token and reuse it until it expires. Requesting a new token on every API call triggers throttling.
</blockquote>


A successful response returns a JSON object with the following parameters:

| Field | Description |
| --- | --- |
| `access_token` | The JWT to include in API requests. |
| `token_type` | Always `Bearer`. |
| `expires_in` | Token lifetime in seconds. |
| `scope` | The scopes granted to this token. |

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 7200,
  "scope": "my-account:main:cdp-api:2026-07:labels:read my-account:main:cdp-api:2026-07:audiences:write"
}
```

For engine-enforced APIs, such as the Context API, the `scope` field contains engine-level scopes instead of resource-level scopes:

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 7200,
  "scope": "my-account:main:context-api:2026-06:e01ce645-3964-4343-9a0c-7d165e653b35"
}
```

For details on scope format, see [Scopes](https://docs.tealium.com/dev-portal-scopes/).

## Make an authenticated request

Include the access token in the `Authorization` header of each API request:

```bash
curl -X GET \
https://api.tealiumapis.com/v{YYYY-MM}/{api}/accounts/tealium-corp/profiles/main/labels \
-H 'Authorization: Bearer {access_token}'
```

Use an asterisk (`*`) as a wildcard to request access to any profile in the URL path. Both of the following requests work with a `tealium-corp:*:cdp-api:2026-07:labels:read` token:

```bash
curl -X GET \
https://api.tealiumapis.com/v{YYYY-MM}/{api}/accounts/tealium-corp/profiles/main/labels \
-H 'Authorization: Bearer {access_token}'

curl -X GET \
https://api.tealiumapis.com/v{YYYY-MM}/{api}/accounts/tealium-corp/profiles/staging/labels \
-H 'Authorization: Bearer {access_token}'
```

## Token expiration and renewal

| Aspect | Details |
| --- | --- |
| Format | JWT signed with RS256. |
| Expiration | Set by the `expires_in` value in the token response (7200 seconds, or 2 hours). |
| Renewal | Request a new token before expiration. There is no refresh token in the client credentials flow. |
| Scope claim | The JWT contains a `scope` claim listing the compound scopes granted to the token. |

## Scope enforcement

The API gateway validates scopes on every request:

1. The gateway extracts the `scope` claim from the JWT.
1. It matches the request context (account, profile, resource, and action) against the token's scopes.
1. If a matching scope is found, the request proceeds.
1. If no matching scope is found, the gateway returns `403 Forbidden`.


<blockquote>
When requesting a token, you can request a subset of your subscribed scopes. Use this scope subsetting to generate a token with only the permissions a specific task requires.
</blockquote>


### Context API engine enforcement

For APIs with engine-level authorization, such as the Context API, the gateway performs an additional check after validating account and profile scopes:

1. The gateway extracts the engine ID from the request URL path (for example, `/engines/{engineId}/...`).
1. It checks whether the token's `scope` claim contains a matching engine scope: `{account}:{profile}:{apiFamily}:{apiVersion}:{engineId}`.
1. The check passes if the token contains the exact engine scope, the engine wildcard `{account}:{profile}:{apiFamily}:{apiVersion}:*`, or the profile wildcard `{account}:*:*`.
1. If no matching scope is found, the gateway returns `403 Forbidden` with a body identifying the missing scope:

```json
{"error":"insufficient_scope","message":"Token does not contain required scope: {account}:{profile}:{apiFamily}:{apiVersion}:{engineId}"}
```

Non-engine resource APIs return the same error envelope, with the compound resource scope in the message.

Account and profile access alone is not sufficient for engine-enforced APIs. The resource owner must also grant engine-level access before your application can call engine-enforced endpoints.

| Scope format | API type | Example |
|---|---|---|
| `{account}:{profile}:{apiFamily}:{apiVersion}:{resource}:{action}` | Resource-scoped APIs | `acme:main:cdp-api:2026-07:labels:read` |
| `{account}:{profile}:{apiFamily}:{apiVersion}:{engineId}` | Engine-enforced APIs | `acme:main:context-api:2026-06:e01ce645-3964-...` |
| `{account}:{profile}:{apiFamily}:{apiVersion}:*` | Engine-enforced APIs (wildcard) | `acme:main:context-api:2026-06:*` |

## Security best practices

* **Never expose client secrets.** Store them in environment variables or a secrets manager. Never commit them to source control.
* **Request minimal scopes.** Only request the scopes your application needs for each operation.
* **Cache tokens until expiry.** Request a new token only when the current one is about to expire, not on every API call.
* **Rotate secrets immediately if compromised.** If you believe your credentials have been exposed, rotate them immediately via the Developer Portal application settings. Rotate regularly as a general practice.
* **Use server-side requests only.** Client credentials are for backend services only. Never use them in browser or mobile clients.
* **Select specific engines.** For engine-enforced APIs, prefer selecting specific engines rather than All engines to follow least-privilege principles.

## Error responses

| HTTP status | Meaning | Resolution |
| --- | --- | --- |
| 401 Unauthorized | Invalid or expired token | Request a new access token. |
| 403 Forbidden | Token is valid but lacks the required scope. | Check your subscription scopes and account/profile assignments. |
| 403 Forbidden | Token lacks engine-level authorization. | Ensure the resource owner has granted access to the specific engine. |
| 400 Bad Request | Invalid token request: wrong `grant_type` or missing fields. | Verify your token request parameters. |
