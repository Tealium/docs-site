---
title: DELETE Group API
description: The DELETE Group API removes an existing group from the account.
url: https://docs.tealium.com/api/v3/scim-api/delete-group-api/
---
## How it works

Use the DELETE method to delete a custom group:

```bash
DELETE /scim/v2/Groups/{id}
```

Built-in groups cannot be deleted.

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication]().

## DELETE operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | URL-parameter | Required | The unique identifier for the group. This value is sent as part of the REST API call. |

Built-in groups (Standard User, Account Admins, User Admins, Privacy Admins, Technical Admins, Profile Admins) cannot be deleted. Attempts to delete built-in groups return an HTTP 400 error. For more information, see [Built-in group protection]().

### Example cURL request

```bash
curl --location --request DELETE &#39;https://developer.tealiumapis.com/scim/v2/Groups/9d379d2c-2601-42d8-842c-579dc3c58612&#39; \
--header &#39;Accept: application/scim&#43;json&#39; \
--header &#39;Authorization: ••••••&#39; \
--header &#39;Cookie: JSESSIONID=0f9b099a-1284-4e41-89ac-38f72bbff66c&#39;

```

### Example response

This call returns a 204 status code.

### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;Invalid ID format.&#34;}` |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;Group {uuid} is a built-in group which is ineligible for deletion.&#34;}`|
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 404 |` {&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;Group not found in account {ACCOUNT}.&#34;}`|
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, POST.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|

