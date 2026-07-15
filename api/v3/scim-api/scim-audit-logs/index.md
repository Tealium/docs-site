---
title: SCIM audit logs
description: Learn how SCIM audit logging records user provisioning events and how to export logs for compliance auditing and troubleshooting.
url: https://docs.tealium.com/api/v3/scim-api/scim-audit-logs/
---
## How it works

SCIM audit logging records every SCIM user provisioning event, such as creates, updates, patches, deletes, and retrievals. Each log entry captures the action type, outcome, target user details, the source that triggered the event, and a correlation ID for tracing.

Use audit logs to verify that the right users have been provisioned, troubleshoot failed provisioning operations, and produce records for compliance audits.

Logs are retained for 12 months. Request and response payloads are not stored.

## What is logged

The following SCIM operations on `/scim/v2/Users` are logged:

| Action | HTTP method |
| --- | --- |
| User Creation | `POST` |
| User Update | `PUT` |
| User Patch | `PATCH` |
| User Retrieval | `GET` |
| User Deletion | `DELETE` |

Each event is recorded regardless of outcome. Failed operations are logged with an `ERROR` outcome and a short error message.

## Export audit logs from the UI

Account Admins and User Admins can export audit logs without calling the API directly.

On the **Manage Permissions** (Platform Permissions) page, select **Export Audit Logs** to download a CSV of all audit logs from the past 12 months for the current account.

The **Export Audit Logs** button is only available in the new permissions experience. It does not appear in the legacy permissions experience.

If no logs exist for the account, a message is displayed. If the export fails, an error message is displayed with a prompt to try again.

## Log fields reference

Each log entry contains the following fields:

| Field | Description |
| --- | --- |
| `timestamp` | Date and time of the event. |
| `action_type` | The SCIM operation performed: `User Creation`, `User Update`, `User Patch`, `User Retrieval`, or `User Deletion`. |
| `resource_type` | The type of SCIM resource affected. Returns `USER` or `GROUP`. |
| `target_email` | Email address of the user who received the change. |
| `target_first_name` | First name of the target user. |
| `target_last_name` | Last name of the target user. |
| `target_user_uuid` | Tealium-assigned UUID for the target user. |
| `external_id` | The identity provider&#39;s identifier for the user. |
| `idp_source` | Name of the identity provider. |
| `http_status` | HTTP response code for the SCIM operation. |
| `outcome` | Result of the operation: `SUCCESS` or `ERROR`. |
| `correlation_id` | Unique identifier for the request. Use this value to trace a specific operation across logs. |
| `account_name` | The Tealium account name. |
| `error_message` | Short description of the error if the outcome is `ERROR`. Empty on success. |

## Filter logs for common tasks

The [GET SCIM Sync Logs API]() supports several query parameters for filtering results. The following examples show how to use filters for common tasks.

**Export logs for a compliance audit (date range)**

To produce a record of all provisioning activity for a specific period, set `from` and `to` to the date range required by the audit:

```bash
curl --location &#39;https://developer.tealiumapis.com/admin/scim-sync/logs?account={ACCOUNT}&amp;from=2025-01-01T00:00:00Z&amp;to=2025-03-31T23:59:59Z&#39; \
--header &#39;Authorization: Bearer {TOKEN}&#39;
```

**Find failed provisioning events**

To identify provisioning failures, filter by `status=ERROR`:

```bash
curl --location &#39;https://developer.tealiumapis.com/admin/scim-sync/logs?account={ACCOUNT}&amp;status=ERROR&#39; \
--header &#39;Authorization: Bearer {TOKEN}&#39;
```

The `error_message` field in each result describes why the operation failed.

**Trace a specific request**

If you have a correlation ID from a support ticket or application log, use `correlationId` to retrieve the exact event:

```bash
curl --location &#39;https://developer.tealiumapis.com/admin/scim-sync/logs?account={ACCOUNT}&amp;correlationId={CORRELATION_ID}&#39; \
--header &#39;Authorization: Bearer {TOKEN}&#39;
```
