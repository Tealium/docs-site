---
title: iQ Revisions API endpoints
description: The GET iQ Revisions API uses JSON objects to retrieve revisions data.
url: https://docs.tealium.com/api-v1/iq-revisions/endpoints/
---
This is an older version of the [current Tealium iQ Revisions API]().

## List revisions

Returns an array of revision IDs. The revision ID is the timestamp of the revision in the form of &#34;YYYYMMDDHHMM&#34;. This ID is used to fetch the revision details.

`GET /v1/accounts/{account}/{profile}/revisions`

### cURL Request

```bash
curl -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/accounts/{account}/{profile}/revisions?utk={token}

```

### Example response

```json
[&#34;201508181719&#34;,
 &#34;201508181718&#34;,
 &#34;201508181717&#34;]

```

The revision IDs are listed in reverse chronological order with the newest revision first.

### Error messages

**400 NOT FOUND**

```
{
   &#34;returnCode&#34; : 1240,
   &#34;message&#34; : &#34;Account was not found&#34;
}

```

```
{
   &#34;returnCode&#34; : 1250,
   &#34;message&#34; : &#34;Profile was not found&#34;
}

```

## Get revision details

Returns the revision details.

`GET /v1/accounts/{account}/{profile}/revisions/{revision_id}/details`

### cURL Request

```bash
curl -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/accounts/{account}/{profile}/revisions/{revision_id}/details?utk={token}

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

### Error Messages

**404 Not Found**

```
{
   &#34;returnCode&#34; : 1240,
   &#34;message&#34; : &#34;Account was not found&#34;
}

```

```
{
   &#34;returnCode&#34; : 1250,
   &#34;message&#34; : &#34;Profile was not found&#34;
}

```

```
{
   &#34;returnCode&#34; : 1260,
  &#34;message&#34; : &#34;Revision details do not exist&#34;
}

```

## Get revision bundle

A _revision bundle_ is the deployable corpus of the published JavaScript files for the target environment in the form of a zip file. If a revision was published, the value from `targets_published` will be used in this endpoint to retrieve the files you want. For example: &#34;prod&#34;.

` GET /v1/accounts/{account}/{profile}/revisions/{revision_id}/{target}`

### cURL Request

```bash
curl -b JSESSION={session_id} \
  http://api.tealiumiq.com/v1/accounts/{account}/{profile}/revisions/{revision_id}/{target}?utk={token} \
  -o utag.zip

```

### Response

The request returns a &#34;.zip&#34; file that contains:

* **utag.js**- the main loader file
* **utag.\*.js**- the vendor tag files. For example: `utag.13.js`.
* **utag.sync.js**- (Optional) the synchronous loader file
* **mobile.html**- (Optional) mobile library configuration
* **manifest.json**- this JSON file contains the same information returned by the Revision Details endpoint minus the SHA256 of the bundle.

### Error Messages

**400 NOT FOUND**

```
{
   &#34;returnCode&#34; : 1270,
   &#34;message&#34; : &#34;The revision bundle requested is not the latest&#34;
}

```
