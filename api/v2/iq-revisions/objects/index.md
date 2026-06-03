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
    &#34;account&#34;: &#34;tealium&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;name&#34;: &#34;Full Release - 2025/01/02 19:53&#34;,
    &#34;time_created&#34;: &#34;Thu 2025.01.02 19:53 GMT&#34;,
    &#34;checksums&#34;: {
        &#34;prod&#34;: {
            &#34;manifest.json&#34;: &#34;df8bb8bdb8bc34f9d70d98ff49fdcf53e7f286520747001538b74357418178a2&#34;,
            &#34;bundle.zip&#34;: &#34;9309364527db38cd33538ca239929c3ed89b7b6990e99b4a41d16b50dd519e35&#34;,
            &#34;utag.sync.js&#34;: &#34;7cdc832b67612bb053f2e4a91ea9eab2aeb4bd26bae9668cbf5bb58bb6a2e9a1&#34;,
            &#34;utag.js&#34;: &#34;3c34236708b14e8fd8a82e5c363d006793fd59fc6f6a6f0367634cf245d16861&#34;,
            &#34;utag.1.js&#34;: &#34;9b911570ac0685a50a3a32ef780a2570b16725779b7336bdbfca2838eea6d216&#34;,
            &#34;utag.v.js&#34;: &#34;31fd720e49c140f869999210c239f3cf89fd7ad0e7fd88b7b7af75612479cbcc&#34;,
            &#34;mobile.html&#34;: &#34;c5e99a1378a590ddf42bbc810d7c941ee98cfd0611abc1bf439d649cdb000bf7&#34;
        }
    },
    &#34;revision_id&#34;: &#34;201712131954&#34;,
    &#34;comment&#34;: &#34;up to date publish&#34;,
    &#34;created_by&#34;: &#34;user@example.com&#34;,
    &#34;targets_published&#34;: [&#34;prod&#34;]
}
```
