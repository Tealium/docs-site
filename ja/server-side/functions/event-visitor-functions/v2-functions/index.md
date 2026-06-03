---
title: イベントおよび訪問機能 V2
description: この記事では、V2 ランタイムを使用するイベントおよび訪問機能についての情報を提供します。
url: https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/v2-functions/
---
Action V2 ランタイムは廃止され、サポートされなくなりました。V2 ランタイムを使用する機能は引き続き実行されますが、コードの変更を保存することはできません。コードの変更を保存するには、ランタイムバージョンを更新する必要があり、これには機能コードの変更が必要になる場合があります。必要なコードの変更については、[V2 機能を V3 ランタイムに移行する]()を参照してください。

新しい機能はデフォルトで V3 ランタイムを使用します。詳細については、[イベントおよび訪問機能 V3]()を参照してください。

## 名前付きエクスポート

Tealium モジュールは、イベントおよび訪問機能用に5つの名前付きエクスポートをエクスポートします: `auth`, `event`, `visitor`, `store`, `tealium`。機能は次のようにこれらの名前付きエクスポートをインポートします:

```js
import { auth, visitor, event, store, tealium } from &#34;tealium&#34;; 
```

## 認証オブジェクト: auth.get()

イベントおよび訪問機能は、Facebook や Google などの一部のサービスプロバイダーにアクセスするために認証が必要です。詳細については、[機能に認証を追加する]()を参照してください。認証を追加すると、アクセストークンが返されます。

アクセストークンは `auth.get()` メソッドに渡され、HTTPリクエストで使用できる認証のIDが返されます。

| **パラメータ** | **データ型** | **説明** |
| --- | --- | --- |
| authName | string | 機能に認証が追加されたときに入力された認証の名前を指定します。 |

## イベントオブジェクト

イベント機能はイベントを変更することはできません。これらの機能はTealiumがイベントを処理した後に呼び出されます。イベントを変更するには、イベント属性のエンリッチメントまたはイベント変換機能を使用するか、Tealiumに送信される前にデータソースでイベントを変更します。

`event` オブジェクトは、イベントフィードによって機能がトリガーされたときに利用可能で、イベントデータを含んでいます。

| **プロパティ** | **データ型** | **説明** |
| --- | --- | --- |
| `event.id` | string | Tealium イベント ID。 |
| `event.visitor_id` | string | Tealium 訪問 ID。 |
| `event.account` | string | Tealium アカウント。 |
| `event.profile` | string | Tealium プロファイル。 |
| `event.data` | object | イベント属性データを含むオブジェクト。例えば `event.data.udo.page_category` や `event.data.udo.order_id` など。 |
| `function getAttributeNameById(id)` | string | 指定された属性の名前を含む文字列を返します。`id` は属性 ID を指定する文字列です。 |
| `function getAttributeValueById(id)` | any | 指定された属性の値を返します。`id` は属性 ID を指定する文字列です。 |

### イベントオブジェクトの例

以下はイベントオブジェクトデータの例です:

```
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
      &#34;ut.profile&#34;: &#34;main&#34;,
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

イベントデータは次のように機能内でアクセスできます:

```
const data = {};
    // DOM 変数は event.dom に格納されます
    data.current_url = event?.dom?.url;
    // 標準 UDO イベント変数は event.data.udo に格納されます
    data.session_id = event?.data?.udo?.tealium_session_id;
    // 第一者 Tealium クッキーは event.firstparty_tealium_cookies に格納されます
    data.trace_id = event?.firstparty_tealium_cookies?.trace_id;
    // メタ変数は event.meta に格納されます
    data.meta_description = event?.meta?.description;
    data.tealium_event = event?.data?.udo?.tealium_event;
    data.tealium_account = event?.data?.udo?.tealium_account;
    data.tealium_profile = event?.data?.udo?.tealium_profile;
```

## ストアオブジェクト: store.get()

`store` オブジェクトはキーと値のペアを格納するために使用され、これらのグローバル変数は複数の機能とデータを共有するために使用することができます。キーは変数の名前です。値は数値または文字列定数です。グローバル変数を追加、編集、削除することができます。機能はグローバル変数の値を取得することができますが、変更することはできません。

V2 機能は、キーをパラメータとして渡すことによって `store.get()` メソッドを呼び出すことでキーの値を取得することができます。

| **パラメータ** | **データ型** | **説明** |
| --- | --- | --- |
| globalParameterKey | string | 取得するグローバル変数のキーを指定します。 |

グローバル変数の追加、編集、使用に関する詳細については、[グローバル変数の管理]()を参照してください。

## Tealium オブジェクト: sendCollectEvent()

`sendCollectEvent()` メソッドはイベントを Tealium Collect HTTP API に送信し、文字列を返します。

| **パラメータ** | **データ型** | **説明** |
| --- | --- | --- |
| event | EventsClientEventObject | Tealium Collect HTTP API に送信するイベントオブジェクト。 |
| account | string | (オプション) 指定された場合、event.tealium_account の値を置き換えます。 |
| profile | string | (オプション) 指定された場合、event.tealium_profile の値を置き換えます。 |
| dataSourceId | string | (オプション) 指定された場合、event.tealium_datasource の値を置き換えます。 |

Tealium Collect HTTP API の `Response` インターフェースは、リクエストへの応答を表します。`Response` モデルは `fetch` API と同じですが、collect クライアントからの結果には URL が含まれていません。
## 訪問オブジェクト

訪問関数は訪問プロファイルを変更することはできません。これらの関数はTealiumが訪問プロファイルを処理した後に呼び出されるためです。訪問プロファイルを変更するには、訪問または訪問属性のエンリッチメントを使用してください。

関数がオーディエンスフィードによってトリガーされたときに利用可能な`visitor`オブジェクトは、訪問データを含んでいます。

| **プロパティ** | **データタイプ** | **説明** |
| --- | --- | --- |
| `visitor.metrics` | Record&amp;lt;string, number&amp;gt; | 訪問のメトリクス。 |
| `visitor.metrics_sets` | Tally&amp;lt;string, number&amp;gt; |     |
| `visitor.dates` | Record&amp;lt;string, number&amp;gt; | 訪問の日付。 |
| `visitor.audiences_joined_at` | Record&amp;lt;string, number&amp;gt; | 訪問がオーディエンスに参加したタイムスタンプ。 |
| `visitor.properties` | Record&amp;lt;string, any&amp;gt; | 訪問のプロパティ。 |
| `visitor.properties.account` | string | Tealiumアカウント。 |
| `visitor.properties.profile` | string | Tealiumプロファイル。 |
| `visitor.properties.visitor_id` | string | Tealium訪問ID。 |
| `visitor.property_sets` | Set&amp;lt;string, any&amp;gt; |     |
| `visitor.audiences` | string\[\] | 参加したオーディエンスのリスト。 |
| `visitor.badges` | string\[\] | バッジのリスト。 |
| `visitor.creation_ts` | number | 訪問の作成タイムスタンプ。 |
| `visitor.flags` | Map&amp;lt;string, Boolean&amp;gt; |     |
| `visitor.current_visit` | Record&amp;lt;string, any&amp;gt; | 現在の訪問オブジェクト。 |
| `visitor.current_visit.metrics` | Record&amp;lt;string, number&amp;gt; | 現在の訪問のメトリクス。 |
| `visitor.current_visit.metrics_sets` | Tally&amp;lt;string, number&amp;gt; |     |
| `visitor.current_visit.dates` | Record&amp;lt;string, number&amp;gt; | 現在の訪問の日付。 |
| `visitor.current_visit.properties` | Record&amp;lt;string, any&amp;gt; | 現在の訪問のプロパティ。 |
| `visitor.current_visit.flags` | Map&amp;lt;string, Boolean&amp;gt; | 現在の訪問のフラグ。 |
| `visitor.current_visit.property_sets` | Set&amp;lt;string, any&amp;gt; | 現在の訪問のプロパティセット。 |
| `visitor.current_visit.creation_ts` | number | 現在の訪問の作成タイムスタンプ。 |
| `visitor.current_visit.total_event_count` | number | 現在の訪問のイベント総数。 |
| `visitor.current_visit.events_compressed` | boolean | 現在の訪問のイベントが圧縮されているか。 |
| `function getAttributeNameById(id)` | string | 指定された属性の名前を含む文字列を返します。`id`は属性IDを指定する文字列です。 |
| `function getAttributeValueById(id)` | any | 指定された属性の値を返します。`id`は属性IDを指定する文字列です。 |

### 訪問オブジェクトの例

以下は訪問オブジェクトデータの例です：

```
{
  &#34;metrics&#34;: {
    &#34;Metric 1&#34;: 1,
    &#34;Metric 2&#34;: 2
  },
  &#34;dates&#34;: {
    &#34;Date 1&#34;: 1603373790000,
    &#34;Date 2&#34;: 1603373522000,
  },
  &#34;properties&#34;: {
    &#34;profile&#34;: &#34;username&#34;,
    &#34;visitor_id&#34;: &#34;017560818b67001bc185a07f1cd703078003405000b7e&#34;,
    &#34;account&#34;: &#34;user-account&#34;,
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
      &#34;Metric 2&#34;: 6,
    },
    &#34;dates&#34;: {
      &#34;Date 1&#34;: 1603373868000,
      &#34;Date 2&#34;: 1603373790000,
    },
    &#34;properties&#34;: {
      &#34;Property 1&#34;: &#34;Chrome&#34;,
      &#34;Property 2&#34;: &#34;https://URL-for-website &#34;,
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