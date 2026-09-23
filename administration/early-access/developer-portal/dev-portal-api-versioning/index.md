---
title: Developer Portal API versioning
description: This article describes how Tealium APIs are versioned, what constitutes a breaking change, and how to migrate between versions.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-api-versioning/
---
## How it works

Tealium APIs use a calendar-based versioning strategy. A new version is released only when a breaking change is introduced. Non-breaking changes such as new endpoints or optional fields are delivered to the current version without releasing a new version. This versioning strategy gives you a predictable, stable integration target with migration timelines.

### Versioning format

Tealium identifies each version by a date in the `YYYY-MM` format, prefixes it with `v`, and includes it in the URL path:

```none
https://api.tealiumapis.com/v{YYYY-MM}/{api-family}/{resource}
│                         │         │            └─ Resource path
│                         │         └───────────── API family (cdp, iq, etc.)
│                         └─────────────────────── Calendar version
└───────────────────────────────────────────────── Global hostname
```

For example:

```none
https://api.tealiumapis.com/v2026-06/cdp/audiences
https://api.tealiumapis.com/v2026-06/cdp/labels
https://api.tealiumapis.com/v2026-10/cdp/audiences
```

### Regional hostnames

There are no regional hostnames to manage. Tealium routes traffic to the nearest region.

## Breaking and non-breaking changes

A new version is created only when a breaking change is introduced. The following are considered breaking changes:

* Removing or renaming an existing field in a response
* Changing the type of an existing field
* Renaming or removing a query parameter or path parameter
* Changing the default behavior of an existing endpoint
* Removing an endpoint entirely
* Changes to required OAuth 2.0 security scopes

The following changes are not breaking and are delivered to the current version:

* Adding a new endpoint
* Adding a new optional field to a request or response
* Adding a new optional query parameter
* Adding new enum values (when clients are expected to handle unknown values gracefully)

For example:

```none
Q1 2026 release
├── New /enrichment endpoint        → no new version needed
├── Optional metadata field added   → no new version needed
└── Current version remains: v2026-01

Q3 2026 release
├── audiences filter parameter renamed  → BREAKING
├── New /segments endpoint          → additive (included)
└── New version cut: v2026-06
    URL changes from /v2026-01/cdp/... to /v2026-06/cdp/...
```

For information about support windows, deprecation signals, and end-of-life timelines, see [API lifecycle](https://docs.tealium.com/dev-portal-api-lifecycle/).

## Incremental migration

Multiple versions run simultaneously during the support window. You can migrate endpoint by endpoint and update the version in the URL path for each API call independently. You do not need to migrate all endpoints at once.

The Developer Portal provides a per-endpoint changelog for each version showing exactly which endpoints have breaking changes and what specifically changed. If an endpoint has no breaking changes, your existing code works unchanged on both the old and new version paths.

For example, when upgrading from 2026-01 to 2026-06:

```none
/cdp/audiences    : 2 changes (filter parameter renamed, new required field)
/cdp/labels       : 1 change (response pagination format)
/cdp/events       : no changes
/cdp/connectors   : no changes
```

With this migration strategy, you can switch `/cdp/events` and `/cdp/connectors` to the new version path immediately with no code changes, then plan the `/cdp/audiences` and `/cdp/labels` migration separately.

```bash
# Migrate /audiences to the new version (has breaking changes)
curl -X GET \
https://api.tealiumapis.com/v2026-06/cdp/audiences \
-H 'Authorization: Bearer {token}'

# Keep /events on the old version (no changes between versions)
curl -X GET \
https://api.tealiumapis.com/v2026-01/cdp/events \
-H 'Authorization: Bearer {token}'
```

## Best practices

1. **Pin your version explicitly**: Always use a specific version in your URL path. Never rely on redirects or a `latest` alias in production. 
1. **Monitor deprecation headers**: Set up monitoring to alert when responses start including `Sunset` headers.
1. **Migrate incrementally**: Update the version in the URL path one endpoint at a time. Both old and new version paths are active simultaneously.
1. **Review the changelog before upgrading**: Focus only on endpoints with actual breaking changes.
1. **Skip intermediate versions when ready**: You do not need to step through every version. Migrate directly from your current version to the latest.