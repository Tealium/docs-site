---
title: コンテキストAPIエンドポイント
description: この記事では、コンテキストAPIエンドポイントについて説明します。
url: https://docs.tealium.com/ja/server-side/context-api/endpoint/
---
## 動作原理

コンテキストAPIエンジンは、あなたの地域、アカウント、およびプロファイルに対してユニークなエンドポイントを作成します。各エンジンは、各エンドポイントにユニークなエンジンIDを割り当てます。

訪問のデータは、エンジンを有効にして訪問がアクティブなセッションを記録し、システム内でイベントを生成した後に利用可能になります。訪問のデータをリクエストしても、彼らがまだアクティブなセッションを記録していない場合、APIはデータを返しません。

訪問のデータを取得するには、[Tealium iQ Advanced JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/)を構成して、コンテキストAPIエンドポイントにリクエストを行います。

## GETメソッド

GETメソッドを使用して、コンテキストAPIエンジンで指定したオーディエンス、バッジ、および属性データを取得します。

### Tealium匿名訪問ID

```bash
GET  https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}/visitors/{IDENTIFIER}?suppressNotFound={SUPPRESS_NOT_FOUND}
```

このコマンドは以下のパラメータを使用します：

| **パラメータ** |**タイプ**| **説明**|
|---| ---| ---|
|`identifier` |文字列<br>パスパラメータ| Tealiumの匿名訪問IDです。|
| `suppressNotFound`| ブール値<br>クエリパラメータ | 訪問が見つからない場合の応答タイプを決定します。デフォルトは `false` です。 <ul><li>`true` - HTTP 200コードと空のレスポンスボディを返します。</li><li>`false` - HTTP 404コードを返します。</li></ul>|

### 訪問ID属性

```bash
GET  https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}?attributeId={attributeId}&attributeValue={attributeValue}&suppressNotFound={SUPPRESS_NOT_FOUND}
```

このコマンドは以下のパラメータを使用します：

| **パラメータ** |**タイプ**| **説明**|
|---| ---| ---|
|`attributeId` |文字列<br>クエリパラメータ| アカウントからの[訪問ID属性](https://docs.tealium.com/visitor-id-attribute/)を表す数値UIDです。|
|`attributeValue`|文字列<br>クエリパラメータ | 検索する値です。特殊文字を含む値はURLエンコードする必要があります。 |
| `suppressNotFound`| ブール値<br>クエリパラメータ | 訪問が見つからない場合の応答タイプを決定します。デフォルトは `false` です。 <ul><li>`true` - HTTP 200コードと空のレスポンスボディを返します。</li><li>`false` - HTTP 404コードを返します。</li></ul>|

匿名ID、ユーザー識別子、および訪問ID属性についての詳細は、[Anonymous IDs, user identifiers, and visitor ID attributes](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)を参照してください。

## オブジェクト

コンテキストAPIは、エンジン構成で指定したオーディエンス、バッジ、および属性フィールドを含むJSONオブジェクトとして訪問データを返します。

次の表は、コンテキストAPIがサポートするデータタイプをまとめたものです：

* バッジ
* ブール値
* 日付
* 数値
* 文字列

PIIとしてマークされた属性はサポートされていません。

オーディエンスと訪問属性は、次のボディ例に示すように、UIDまたは名前で返されるように構成できます：

### 名前の例

次の例は、属性の名前を使用した典型的なJSONペイロードを示しています：

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

次の例は、属性のUIDを使用した典型的なJSONペイロードを示しています：

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

コンテキストAPIリクエストには次のHTTPヘッダーが必要です：

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
|403 |コンテキストAPIエンジンが有効になっていません。|
|404 |見つかりません。Tealium訪問IDにはデータベースにデータが保存されていません。|
