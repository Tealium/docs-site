---
title: iQ Revisions API endpoints
description: The GET iQ Revisions API uses JSON objects to retrieve revisions data.
url: https://docs.tealium.com/api-v1/iq-revisions/endpoints/
---
This is an older version of the [current Tealium iQ Revisions API](https://docs.tealium.com/about-iq-revisions/).

## List revisions

Returns an array of revision IDs. The revision ID is the timestamp of the revision in the form of "YYYYMMDDHHMM". This ID is used to fetch the revision details.

`GET /v1/accounts/{account}/{profile}/revisions`

### cURL Request

```bash
curl -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/accounts/{account}/{profile}/revisions?utk={token}

```

### Example response

```json
["201508181719",
 "201508181718",
 "201508181717"]

```


<blockquote>
The revision IDs are listed in reverse chronological order with the newest revision first.
</blockquote>


### Error messages

**400 NOT FOUND**

```
{
   "returnCode" : 1240,
   "message" : "Account was not found"
}

```

```
{
   "returnCode" : 1250,
   "message" : "Profile was not found"
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
    "account": "tealium",
    "profile": "profile",
    "name": "Full Release - 2016/12/13 19:53",
    "time_created": "Tue 2016.12.13 19:54 GMT",
    "checksums": {
        "prod": {
            "manifest.json": "df8bb8bdb8bc34f9d70d98ff49fdcf53e7f286520747001538b74357418178a2",
            "bundle.zip": "9309364527db38cd33538ca239929c3ed89b7b6990e99b4a41d16b50dd519e35",
            "utag.js": "3c34236708b14e8fd8a82e5c363d006793fd59fc6f6a6f0367634cf245d16861",
            "utag.1.js": "9b911570ac0685a50a3a32ef780a2570b16725779b7336bdbfca2838eea6d216",
            "utag.2.js": "0d3cbf8b3d275d181c2140c2eab88ead3c9f2002b5260d9ebd9f23cb7b60de9a"
        }
    },
    "revision_id": "201612131954",
    "comment": "up to date publish",
    "created_by": "user@example.com",
    "targets_published": ["prod"]
}

```

### Error Messages

**404 Not Found**

```
{
   "returnCode" : 1240,
   "message" : "Account was not found"
}

```

```
{
   "returnCode" : 1250,
   "message" : "Profile was not found"
}

```

```
{
   "returnCode" : 1260,
  "message" : "Revision details do not exist"
}

```

## Get revision bundle

A _revision bundle_ is the deployable corpus of the published JavaScript files for the target environment in the form of a zip file. If a revision was published, the value from `targets_published` will be used in this endpoint to retrieve the files you want. For example: "prod".

` GET /v1/accounts/{account}/{profile}/revisions/{revision_id}/{target}`

### cURL Request

```bash
curl -b JSESSION={session_id} \
  http://api.tealiumiq.com/v1/accounts/{account}/{profile}/revisions/{revision_id}/{target}?utk={token} \
  -o utag.zip

```

### Response

The request returns a ".zip" file that contains:

* **utag.js**- the main loader file
* **utag.\*.js**- the vendor tag files. For example: `utag.13.js`.
* **utag.sync.js**- (Optional) the synchronous loader file
* **mobile.html**- (Optional) mobile library configuration
* **manifest.json**- this JSON file contains the same information returned by the Revision Details endpoint minus the SHA256 of the bundle.

### Error Messages

**400 NOT FOUND**

```
{
   "returnCode" : 1270,
   "message" : "The revision bundle requested is not the latest"
}

```
