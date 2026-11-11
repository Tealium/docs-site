---
title: データレコード関数について
description: この記事では、Data Cloud Activation のデータレコード関数の概要について説明します。
url: https://docs.tealium.com/ja/server-side/functions/data-record-functions/data-record-functions/
---

<blockquote>
Data Cloud Activation 関数を有効にするには、**管理メニュー** > **サーバーサイド構成** > **CloudStream コネクタ**に移動し、**CloudStream コネクタを有効化**を `On` に構成して、**保存**をクリックします。
</blockquote>


## 仕組み

Data Cloud Activation の関数は、Data Cloud Activation データパイプライン内で実行され、クラウドデータソースからクエリされたデータレコードにアクセスできます。Data Cloud Activation プロファイル内で関数を使用して、他のシステムからデータを取得したり、データを拡充したり、他のエンドポイントへデータを送信したりできます。

Data Cloud Activation 関数の追加と管理は、以下の点を除き、他の関数の管理と同じです。

* カスタムアクション関数を作成するときは、オーディエンスやイベントを選択する代わりに、[クラウドデータソース](https://docs.tealium.com/about-cloud-data-sources/)と[セグメント](https://docs.tealium.com/manage-data-cloud-activation-segments/)を選択します。
* 各 Data Cloud Activation 関数では、1 つのデータソースのデータのみを使用できます。追加のデータソースからデータをアクティベートする場合は、データソースごとに個別の関数を構成します。
* セグメントに複数のデータソースからマッピングされた属性が含まれている場合、関数で使用できるのは選択したデータソースの属性のみです。

## トリガー

データレコード関数は、データレコードが処理される前と後に実行されます。

### 変換

変換関数は、次のデータパイプライン図に示すように、データレコードが処理される前に実行されます。

![](https://docs.tealium.com/images/server-side/transformations-data-record-pipeline.png)

パイプラインのこの時点で関数を使用し、処理前に[データレコードオブジェクト](#data-record-object)とその値を変換します。

詳細については、[about-data-transformation-functions](https://docs.tealium.com/about-data-transformation-functions/)を参照してください。

### カスタムアクション

カスタムアクション関数は、次のデータパイプライン図に示すように、データレコードが処理された後に実行されます。

![](https://docs.tealium.com/images/server-side/functions-data-record-pipeline.png)

パイプラインのこの時点で関数をアクティベーションとして使用し、データレコードを他のシステムへ送信します。


<blockquote>
データパイプラインのこの時点では、`dataRecord` オブジェクトを変更してもシステムの他の部分には影響しません。
</blockquote>


## ランタイムバージョン

データレコード変換関数のランタイムバージョンはイベントデータ用のものと同じですが、以下の変更が含まれています。

* `crypto-es` ライブラリが削除され、[`tealium/crypto`](https://docs.tealium.com/function-modules/#crypto)に置き換えられています。

カスタムアクションのランタイムバージョンは、[イベント関数および訪問関数 V3](https://docs.tealium.com/event-visitor-functions-v3/)と同じですが、以下の変更が含まれています。

* `track` ライブラリが削除されています。
* データレコードを新しいイベントとして Tealium に送り返すことはできません。

## transform() 関数

変換データレコード関数を作成するときは、`$.dataSourceId` フィールドをトリガールールの条件として使用する必要があります。この条件を使用して、クラウドデータソースのデータソースキーを参照します。

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


クラウドデータソースを選択してトリガールールを構成すると、関数コードエディターの**コード**タブに次のデフォルトコードが表示されます。

```js
import flatten from "tealium/util/flatten/v2";

// "transform" function allows you to access data record and apply changes
transform((dataRecord) => {
    // change are applied via the mutation of the original record
    console.log(JSON.stringify(flatten(dataRecord), null, 2));
})
```

## activate() 関数

カスタムアクションのデータレコード関数を作成すると、関数コードエディターの**コード**タブにデフォルトコードが表示されます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_function_details.png)

このコードには、`activate()` 関数とその入力パラメータが含まれています。

```js
activate(async ({ dataRecord, helper }) => {
  ...
});
```

データレコード関数には、[`dataRecord` オブジェクト](#data-record-object)と `helper` オブジェクトがあります。

`helper` パラメータには、認証情報の取得とグローバル変数の取得に使用する `helper.getAuth()` および `helper.getGlobalVariable()` が用意されています。詳細については、を参照してください。


<blockquote>
認証トークンは、HTTP リクエスト内の関数からのみ参照できます。HTTP リクエスト外でトークンを参照しようとすると、そのトークンは UUID プレースホルダーに置き換えられます。
</blockquote>


## データレコードオブジェクト


<blockquote>
Tealium Collect で使用する変換関数については、[イベントパラメータ](https://docs.tealium.com/transforms-event-parameter/)を参照してください。
</blockquote>


`dataRecord` オブジェクトは、Data Cloud Activation 関数およびクラウドデータソースで使用でき、次のプロパティを含みます。

| プロパティ | データ型 | 説明 |
| -------- | --------- | ----------- |
| `account` | string | Tealium アカウント名。 |
| `data` | object | クラウドデータソースからクエリされたデータレコード。`dataRecord.data.udo` で参照されます。 |
| `event_id` | string | Tealium イベント ID。 |
| `post_time` | number | データレコードがクエリされた時刻を示すタイムスタンプ。 |
| `profile` | string | Tealium プロファイル名。 |
| `dataSourceId` | string | データソースの ID。|

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

次のデータレコード関数の例では、Tealium Crypto ライブラリを使用してデータレコードのメールアドレス属性（`CDW_Column3_EmailAddress`）をハッシュ化し、そのデータレコードを Webhook に送信します。

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