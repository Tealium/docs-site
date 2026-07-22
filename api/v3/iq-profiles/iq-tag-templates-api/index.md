---
title: iQ Tag Template API
description: The iQ Tag Template API uses a PATCH method to update profile tag templates.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-tag-templates-api/
---
To learn more about this API and available object fields, see [iQ Profiles API](https://docs.tealium.com/iq-profiles-v3-api/) and [iQ Profiles Objects](https://docs.tealium.com/iq-profiles-api-objects/).

## How it works

After you create a tag, you can use the iQ Tag Template API to edit the tag template.

Use the `PATCH` method to update components in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/templates/{TEMPLATE_ID}
```

When you use the PATCH method, you are making changes to your profile tag templates programmatically using a save or save-as. After making changes with the API, you must still log into the application to publish.

### Example cURL request

```bash
curl --location --request PATCH \
  --url https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/templates/79 \
  --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9' \
  --header 'Content-Type: application/json' \
  --data '
```

## Authentication


<blockquote>
The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.
</blockquote>


To learn about generating a bearer token from the API key, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).

## Profile fields

Profile tag templates are JSON objects that contain the following possible fields:

| OBJECT | TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| `versionTitle` | String | Optional | The title of the resulting saved version.<br>Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`<br>Default with `saveType` set to `save`: Existing version title |
| `saveType` | String | Optional| The type of save to perform with the PATCH request: `save` or `saveAs`. Default is `saveAs`. |
| `notes` | String | Required | Additional notes about the publish version. |
| `templateData.content` | Object | Required | The tag template content you want to update.|

### Example response

```json
{
  "versionTitle": "Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes": "version notes",
  "templateData": {
    "content": "testing a template update"
  }
}
```

## PATCH operation parameters

To add or remove a tag template, you must add or remove the tag.

## Update tag template

This PATCH method takes a profile object and additional tag template fields.

### Example request

```json
{
  "versionTitle": "test version",
  "saveType": "saveAs",
  "notes": "version notes",
  "templateData": {
    "content": "testing a template update"
  }
}
```

## Error messages

Potential error messages for this endpoint:

| ERROR CODE | ERROR MESSAGE |
| --- | --- |
| 400 | `"Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}"`<br>`"patchProfile.arg2.notes: must not be empty"`|
| 404 | `"Profile not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Profile library not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Profile (legacy) not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Users are currently viewing the same account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Latest version not found - {ACCOUNT} \| profile: {PROFILE}"` |
| 409 | `"Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSION}"` |
| 500 | `"Profile: {PROFILE} inherits from library profile"`<br>`"Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}"`|