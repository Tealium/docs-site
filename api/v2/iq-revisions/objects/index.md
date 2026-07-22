---
title: iQ Revisions objects
description: Revisions are returned as JSON objects.
url: https://docs.tealium.com/api/v2/iq-revisions/objects/
---## Available fields

| Parameter | Type | Description |
|---|---|---|
| `revision_id` | string | The timestamp of the revision represented as a string in the format of `YYYYMMDDHHMMSS`. |
| `created_by` | email | The email of the user that created the revision. |
| `comment` | string | The comment left by the user at the time the revision was created. |
| `targets_published` | array | An array of the environment names for the publish targets used. |
| `name` | string | The name given to the revision. |
| `time_created` | string | A string representation of the time of creation, for example:  `Tue 2017.12.13 19:54 GMT`. |
| `account` | string | The account name for the revision. |
| `profile` | string | The profile name for the revision. |
| `checksums` | object | The values in `targets_published` is a key factor in the `checksums` object. The values contain a `checksums` value for each JavaScript file published to that target.|


## Example response

```json
{
    "account": "tealium",
    "profile": "main",
    "name": "Full Release - 2025/01/02 19:53",
    "time_created": "Thu 2025.01.02 19:53 GMT",
    "checksums": {
        "prod": {
            "manifest.json": "df8bb8bdb8bc34f9d70d98ff49fdcf53e7f286520747001538b74357418178a2",
            "bundle.zip": "9309364527db38cd33538ca239929c3ed89b7b6990e99b4a41d16b50dd519e35",
            "utag.sync.js": "7cdc832b67612bb053f2e4a91ea9eab2aeb4bd26bae9668cbf5bb58bb6a2e9a1",
            "utag.js": "3c34236708b14e8fd8a82e5c363d006793fd59fc6f6a6f0367634cf245d16861",
            "utag.1.js": "9b911570ac0685a50a3a32ef780a2570b16725779b7336bdbfca2838eea6d216",
            "utag.v.js": "31fd720e49c140f869999210c239f3cf89fd7ad0e7fd88b7b7af75612479cbcc",
            "mobile.html": "c5e99a1378a590ddf42bbc810d7c941ee98cfd0611abc1bf439d649cdb000bf7"
        }
    },
    "revision_id": "201712131954",
    "comment": "up to date publish",
    "created_by": "user@example.com",
    "targets_published": ["prod"]
}
```
