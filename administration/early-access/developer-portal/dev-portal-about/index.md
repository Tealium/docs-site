---
title: About the Tealium Developer Portal
description: Learn how applications, subscriptions, scopes, and OAuth2 authentication work in the Tealium Developer Portal.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-about/
---
The [Tealium Developer Portal](https://app.tealiumapis.com/) is a self-service platform for managing programmatic access to Tealium APIs for Tealium account holders, third-party developers, and agencies building integrations for Tealium customers. From the Developer Portal you can create OAuth2 applications, subscribe to APIs with fine-grained scope control, manage credentials, and monitor API usage.

## How it works

The portal organizes access around four interconnected concepts:

* [**Applications**](#applications) hold credentials.
* [**Subscriptions**](#subscriptions) connect applications to APIs.
* [**Scopes**](#scopes) define what an application is authorized to access.
* [**Authentication**](#authentication) describes how tokens are obtained and validated on every request.

### Applications

An application is an OAuth2 client, a named credential holder that represents a system or service making API calls. Each application has two pieces of identity:

* **Client ID:** A public identifier included in every token request.
* **Client secret:** A private credential used with the client ID to prove the application's identity.

Create one application per integration. A single integration may require subscriptions to multiple APIs, and one application can hold all of those subscriptions. For example, create one application for an analytics dashboard and a separate one for a data pipeline.

Manage your applications from the **Applications** tab in the Developer Portal. For more information, see [Applications](https://docs.tealium.com/dev-portal-applications/).

### Subscriptions

A subscription connects an application to a specific API. When you create a subscription, you specify:

* Which API the application can call.
* The access levels (scopes) the application is granted for that API.
* The Tealium accounts and profiles the application can access.

Without a subscription to an API, an application cannot request tokens for that API. An application can subscribe to multiple APIs, each with a separate scope and account configuration.

Manage your subscriptions from the **Subscriptions** tab in the Developer Portal. For more information, see [Subscriptions](https://docs.tealium.com/dev-portal-subscriptions/).

### Scopes

Scopes define the exact access an application is granted. Tealium uses compound scopes that encode the full access context in a single string:

```none
{account}:{profile}:{apiFamily}:{apiVersion}:{resource}:{action}
```

For example, `my-account:main:cdp-api:2026-07:audiences:read` grants read access to audiences in the `main` profile of `my-account`, on version 2026-07 of the CDP API.

When you subscribe to an API, you select the maximum set of scopes the application is allowed to request. When requesting a token, you can request any subset of those subscribed scopes. Requesting a subset of scopes generates a token scoped to a specific task, even if the application's subscription grants broader access.

For full scope reference including engine-level scopes, see [Scopes](https://docs.tealium.com/dev-portal-scopes/).

### Authentication

All Tealium API requests require a bearer token. Tokens are short-lived JWTs obtained using the OAuth2 Client Credentials grant. Your application presents its client ID and secret to the token endpoint, which returns a signed token the API gateway validates on every request.

```none
Application                 Token Endpoint           API Gateway
    |                            |                        |
    |-- POST /oauth/token ------>|                        |
    |   client_id                |                        |
    |   client_secret            |                        |
    |   scope                    |                        |
    |<-- access_token (JWT) -----|                        |
    |                            |                        |
    |-- GET /api/endpoint ------------------------------->|
    |   Authorization: Bearer {token}                     |
    |<-- 200 OK ------------------------------------------|
```

Tokens expire after two hours. There is no refresh token. Your application requests a new token when the current one expires. Cache tokens and reuse them within their lifetime to avoid throttling.

The gateway validates the token's scope claim on every request. If the token lacks the required account, profile, API, version, resource, and action combination, the gateway returns `403 Forbidden`.

For full details on token requests, scope enforcement, and security best practices, see [Authentication](https://docs.tealium.com/dev-portal-authentication/).

### Developer portal workflow

A complete integration follows this sequence:

1. **Create an application:** Establishes the OAuth2 client identity (client ID and secret).
1. **Subscribe to an API:** Selects which APIs, scopes, and Tealium accounts the application can access.
1. **Request a token:** The application presents its credentials and receives a JWT scoped to the subscribed access.
1. **Call the API:** The application includes the token in every request. The gateway validates the scope claim and executes the call.

## Third-party access

If you are a third-party developer or agency building an integration for a Tealium customer, the Developer Portal supports a delegated authorization model:

1. Create an application and subscribe to the APIs you need.
1. Share your application ID with the resource owner.
1. The resource owner looks up your application in the Developer Portal and grants it access to their specific accounts, profiles, and engines.
1. Your tokens then include scopes for those resources.

The resource owner controls exactly which accounts, profiles, and engines they grant and can modify or revoke that access at any time.

For details, see [Third-party app access](https://docs.tealium.com/dev-portal-third-party-app-access/).

## Get started

To start making API calls:

1. Read the [getting started tutorial](https://docs.tealium.com/dev-portal-getting-started/) for a step-by-step walkthrough.
1. Use [Applications](https://docs.tealium.com/dev-portal-applications/) to create your first application and subscribe to APIs.
1. Use [Authentication and credentials](https://docs.tealium.com/dev-portal-authentication/) to request tokens and make API calls.
