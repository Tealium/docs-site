---
title: iQ Revisions objects
description: Revisions are returned as JSON objects.
url: https://docs.tealium.com/api-v1/iq-revisions/data-objects/
---
This is an older version of the [current Tealium iQ Revisions API](https://docs.tealium.com/about-iq-revisions/).

Revisions are returned as JSON objects containing the following fields:

|Name| Type| Description|
|---| ---| ---|
|revision_id| string| The timestamp of the revision ,represented as a string in the format of `YYYYMMDDHHMMSS`.|
|created_by| email| The email of the user that created the revision.|
|comment| string| The comment left by the user.|
|targets_published| array| Array of environment names of the publish targets used.|
|name| string| The name given to the revision.|
|time_created| string| A string representation of the time of creation. For example: "Tue 2016.12.13 19:54 GMT".|
|account| string| The account name of the revision.|
|profile| string| The profile name of the revision.|
|checksums| object|  Each value in `targets_published` is a key in this object, the value of which is an object containing a checksum value for each JavaScript file published to that target. Example: ``` "targets_published" : ["dev"], "checksums" : {     "dev": {         "manifest.json" : "<CHECKSUM HERE>",         "bundle.zip"    : "<CHECKSUM HERE>",         "utag.js"       : "<CHECKSUM HERE>",         "utag.1.js"     : "<CHECKSUM HERE>"     } } ``` |

## Example response

```json
{
    "account": "tealium",
    "profile": "main",
    "name": "Full Release - 2016/12/13 19:53",
    "time_created": "Tue 2016.12.13 19:54 GMT",
    "checksums": {
        "prod": {
            "manifest.json": "df8bb8bdb8bc34f9d70d98ff49fdcf53e7f286520747001538b74357418178a2",
            "bundle.zip": "9309364527db38cd33538ca239929c3ed89b7b6990e99b4a41d16b50dd519e35",
            "utag.sync.js": "7cdc832b67612bb053f2e4a91ea9eab2aeb4bd26bae9668cbf5bb58bb6a2e9a1",
            "utag.js": "3c34236708b14e8fd8a82e5c363d006793fd59fc6f6a6f0367634cf245d16861",
            "utag.1.js": "9b911570ac0685a50a3a32ef780a2570b16725779b7336bdbfca2838eea6d216"
        }
    },
    "revision_id": "201612131954",
    "comment": "up to date publish",
    "created_by": "user@example.com",
    "targets_published": ["prod"]
}
```

