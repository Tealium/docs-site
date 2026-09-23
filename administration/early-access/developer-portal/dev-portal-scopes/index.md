---
title: Developer Portal scopes
description: Understand how Tealium compound scopes control resource and action access in API tokens.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-scopes/
---
Scopes provide fine-grained access control over what resources and actions your application can perform. Each subscription grants access to specific API endpoints based on the scopes you configure.

When subscribing to an API, you select which scopes your application needs. Apply the principle of least privilege: request only the scopes your application actually requires. For more information, see [Subscriptions](https://docs.tealium.com/dev-portal-subscriptions/).

## Compound scopes

Tealium uses compound scopes that encode the full access context in a single string:

```none
{account}:{profile}:{apiFamily}:{apiVersion}:{resource}:{action}
```

| Component | Description | Example |
|---|---|---|
| Account | The Tealium account the scope applies to | `my-company` |
| Profile | The profile within the account. Use `*` for all profiles. | `main`, `*`, `prod-web` |
| API family | Which API the scope authorizes. Taken from the API itself; you do not choose it. | `cdp-api`, `context-api` |
| API version | Which version of that API. Use `*` to cover every version. | `2026-07`, `*` |
| Resource | The type of resource being accessed | `labels`, `audiences`, `events` |
| Action | The operation permitted on the resource | `read`, `write`, `delete`, `manage` |

For example:

* `my-account:main:cdp-api:2026-07:labels:read`: Reads labels from the `main` profile in `my-account`, on version 2026-07 of the CDP API.
* `my-account:*:cdp-api:2026-07:audiences:write`: Writes audiences across all profiles in `my-account`.
* `my-account:main:cdp-api:2026-07:*:*`: Every scope the API offers, including scopes added later.
* `my-account:main:cdp-api:*:labels:read`: Reads labels on every version of the CDP API.

The asterisk (`*`) wildcard can be used in any position and matches every value of that segment. To request every scope an API offers, both the resource and the action position must be `*`: `{account}:{profile}:{apiFamily}:{apiVersion}:*:*`. A single trailing asterisk is a different format: it is the engine wildcard described below.

## Engine-level scopes

Some APIs, such as the Context API, require engine-level authorization in addition to account and profile access. For these APIs, tokens carry engine-level compound scopes:

```none
{account}:{profile}:{apiFamily}:{apiVersion}:{engineId}
```

| Component | Description | Example |
|---|---|---|
| Account | The Tealium account the scope applies to | `my-company` |
| Profile | The profile within the account | `main`, `prod-web` |
| API family | Which API the scope authorizes | `context-api` |
| API version | Which version of that API | `2026-06`, `*` |
| Engine ID | The specific Moments engine | `e01ce645-3964-...`. Use `*` for all engines in the profile. |

For example:

* `my-account:main:context-api:2026-06:e01ce645-3964-4343-9a0c-7d165e653b35`: Access to a specific engine in the `main` profile of `my-account`.
* `my-account:main:context-api:2026-06:*`: Access to all engines in the `main` profile of `my-account`.

When a subscription to an engine-enforced API also grants resource scopes, the two are combined into a single scope:

```none
{account}:{profile}:{apiFamily}:{apiVersion}:{engineId}:{resource}:{action}
```

For example, `my-account:main:context-api:2026-06:e01ce645-3964-4343-9a0c-7d165e653b35:actions:read` reads actions from that one engine.

Engine scopes are added to your tokens automatically when a resource owner grants engine access during subscription or via [third-party app access](https://docs.tealium.com/dev-portal-third-party-app-access/). You do not need to manually request engine scopes: they are derived from the engine selections made during the grant process.
