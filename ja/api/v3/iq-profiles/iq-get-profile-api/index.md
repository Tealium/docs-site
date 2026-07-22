---
title: iQ GETプロファイルAPI
description: iQ GETプロファイルAPIは、iQタグ管理アカウントのプロファイルを取得し、特定の構成コンポーネントとバージョン履歴を含みます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-get-profile-api/
---
## 動作方法

GETメソッドを使用してアカウントプロファイルを取得します：

```bash
GET /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}?includes={INCLUDE}&publishVersion={PUBLISH_VERSION}
```

## 認証


<blockquote>
Bearerトークンは、すべてのAPI呼び出しを認証するために使用され、APIキーは認証呼び出しでのみ使用されます。Bearerトークンに加えて、認証応答には、後続のサーバーサイドAPI呼び出しで使用する必要がある地域固有のホスト名が含まれています。
</blockquote>


APIキーからBearerトークンを生成する方法については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/)を参照してください。

## GET操作のパラメータ

このコマンドは以下のパラメータを使用します：

|パラメータ| タイプ| 必須| 説明|
|---| ---| ---| ---|
|publishVersion| 文字列| 任意| 取得するプロファイルのバージョンID。このパラメータを省略すると、最新のバージョンが取得されます。<br> バージョンIDは `YYYYMMDDhhmm` の形式です<br> 例：`"202202111806"`|
|includes| 配列| 任意| 応答に含める構成コンポーネントの配列。含める各コンポーネントに対してこのクエリ文字列パラメータを追加します。<br> 例えば、変数と拡張機能を取得するには：`&includes=variables&includes=extensions` デフォルト：なし<br> 値：`loadRules`, `tags`, `tags.templateList`, `tags.template`, `extensions`, `variables`, `events` , および `versionIDs` |


<blockquote>
プロファイルのタグテンプレートリストを取得するには、GETリクエストに `tags` と `tags.templateList` を含める必要があります。例えば、`&includes=tags&includes=tags.templateList`。<br> タグテンプレート自体を取得するには、`tags` と `tags.template` を含めます。例えば、`&includes=tags&includes=tags.template`。
</blockquote>


### cURLリクエストの例

```bash
curl -H 'Authorization: Bearer {token}' \
https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}?includes=loadRules&includes=extensions&includes=tags&includes=tags.template&includes=variables&includes=events&includes=versionIds&publishVersion=202003161355
```
### 例の応答



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
                "loadRules": [, "/ja/early-access/api/api-v3/iq-profiles/iq-get-profile-api"]
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
            , "/ja/early-access/api/api-v3/iq-profiles/iq-get-profile-api"]
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
            "configuration": [, "/ja/early-access/api/api-v3/iq-profiles/iq-get-profile-api"]
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
            "configuration": [, "/ja/early-access/api/api-v3/iq-profiles/iq-get-profile-api"]
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

### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

|エラーコード| エラーメッセージ|
|---| ---|
|400|  `"プロファイルライブラリが古くなっています。プロファイルをパッチする前に変更をマージしてください - {ACCOUNT} \| プロファイル: {PROFILE}"`<br>  `"変数の検証に失敗しました - variableId: {VARIABLE ID} \| {ACCOUNT} \| プロファイル: {PROFILE}. 原因: {cause}"` |
|404|  `"プロファイルが見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"`<br>   `"プロファイルライブラリが見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"` <br>   `"プロファイル（レガシー）が見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"` <br>      `"次の拡張IDの取得エラー - {ACCOUNT} プロファイル: {PROFILE}"`  |
|409|`"同じアカウントを現在他のユーザーが閲覧中です: {ACCOUNT} \| プロファイル: {PROFILE}"` <br>  `"プロファイル拡張との競合: _id: {ID}, extType: {TYPE}, name: {NAME} - {ACCOUNT} \| プロファイル: {PROFILE}"` |
|500|  `"拡張のためのjson処理エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"` |