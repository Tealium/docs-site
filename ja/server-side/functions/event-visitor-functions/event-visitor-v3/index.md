---
title: イベントおよび訪問関数 V3
description: この記事では、V3ランタイムを使用するイベントおよび訪問関数についての情報を提供します。
url: https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/event-visitor-v3/
---
## activate() 関数

V3イベントまたは訪問関数を作成すると、関数コードエディタの**コード**タブにデフォルトコードが表示されます。このコードには `activate()` 関数とその入力パラメータが含まれています。

イベント関数には[`event object`](#event-object)と[`helper` object](#helper-object)があります。

```js
activate(async ({ event, helper }) =&gt; {
  ...
});
```

訪問関数には[`visitor` object](#visitor-object)、[`visit` object](#visit-object)、および[`helper` object](#helper-object)があります。

```js
activate(async ({ visitor, visit, helper }) =&gt; {
  ...
});
```

`helper` パラメータは `helper.getAuth()` と `helper.getGlobalVariable()` を提供し、認証の取得とグローバル変数の取得を行います。

デフォルトコードの最初の行と最後の行の間のコードを必要に応じて変更してください。

認証トークンはHTTPリクエスト内の関数からのみ参照できます。HTTPリクエストの外でトークンを参照しようとすると、トークンはUUIDプレースホルダーに置き換えられます。

## track() 関数

関数はグローバル `track()` メソッドを使用してイベントをTealium Collectに送信できます。

`track()` には2つの入力パラメータがあります：

* `data` オブジェクト：Tealium Collectに送信されるイベントデータ。
* `config` オブジェクト：（オプション）以下のフィールドを含みます：
    * `tealium_account`：アカウント名。
    * `tealium_profile`：プロファイル名。
    * `tealium_datasource`：データソースキー。
    `tealium_account`、`tealium_profile`、および`tealium_datasource`フィールドが`data`オブジェクトに含まれている場合、`config`オブジェクトは必要ありません。

各関数呼び出しは `track()` を最大6回まで呼び出すことができます。

以下の例は、`data` と `config` パラメータで `track()` を呼び出しています：

```js
track(data, {
            tealium_account: event.account,
            tealium_profile: event.profile,
            tealium_datasource: &#39;x3p4b7&#39;
        })  
        .then(response =&gt; {

        // レスポンスを処理するコードはここに記述します

        })
```

以下の例は、`data` パラメータのみで `track()` を呼び出しています：

```js
track(data)  
  .then(response =&gt; {

    // レスポンスを処理するコードはここに記述します

  })
```

`track()` 関数の詳細な例については、[Tealium Collect HTTP APIにイベントを送信する]()を参照してください。

## イベントオブジェクト

`event` データオブジェクトはイベント関数で利用可能で、イベントデータを含んでいます。

データパイプラインでイベント関数が実行される時点で、イベントデータオブジェクトの変更はシステムの他の部分には影響しません。データパイプラインに影響を与えるためにイベントデータを変更するには、イベント属性のエンリッチメントまたは[データ変換関数]()を使用してください。

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
  &#34;account&#34;: &#34;your-account&#34;,
  &#34;profile&#34;: &#34;main&#34;,
  &#34;event_id&#34;: &#34;run-test-event-id&#34;,
  &#34;visitor_id&#34;: &#34;run-test-visitor-id&#34;,
  &#34;data&#34;: {
    &#34;dom&#34;: {
      &#34;viewport_height&#34;: 766,
      &#34;referrer&#34;: &#34;&#34;,
      &#34;viewport_width&#34;: 1440,
      &#34;domain&#34;: &#34;www.example.com&#34;,
      &#34;title&#34;: &#34;Home Page&#34;,
      &#34;query_string&#34;: &#34;q=help&#34;,
      &#34;hash&#34;: &#34;&#34;,
      &#34;url&#34;: &#34;https://www.example.com/?q=help&#34;,
      &#34;pathname&#34;: &#34;/&#34;
    },
    &#34;udo&#34;: {
      &#34;tealium_event&#34;: &#34;page_view&#34;,
      &#34;ut.account&#34;: &#34;your-account&#34;,
      &#34;ut.visitor_id&#34;: &#34;0176cb4f3482110a5ba4702e147b0006d005a065104f2&#34;,
      &#34;page_name&#34;: &#34;Home Page&#34;,
      &#34;ut.event&#34;: &#34;view&#34;,
      &#34;search_keyword&#34;: &#34;help&#34;,
      &#34;ut.domain&#34;: &#34;example.com&#34;,
      &#34;tealium_profile&#34;: &#34;main&#34;,
      &#34;ut.version&#34;: &#34;ut4.46.202006020705&#34;,
      &#34;tealium_session_id&#34;: &#34;1609910608323&#34;,
      &#34;tealium_account&#34;: &#34;your-account&#34;,
      &#34;ut.profile&#34;: &#34;main&#34;
    },
    &#34;firstparty_tealium_cookies&#34;: {
      &#34;utag_main__sn&#34;: &#34;12&#34;,
      &#34;utag_main_dc_visit&#34;: &#34;12&#34;,
      &#34;utag_main_ses_id&#34;: &#34;1609910610822&#34;,
      &#34;utag_main_dc_region&#34;: &#34;us-east-1&#34;,
      &#34;utag_main__st&#34;: &#34;1609913306118&#34;,
      &#34;utag_main_v_id&#34;: &#34;0176cb4f3482110a5ba4702e147b0006d005a065104f2&#34;,
      &#34;utag_main__se&#34;: &#34;66&#34;,
      &#34;utag_main__ss&#34;: &#34;0&#34;,
      &#34;utag_main_dc_event&#34;: &#34;60&#34;,
      &#34;utag_main__pn&#34;: &#34;5&#34;
    }
  },
  &#34;env&#34;: &#34;prod&#34;,
  &#34;post_time&#34;: 1537305808000
}
```

## 訪問オブジェクト

`visitor` データオブジェクトは訪問関数で利用可能で、訪問データを含んでいます。

データパイプラインで訪問関数が実行される時点で、訪問データオブジェクトの変更はシステムの他の部分には影響しません。システムに永続する訪問データオブジェクトの変更を行うには、訪問属性のエンリッチメントを使用してください。

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
    &#34;metrics&#34;: {
        &#34;Metric 1&#34;: 1,
        &#34;Metric 2&#34;: 2
    },
    &#34;dates&#34;: {
        &#34;Date 1&#34;: 1603373790000,
        &#34;Date 2&#34;: 1603373522000
    },
    &#34;properties&#34;: {
        &#34;profile&#34;: &#34;username&#34;,
        &#34;visitor_id&#34;: &#34;017560818b67001bc185a07f1cd703078003405000b7e&#34;,
        &#34;account&#34;: &#34;user-account&#34;
    },
    &#34;metrics_sets&#34;: {
        &#34;Product Categories Purchased&#34;: {
            &#34;Shoes&#34;: 1,
            &#34;Pants&#34;: 3,
            &#34;Shirts&#34;: 7,
            &#34;Shorts&#34;: 2
        }
    },
    &#34;sequences&#34;: {
        &#34;Hotel Search Timeline&#34;: [
            {
                &#34;timestamp&#34;: 1681858801598,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Paradise Island&#34;
                }
            },
            {
                &#34;timestamp&#34;: 1681860398985,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Skokie&#34;
                }
            },
            {
                &#34;timestamp&#34;: 1681860423335,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Las Vegas&#34;
                }
            }
        ]
    },
    &#34;funnels&#34;: {
        &#34;Purchase Funnel&#34;: {
            &#34;completed&#34;: true,
            &#34;steps&#34;: {
                &#34;1&#34;: {
                    &#34;timestamp&#34;: 1636661624226,
                    &#34;snapshot&#34;: {
                        &#34;product_name&#34;: &#34;Skinny Jeans&#34;
                    }
                },
                &#34;2&#34;: {
                    &#34;timestamp&#34;: 1636661624227
                },
                &#34;3&#34;: {
                    &#34;timestamp&#34;: 1636661624228
                },
                &#34;4&#34;: {
                    &#34;timestamp&#34;: 1636661624229,
                    &#34;snapshot&#34;: {
                        &#34;order_id&#34;: &#34;0123456789&#34;,
                        &#34;order_total&#34;: &#34;34.98&#34;
                    }
                }
            }
        }
    },
    &#34;audiences&#34;: [
        &#34;Audience 1&#34;,
        &#34;Audience 2&#34;
    ],
    &#34;badges&#34;: [
        &#34;Badge 1&#34;,
        &#34;Badge 2&#34;
    ],
    &#34;creation_ts&#34;: 1603373522000,
    &#34;current_visit&#34;: {
        &#34;metrics&#34;: {
            &#34;Metric 1&#34;: 1.3,
            &#34;Metric 2&#34;: 6
        },
        &#34;dates&#34;: {
            &#34;Date 1&#34;: 1603373868000,
            &#34;Date 2&#34;: 1603373790000
        },
        &#34;properties&#34;: {
            &#34;Property 1&#34;: &#34;Chrome&#34;,
            &#34;Property 2&#34;: &#34;https://URL-for-website &#34;
        },
        &#34;flags&#34;: {
            &#34;Flag 1&#34;: true,
            &#34;Flag 2&#34;: false
        },
        &#34;property_sets&#34;: {
            &#34;Property Set 1&#34;: [
                &#34;Mac desktop&#34;
            ],
            &#34;Property Set 2&#34;: [
                &#34;Chrome&#34;
            ]
        },
        &#34;creation_ts&#34;: 1603373790000,
        &#34;total_event_count&#34;: 2,
        &#34;events_compressed&#34;: false
    },
    &#34;audiences_joined_at&#34;: {
        &#34;Audience 1&#34;: 1603363523014,
        &#34;Audience 2&#34;: 1603363523014
    }
}
```

## 訪問オブジェクト

`visit` オブジェクトは訪問関数で利用可能で、現在の訪問のデータを含んでいます。

データパイプラインで訪問関数が実行される時点で、訪問データオブジェクトへの変更はシステムの他の部分には影響しません。システムに永続する訪問データオブジェクトの変更を行うには、訪問属性のエンリッチメントを使用してください。

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
    &#34;metrics&#34;: {
        &#34;Metric 1&#34;: 1.3,
        &#34;Metric 2&#34;: 6
    },
    &#34;dates&#34;: {
        &#34;Date 1&#34;: 1603373868000,
        &#34;Date 2&#34;: 1603373790000
    },
    &#34;properties&#34;: {
        &#34;Property 1&#34;: &#34;Chrome&#34;,
        &#34;Property 2&#34;: &#34;https://URL-for-website &#34;
    },
    &#34;flags&#34;: {
        &#34;Flag 1&#34;: true,
        &#34;Flag 2&#34;: false
    },
    &#34;metrics_sets&#34;: {
        &#34;Product Categories Purchased&#34;: {
            &#34;Shoes&#34;: 1,
            &#34;Pants&#34;: 3,
            &#34;Shirts&#34;: 7,
            &#34;Shorts&#34;: 2
        }
    },
    &#34;property_sets&#34;: {
        &#34;Property Set 1&#34;: [
            &#34;Mac desktop&#34;
        ],
        &#34;Property Set 2&#34;: [
            &#34;Chrome&#34;
        ]
    },
    &#34;sequences&#34;: {
        &#34;Hotel Search Timeline&#34;: [
            {
                &#34;timestamp&#34;: 1681858801598,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Paradise Island&#34;
                }
            },
            {
                &#34;timestamp&#34;: 1681860398985,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Skokie&#34;
                }
            },
            {
                &#34;timestamp&#34;: 1681860423335,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Las Vegas&#34;
                }
            }
        ]
    },
    &#34;funnels&#34;: {
        &#34;Purchase Funnel&#34;: {
            &#34;completed&#34;: true,
            &#34;steps&#34;: {
                &#34;1&#34;: {
                    &#34;timestamp&#34;: 1636661624226,
                    &#34;snapshot&#34;: {
                        &#34;product_name&#34;: &#34;Skinny Jeans&#34;
                    }
                },
                &#34;2&#34;: {
                    &#34;timestamp&#34;: 1636661624227
                },
                &#34;3&#34;: {
                    &#34;timestamp&#34;: 1636661624228
                },
                &#34;4&#34;: {
                    &#34;timestamp&#34;: 1636661624229,
                    &#34;snapshot&#34;: {
                        &#34;order_id&#34;: &#34;0123456789&#34;,
                        &#34;order_total&#34;: &#34;34.98&#34;
                    }
                }
            }
        }
    },
    &#34;creation_ts&#34;: 1603373790000,
    &#34;total_event_count&#34;: 2,
    &#34;events_compressed&#34;: false
}
```

## ヘルパーオブジェクト

`helper` オブジェクトは、`helper.getGlobalVariable()` および `helper.getAuth()` メソッドを提供します。

### `helper.getGlobalVariable()`

関数は `helper.getGlobalVariable()` を使用してグローバル変数を取得します。

グローバル変数を取得するには、パラメータとしてキーを渡します：

```
activate(({ helper }) =&gt; {
  console.log(helper.getGlobalVariable(&#34;TEST_GLOBAL_VAR&#34;));
});
```

グローバル変数の追加および編集についての詳細は、[グローバル変数の管理]()を参照してください。

### `helper.getAuth()`

関数は `helper.getAuth()` を使用して、関数に追加された認証を取得します。

認証を取得するには、認証トークンの名前をパラメータとして渡します：

```
activate(({ helper }) =&gt; {
    console.log(helper.getAuth(&#34;auth_token_name&#34;));
})
```

関数に認証を追加する方法についての情報は、[イベントまたは訪問関数に認証を追加する]()を参照してください。

認証トークンはHTTPリクエスト内の関数によってのみ参照できます。HTTPリクエストの外でトークンを参照しようとすると、トークンはUUIDプレースホルダーに置き換えられます。