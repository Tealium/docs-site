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
| メインオブジェクト | object|  各属性データタイプのサブオブジェクトを持つ訪問オブジェクト：&lt;ul&gt;&lt;li&gt;ステッチされた訪問ID: `replaces : [ ]`&lt;/li&gt;&lt;li&gt;数字/数字の配列: `&#34;metrics&#34; : { }, &#34;metric_lists&#34; : { }`&lt;/li&gt;&lt;li&gt;文字列/文字列の配列/文字列のセット: `&#34;properties&#34; : { }, &#34;property_lists&#34; : { }, &#34;property_sets&#34; : { }`&lt;/li&gt;&lt;li&gt;ブール値/ブール値の配列: `&#34;flags&#34; : { }, &#34;flag_lists&#34; : { }`&lt;/li&gt;&lt;li&gt;日付: `&#34;dates&#34; : { }`&lt;/li&gt;&lt;li&gt;バッジ: `&#34;badges&#34; : { }`&lt;/li&gt;&lt;li&gt;集計: `&#34;metric_sets&#34; : { }`&lt;/li&gt;&lt;li&gt;タイムライン: `&#34;sequences&#34; : { }`&lt;/li&gt;&lt;li&gt;ファネル: `&#34;funnels&#34; : { }`&lt;/li&gt;&lt;/ul&gt; |
| `current_visit` | オブジェクト|  &lt;ul&gt;&lt;li&gt;最後のイベント `last_event: { }`&lt;/li&gt;&lt;li&gt;イベント `events: [ {}, {}, ...]`&lt;/li&gt;&lt;/ul&gt; |
## JSONファイルテンプレート

```json
// 訪問記録
{
    // 数値属性（訪問スコープ）
    &#34;metrics&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: NUMERIC_VALUE,
        ...
    },

    // 日付属性（訪問スコープ）
    &#34;dates&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: UNIX_TIMESTAMP,
        &#34;audience_ACCOUNT_PROFILE_ID_count_ts&#34;: UNIX_TIMESTAMP,
        ...
    },

    // 文字列属性（訪問スコープ）
    &#34;properties&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: &#34;STRING_VALUE&#34;,
        ...
    },

    // 文字列の配列属性（訪問スコープ）
    &#34;property_lists&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: [&#34;STRING_VALUE&#34;, ...],
        ...
    },

    // 文字列のセット属性（訪問スコープ）
    &#34;property_sets&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: {
            &#34;STRING_VALUE&#34;: 1,
            ...
        },
        ...
    },

    // ブール属性（訪問スコープ）
    &#34;flags&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: true|false,
        ...
    },

    // 訪問スティッチング
    &#34;replaces&#34;: [&#34;45-CHAR-ALPHANUMERIC&#34;, &#34;__ACCOUNT_PROFILE__ATTRIBUTE_ID_VALUE__&#34;, ...],

    // オーディエンス
    &#34;audiences&#34;: [&#34;AUDIENCE_NAME&#34;, ...],

    // バッジ
    &#34;badges&#34;: [&#34;BADGE_NAME&#34;, ...],

    &#34;preloaded&#34;: false,

    // 数値の配列
    &#34;metric_lists&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: [VALUE, ...],
        ...
    },

    // 集計（訪問スコープ）
    &#34;metric_sets&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: {
            &#34;ENTRY_NAME&#34;: VALUE,
            ...
        },
        ...
    },
    &#34;creation_ts&#34;: UNIX_TIMESTAMP,
    &#34;_id&#34;: &#34;GUID&#34;,
    &#34;_partition&#34;: NUMBER,
    &#34;shard_token&#34;: NUMBER,

    // タイムライン（訪問スコープ）
    &#34;sequences&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: [
            {
                &#34;timestamp&#34;: UNIX_TIMESTAMP,
                &#34;snapshot&#34;: {
                    &#34;ATTRIBUTE_NAME&#34;: &#34;STRING_VALUE&#34;
                }
            },
            ...
        ]
    },

    // ファネル（訪問スコープ）
    &#34;funnels&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: {
            &#34;completed&#34;: true|false,
            &#34;steps&#34;: {
                &#34;1&#34;: {
                    &#34;timestamp&#34;: UNIX_TIMESTAMP,
                    &#34;snapshot&#34;: {
                        &#34;ATTRIBUTE_NAME&#34;: &#34;STRING_VALUE&#34;
                    }
                },
                &#34;2&#34;: {
                    &#34;timestamp&#34;: UNIX_TIMESTAMP
                },
                ...
            }
        }
    },

    // 現在の訪問記録
    &#34;current_visit&#34;: {
        // 数値属性（訪問スコープ）
        &#34;metrics&#34;: {
            &#34;ATTRIBUTE_NAME&#34;: NUMERIC_VALUE,
            ...
        },

        // 日付属性（訪問スコープ）
        &#34;dates&#34;: {
            &#34;ATTRIBUTE_NAME&#34;: UNIX_TIMESTAMP,
            ...
            &#34;last_event_ts&#34;: UNIX_TIMESTAMP
        },

        // 文字列属性（訪問スコープ）
        &#34;properties&#34;: {
            &#34;ATTRIBUTE_NAME&#34;: &#34;STRING_VALUE&#34;,
            ...
        },

        // ブール属性（訪問スコープ）
        &#34;flags&#34;: {
            &#34;ATTRIBUTE_NAME&#34;: true|false,
            ...
        },

        // 現在の訪問からのイベント
        &#34;events&#34;: [{
            &#34;account&#34;: &#34;ACCOUNT&#34;,
            &#34;profile&#34;: &#34;PROFILE&#34;,
            &#34;selector&#34;: &#34;2&#34;,
            &#34;env&#34;: &#34;prod&#34;,
            &#34;tags&#34;: {
                &#34;TAG_UID&#34;: {
                    &#34;executed&#34;: true|false,
                    &#34;type&#34;: VENDOR_ID,
                    &#34;profile&#34;: &#34;PROFILE&#34;
                },
                ...
            }
            &#34;data&#34;: {
                // 組み込みDOM変数
                &#34;dom&#34;: {
                    &#34;viewport_height&#34;: 976,
                    &#34;referrer&#34;: &#34;https://www.google.com/&#34;,
                    &#34;viewport_width&#34;: 1680,
                    &#34;domain&#34;: &#34;example.com&#34;,
                    &#34;title&#34;: &#34;PAGE_TITLE&#34;,
                    &#34;query_string&#34;: &#34;&#34;,
                    &#34;hash&#34;: &#34;&#34;,
                    &#34;url&#34;: &#34;FULL_URL&#34;,
                    &#34;pathname&#34;: &#34;/&#34;
                },

                // ユニバーサルデータオブジェクト変数
                &#34;udo&#34;: {
                    &#34;UDO_VARIABLE_NAME&#34; : &#34;VALUE&#34;,
                    ...
                    &#34;tealium_account&#34;: &#34;ACCOUNT&#34;,
                    &#34;tealium_datasource&#34;: &#34;DATA_SOURCE_KEY&#34;,
                    &#34;tealium_environment&#34;: &#34;prod&#34;,
                    &#34;tealium_event&#34;: &#34;view&#34;,
                    &#34;tealium_firstparty_visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
                    &#34;tealium_library_name&#34;: &#34;utag.js&#34;,
                    &#34;tealium_library_version&#34;: &#34;4.44.0&#34;,
                    &#34;tealium_profile&#34;: &#34;PROFILE&#34;
                    &#34;tealium_random&#34;: &#34;MATH_RANDOM&#34;,
                    &#34;tealium_session_id&#34;: &#34;UNIX_TIMESTAMP&#34;,
                    &#34;tealium_timestamp_epoch&#34;: UNIX_TIMESTAMP,
                    &#34;tealium_timestamp_local&#34;: &#34;YYYY-MM-DDTHH:MM:SS.mmm&#34;,
                    &#34;tealium_timestamp_utc&#34;: &#34;2017-10-29T23:10:24.363Z&#34;,
                    &#34;tealium_visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;
                },

                // JavaScriptページ変数
                &#34;js&#34;: {
                    &#34;VARIABLE_NAME&#34;: VALUE,
                    ...
                },

                // クッキー
                &#34;firstparty_tealium_cookies&#34;: {
                    &#34;utag_main_v_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
                    &#34;COOKIE_NAME&#34; : VALUE,
                    ...
                },

                // メタデータ変数
                &#34;meta&#34;: {
                    &#34;META_TAG_NAME&#34;: VALUE,
                    ...
                }
            },
            &#34;type&#34;: &#34;LIVE&#34;,
            &#34;enrichmentOnly&#34;: false,
            &#34;event_id&#34;: &#34;GUID&#34;,
            &#34;visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
            &#34;post_time&#34;: UNIX_TIMESTAMP,
            &#34;page_url&#34;: {
                &#34;full_url&#34;: &#34;URL&#34;,
                &#34;scheme&#34;: &#34;https&#34;,
                &#34;domain&#34;: &#34;example.com&#34;,
                &#34;path&#34;: &#34;/&#34;
            },
            &#34;referrer_url&#34;: {
                &#34;full_url&#34;: &#34;FULL_URL&#34;,
                &#34;scheme&#34;: &#34;https&#34;,
                &#34;domain&#34;: &#34;example.com&#34;,
                &#34;path&#34;: &#34;/&#34;
            },
            &#34;useragent&#34;: &#34;USER_AGENT&#34;,
            &#34;client_ip&#34;: &#34;IP_ADDRESS&#34;,
            &#34;_dctrace&#34;: [&#34;COLLECTION_SERVER&#34;, ...],
            &#34;new_visitor&#34;: true|false
        }],

        // 文字列のセット
        &#34;property_sets&#34;: {
            &#34;SET_NAME&#34;: [&#34;VALUE&#34;, ...],
            ...
        },
        &#34;creation_ts&#34;: UNIX_TIMESTAMP,
        &#34;_id&#34;: &#34;GUID&#34;,
        &#34;shard_token&#34;: NUMERIC_VALUE,
        &#34;last_event&#34;: {
            &#34;account&#34;: &#34;ACCOUNT&#34;,
            &#34;profile&#34;: &#34;PROFILE&#34;,
            &#34;selector&#34;: &#34;2&#34;,
            &#34;env&#34;: &#34;prod&#34;,
            &#34;tags&#34;: {
                &#34;TAG_UID&#34;: {
                    &#34;executed&#34;: true|false,
                    &#34;type&#34;: VENDOR_ID,
                    &#34;profile&#34;: &#34;PROFILE&#34;
                },
                ...
            },
            &#34;data&#34;: {
                // 組み込みDOM変数
                &#34;dom&#34;: {
                    &#34;viewport_height&#34;: 976,
                    &#34;referrer&#34;: &#34;https://www.google.com/&#34;,
                    &#34;viewport_width&#34;: 1680,
                    &#34;domain&#34;: &#34;example.com&#34;,
                    &#34;title&#34;: &#34;PAGE_TITLE&#34;,
                    &#34;query_string&#34;: &#34;&#34;,
                    &#34;hash&#34;: &#34;&#34;,
                    &#34;url&#34;: &#34;FULL_URL&#34;,
                    &#34;pathname&#34;: &#34;/&#34;
                },
                // ユニバーサルデータオブジェクト変数
                &#34;udo&#34;: {
                    &#34;UDO_VARIABLE_NAME&#34; : &#34;VALUE&#34;,
                    ...
                    &#34;tealium_account&#34;: &#34;ACCOUNT&#34;,
                    &#34;tealium_datasource&#34;: &#34;DATA_SOURCE_KEY&#34;,
                    &#34;tealium_environment&#34;: &#34;prod&#34;,
                    &#34;tealium_event&#34;: &#34;view&#34;,
                    &#34;tealium_firstparty_visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
                    &#34;tealium_library_name&#34;: &#34;utag.js&#34;,
                    &#34;tealium_library_version&#34;: &#34;4.44.0&#34;,
                    &#34;tealium_profile&#34;: &#34;PROFILE&#34;
                    &#34;tealium_random&#34;: &#34;MATH_RANDOM&#34;,
                    &#34;tealium_session_id&#34;: &#34;UNIX_TIMESTAMP&#34;,
                    &#34;tealium_timestamp_epoch&#34;: UNIX_TIMESTAMP,
                    &#34;tealium_timestamp_local&#34;: &#34;YYYY-MM-DDTHH:MM:SS.mmm&#34;,
                    &#34;tealium_timestamp_utc&#34;: &#34;2017-10-29T23:10:24.363Z&#34;,
                    &#34;tealium_visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;
                },

                // JavaScriptページ変数
                &#34;js&#34;: {
                    &#34;VARIABLE_NAME&#34;: VALUE,
                    ...
                },

                // クッキー
                &#34;firstparty_tealium_cookies&#34;: {
                    &#34;utag_main_v_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
                    &#34;COOKIE_NAME&#34; : VALUE,
                    ...
                },

                // メタデータ変数
                &#34;meta&#34;: {
                    &#34;META_TAG_NAME&#34;: VALUE,
                    ...
                }
            },
            &#34;type&#34;: &#34;LIVE&#34;,
            &#34;enrichmentOnly&#34;: false,
            &#34;event_id&#34;: &#34;GUID&#34;,
            &#34;visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
            &#34;post_time&#34;: UNIX_TIMESTAMP,
            &#34;page_url&#34;: {
                &#34;full_url&#34;: &#34;URL&#34;,
                &#34;scheme&#34;: &#34;https&#34;,
                &#34;domain&#34;: &#34;example.com&#34;,
                &#34;path&#34;: &#34;/&#34;
            },
            &#34;referrer_url&#34;: {
                &#34;full_url&#34;: &#34;FULL_URL&#34;,
                &#34;scheme&#34;: &#34;https&#34;,
                &#34;domain&#34;: &#34;example.com&#34;,
                &#34;path&#34;: &#34;/&#34;
            },
            &#34;useragent&#34;: &#34;USER_AGENT&#34;,
            &#34;client_ip&#34;: &#34;IP_ADDRESS&#34;,
            &#34;_dctrace&#34;: [&#34;COLLECTION_SERVER&#34;, ...],
            &#34;new_visitor&#34;: true|false
        }],

```
                    &#34;tealium_visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;
                },
                // Javascriptページ変数
                &#34;js&#34;: {
                    &#34;VARIABLE_NAME&#34;: VALUE,
                    ...
                },
                // クッキー
                &#34;firstparty_tealium_cookies&#34;: {
                    &#34;utag_main_v_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
                    &#34;COOKIE_NAME&#34; : VALUE,
                    ...
                },
                // メタデータ変数
                &#34;meta&#34;: {
                    &#34;META_TAG_NAME&#34;: VALUE,
                    ...
                }
            },
            &#34;type&#34;: &#34;LIVE&#34;,
            &#34;enrichmentOnly&#34;: true|false,
            &#34;event_id&#34;: &#34;GUID&#34;,
            &#34;visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
            &#34;post_time&#34;: UNIX_TIMESTAMP,
            &#34;page_url&#34;: {
                &#34;full_url&#34;: &#34;URL&#34;,
                &#34;scheme&#34;: &#34;https&#34;,
                &#34;domain&#34;: &#34;example.com&#34;,
                &#34;path&#34;: &#34;/&#34;
            },
            &#34;referrer_url&#34;: {
                &#34;full_url&#34;: &#34;FULL_URL&#34;,
                &#34;scheme&#34;: &#34;https&#34;,
                &#34;domain&#34;: &#34;example.com&#34;,
                &#34;path&#34;: &#34;/&#34;
            },
            &#34;useragent&#34;: &#34;USER_AGENT&#34;,
            &#34;client_ip&#34;: &#34;IP_ADDRESS&#34;,
            &#34;_dctrace&#34;: [&#34;COLLECTION_SERVER&#34;, ...],
            &#34;new_visitor&#34;: true|false
        },
        &#34;_dc_ttl_&#34;: 1800000,
        &#34;total_event_count&#34;: 2,
        &#34;events_compressed&#34;: false
    },
    &#34;_dctrace&#34;: [&#34;COLLECTION_SERVER_ID&#34;, ...],
    &#34;new_visitor&#34;: true|false,
    &#34;audiences_joined_at&#34;: {
        &#34;ACCOUNT_PROFILE_AUDIENCE_ID&#34;: {
            &#34;$date&#34;: &#34;YYYY-MM-DDTHH:MM:SS.mmmZ&#34;
        },
        ...
    },
    &#34;last_visit_id&#34;: &#34;GUID&#34;
},
// 追加の訪問記録
...
```