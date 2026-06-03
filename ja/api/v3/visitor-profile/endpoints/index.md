---
title: 訪問プロファイルAPIエンドポイント
description: 訪問プロファイルAPIを使用して、訪問の記録を取得し、過去の訪問情報を取得できます。
url: https://docs.tealium.com/ja/api/v3/visitor-profile/endpoints/
---
## GET 訪問

この呼び出しには、認証APIで返された地域固有のホストを使用する必要があります。詳細については、[認証]()を参照してください。

訪問の記録を取得するには、以下のGETコマンドを使用します：

```bash
GET /v3/customer/visitor/accounts/{account}/profiles/{profile}?attributeId={attributeId}&amp;attributeValue={attributeValue}&amp;prettyName={prettyName}&amp;responseFilters=[&#34;{attributeId}&#34;, &#34;{attributeId}&#34;]
```

このコマンドは以下のパラメータを使用します：

* `attributeId`
  * アカウントからの[訪問ID属性]()を表す数値ID。
* `attributeValue`
  * 検索する値。
  * 特殊文字を含む値はURLエンコードする必要があります。
* `prettyName`
  * 属性キーがレスポンスでどのように表示されるかを示すブール値：
    * `true` – 属性は「Lifetime Order Value」のようなユーザーフレンドリーな名前で表示されます。
    * `false` – 属性は「28471」のような数値IDで表示されます。
* `searchPriority`
    * JSON文字列配列として渡されるリクエストのデータソース。デフォルトは `[&#34;live&#34;, &#34;historical&#34;]` です。
        * `[&#34;live&#34;]` – 現在の訪問に関するウェブサイトからのライブデータを取得します。
        * `[&#34;historical&#34;]` — 訪問が完了した後30分間の待機期間を経て、ウェブサイトからの歴史的データを取得します。
        * `[&#34;live&#34;, &#34;historical&#34;]` — APIはライブ訪問データを取得しようとします。ライブ訪問データが利用できない場合、APIは歴史的訪問データを取得します。
        * `[&#34;historical&#34;, &#34;live&#34;]` — APIは歴史的訪問データを取得しようとします。歴史的データが利用できない場合、APIはライブ訪問データを取得します。
* `responseFilters`
    * 訪問データをフィルタリングするためのIDのJSON配列。構成されていない場合、APIはすべての訪問データを返します。構成されている場合、`responseFilters`に含まれる`attributeId`の値がレスポンスに返されます。
    * APIが一度に返すことができる`attributeId`の最大数は150です。150を超える`attributeId`の値を提供した場合、APIは最初の150のIDのみを返します。
    * 例：`responseFilters=[&#34;5051&#34;, &#34;5016&#34;]`

### 例 cURLリクエスト

```bash
curl --location -g --request \
GET &#39;https://us-east-1-platform.tealiumapis.com/v3/customer/visitor/accounts/{account}/profiles/{profile}?attributeId=5013&amp;attributeValue=liveOnly&amp;searchPriority=[&#34;live&#34;, &#34;historical&#34;]&amp;responseFilters=[&#34;5051&#34;, &#34;5016&#34;]&#39; \
--header &#39;Authorization: Bearer {token}&#39;
```

### 例 レスポンス

レスポンスの形式については、訪問オブジェクトの例を参照してください。

### エラーメッセージ

このエンドポイントに関連する可能性のあるエラーメッセージは次のとおりです：

| エラーメッセージ | 説明 |
| --- | --- |
| 400 | `{&#34;message&#34;: &#34;You are missing an attribute Id or Attribute Value&#34;}` |
| 401 | `{&#34;message&#34;: &#34;Unauthorized&#34;}` |
| 404 | `訪問が見つかりませんでした、空のレスポンスです。`&lt;br&gt;`{&#34;message&#34;: &#34;Invalid query parameter value for &#39;searchPriority&#39; detected.&#34;}` |

## GET 歴史的訪問

この呼び出しには、認証APIで返された地域固有のホストを使用する必要があります。詳細については、[認証]()を参照してください。

GET 歴史的訪問メソッドは、歴史的訪問のみを検索することにより、より高速なレスポンス時間を実現するために最適化されています。

歴史的訪問の記録を取得するには、以下のGETコマンドを使用します：

```bash
GET &#39;/v3/customer/visitor/historical/accounts/{account}/profiles/{profile}?attributeId={attributeId}&amp;attributeValue={attributeValue}&amp;prettyName={prettyName}&amp;responseFilters=[&#34;{attributeId}&#34;, &#34;{attributeId}&#34;]&#39;
```

このコマンドは以下のパラメータを使用します：

* `attributeId`
  * アカウントからの[訪問ID属性]()を表す数値ID。
* `attributeValue`
    * 検索する値。
    * 特殊文字を含む値はURLエンコードする必要があります。
* `prettyName`
  * 属性キーがレスポンスでどのように表示されるかを示すブール値：
     * `true` – 属性は「Lifetime Order Value」のようなユーザーフレンドリーな名前で表示されます。
     * `false` – 属性は「28471」のような数値IDで表示されます。
* `responseFilters`
    * 訪問データをフィルタリングするためのIDのJSON配列。構成されていない場合、APIはすべての訪問データを返します。構成されている場合、`responseFilters`に含まれる`attributeId`の値がレスポンスに返されます。APIが一度に返すことができる`attributeId`の最大数は150です。150を超える`attributeId`の値を提供した場合、APIは最初の150のIDのみを返します。

### 例 cURLリクエスト

```bash
curl --location -g --request \
GET &#39;https://us-east-1-platform.tealiumapis.com/v3/customer/visitor/historical/{account}/profiles/{profile}?attributeId=5013&amp;attributeValue=liveOnly&amp;responseFilters=[&#34;5051&#34;, &#34;5016&#34;]&#39; \
--header &#39;Authorization: Bearer {token}&#39;
```

### 例 レスポンス

レスポンスの形式については、訪問オブジェクトの例を参照してください。

### エラーメッセージ

このエンドポイントに関連する可能性のあるエラーメッセージは次のとおりです：

| エラーメッセージ | 説明 |
| --- | --- |
| 400 | `{&#34;message&#34;: &#34;You are missing an attribute Id or Attribute Value&#34;}` |
| 401 | `{&#34;message&#34;: &#34;Unauthorized&#34;}` |
| 404 |`訪問が見つかりませんでした、空のレスポンスです。` |
