---
title: AudienceStore データガイド
description: この記事は、AudienceStoreを通じて提供される訪問レベルの属性の概要です。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/audiencestore-data-guide/
---
AudienceStoreは、AudienceStreamから訪問レベルのデータを収集し、エクスポートするための最も効率的な方法を提供します。訪問データはフラットなJSONファイルに圧縮され、TealiumのAmazon S3バケットからダウンロードできるようになります。各ファイルには、オーディエンス内の各訪問レコードを表す複数のJSONオブジェクトが含まれています。

## 訪問レコードの作成、更新、削除操作

* **訪問レコードの作成**  
訪問レコードはセッションが終了した後に作成されます。レコードがDataAccessに表示されるまでには約1時間かかります。

* **訪問レコードの更新**  
訪問がサイトを再訪した場合、セッションの終了時に訪問レコードが更新されます。訪問レコードに対して[訪問スティッチング]()が開始された場合、既存のプロファイルは一時的に削除され、ステッチされたプロファイルが再挿入されます。

* **訪問レコードの削除**  
訪問レコードは、契約で指定された保持期間に基づいて削除されます。保持期間内に更新されていない訪問レコードは削除され、回復することはできません。例えば、保持期間が30日の場合、過去30日間に更新されていないすべての訪問レコードが削除されます。

## AudienceStoreへ送信されるデータ
                                 
AudienceStoreコネクタは訪問データをAudienceStoreに送信するために**訪問データの送信**アクションを使用します。このアクションで**現在の訪問データを含む**オプションが選択されている場合、`current_visit`オブジェクトの`events`配列には、AudienceStreamで定義されているイベント属性のみが含まれます（属性またはエンリッチメントとして定義されています）。

以下のイベントデータ属性は常に`events`配列に含まれます：

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

訪問レコード（プロファイル）は、以下のフィールドを含むJSONオブジェクトとして保存されます：

|オブジェクト名| タイプ| 説明|
|---| ---| ---|
| メインオブジェクト | object|  各属性データタイプのサブオブジェクトを持つ訪問オブジェクト：<ul><li>ステッチされた訪問ID: `replaces : [ ]`</li><li>数字/数字の配列: `"metrics" : { }, "metric_lists" : { }`</li><li>文字列/文字列の配列/文字列のセット: `"properties" : { }, "property_lists" : { }, "property_sets" : { }`</li><li>ブール値/ブール値の配列: `"flags" : { }, "flag_lists" : { }`</li><li>日付: `"dates" : { }`</li><li>バッジ: `"badges" : { }`</li><li>集計: `"metric_sets" : { }`</li><li>タイムライン: `"sequences" : { }`</li><li>ファネル: `"funnels" : { }`</li></ul> |
| `current_visit` | オブジェクト|  <ul><li>最後のイベント `last_event: { }`</li><li>イベント `events: [ {}, {}, ...]`</li></ul> |
## JSONファイルテンプレート

```json
// 訪問記録
{
    // 数値属性（訪問スコープ）
    "metrics": {
        "ATTRIBUTE_NAME": NUMERIC_VALUE,
        ...
    },

    // 日付属性（訪問スコープ）
    "dates": {
        "ATTRIBUTE_NAME": UNIX_TIMESTAMP,
        "audience_ACCOUNT_PROFILE_ID_count_ts": UNIX_TIMESTAMP,
        ...
    },

    // 文字列属性（訪問スコープ）
    "properties": {
        "ATTRIBUTE_NAME": "STRING_VALUE",
        ...
    },

    // 文字列の配列属性（訪問スコープ）
    "property_lists": {
        "ATTRIBUTE_NAME": ["STRING_VALUE", ...],
        ...
    },

    // 文字列のセット属性（訪問スコープ）
    "property_sets": {
        "ATTRIBUTE_NAME": {
            "STRING_VALUE": 1,
            ...
        },
        ...
    },

    // ブール属性（訪問スコープ）
    "flags": {
        "ATTRIBUTE_NAME": true|false,
        ...
    },

    // 訪問スティッチング
    "replaces": ["45-CHAR-ALPHANUMERIC", "__ACCOUNT_PROFILE__ATTRIBUTE_ID_VALUE__", ...],

    // オーディエンス
    "audiences": ["AUDIENCE_NAME", ...],

    // バッジ
    "badges": ["BADGE_NAME", ...],

    "preloaded": false,

    // 数値の配列
    "metric_lists": {
        "ATTRIBUTE_NAME": [VALUE, ...],
        ...
    },

    // 集計（訪問スコープ）
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

    // タイムライン（訪問スコープ）
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

    // ファネル（訪問スコープ）
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

    // 現在の訪問記録
    "current_visit": {
        // 数値属性（訪問スコープ）
        "metrics": {
            "ATTRIBUTE_NAME": NUMERIC_VALUE,
            ...
        },

        // 日付属性（訪問スコープ）
        "dates": {
            "ATTRIBUTE_NAME": UNIX_TIMESTAMP,
            ...
            "last_event_ts": UNIX_TIMESTAMP
        },

        // 文字列属性（訪問スコープ）
        "properties": {
            "ATTRIBUTE_NAME": "STRING_VALUE",
            ...
        },

        // ブール属性（訪問スコープ）
        "flags": {
            "ATTRIBUTE_NAME": true|false,
            ...
        },

        // 現在の訪問からのイベント
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
                // 組み込みDOM変数
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

                // ユニバーサルデータオブジェクト変数
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

                // JavaScriptページ変数
                "js": {
                    "VARIABLE_NAME": VALUE,
                    ...
                },

                // クッキー
                "firstparty_tealium_cookies": {
                    "utag_main_v_id": "45-CHAR-ALPHANUMERIC",
                    "COOKIE_NAME" : VALUE,
                    ...
                },

                // メタデータ変数
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

        // 文字列のセット
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
                // 組み込みDOM変数
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
                // ユニバーサルデータオブジェクト変数
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

                // JavaScriptページ変数
                "js": {
                    "VARIABLE_NAME": VALUE,
                    ...
                },

                // クッキー
                "firstparty_tealium_cookies": {
                    "utag_main_v_id": "45-CHAR-ALPHANUMERIC",
                    "COOKIE_NAME" : VALUE,
                    ...
                },

                // メタデータ変数
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

```
                    "tealium_visitor_id": "45-CHAR-ALPHANUMERIC"
                },
                // Javascriptページ変数
                "js": {
                    "VARIABLE_NAME": VALUE,
                    ...
                },
                // クッキー
                "firstparty_tealium_cookies": {
                    "utag_main_v_id": "45-CHAR-ALPHANUMERIC",
                    "COOKIE_NAME" : VALUE,
                    ...
                },
                // メタデータ変数
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
// 追加の訪問記録
...
```