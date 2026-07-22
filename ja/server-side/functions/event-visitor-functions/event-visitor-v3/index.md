---
title: イベントおよび訪問関数 V3
description: この記事では、V3ランタイムを使用するイベントおよび訪問関数についての情報を提供します。
url: https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/event-visitor-v3/
---
## activate() 関数

V3イベントまたは訪問関数を作成すると、関数コードエディタの**コード**タブにデフォルトコードが表示されます。このコードには `activate()` 関数とその入力パラメータが含まれています。

イベント関数には[`event object`](#event-object)と[`helper` object](#helper-object)があります。

```js
activate(async ({ event, helper }) => {
  ...
});
```

訪問関数には[`visitor` object](#visitor-object)、[`visit` object](#visit-object)、および[`helper` object](#helper-object)があります。

```js
activate(async ({ visitor, visit, helper }) => {
  ...
});
```

`helper` パラメータは `helper.getAuth()` と `helper.getGlobalVariable()` を提供し、認証の取得とグローバル変数の取得を行います。

デフォルトコードの最初の行と最後の行の間のコードを必要に応じて変更してください。


<blockquote>
認証トークンはHTTPリクエスト内の関数からのみ参照できます。HTTPリクエストの外でトークンを参照しようとすると、トークンはUUIDプレースホルダーに置き換えられます。
</blockquote>


## track() 関数

関数はグローバル `track()` メソッドを使用してイベントをTealium Collectに送信できます。

`track()` には2つの入力パラメータがあります：

* `data` オブジェクト：Tealium Collectに送信されるイベントデータ。
* `config` オブジェクト：（オプション）以下のフィールドを含みます：
    * `tealium_account`：アカウント名。
    * `tealium_profile`：プロファイル名。
    * `tealium_datasource`：データソースキー。
    `tealium_account`、`tealium_profile`、および`tealium_datasource`フィールドが`data`オブジェクトに含まれている場合、`config`オブジェクトは必要ありません。


<blockquote>
各関数呼び出しは `track()` を最大6回まで呼び出すことができます。
</blockquote>


以下の例は、`data` と `config` パラメータで `track()` を呼び出しています：

```js
track(data, {
            tealium_account: event.account,
            tealium_profile: event.profile,
            tealium_datasource: 'x3p4b7'
        })  
        .then(response => {

        // レスポンスを処理するコードはここに記述します

        })
```

以下の例は、`data` パラメータのみで `track()` を呼び出しています：

```js
track(data)  
  .then(response => {

    // レスポンスを処理するコードはここに記述します

  })
```

`track()` 関数の詳細な例については、[Tealium Collect HTTP APIにイベントを送信する](https://docs.tealium.com/v3-event-visitor-function-examples/#send-an-event-to-the-tealium-collect-http-api)を参照してください。

## イベントオブジェクト

`event` データオブジェクトはイベント関数で利用可能で、イベントデータを含んでいます。


<blockquote>
データパイプラインでイベント関数が実行される時点で、イベントデータオブジェクトの変更はシステムの他の部分には影響しません。データパイプラインに影響を与えるためにイベントデータを変更するには、イベント属性のエンリッチメントまたは[データ変換関数](https://docs.tealium.com/about-data-transformation-functions/)を使用してください。
</blockquote>


| プロパティ | データタイプ | 説明 |
| --- | --- | --- |
| `account` | string | Tealiumアカウント。 |
| `data` | object | データレイヤーで、イベントデータを含みます。 |
| `env` | string | 実行環境。値は `qa`、`dev`、または `prod` です。 |
| `event_id` | string | TealiumイベントID。 |
| `post_time` | number | イベントが発生した時刻のタイムスタンプ。 |
| `profile` | string | Tealiumプロファイル。 |
| `useragent` | string | ユーザーエージェントを表す文字列、例えばブラウザです。 |
| `visitor_id` | string | Tealium訪問ID。 |
| `function getAttributeNameById(id)` | string | 指定された属性の名前を含む文字列を返します。`id`は属性IDを指定する文字列です。 |
| `function getAttributeValueById(id)` | any | 指定された属性の値を返します。`id`は属性IDを指定する文字列です。 |

`data` オブジェクトには、受信イベントのデータが含まれています。

| プロパティ | タイプ | 説明 |
| --- | --- | --- |
| `dom` | Object | 標準ページデータ。 |
| `firstparty_tealium_cookies` | Object | ブラウザのすべてのクッキー。 |
| `js` | Object | ページのJavaScript変数。 |
| `meta` | Object | ウェブページのメタタグからのデータ。 |
| `udo` | Object | 受信イベントのプロパティを含むユニバーサルデータオブジェクト。 |

### イベントオブジェクトの例

以下はイベントオブジェクトデータの例です：

```json
{
  "account": "your-account",
  "profile": "main",
  "event_id": "run-test-event-id",
  "visitor_id": "run-test-visitor-id",
  "data": {
    "dom": {
      "viewport_height": 766,
      "referrer": "",
      "viewport_width": 1440,
      "domain": "www.example.com",
      "title": "Home Page",
      "query_string": "q=help",
      "hash": "",
      "url": "https://www.example.com/?q=help",
      "pathname": "/"
    },
    "udo": {
      "tealium_event": "page_view",
      "ut.account": "your-account",
      "ut.visitor_id": "0176cb4f3482110a5ba4702e147b0006d005a065104f2",
      "page_name": "Home Page",
      "ut.event": "view",
      "search_keyword": "help",
      "ut.domain": "example.com",
      "tealium_profile": "main",
      "ut.version": "ut4.46.202006020705",
      "tealium_session_id": "1609910608323",
      "tealium_account": "your-account",
      "ut.profile": "main"
    },
    "firstparty_tealium_cookies": {
      "utag_main__sn": "12",
      "utag_main_dc_visit": "12",
      "utag_main_ses_id": "1609910610822",
      "utag_main_dc_region": "us-east-1",
      "utag_main__st": "1609913306118",
      "utag_main_v_id": "0176cb4f3482110a5ba4702e147b0006d005a065104f2",
      "utag_main__se": "66",
      "utag_main__ss": "0",
      "utag_main_dc_event": "60",
      "utag_main__pn": "5"
    }
  },
  "env": "prod",
  "post_time": 1537305808000
}
```

## 訪問オブジェクト

`visitor` データオブジェクトは訪問関数で利用可能で、訪問データを含んでいます。


<blockquote>
データパイプラインで訪問関数が実行される時点で、訪問データオブジェクトの変更はシステムの他の部分には影響しません。システムに永続する訪問データオブジェクトの変更を行うには、訪問属性のエンリッチメントを使用してください。
</blockquote>


| **プロパティ** | **データタイプ** | **説明**  |
| --- | --- | --- |
| `badges` | string[] | バッジ属性。 |
| `metrics` | object(key, number) | 数値属性。 |
| `properties` | object(key, string) | 文字列属性。 |
| `dates` | object(key, epoch) | エポック形式の日付属性。 |
| `flags` | object(key, boolean) | ブール属性。 |
| `metrics_sets` | object(key, object(key, number)) | 集計属性。 |
| `property_sets` | object(key, string[]) | 文字列のセット属性。 |
| `funnels` | object (例を参照) | ファネル属性。 |
| `sequences` | object (例を参照) | タイムライン属性。 |
| `property_lists` | object(key, string[]) | 文字列の配列属性。 |
| `metric_lists` | object(key, number[]) | 数値の配列属性。 |
| `flag_lists` | object(key, boolean[]) | ブールの配列属性。 |
| `secondary_ids` | string | ユーザー識別子、例えばメールアドレス、ソーシャルメディアID、または顧客ID。 |
| `audiences` | string[] | 訪問が現在所属しているオーディエンス。 |
| `creation_ts` | epoch | 訪問作成タイムスタンプ。 |
| `new_visitor` | boolean | これが新しい訪問であるかどうかを示します。 |
| `audiences_joined_at` | number | 訪問がオーディエンスに参加したタイムスタンプ。 |
| `current_visit` | visit object | 現在の訪問のデータ。 |
| `function getAttributeNameById(id)` | string | 指定された属性IDの名前を含む文字列を返します。`id`は属性IDを含む文字列です。 |
| `function getAttributeValueById(id)` | any | 指定された属性IDの値を返します。`id`は属性IDを含む文字列です。
### 訪問オブジェクトの例

以下は、`visitor` オブジェクトデータの例です：

```json
{
    "metrics": {
        "Metric 1": 1,
        "Metric 2": 2
    },
    "dates": {
        "Date 1": 1603373790000,
        "Date 2": 1603373522000
    },
    "properties": {
        "profile": "username",
        "visitor_id": "017560818b67001bc185a07f1cd703078003405000b7e",
        "account": "user-account"
    },
    "metrics_sets": {
        "Product Categories Purchased": {
            "Shoes": 1,
            "Pants": 3,
            "Shirts": 7,
            "Shorts": 2
        }
    },
    "sequences": {
        "Hotel Search Timeline": [
            {
                "timestamp": 1681858801598,
                "snapshot": {
                    "Searched Hotel City": "Paradise Island"
                }
            },
            {
                "timestamp": 1681860398985,
                "snapshot": {
                    "Searched Hotel City": "Skokie"
                }
            },
            {
                "timestamp": 1681860423335,
                "snapshot": {
                    "Searched Hotel City": "Las Vegas"
                }
            }
        ]
    },
    "funnels": {
        "Purchase Funnel": {
            "completed": true,
            "steps": {
                "1": {
                    "timestamp": 1636661624226,
                    "snapshot": {
                        "product_name": "Skinny Jeans"
                    }
                },
                "2": {
                    "timestamp": 1636661624227
                },
                "3": {
                    "timestamp": 1636661624228
                },
                "4": {
                    "timestamp": 1636661624229,
                    "snapshot": {
                        "order_id": "0123456789",
                        "order_total": "34.98"
                    }
                }
            }
        }
    },
    "audiences": [
        "Audience 1",
        "Audience 2"
    ],
    "badges": [
        "Badge 1",
        "Badge 2"
    ],
    "creation_ts": 1603373522000,
    "current_visit": {
        "metrics": {
            "Metric 1": 1.3,
            "Metric 2": 6
        },
        "dates": {
            "Date 1": 1603373868000,
            "Date 2": 1603373790000
        },
        "properties": {
            "Property 1": "Chrome",
            "Property 2": "https://URL-for-website "
        },
        "flags": {
            "Flag 1": true,
            "Flag 2": false
        },
        "property_sets": {
            "Property Set 1": [
                "Mac desktop"
            ],
            "Property Set 2": [
                "Chrome"
            ]
        },
        "creation_ts": 1603373790000,
        "total_event_count": 2,
        "events_compressed": false
    },
    "audiences_joined_at": {
        "Audience 1": 1603363523014,
        "Audience 2": 1603363523014
    }
}
```

## 訪問オブジェクト

`visit` オブジェクトは訪問関数で利用可能で、現在の訪問のデータを含んでいます。


<blockquote>
データパイプラインで訪問関数が実行される時点で、訪問データオブジェクトへの変更はシステムの他の部分には影響しません。システムに永続する訪問データオブジェクトの変更を行うには、訪問属性のエンリッチメントを使用してください。
</blockquote>


| **プロパティ** | **データタイプ** | **説明** |
| --- | --- | --- |
| `metrics` | object(key, number) | 数値属性。 |
| `properties` | object(key, string) | 文字列属性。 |
| `dates` | object(key, epoch) | エポック形式の日付属性。 |
| `flags` | object(key, boolean) | ブール属性。 |
| `metrics_sets` | object(key, object(key, number)) | 集計属性。 |
| `property_sets` | object(key, string[]) | 文字列のセット属性。 |
| `funnels` | object (例を参照) | ファネル属性。 |
| `sequences` | object (例を参照) | タイムライン属性。 |
| `property_lists` | object(key, string[]) | 文字列の配列属性。 |
| `metric_lists` | object(key, number[]) | 数値の配列属性。 |
| `flag_lists` | object(key, boolean[]) | ブールの配列属性。 |
| `events_compressed` | boolean | イベントが圧縮されているかどうかを示します。 |
| `total_event_count` | number | イベントの総数。 |
| `creation_ts` | number | 訪問作成タイムスタンプ。 |
| `function getAttributeNameById(id)` | string | 指定された属性IDの名前を含む文字列を返します。`id`は属性IDを含む文字列です。 |
| `function getAttributeValueById(id)` | any | 指定された属性IDの値を返します。`id`は属性IDを含む文字列です。 |

### 訪問オブジェクトの例

以下は、`visit` オブジェクトデータの例です：

```json
{
    "metrics": {
        "Metric 1": 1.3,
        "Metric 2": 6
    },
    "dates": {
        "Date 1": 1603373868000,
        "Date 2": 1603373790000
    },
    "properties": {
        "Property 1": "Chrome",
        "Property 2": "https://URL-for-website "
    },
    "flags": {
        "Flag 1": true,
        "Flag 2": false
    },
    "metrics_sets": {
        "Product Categories Purchased": {
            "Shoes": 1,
            "Pants": 3,
            "Shirts": 7,
            "Shorts": 2
        }
    },
    "property_sets": {
        "Property Set 1": [
            "Mac desktop"
        ],
        "Property Set 2": [
            "Chrome"
        ]
    },
    "sequences": {
        "Hotel Search Timeline": [
            {
                "timestamp": 1681858801598,
                "snapshot": {
                    "Searched Hotel City": "Paradise Island"
                }
            },
            {
                "timestamp": 1681860398985,
                "snapshot": {
                    "Searched Hotel City": "Skokie"
                }
            },
            {
                "timestamp": 1681860423335,
                "snapshot": {
                    "Searched Hotel City": "Las Vegas"
                }
            }
        ]
    },
    "funnels": {
        "Purchase Funnel": {
            "completed": true,
            "steps": {
                "1": {
                    "timestamp": 1636661624226,
                    "snapshot": {
                        "product_name": "Skinny Jeans"
                    }
                },
                "2": {
                    "timestamp": 1636661624227
                },
                "3": {
                    "timestamp": 1636661624228
                },
                "4": {
                    "timestamp": 1636661624229,
                    "snapshot": {
                        "order_id": "0123456789",
                        "order_total": "34.98"
                    }
                }
            }
        }
    },
    "creation_ts": 1603373790000,
    "total_event_count": 2,
    "events_compressed": false
}
```

## ヘルパーオブジェクト

`helper` オブジェクトは、`helper.getGlobalVariable()` および `helper.getAuth()` メソッドを提供します。

### `helper.getGlobalVariable()`

関数は `helper.getGlobalVariable()` を使用してグローバル変数を取得します。

グローバル変数を取得するには、パラメータとしてキーを渡します：

```
activate(({ helper }) => {
  console.log(helper.getGlobalVariable("TEST_GLOBAL_VAR"));
});
```

グローバル変数の追加および編集についての詳細は、[グローバル変数の管理]()を参照してください。

### `helper.getAuth()`

関数は `helper.getAuth()` を使用して、関数に追加された認証を取得します。

認証を取得するには、認証トークンの名前をパラメータとして渡します：

```
activate(({ helper }) => {
    console.log(helper.getAuth("auth_token_name"));
})
```

関数に認証を追加する方法についての情報は、[イベントまたは訪問関数に認証を追加する]()を参照してください。


<blockquote>
認証トークンはHTTPリクエスト内の関数によってのみ参照できます。HTTPリクエストの外でトークンを参照しようとすると、トークンはUUIDプレースホルダーに置き換えられます。
</blockquote>
