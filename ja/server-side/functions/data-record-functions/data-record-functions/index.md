---
title: データレコード機能について
description: この記事では、CloudStreamのデータレコード機能の概要について説明します。
url: https://docs.tealium.com/ja/server-side/functions/data-record-functions/data-record-functions/
---

<blockquote>
CloudStream機能を有効にするには、**管理メニュー** > **サーバーサイド構成** > **CloudStreamコネクタ**に移動し、**CloudStreamコネクタを有効にする**を`On`に構成し、**保存**をクリックします。
</blockquote>


## 動作原理

CloudStreamの機能はCloudStreamデータパイプライン内で実行され、クラウドデータソースから照会されたデータレコードにアクセスできます。CloudStreamプロファイル内の機能を使用して、他のシステムからデータを取得したり、データを増強したり、データを他のエンドポイントに送信したりします。

CloudStream機能の追加と管理は、他の機能の管理と同じですが、以下の例外があります：

* カスタムアクション機能を作成する場合、対象者やイベントを選択する代わりに、[クラウドデータソース](https://docs.tealium.com/about-cloud-data-sources/)と[セグメント](https://docs.tealium.com/manage-cloudstream-segments/)を選択します。
* 各CloudStream機能は1つのデータソースからのデータのみを使用できます。追加のデータソースからデータをアクティブにする場合は、それぞれに対して別の機能を構成します。
* セグメントに複数のデータソースからマッピングされた属性が含まれている場合、選択したデータソースの属性のみが機能で利用可能です。

## トリガー

データレコード機能は、データレコードが処理される前後に実行されます。

### 変換

変換機能は、データレコードが処理される前に実行されます。以下のデータパイプライン図に示されています：

![](https://docs.tealium.com/images/server-side/transformations-data-record-pipeline.png)

このパイプラインの時点で機能を使用して、処理される前に[データレコードオブジェクト](#data-record-object)とその値を変換します。

詳細については、[about-data-transformation-functions](https://docs.tealium.com/about-data-transformation-functions/)を参照してください。

### カスタムアクション

カスタムアクション機能は、データレコードが処理された後に実行されます。以下のデータパイプライン図に示されています：

![](https://docs.tealium.com/images/server-side/functions-data-record-pipeline.png)

このパイプラインの時点で機能を使用して、データレコードを他のシステムに送信します。


<blockquote>
このデータパイプラインの時点での`dataRecord`オブジェクトの変更は、システムの他の部分には影響しません。
</blockquote>


## ランタイムバージョン

データレコード変換機能のランタイムバージョンはイベントデータと同じですが、以下の変更が含まれます：

* `crypto-es`ライブラリが削除され、[`tealium/crypto`](https://docs.tealium.com/function-modules/#crypto)に置き換えられます。

カスタムアクションのランタイムバージョンは[イベントおよび訪問機能V3](https://docs.tealium.com/event-visitor-functions-v3/)と同じですが、以下の変更が含まれます：

* `track`ライブラリが削除されました。
* データレコードは新しいイベントとしてTealiumに送り返すことはできません。

## transform()関数

変換データレコード機能を作成する場合、トリガールールの条件として`$.dataSourceId`フィールドを使用する必要があります。この条件を使用して、クラウドデータソースからデータソースキーを参照します。

例：

[
  [
    {
      "input": "$.dataSourceId",
      "operator": "equals",
      "filter": "aq68ur"
    }
  ]
]


クラウドデータソースを選択し、トリガールールを構成した後、関数コードエディタの**コード**タブに次のデフォルトコードが表示されます：

```js
import flatten from "tealium/util/flatten/v2";

// "transform"関数を使用してデータレコードにアクセスし、変更を適用します
transform((dataRecord) => {
    // 元のレコードの変更を通じて変更が適用されます
    console.log(JSON.stringify(flatten(dataRecord), null, 2));
})
```

## activate()関数

カスタムアクションデータレコード機能を作成する場合、デフォルトのコードが関数コードエディタの**コード**タブに表示されます：

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_function_details.png)

このコードには`activate()`関数とその入力パラメータが含まれています。

```js
activate(async ({ dataRecord, helper }) => {
  ...
});
```

データレコード機能には[`dataRecordオブジェクト`](#data-record-object)と`helper`オブジェクトがあります。

`helper`パラメータは`helper.getAuth()`と`helper.getGlobalVariable()`を提供して、認証を取得し、グローバル変数を取得します。詳細については、を参照してください。


<blockquote>
認証トークンはHTTPリクエスト内の関数によってのみ参照できます。HTTPリクエストの外でトークンを参照しようとすると、トークンはUUIDプレースホルダーに置き換えられます。
</blockquote>


## データレコードオブジェクト


<blockquote>
Tealium Collectで使用される変換機能については、[イベントパラメータ](https://docs.tealium.com/transforms-event-parameter/)を参照してください。
</blockquote>


`dataRecord`オブジェクトはCloudStream機能とクラウドデータソースで利用可能で、次のプロパティを含んでいます：

| プロパティ | データタイプ | 説明 |
| -------- | --------- | ----------- |
| `account` | 文字列 | Tealiumアカウント名。 |
| `data` | オブジェクト | クラウドデータソースから照会されたデータレコード、`dataRecord.data.udo`で参照されます。 |
| `event_id` | 文字列 | TealiumイベントID。 |
| `post_time` | 数値 | データレコードが照会された時刻を示すタイムスタンプ。 |
| `profile` | 文字列 | Tealiumプロファイル名。 |
| `dataSourceId` | 文字列 | データソースのID。|

データレコードオブジェクトの例：

```json
{
  "account": "your-account",
  "profile": "your-profile",
  "data": {
    "udo": {
      "CDW_Column1_Timestamp": 1753077016157,
      "CDW_Column2_Id": 10,
      "CDW_Column3_EmailAddress": "user@example.com",
      "_dc_ttl_": 60000,
      "tealium_datasource": "abcdefg",
      "tealium_event": "data_ingestion"
    }
  },
  "dataSourceId": "abcdefg",
  "event_id": "cf8bd406-787b-4fe9-8b45-7782e6663708",
  "post_time": 1753774131897,
}
```

## 例

これは、データレコードからメールアドレス属性（`CDW_Column3_EmailAddress`）をハッシュ化し、その後データレコードをウェブフックに送信するTealium Cryptoライブラリを使用するデータレコード機能の例です。

```javascript
import C from "tealium/crypto";

const send = async (data) => {
        console.log("Sending: " + JSON.stringify(data, null, 2));

        return fetch("https://example.com/example-webhook/", {
        method: 'POST',
        headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
});
}

activate(async ({ dataRecord }) => {
    const data = { ...dataRecord.data.udo  };

    data.tc_email = C.SHA3(dataRecord.data.udo.CDW_Column3_EmailAddress).toString(C.enc.Hex);

try {
    await send(data);
    } catch (e) {
        console.error("Failed to send the data. " + e);
    }
});
```