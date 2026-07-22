---
title: Moments API エンドポイント
description: この記事ではMoments APIのエンドポイントについて説明します。
url: https://docs.tealium.com/ja/server-side/moments-api/endpoint/
---
## 動作原理

Moments APIエンジンは、あなたの地域、アカウント、およびプロファイルに対してユニークなエンドポイントを作成します。各エンジンは各エンドポイントにユニークなエンジンIDを割り当てます。

訪問のデータは、エンジンを有効にして訪問がアクティブなセッションを記録し、システムでイベントを生成した後に利用可能になります。訪問のデータをリクエストしても、彼らがまだアクティブなセッションを記録していない場合、APIはデータを返しません。

訪問のデータを取得するには、[Tealium iQ Advanced JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/)を構成してMoments APIエンドポイントにリクエストを行います。

## GETメソッド

GETメソッドを使用して、Moments APIエンジンで指定したオーディエンス、バッジ、および属性データを取得します。

### Tealium匿名訪問ID

```bash
GET  https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}/visitors/{IDENTIFIER}?suppressNotFound={SUPPRESS_NOT_FOUND}
```

このコマンドは以下のパラメータを使用します：

| **パラメータ** |**タイプ**| **説明**|
|---| ---| ---|
|`identifier` |String<br>パスパラメータ| Tealiumの匿名訪問IDです。|
| `suppressNotFound`| Boolean<br>クエリパラメータ | 訪問が見つからない場合の応答タイプを決定します。デフォルトは `false` です。 <ul><li>`true` - HTTP 200コードと空のレスポンスボディを返します。</li><li>`false` - HTTP 404コードを返します。</li></ul>|

### 訪問ID属性

```bash
GET  https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}?attributeId={attributeId}&attributeValue={attributeValue}&suppressNotFound={SUPPRESS_NOT_FOUND}
```

このコマンドは以下のパラメータを使用します：

| **パラメータ** |**タイプ**| **説明**|
|---| ---| ---|
|`attributeId` |String<br>クエリパラメータ| アカウントからの[訪問ID属性](https://docs.tealium.com/visitor-id-attribute/)を表す数値UIDです。|
|`attributeValue`|String<br>クエリパラメータ | 検索する値です。特殊文字を含む値はURLエンコードする必要があります。 |
| `suppressNotFound`| Boolean<br>クエリパラメータ | 訪問が見つからない場合の応答タイプを決定します。デフォルトは `false` です。 <ul><li>`true` - HTTP 200コードと空のレスポンスボディを返します。</li><li>`false` - HTTP 404コードを返します。</li></ul>|

匿名IDと二次訪問IDについての詳細は、[匿名ID、ユーザー識別子、および訪問ID属性](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)を参照してください。

## オブジェクト

Moments APIは、エンジン構成で指定したオーディエンス、バッジ、および属性フィールドを含むJSONオブジェクトとして訪問データを返します。

以下の表は、Moments APIがサポートするデータタイプをまとめたものです：

* バッジ
* ブール値
* 日付
* 数値
* 文字列

PIIとしてマークされた属性はサポートされていません。

オーディエンスと訪問属性は、UIDまたは名前で返されるように構成できます。以下のボディ例で見られるように：

### 名前の例

以下の例は、属性の名前を使用した典型的なJSONペイロードを示しています：

```json
{
    "audiences": [
        "30 Days Since Last Login"
    ],
    "badges": [
        "Frequent visitor"
    ],
    "metrics": {
        "Total direct visits": 1
    },
    "properties": {
        "Company Name": "<attr_value>"
    },
    "flags": {
        "Returning visitor": false
    },
    "dates": {
        "First visit": 1491233145706
    }
}

```

### UIDの例

以下の例は、属性のUIDを使用した典型的なJSONペイロードを示しています：

```json
{
    "audiences": [
        "tealium_main_205"
    ],
    "badges": [
        "31"
    ],
    "metrics": {
        "15": 1
    },
    "properties": {
        "27330": "<attr_value>"
    },
    "flags": {
        "27": false
    },
    "dates": {
        "23": 1491233145706
    }
}
```

## ヘッダー

Moments APIリクエストには次のHTTPヘッダーが必要です：

* **Referer** - ドメイン許可リストと比較される値です。リファラーと許可リストが一致しない場合、リクエストは拒否されます。
  * 例：`https://www.example.com/`
* **Origin** - JavaScriptからAPIを呼び出す際にCORSエラーを処理するために使用される値です。
  * 例：`https://www.example.com/`

### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

|**ステータスコード**|**説明**|
|---|---|
|200 |ステータスOK。リクエストは成功しました。|
|400 |不正なリクエストです。|
|403 |Moments APIエンジンが有効になっていません。|
|404 |見つかりません。Tealium訪問IDにはデータベースに保存されているモーメントがありません。|