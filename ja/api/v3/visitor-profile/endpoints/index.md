---
title: 訪問プロファイルAPIエンドポイント
description: 訪問プロファイルAPIを使用して、訪問の記録を取得し、過去の訪問情報を取得できます。
url: https://docs.tealium.com/ja/api/v3/visitor-profile/endpoints/
---
## GET 訪問


<blockquote>
この呼び出しには、認証APIで返された地域固有のホストを使用する必要があります。詳細については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/)を参照してください。
</blockquote>


訪問記録を取得するには、以下のGETコマンドを使用します：

```bash
GET /v3/customer/visitor/accounts/{account}/profiles/{profile}?attributeId={attributeId}&attributeValue={attributeValue}&prettyName={prettyName}&responseFilters=["{attributeId}", "{attributeId}"]
```

このコマンドは以下のパラメータを使用します：

* `attributeId`
  * アカウントからの[訪問ID属性](https://docs.tealium.com/visitor-id-attribute/)を表す数値ID。
* `attributeValue`
  * 検索する値。
  * 特殊文字を含む値はURLエンコードする必要があります。
* `prettyName`
  * 属性キーがレスポンスでどのように表示されるかを示すブール値：
    * `true` – 属性は「ライフタイムオーダーバリュー」のようなユーザーフレンドリーな名前で表示されます。
    * `false` – 属性は「28471」のような数値IDで表示されます。
* `searchPriority`
    * リクエストのデータソースをJSON文字列配列として渡します。デフォルトは `["live", "historical"]` です。
        * `["live"]` – 現在の訪問に関するウェブサイトからのライブデータを取得します。
        * `["historical"]` — 30分の待機期間後に完了した訪問に関するウェブサイトからの歴史的データを取得します。
        * `["live", "historical"]` — APIはライブ訪問データを取得しようとします。ライブ訪問データが利用できない場合、APIは歴史的訪問データを取得します。
        * `["historical", "live"]` — APIは歴史的訪問データを取得しようとします。歴史的データが利用できない場合、APIはライブ訪問データを取得します。
* `responseFilters`
    * 訪問データをフィルタリングするためのIDのJSON配列。構成されていない場合、APIはすべての訪問データを返します。構成されている場合、`responseFilters`に含まれる`attributeId`値がレスポンスで返されます。
    * APIが一度に返すことができる`attributeId`値の最大数は150です。150を超える`attributeId`値を提供した場合、APIは最初の150個のIDのみを返します。
    * 例：`responseFilters=["5051", "5016"]`

### 権限要件

* サーバーサイドのリーダー、エディター、またはパブリッシャーのレガシー権限、または
* 最低限の**閲覧**訪問ルックアッププラットフォーム権限

### cURLリクエストの例

```bash
curl --location -g --request \
GET 'https://us-east-1-platform.tealiumapis.com/v3/customer/visitor/accounts/{account}/profiles/{profile}?attributeId=5013&attributeValue=liveOnly&searchPriority=["live", "historical"]&responseFilters=["5051", "5016"]' \
--header 'Authorization: Bearer {token}'
```

### レスポンスの例

レスポンスの形式については、例の訪問オブジェクトを参照してください。

### エラーメッセージ

このエンドポイントに関する潜在的なエラーメッセージは以下の通りです：

| エラーメッセージ | 説明 |
| --- | --- |
| 400 | `{"message": "属性IDまたは属性値が不足しています"}` |
| 401 | `{"message": "許可されていません"}` |
| 404 | `訪問が見つかりませんでした、空のレスポンスです。`<br>`{"message": "'searchPriority'の無効なクエリパラメータ値が検出されました。"}` |

## GET 歴史的訪問


<blockquote>
この呼び出しには、認証APIで返された地域固有のホストを使用する必要があります。詳細については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/)を参照してください。
</blockquote>


GET 歴史的訪問メソッドは、歴史的訪問のみを検索することにより、より高速なレスポンス時間を実現するために最適化されています。

歴史的訪問記録を取得するには、以下のGETコマンドを使用します：

```bash
GET '/v3/customer/visitor/historical/accounts/{account}/profiles/{profile}?attributeId={attributeId}&attributeValue={attributeValue}&prettyName={prettyName}&responseFilters=["{attributeId}", "{attributeId}"]'
```

このコマンドは以下のパラメータを使用します：

* `attributeId`
  * アカウントからの[訪問ID属性](https://docs.tealium.com/visitor-id-attribute/)を表す数値ID。
* `attributeValue`
    * 検索する値。
    * 特殊文字を含む値はURLエンコードする必要があります。
* `prettyName`
  * 属性キーがレスポンスでどのように表示されるかを示すブール値：
     * `true` – 属性は「ライフタイムオーダーバリュー」のようなユーザーフレンドリーな名前で表示されます。
     * `false` – 属性は「28471」のような数値IDで表示されます。
* `responseFilters`
    * 訪問データをフィルタリングするためのIDのJSON配列。構成されていない場合、APIはすべての訪問データを返します。構成されている場合、`responseFilters`に含まれる`attributeId`値がレスポンスで返されます。APIが一度に返すことができる`attributeId`値の最大数は150です。150を超える`attributeId`値を提供した場合、APIは最初の150個のIDのみを返します。

### 権限要件

* サーバーサイドのリーダー、エディター、またはパブリッシャーのレガシー権限、または
* 最低限の**閲覧**訪問ルックアッププラットフォーム権限

### cURLリクエストの例

```bash
curl --location -g --request \
GET 'https://us-east-1-platform.tealiumapis.com/v3/customer/visitor/historical/{account}/profiles/{profile}?attributeId=5013&attributeValue=liveOnly&responseFilters=["5051", "5016"]' \
--header 'Authorization: Bearer {token}'
```

### レスポンスの例

レスポンスの形式については、例の訪問オブジェクトを参照してください。

### エラーメッセージ

このエンドポイントに関する潜在的なエラーメッセージは以下の通りです：

| エラーメッセージ | 説明 |
| --- | --- |
| 400 | `{"message": "属性IDまたは属性値が不足しています"}` |
| 401 | `{"message": "許可されていません"}` |
| 404 |`訪問が見つかりませんでした、空のレスポンスです。` |