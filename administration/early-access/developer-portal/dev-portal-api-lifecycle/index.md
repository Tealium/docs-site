---
title: Developer Portal API lifecycle
description: This article describes the support phases for Tealium API versions, deprecation signals, and what to expect at each lifecycle stage.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-api-lifecycle/
---
Each Tealium API version moves through three lifecycle phases. The phase determines the level of support you receive and the action, if any, that you need to take.

## Preview APIs

Some APIs are released in preview before they receive a stable version. Preview APIs are not covered by the calendar-version support policy. Their endpoints, payloads, and scopes may change without notice.

To subscribe to a preview API, your organization must have a signed early access agreement with Tealium. At the review step in the subscription wizard, you must confirm this agreement and acknowledge which account profiles you are granting access to before the subscription is created.

## Lifecycle phases

| Phase | Window (after version release) | Support level | Action required |
| --- | --- | --- | --- |
| Active | 0–24 months | Bug fixes, security patches, and non-breaking enhancements applied. | No action required. |
| End of Support | 24–36 months | The API remains functional but receives no new features or non-critical fixes. Responses include `Sunset` and `Deprecation` headers. When a version enters End of Support, a successor version is identified automatically. | Plan your migration. |
| End of Life (EOL) | 36+ months | No longer available. Requests return HTTP 410 unless you have an approved contract extension. | Migrate before this date or renew contract for a formal extension. |

You are not required to upgrade every quarter. You can safely skip intermediate versions and upgrade directly to the latest when you are ready. Each version is independently supported for the full 36-month lifecycle. For more information, see [API versioning](https://docs.tealium.com/dev-portal-api-versioning/).

The Developer Portal API Catalog shows the version and support end date for each API on its catalog card.

## Deprecation signals

When a version enters End of Support, each API response includes the following headers:

* **`Sunset`**: The date when the version reaches End of Life.
* **`Deprecation`**: Set to `true` on all responses from deprecated versions.
* **`Link`**: Points to the successor version URL.

The following example shows all three headers on a response from a version entering End of Support, with a sunset date of June 2029 and a successor version at `v2026-10`:

```none
HTTP/1.1 200 OK
Sunset: Mon, 01 Jun 2029 00:00:00 GMT
Deprecation: true
Link: </2026-10/cdp/audiences>; rel="successor-version"
```