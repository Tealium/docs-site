---
title: iQ Tag Template API
description: The iQ Tag Template API uses a PATCH method to update profile tag templates.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-tag-templates-api/
---
To learn more about this API and available object fields, see [iQ Profiles API]() and [iQ Profiles Objects]().

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
  --header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39; \
  --header &#39;Content-Type: application/json&#39; \
  --data &#39;
```

## Authentication

The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.

To learn about generating a bearer token from the API key, see [Authentication]().

## Profile fields

Profile tag templates are JSON objects that contain the following possible fields:

| OBJECT | TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| `versionTitle` | String | Optional | The title of the resulting saved version.&lt;br&gt;Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`&lt;br&gt;Default with `saveType` set to `save`: Existing version title |
| `saveType` | String | Optional| The type of save to perform with the PATCH request: `save` or `saveAs`. Default is `saveAs`. |
| `notes` | String | Required | Additional notes about the publish version. |
| `templateData.content` | Object | Required | The tag template content you want to update.|

### Example response

```json
{
  &#34;versionTitle&#34;: &#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes&#34;,
  &#34;templateData&#34;: {
    &#34;content&#34;: &#34;testing a template update&#34;
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
  &#34;versionTitle&#34;: &#34;test version&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes&#34;,
  &#34;templateData&#34;: {
    &#34;content&#34;: &#34;testing a template update&#34;
  }
}
```

## Error messages

Potential error messages for this endpoint:

| ERROR CODE | ERROR MESSAGE |
| --- | --- |
| 400 | `&#34;Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;patchProfile.arg2.notes: must not be empty&#34;`|
| 404 | `&#34;Profile not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Profile library not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Profile (legacy) not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Users are currently viewing the same account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Latest version not found - {ACCOUNT} \| profile: {PROFILE}&#34;` |
| 409 | `&#34;Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSION}&#34;` |
| 500 | `&#34;Profile: {PROFILE} inherits from library profile&#34;`&lt;br&gt;`&#34;Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}&#34;`|