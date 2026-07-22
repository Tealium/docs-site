---
title: GET SCIM Sync Logs API
description: The GET SCIM Sync Logs API exports a record of SCIM user provisioning events.
url: https://docs.tealium.com/api/v3/scim-api/get-scim-sync-logs-api/
---
## How it works

Use the GET method to retrieve SCIM audit log entries:

```bash
GET /admin/scim-sync/logs
```

For more information about SCIM audit logging, see [SCIM audit logs](https://docs.tealium.com/scim-audit-logs/).

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## GET operation parameters

This endpoint requires Account Admin or User Admin permissions and takes the following parameters:

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `account` | String | Required | The Tealium account name. |
| `from` | String | Optional | The start of the date range in ISO 8601 format. Defaults to 30 days before `to` if omitted. |
| `to` | String | Optional | The end of the date range in ISO 8601 format. Defaults to the current date and time. |
| `status` | String | Optional | Filter by outcome. Valid values: `SUCCESS`, `ERROR`. |
| `action` | String | Optional | Filter by action type. Case-sensitive. Valid values: `User Creation`, `User Update`, `User Patch`, `User Retrieval`, `User Deletion`. |
| `source` | String | Optional | Filter by event source. Case-sensitive. Valid values: `SCIM_API`, `UI`, `INTERNAL_API`, `SYSTEM`. |
| `userEmail` | String | Optional | Case-insensitive substring match on the target user's email address. |
| `correlationId` | String | Optional | Exact match on correlation ID. |
| `format` | String | Optional | Response format. Valid values: `csv` (default), `json`. |
| `limit` | Integer | Optional | Maximum number of log entries to return. Default is `1000`. Maximum is `5000`. |

### Example cURL request

```bash
curl --location 'https://developer.tealiumapis.com/admin/scim-sync/logs?account={ACCOUNT}&from=2025-01-01T00:00:00Z&to=2025-01-31T23:59:59Z&format=json&status=ERROR' \
--header 'Authorization: Bearer {TOKEN}'
```

### Example response



| timestamp | action_type | resource_type | target_email | target_first_name | target_last_name | target_user_uuid | external_id | idp_source | http_status | outcome | correlation_id | account_name | error_message |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
| 2025-10-13 23:01:15.684Z | User Creation | USER | test.userXZ4@example.com | Test | User | | | | 409 | ERROR | a211d118-f6db-49ec-8a85-05f46742954d | admin1 | User already exists in the given account. |
| 2025-10-13 22:51:57.472Z | User Patch | USER | test.userxz4@example.com | | User | aa580e7f-569c-460e-b7e0-a73416161949 | | | 200 | SUCCESS | 019f36c9-3018-418c-b877-41450d845fca | admin1 | |
| 2025-10-13 22:47:00.753Z | User Patch | USER | test.userxz4@example.com | john | User | aa580e7f-569c-460e-b7e0-a73416161949 | | | 200 | SUCCESS | 0e79ebfd-76f0-40f9-8e6e-20f105b53e46 | admin1 | |
| 2025-10-13 22:46:54.604Z | User Update | USER | | | | aa580e7f-569c-460e-b7e0-a73416161949 | | | 400 | ERROR | c9f40bc4-62da-4d10-8fe5-08fddf4686cd | admin1 | userName is required. |



### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{"message": "Account parameter is required."}` |
| 400 | `{"message": "Invalid date format. Use ISO-8601 format (e.g., 2023-01-01T00:00:00Z)."}` |
| 400 | `{"message": "Invalid date range: 'from' must be before 'to'."}` |
| 400 | `{"message": "Limit must be between 1 and 5000."}` |
| 400 | `{"message": "Invalid status. Must be SUCCESS or ERROR."}` |
| 400 | `{"message": "Invalid source. Must be SCIM_API, UI, INTERNAL_API, or SYSTEM."}` |
| 403 | `{"message": "Unauthorized access."}` |
| 405 | `{"message": "Method is not allowed on this endpoint. Allowed methods: GET."}` |
| 500 | `{"message": "Error processing request."}` |
