---
title: iQ Publish API
description: Use the iQ Publish API to publish a saved profile version, check publish status, or save and publish in one operation.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-publish-api/
---
To learn more about this API and available object fields, see [iQ Profiles API](https://docs.tealium.com/iq-profiles-v3-api/) and [iQ Profiles Objects](https://docs.tealium.com/iq-profiles-api-objects/).

## How it works

The iQ Publish API extends the `/v3/tiq` API surface with three publish capabilities. You can publish an existing saved version to one or more environments, poll the status of a publish request, or combine a profile save and publish into a single PATCH operation.

## Authentication


<blockquote>
The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.
</blockquote>


To learn about generating a bearer token from the API key, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).

## Publish an existing version

Use this endpoint when a saved profile version already exists and you want to publish it without modifying the profile. You must supply the exact `versionId` to publish. The API does not implicitly publish the latest version.

```bash
POST /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/publish
```

### Request parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `versionId` | String | Yes | The version ID of the saved profile to publish. Version IDs use the format `YYYYMMDDhhmm`. For example, `202608131215`. |
| `operatorId` | String | Yes | An email address recorded in the publish history for audit purposes. This field is not derived from the bearer token automatically. |
| `publishTargets` | Array of strings | Yes | One or more target environment names. Default targets are `dev`, `qa`, and `prod`. Custom environments may also be used as targets when configured on the profile. For more information, see [Custom publish environments](https://docs.tealium.com/custom-publish-environments/). Target names must contain only letters, numbers, and dashes. |
| `title` | String | Yes | The publish title. Titles longer than 128 characters are rejected. |
| `notes` | String | Yes | Notes recorded with the publish request. |

If the request includes multiple targets, all targets must pass the permission check. The API rejects the entire request if you lack permission for any requested target.

### Example request

```bash
curl --request POST \
  --url "https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/publish" \
  --header "Authorization: Bearer {TOKEN}" \
  --header "Content-Type: application/json" \
  --header "Accept: application/json" \
  --data '{
    "versionId": "202608131215",
    "operatorId": "user@example.com",
    "publishTargets": ["qa"],
    "title": "API publish",
    "notes": "Publishing version 202608131215 to QA"
  }'
```

### Response

A successful response means the publish request was accepted and queued, not that publishing is complete. Use the `publishId` from the response to poll the [status endpoint](#check-publish-status).

```json
{
  "publishId": "212ab1da-7503-4691-bf87-f892b450ed5a",
  "account": "my_account",
  "profile": "main",
  "versionId": "202608131215",
  "operatorId": "user@example.com",
  "createdDate": "2026-08-13T20:16:01 UTC",
  "publishTargets": [
    {
      "target": "qa",
      "publishTargetId": "83ff6319-de94-4ac0-b05a-7f19bfb8e34f",
      "distroDate": null
    }
  ],
  "title": "API publish",
  "revisionId": "202608131215",
  "notes": "Publishing version 202608131215 to QA"
}
```

| Field | Description |
| --- | --- |
| `publishId` | UUID for the publish request. Use this value to poll the status endpoint. |
| `account` | The Tealium account name. |
| `profile` | The Tealium profile name. |
| `versionId` | The profile version submitted for publish. |
| `operatorId` | The email address supplied in the request and recorded in the publish history for audit purposes. |
| `createdDate` | The publish request creation time in UTC. |
| `publishTargets` | Target records created for the publish request. Each entry contains `target`, `publishTargetId`, and `distroDate`. |
| `title` | The publish title supplied in the request. |
| `notes` | The publish notes supplied in the request. |
| `revisionId` | The revision identifier associated with the published profile data. |

### Error codes

| Error code | Description |
| --- | --- |
| 400 | Missing required field, malformed target name, or title longer than 128 characters. |
| 401 | Missing or malformed bearer token. |
| 403 | Insufficient publish permission for the account, profile, or one or more requested targets. |
| 404 | Account, profile, or version identifier not found. |
| 409 | Concurrent user or publish conflict. |
| 422 | Publish target validation failed or profile referential integrity error. |

## Check publish status

Use this endpoint to poll the status of a publish request after a POST publish or PATCH save-and-publish call.

```bash
GET /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/publish/{PUBLISH_ID}/status
```

### Path parameters

| Parameter | Description |
| --- | --- |
| `ACCOUNT` | The Tealium account name. |
| `PROFILE` | The Tealium profile name. |
| `PUBLISH_ID` | The `publishId` returned by the POST publish endpoint, or the `publish.data.publishId` value in a PATCH save-and-publish response. |

### Example request

```bash
curl --request GET \
  --url "https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/publish/{PUBLISH_ID}/status" \
  --header "Authorization: Bearer {TOKEN}" \
  --header "Accept: application/json"
```

### Response

```json
{
  "publishId": "212ab1da-7503-4691-bf87-f892b450ed5a",
  "publishTargetEventResponses": [
    {
      "publishTargetEventId": "02b71e23-8927-4156-9df0-1f9a87125a44",
      "publishTargetId": "83ff6319-de94-4ac0-b05a-7f19bfb8e34f",
      "publishTargetEventType": "tag_generation_queued",
      "publishTargetState": "queued",
      "detail": null,
      "createdDate": "2026-08-13T20:16:01 UTC"
    }
  ]
}
```

| Field | Description |
| --- | --- |
| `publishId` | UUID identifying the overall publish request. |
| `publishTargetEventResponses` | One status entry for each target event record. Check the latest state for each target. |
| `publishTargetEventId` | UUID identifying the status event record. This value changes as the target progresses. |
| `publishTargetId` | UUID identifying the target submission within the publish request. |
| `publishTargetEventType` | The lifecycle event type emitted by the publish service. |
| `publishTargetState` | The coarse state derived from the event type. |
| `detail` | Optional diagnostic detail. This value may be `null`. |
| `createdDate` | UTC timestamp for the event. |

### Publish states

| Event type | State | Meaning |
| --- | --- | --- |
| `initialising_publish` | `queued` | The request is being initialized. |
| `tag_generation_queued` | `queued` | The target is waiting for tag generation. |
| `tag_generation_started` | `processing` | Tag generation has started. |
| `publish_distro_queued` | `processing` | Distribution is queued. |
| `publish_distro_starting` | `processing` | Distribution is starting. |
| `publish_success` | `published` | The target completed successfully. |
| `publish_fail` | `stopped` | The target failed or was stopped. |

For requests with multiple targets, check the state of every target. A publish is complete only when all targets reach `published`. A publish has failed when any target reaches `stopped`.

The status endpoint is rate-limited to one request per second per publish ID. Publish status does not change rapidly, so polling more frequently is unnecessary and returns a `429` error.

### Error codes

| Error code | Description |
| --- | --- |
| 401 | Missing or malformed bearer token. |
| 403 | Insufficient publish permission for the account or profile. |
| 404 | Account, profile, or publish identifier not found. |
| 429 | Request rate exceeded. Poll no more than once per second. |

## Save and publish

Use this endpoint when you want to save a profile change and publish the resulting version in one operation. The service uses the version created by the save. Do not supply a `versionId` for the publish portion.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

Use the same `operationList` body as the existing PATCH operations for tags, variables, load rules, events, and extensions. Add the following fields to enable save-and-publish.

### Publish fields

All fields in the following table are required when `publish` is `true`.

| Field | Type | Description |
| --- | --- | --- |
| `publish` | Boolean | Set to `true` to enable save-and-publish. When absent or `false`, the existing PATCH save behavior is used. |
| `publishTargets` | Array of strings | Target environment names to publish to after the save. Default targets are `dev`, `qa`, and `prod`. Custom environments may also be used when configured on the profile. For more information, see [Custom publish environments](https://docs.tealium.com/custom-publish-environments/). |
| `publishTitle` | String | The publish title. Set this to the same value as `title`. Titles longer than 128 characters are rejected. |
| `publishNote` | String | Notes recorded with the publish request. Set this to the same value as `notes`. |
| `operatorId` | String | An email address recorded in the publish history for audit purposes. This field is not derived from the bearer token automatically. |


<blockquote>
The `notes` and `versionTitle` fields are the save note and version title recorded when the profile is saved. The `publishNote` and `publishTitle` fields are recorded separately when the publish operation runs. Provide all four fields when performing a save-and-publish operation.
</blockquote>


### Example request

```bash
curl --request PATCH \
  --url "https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}" \
  --header "Authorization: Bearer {TOKEN}" \
  --header "Content-Type: application/json" \
  --header "Accept: application/json" \
  --data '{
    "versionTitle": "API patch publish",
    "saveType": "saveAs",
    "parentVersion": "202608131150",
    "notes": "Added page_type variable",
    "operationList": [
      {
        "op": "add",
        "path": "/variables",
        "value": {
          "object": "variable",
          "name": "page_type",
          "alias": "Page Type",
          "type": "udo",
          "notes": "UDO variable"
        }
      }
    ],
    "publish": true,
    "publishTargets": ["qa"],
    "publishTitle": "API patch publish",
    "publishNote": "Added page_type variable",
    "operatorId": "user@example.com"
  }'
```

### Response

When `publish` is `true`, the response contains two top-level sections: `profile` and `publish`.

**Success response**

```json
{
  "profile": {
    "account": "my_account",
    "profile": "main",
    "version": "202608131215",
    "minorVersion": "202608131215"
  },
  "publish": {
    "status": "success",
    "data": {
      "publishId": "212ab1da-7503-4691-bf87-f892b450ed5a",
      "account": "my_account",
      "profile": "main",
      "versionId": "202608131215",
      "operatorId": "user@example.com",
      "createdDate": "2026-08-13T20:16:01 UTC",
      "publishTargets": [
        {
          "target": "qa",
          "publishTargetId": "83ff6319-de94-4ac0-b05a-7f19bfb8e34f",
          "distroDate": null
        }
      ],
      "title": "API patch publish",
      "revisionId": "202608131215",
      "notes": "Added page_type variable"
    }
  }
}
```

**Failure response** (save succeeded, publish failed)

```json
{
  "profile": {
    "account": "my_account",
    "profile": "main",
    "version": "202608131215",
    "minorVersion": "202608131215"
  },
  "publish": {
    "status": "failed",
    "data": {
      "message": "Publish permission denied for target: prod",
      "account": "my_account",
      "profile": "main",
      "versionId": "202608131215"
    }
  }
}
```

| Field | Description |
| --- | --- |
| `profile` | The saved profile response. The `version` field contains the version ID used for the publish. |
| `publish.status` | `success` when the publish was submitted successfully. `failed` when a permission, validation, or publish-stage error occurred. |
| `publish.data` | The publish response data. On success, this contains `publishId` and target records. On failure, this contains error details. |


<blockquote>
The save and publish steps are not atomic. If the save completes and the publish fails, the API does not reverse the profile save. Verify the profile state with a GET request before retrying.
</blockquote>


### Error codes

An HTTP 200 response does not confirm that publishing succeeded. Always check `publish.status`. When `publish.status` is `failed`, the profile saved successfully but the publish did not. Use `publish.data.publishId` to poll the status endpoint only when `publish.status` is `success`.

| Error code | Description |
| --- | --- |
| 400 | Missing required field, malformed target name, invalid PATCH body, or title longer than 128 characters. |
| 401 | Missing or malformed bearer token. |
| 403 | Insufficient publish permission for the account, profile, or one or more requested targets. |
| 404 | Account, profile, or version identifier not found. |
| 409 | Concurrent user or publish conflict. |
| 422 | Publish target validation failed or profile referential integrity error. |
| 429 | Request rate exceeded. |
