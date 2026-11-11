---
title: AudienceStoreデータガイド
description: この記事では、AudienceStoreを通じて利用できる訪問レベルの属性について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/audiencestore-data-guide/
---
AudienceStoreは、顧客データプラットフォーム（CDP）から訪問レベルのデータを収集し、エクスポートするための最も効率的な方法を提供します。訪問データはフラット化されたJSONファイルに圧縮され、TealiumのAmazon S3バケットからダウンロードできるようになります。各ファイルには、オーディエンス内の各訪問レコードを表す複数のJSONオブジェクトが含まれます。

## 訪問レコードの作成、更新、削除操作

* **訪問レコードの作成**  
訪問レコードは、セッションの終了後に作成されます。レコードがDataAccessに表示されるまでには約1時間かかります。

* **訪問レコードの更新**  
訪問がサイトを再訪すると、セッション終了時に訪問レコードが更新されます。訪問レコードに対して[訪問のスティッチング]()が開始されると、既存のプロファイルが一時的に削除され、スティッチングされたプロファイルが再挿入されます。

* **訪問レコードの削除**  
訪問レコードは、契約で指定された保持期間に基づいて削除されます。保持期間内に更新されなかった訪問レコードは削除され、復元できません。たとえば、保持期間が30日間の場合、過去30日間に更新されなかったすべての訪問レコードが削除されます。

## AudienceStoreに送信されるデータ

訪問データをAudienceStoreに送信するAudienceStoreコネクタには、訪問レコードデータの送信に使用する**訪問データを送信**アクションがあります。このアクションで**現在の訪問データを含める**オプションを選択した場合、`current_visit`オブジェクトの`events`配列には、CDPでも定義されているイベント属性（属性またはエンリッチメントとして定義されたもの）のみが含まれます。

以下のイベントデータ属性は、常に`events`配列に含まれます。

```
_dc_ttl_
_dctrace
account
consent_*
cp.CONSENTMGR
enrichmentOnly
env
event_id
new_visitor
page_url
post_time
profile
profile_revision
selector
tags
tealium_*
trace_id
type
useragent
visitor_id
```

## 訪問レコードの形式

訪問レコード（プロファイル）は、以下のフィールドを含むJSONオブジェクトとして保存されます。

|オブジェクト名|型|説明|
|---|---|---|
| メインオブジェクト | オブジェクト | 各属性データ型のサブオブジェクトを含む訪問オブジェクト：<ul><li>スティッチングされた訪問ID：`replaces : [ ]`</li><li>数値／数値の配列：`"metrics" : { }, "metric_lists" : { }`</li><li>文字列／文字列の配列／文字列のセット：`"properties" : { }, "property_lists" : { }, "property_sets" : { }`</li><li>ブール値／ブール値の配列：`"flags" : { }, "flag_lists" : { }`</li><li>日付：`"dates" : { }`</li><li>バッジ：`"badges" : { }`</li><li>集計：`"metric_sets" : { }`</li><li>タイムライン：`"sequences" : { }`</li><li>ファネル：`"funnels" : { }`</li></ul> |
| `current_visit` | オブジェクト | <ul><li>最後のイベント `last_event: { }`</li><li>イベント `events: [ {}, {}, ...]`</li></ul> |
## JSON ファイルテンプレート

```json
// Visitor Record
{
    // Number attributes (Visitor Scope)
    "metrics": {
        "ATTRIBUTE_NAME": NUMERIC_VALUE,
        ...
    },

    // Date attributes (Visitor Scope)
    "dates": {
        "ATTRIBUTE_NAME": UNIX_TIMESTAMP,
        "audience_ACCOUNT_PROFILE_ID_count_ts": UNIX_TIMESTAMP,
        ...
    },

    // String attributes (Visitor Scope)
    "properties": {
        "ATTRIBUTE_NAME": "STRING_VALUE",
        ...
    },

    // Array of Strings attributes (Visitor Scope)
    "property_lists": {
        "ATTRIBUTE_NAME": ["STRING_VALUE", ...],
        ...
    },

    // Set of Strings attributes (Visitor Scope)
    "property_sets": {
        "ATTRIBUTE_NAME": {
            "STRING_VALUE": 1,
            ...
        },
        ...
    },

    // Boolean attributes (Visitor Scope)
    "flags": {
        "ATTRIBUTE_NAME": true|false,
        ...
    },

    // Visitor Stitching
    "replaces": ["45-CHAR-ALPHANUMERIC", "__ACCOUNT_PROFILE__ATTRIBUTE_ID_VALUE__", ...],

    // Audiences
    "audiences": ["AUDIENCE_NAME", ...],

    // Badges
    "badges": ["BADGE_NAME", ...],

    "preloaded": false,

    // Array of Numbers
    "metric_lists": {
        "ATTRIBUTE_NAME": [VALUE, ...],
        ...
    },

    // Tallies (Visitor Scope)
    "metric_sets": {
        "ATTRIBUTE_NAME": {
            "ENTRY_NAME": VALUE,
            ...
        },
        ...
    },
    "creation_ts": UNIX_TIMESTAMP,
    "_id": "GUID",
    "_partition": NUMBER,
    "shard_token": NUMBER,

    // Timelines (Visitor Scope)
    "sequences": {
        "ATTRIBUTE_NAME": [
            {
                "timestamp": UNIX_TIMESTAMP,
                "snapshot": {
                    "ATTRIBUTE_NAME": "STRING_VALUE"
                }
            },
            ...
        ]
    },

    // Funnels (Visitor Scope)
    "funnels": {
        "ATTRIBUTE_NAME": {
            "completed": true|false,
            "steps": {
                "1": {
                    "timestamp": UNIX_TIMESTAMP,
                    "snapshot": {
                        "ATTRIBUTE_NAME": "STRING_VALUE"
                    }
                },
                "2": {
                    "timestamp": UNIX_TIMESTAMP
                },
                ...
            }
        }
    },

    // Current Visit Record
    "current_visit": {
        // Number attributes (Visit scope)
        "metrics": {
            "ATTRIBUTE_NAME": NUMERIC_VALUE,
            ...
        },

        // Date attributes (Visit scope)
        "dates": {
            "ATTRIBUTE_NAME": UNIX_TIMESTAMP,
            ...
            "last_event_ts": UNIX_TIMESTAMP
        },

        // String attributes (Visit scope)
        "properties": {
            "ATTRIBUTE_NAME": "STRING_VALUE",
            ...
        },

        // Boolean attributes (Visitor Scope)
        "flags": {
            "ATTRIBUTE_NAME": true|false,
            ...
        },

        // Events From Current Visit
        "events": [{
            "account": "ACCOUNT",
            "profile": "PROFILE",
            "selector": "2",
            "env": "prod",
            "tags": {
                "TAG_UID": {
                    "executed": true|false,
                    "type": VENDOR_ID,
                    "profile": "PROFILE"
                },
                ...
            }
            "data": {
                // Built-In DOM Variables
                "dom": {
                    "viewport_height": 976,
                    "referrer": "https://www.google.com/",
                    "viewport_width": 1680,
                    "domain": "example.com",
                    "title": "PAGE_TITLE",
                    "query_string": "",
                    "hash": "",
                    "url": "FULL_URL",
                    "pathname": "/"
                },

                // Universal Data Object variables
                "udo": {
                    "UDO_VARIABLE_NAME" : "VALUE",
                    ...
                    "tealium_account": "ACCOUNT",
                    "tealium_datasource": "DATA_SOURCE_KEY",
                    "tealium_environment": "prod",
                    "tealium_event": "view",
                    "tealium_firstparty_visitor_id": "45-CHAR-ALPHANUMERIC",
                    "tealium_library_name": "utag.js",
                    "tealium_library_version": "4.44.0",
                    "tealium_profile": "PROFILE"
                    "tealium_random": "MATH_RANDOM",
                    "tealium_session_id": "UNIX_TIMESTAMP",
                    "tealium_timestamp_epoch": UNIX_TIMESTAMP,
                    "tealium_timestamp_local": "YYYY-MM-DDTHH:MM:SS.mmm",
                    "tealium_timestamp_utc": "2017-10-29T23:10:24.363Z",
                    "tealium_visitor_id": "45-CHAR-ALPHANUMERIC"
                },

                // Javascript Page Variables
                "js": {
                    "VARIABLE_NAME": VALUE,
                    ...
                },

                // Cookies
                "firstparty_tealium_cookies": {
                    "utag_main_v_id": "45-CHAR-ALPHANUMERIC",
                    "COOKIE_NAME" : VALUE,
                    ...
                },

                // Meta Data Variables
                "meta": {
                    "META_TAG_NAME": VALUE,
                    ...
                }
            },
            "type": "LIVE",
            "enrichmentOnly": false,
            "event_id": "GUID",
            "visitor_id": "45-CHAR-ALPHANUMERIC",
            "post_time": UNIX_TIMESTAMP,
            "page_url": {
                "full_url": "URL",
                "scheme": "https",
                "domain": "example.com",
                "path": "/"
            },
            "referrer_url": {
                "full_url": "FULL_URL",
                "scheme": "https",
                "domain": "example.com",
                "path": "/"
            },
            "useragent": "USER_AGENT",
            "client_ip": "IP_ADDRESS",
            "_dctrace": ["COLLECTION_SERVER", ...],
            "new_visitor": true|false
        }],

        // Sets of Strings
        "property_sets": {
            "SET_NAME": ["VALUE", ...],
            ...
        },
        "creation_ts": UNIX_TIMESTAMP,
        "_id": "GUID",
        "shard_token": NUMERIC_VALUE,
        "last_event": {
            "account": "ACCOUNT",
            "profile": "PROFILE",
            "selector": "2",
            "env": "prod",
            "tags": {
                "TAG_UID": {
                    "executed": true|false,
                    "type": VENDOR_ID,
                    "profile": "PROFILE"
                },
                ...
            },
            "data": {
                // Built-In DOM Variables
                "dom": {
                    "viewport_height": 976,
                    "referrer": "https://www.google.com/",
                    "viewport_width": 1680,
                    "domain": "example.com",
                    "title": "PAGE_TITLE",
                    "query_string": "",
                    "hash": "",
                    "url": "FULL_URL",
                    "pathname": "/"
                },
                // Universal Data Object variables
                "udo": {
                    "UDO_VARIABLE_NAME" : "VALUE",
                    ...
                    "tealium_account": "ACCOUNT",
                    "tealium_datasource": "DATA_SOURCE_KEY",
                    "tealium_environment": "prod",
                    "tealium_event": "view",
                    "tealium_firstparty_visitor_id": "45-CHAR-ALPHANUMERIC",
                    "tealium_library_name": "utag.js",
                    "tealium_library_version": "4.44.0",
                    "tealium_profile": "PROFILE"
                    "tealium_random": "MATH_RANDOM",
                    "tealium_session_id": "UNIX_TIMESTAMP",
                    "tealium_timestamp_epoch": UNIX_TIMESTAMP,
                    "tealium_timestamp_local": "YYYY-MM-DDTHH:MM:SS.mmm",
                    "tealium_timestamp_utc": "2017-10-29T23:10:24.363Z",
                    "tealium_visitor_id": "45-CHAR-ALPHANUMERIC"
                },
                // Javascript Page Variables
                "js": {
                    "VARIABLE_NAME": VALUE,
                    ...
                },
                // Cookies
                "firstparty_tealium_cookies": {
                    "utag_main_v_id": "45-CHAR-ALPHANUMERIC",
                    "COOKIE_NAME" : VALUE,
                    ...
                },
                // Meta Data Variables
                "meta": {
                    "META_TAG_NAME": VALUE,
                    ...
                }
            },
            "type": "LIVE",
            "enrichmentOnly": true|false,
            "event_id": "GUID",
            "visitor_id": "45-CHAR-ALPHANUMERIC",
            "post_time": UNIX_TIMESTAMP,
            "page_url": {
                "full_url": "URL",
                "scheme": "https",
                "domain": "example.com",
                "path": "/"
            },
            "referrer_url": {
                "full_url": "FULL_URL",
                "scheme": "https",
                "domain": "example.com",
                "path": "/"
            },
            "useragent": "USER_AGENT",
            "client_ip": "IP_ADDRESS",
            "_dctrace": ["COLLECTION_SERVER", ...],
            "new_visitor": true|false
        },
        "_dc_ttl_": 1800000,
        "total_event_count": 2,
        "events_compressed": false
    },
    "_dctrace": ["COLLECTION_SERVER_ID", ...],
    "new_visitor": true|false,
    "audiences_joined_at": {
        "ACCOUNT_PROFILE_AUDIENCE_ID": {
            "$date": "YYYY-MM-DDTHH:MM:SS.mmmZ"
        },
        ...
    },
    "last_visit_id": "GUID"
},
// Additional Visitor Records
...
```