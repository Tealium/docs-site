---
title: iQ GET Profile API
description: The iQ GET Profile API retrieves an iQ Tag Management account profile, including specific configuration components and version history.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-get-profile-api/
---
## How it works

Use the GET method to retrieve an account profile:

```bash
GET /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}?includes={INCLUDE}&publishVersion={PUBLISH_VERSION}
```

## Authentication


<blockquote>
The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.
</blockquote>


To learn about generating a bearer token from the API key, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).

## GET operation parameters

This command uses the following parameters:

|Parameter| Type| Required| Description|
|---| ---| ---| ---|
|publishVersion| String| Optional| The version ID of the profile to retrieve. If you omit this parameter, the most recent version is retrieved.<br> Version IDs are in the format `YYYYMMDDhhmm`<br> Example: `"202202111806"`|
|includes| Array| Optional| An array of the configuration components to include in the response. Add this query string parameter for each component to include.<br> For example, to get variables and extensions: `&includes=variables&includes=extensions` Default: none<br> Values: `loadRules`, `tags`, `tags.templateList`, `tags.template`, `extensions`, `variables`, `events` , and `versionIDs` |


<blockquote>
To retrieve the list of tag templates for a profile, your GET request must include `tags` and `tags.templateList`. For example, `&includes=tags&includes=tags.templateList`.<br> To retrieve the tag templates themselves, include `tags` and `tags.template`. For example, `&includes=tags&includes=tags.template`.
</blockquote>


### Example cURL request

```bash
curl -H 'Authorization: Bearer {token}' \
https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}?includes=loadRules&includes=extensions&includes=tags&includes=tags.template&includes=variables&includes=events&includes=versionIds&publishVersion=202003161355
```

### Example response

 

```json
{
    "account": "my_account",
    "profile": "main",
    "versionTitle": "Version 2022.03.22.2108",
    "version": "202203222108",
    "minorVersion": "202203222108",
    "parentVersion": "202309191127",
    "creation": "202201131654",
    "customTargets": null,
    "versionDetails": {
        "environmentVersions": {
            "qa": true,
            "prod": false,
            "dev": true
        },
        "user": "user1@tealium.com",
        "notes": ""
    },
    "environmentVersions": {
        "qa": "202203222108",
        "prod": "202203222108",
        "dev": "202203222108"
    },
    "dataCloudLinkedProfiles": "{}",
    "libraryType": "NONE",
    "linkedProfiles": null,
    "linkedLibraries": [
        {
            "environment": "Dev",
            "name": "LibraryName",
            "required": true
        },
        {
            "environment": "Prod",
            "name": "LibraryName",
            "required": true
        }
    ],
    "variables":[
        {
            "id": 37,
            "uniqueIdentifier": "dom.viewport_height",
            "name": "viewport_height",
            "alias": "Viewport Height",
            "type": "dom",
            "notes": null,
            "context": null,
            "library": null,
            "imported": null,
            "usedIn": {
                "tags": [],
                "events": [],
                "extensions": [],
                "consent": [],
                "loadRules": []
            }
        }
    ],
   "loadRules":[
        {
            "id":2,
            "name":"US Site Only",
            "status":"active",
            "library": null,
            "notes": "notes 1",
            "startDate": "202203010000",
            "endDate": "202203152359",
            "environmentVersions": {
                "qa": "202203222108",
                "prod": "202203222108",
                "dev": "202203222108"
            },
            "usedIn": {
                "tags": [],
                "extensions": [],
                "consent": [
                   "gdpr"
                ],
                "loadRules": null
            },
            "loadRuleCondition": [
                [
                    {
                        "variable": "js.variable1",
                        "operator": "contains",
                        "value": "1"
                    },
                    {
                        "variable": "js.order_discount",
                        "operator": "does_not_equal",
                        "value": "2"
                    },
                ],
                [
                    {
                        "variable": "dom.viewport_height",
                        "operator": "does_not_end_with_ignore_case",
                        "value": "3"},
                    {
                        "variable": "meta.metadata",
                        "operator": "does_not_equal_ignore_case",
                        "value": "7"
                    }
                ],
            ]
        }
    ],
    "extensions":[
       {
            "id":4,
            "extensionId": 100036,
            "extenstionType": "Javascript Code",
            "name": "Build Data Layer",
            "library": "synclib",
            "scope": "Pre Loader",
            "occurrence": "Run Always",
            "notes": "",
            "loadRule": null,
            "status":"active",
            "selectedTargets": {
                "qa": true,
                "prod": true,
                "dev": true
            },
            "environmentVersions": {
                "qa": "202204072336",
                "prod": "202204072336",
                "dev": "202204072336"
            },
            "conditions":null,
            "configuration": []
       },
       {
            "id":70,
            "extensionId": 100036,
            "type":"Set Data Values",
            "name":"Set Checkout Step 1 Complete Event",
            "library": "synclib",
            "status":"inactive",
            "scope":"global",
            "occurrence": "Run Always",
            "notes":"",
            "loadRule": null,
            "selectedTargets": {
                "qa": true,
                "prod": true,
                "dev": true
            },
            "environmentVersions": {
                "qa": "202204072336",
                "prod": "202204072336",
                "dev": "202204072336"
            },
            "conditions":null,
            "configuration": []
       }
    ],
    "tags":[
        {
            "id": "322",
            "tagId":"20048",
            "tagName":"Twitter",
            "name":"Twitter",
            "library": null,
            "status":"active",
            "notes":"",
            "loadRule":"50,3",
            "loadRuleJoinOperator":"all",
            "dataMappings":[
                { 
                    "mappings": [
                        "a1",
                        "a2"
                    ],
                    "type": "dom",
                    "variable": "title"
                },
                {
                    "mappings": [
                        "a3",
                        "a4"
                    ],
                    "type": "static.text",
                    "variable": "height"
                }
            ],
            "selectedTargets": {
                "qa": true,
                "prod": true,
                "dev": true
            },
            "environmentVersions": {
                "qa": "202203222108",
                "prod": "202203222108",
                "dev": "202203222108"
            },
            "advancedConfiguration": {
                "bundleFlag": false,
                "syncLoadType": true,
                "optOut": true,
                "sendFlag": true,
                "scriptSource": "",
                "tagTiming": "DOM Ready"
            },
            "configuration": {
                "config_EMUserSecret": "",
                "multipleLoadRules": "3,2",
                "_multipleLoadRules": "3,2"
           },
           "rules": {
               "apply": null,
               "exclude": null
           },
           "template": null
       }
    ],
    "events": [
        {
            "id": 25,
            "eventId": 100045,
            "name": "Home and Decor Homepage Click",
            "status": "active",
            "eventType": "mouseevents",
            "scope": "DOM Ready",
            "trackingEvent": "link",
            "notes": "",
            "library": null,
            "eventLoadRuleList": "all",
            "eventTrigger": {
                "object": "mouseevents",
                "cssSelector": "",
                "title": "Mouse Events",
                "mouseEvent": "mousedown",
                "triggerFrequency": "runAlways"
            },
            "selectedTargets": {
                "prod": true,
                "dev": true,
                "qa": true
            },
            "environmentVersions": {
                "qa": "202301202252",
                "prod": "202301202252",
                "dev": "202301202252"
            },
            "eventVariables": [
                {
                    "variable": "udo.tealium_event",
                    "type": "text",
                    "value": "mousedown"
                }
            ],
            "rules": {
                "apply": null,
                "exclude": null
            },
            "usedIn": {
                "tags": [],
                "events": null,
                "extensions": null,
                "consent": null,
                "loadRules": null
            }
        }
    ],
    "versionIds": [
        "202309191128",
        "202309191127",
        "202309061342"
    ],
    "templateList": null
}
```


### Error messages

Potential error messages for this endpoint:

|Error Code| Error Message|
|---| ---|
|400|  `"Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}"`<br>  `"Variable validation failed - variableId: {VARIABLE ID} \| {ACCOUNT} \| profile: {PROFILE}. Cause: {cause}"` |
|404|  `"Profile not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>   `"Profile library not found - account: {ACCOUNT} \| profile: {PROFILE}"` <br>   `"Profile (legacy) not found - account: {ACCOUNT} \| profile: {PROFILE}"` <br>      `Error in getting next extension id - {ACCOUNT} profile: {PROFILE}"`  |
|409|`"Users are currently viewing the same account: {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Conflict with profile extension: _id: {ID}, extType: {TYPE}, name: {NAME} - {ACCOUNT} \| profile: {PROFILE}"` |
|500|  `"Error processing json for extension - account: {ACCOUNT} \| profile: {PROFILE}"` |
