---
title: iQ Revisions API endpoints
description: The GET iQ Revisions API uses JSON objects to retrieve revisions data.
url: https://docs.tealium.com/api/v2/iq-revisions/endpoints/
---
## GET revisions

GET Revisions returns an array of revision IDs. The revision ID is the timestamp of the revision in the form of `YYYYMMDDHHMM`. This ID is used to fetch the revision details.

Use the following GET command to list revisions:

```bash
GET /v2/manifest/accounts/{account}/profiles/{profile}/revisions
```

### Example cURL request

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://api.tealiumiq.com/v2/manifest/accounts/{account}/profiles/{profile}/revisions
```

### Example response

```json
[&#34;201508181719&#34;,
 &#34;201508181718&#34;,
 &#34;201508181717&#34;]
```

Revision IDs are listed in reverse chronological order with the newest revision listed first.

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
| 404 Not Found |  `{&#34;returnCode&#34; : 1240, &#34;message&#34; : &#34;Account was not found&#34;}` |
| 404 Not Found | `{&#34;returnCode&#34; : 1250, &#34;message&#34; : &#34;Profile was not found&#34;}` |

## Get revision details

GET Revision Details returns the details for the specified revision.

Use the following GET command to return details about a revision:

```bash
GET /v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/details
```

### Example cURL request

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://api.tealiumiq.com/v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/details
```

### Example Response

```json
{
    &#34;account&#34;: &#34;tealium&#34;,
    &#34;profile&#34;: &#34;profile&#34;,
    &#34;name&#34;: &#34;Full Release - 2016/12/13 19:53&#34;,
    &#34;time_created&#34;: &#34;Tue 2016.12.13 19:54 GMT&#34;,
    &#34;checksums&#34;: {
        &#34;prod&#34;: {
            &#34;manifest.json&#34;: &#34;df8bb8bdb8bc34f9d70d98ff49fdcf53e7f286520747001538b74357418178a2&#34;,
            &#34;bundle.zip&#34;: &#34;9309364527db38cd33538ca239929c3ed89b7b6990e99b4a41d16b50dd519e35&#34;,
            &#34;utag.js&#34;: &#34;3c34236708b14e8fd8a82e5c363d006793fd59fc6f6a6f0367634cf245d16861&#34;,
            &#34;utag.1.js&#34;: &#34;9b911570ac0685a50a3a32ef780a2570b16725779b7336bdbfca2838eea6d216&#34;,
            &#34;utag.2.js&#34;: &#34;0d3cbf8b3d275d181c2140c2eab88ead3c9f2002b5260d9ebd9f23cb7b60de9a&#34;
        }
    },
    &#34;revision_id&#34;: &#34;201612131954&#34;,
    &#34;comment&#34;: &#34;up to date publish&#34;,
    &#34;created_by&#34;: &#34;user@example.com&#34;,
    &#34;targets_published&#34;: [&#34;prod&#34;]
}
```

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
|404 Not Found| `{&#34;returnCode&#34; : 1240, &#34;message&#34; : &#34;Account was not found&#34; }` |  
|404 Not Found| `{&#34;returnCode&#34; : 1250, &#34;message&#34; : &#34;Profile was not found&#34; }` |
|404 Not Found| `{&#34;returnCode&#34; : 1260, &#34;message&#34; : &#34;Revision details do not exist&#34;}` |

## GET revision bundle

A _revision bundle_ is the deployable combination of published JavaScript files for the target environment in the form of a `.zip` file. If a revision was published, the value from `targets_published` is used in this endpoint to retrieve the files you want, such as `prod`.

```bash
GET /v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/environments/{environment}
```

This endpoint only works for the latest published revision, not previous revisions.

### Example cURL request

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://api.tealiumiq.com/v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/environments/{environment}
--output distro.zip
```

### Example response

The response for the cURL command is the return of a `.zip` file containing the following individual files:

| File Name| Contents|
|---| ---|
| `utag.js`| The main loader file|
| `utag.*.js`|  The vendor tag files, such as `utag.13.js`|
| `utag.sync.js`| (Optional) Contains the synchronous loader file  |
| `mobile.html `| (Optional) Contains the mobile library configuration |
| `manifest.json`|  A JSON file containing the  information returned by the Revision Details endpoint. Note: The SHA256 for the bundle is not included.|

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
|404 Not Found|  `{&#34;returnCode&#34; : 1270, &#34;message&#34; : &#34;The revision bundle requested is not the latest&#34;}` |