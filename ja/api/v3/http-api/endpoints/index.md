---
title: HTTP API エンドポイント
description: HTTP APIを使用してTealiumにデータを送信できます。
url: https://docs.tealium.com/ja/api/v3/http-api/endpoints/
---
## GETメソッド

GETメソッドは、エンドポイントのクエリ文字列にキーと値のペアを使用してデータを渡します。この方法は、HTMLベースの実装と互換性を持たせるために1x1の透明GIFを返します。

### `/event`の例

#### cURLリクエストの例

```bash
curl -i -X GET 'https://{host}/v3/collect/event?tealium_account={account}&tealium_profile={profile}&tealium_event=user_login&email_address=user@example.com'
--header 'Authorization: Bearer eyJ0**'
```

#### レスポンスの例

```bash
< HTTP/2 200
< date: Fri, 15 Jul 2022 00:08:50 GMT
< content-type: image/gif
< content-length: 43
< x-amzn-requestid: 03bb378a-2619-4440-9d5a-c1e7d0e8d2ae
< x-amzn-remapped-content-length: 43
< x-region: us-east-1
< x-acc: {account}:{profile}:2:event
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-amzn-remapped-connection: keep-alive
< x-uuid: f513ef4b-5870-4fa4-b908-38c5e12bf3e4
< x-amz-apigw-id: VSBy2Fu6oAMFezA=
< vary: Origin
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-serverid: uconnect_i-0182b50695a2297ec
< expires: Fri, 15 Jul 2022 00:08:50 GMT
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< x-tid: f513ef4b58704fa4b90838c5e12bf3e4
< pragma: no-cache
< x-amzn-remapped-date: Fri, 15 Jul 2022 00:08:50 GMT
```

## POSTメソッド

POSTメソッドはJSONペイロードをサポートしており、リクエストヘッダーには`Content-Type: application/json`を構成し、ペイロードは有効なJSON文字列としてフォーマットする必要があります。

### `/event`の例

#### cURLリクエストの例

```bash
curl --location --request POST 'https://{host}/v3/collect/event' --header 'Authorization: Bearer eyJ0eXA***' --header 'Content-Type: application/json' --data-raw '{
"tealium_account": "{account}",
"tealium_datasource": "abc123",
"tealium_profile": "{profile}",
"tealium_event": "page_view",
"page_type": "123",
"page_name": "testName"
}'
```

#### レスポンスの例

```bash
< HTTP/2 200
< date: Fri, 15 Jul 2022 00:08:03 GMT
< content-type: application/json
< content-length: 0
< x-amzn-requestid: ad5c154f-3053-4991-9a60-45b35745eba7
< x-region: us-east-1
< x-acc: {account}:main:2:event
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-amzn-remapped-connection: keep-alive
< x-uuid: 1d6b9c12-16c3-44a9-95c9-78afeabaf8e0
< x-amz-apigw-id: VSBroH24oAMFXpQ=
< vary: Origin
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-serverid: uconnect_i-0a95ad51791af67ac
< expires: Fri, 15 Jul 2022 00:08:03 GMT
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< x-tid: abc123_071422_1
< pragma: no-cache
< x-amzn-remapped-date: Fri, 15 Jul 2022 00:08:03 GMT
```

### `/bulk-event`の例

#### cURLリクエストの例

```bash
curl --location --request POST 'https://{host}/v3/collect/bulk-event' \
--header 'Authorization: Bearer eyJ0eXAi***' \
--header 'Content-Type: application/json' \
--data-raw '{
    "shared": {
      "tealium_account": "{account}",
      "tealium_profile": "{profile}",
      "tealium_environment": "prod",
      "tealium_datasource": "{datasource}",
      "tealium_visitor_id": "abc123_071222_1"
    },
    "events": [
      {
        "page_name": "test1",
        "tealium_event": "page_view"
      },
      {
        "page_name": "test2",
        "tealium_event": "page_view"
      }
    ]
}'
```

#### レスポンスの例

```bash
< HTTP/2 200
< date: Fri, 15 Jul 2022 00:07:37 GMT
< content-type: application/json
< content-length: 0
< x-amzn-requestid: 11f79456-cdb8-4ccc-8cc7-e8a54db79414
< x-region: us-east-1
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-amzn-remapped-connection: keep-alive
< x-uuid: 7277c009-f9f5-47a2-9fe6-61f05c98e6fd
< x-amz-apigw-id: VSBnlEqkIAMFbFA=
< vary: Origin
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-serverid: uconnect_i-01e68ac980b602444
< expires: Fri, 15 Jul 2022 00:07:37 GMT
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< pragma: no-cache
< x-amzn-remapped-date: Fri, 15 Jul 2022 00:07:37 GMT
```

### `/integration/event`の例

#### cURLリクエストの例

```bash
curl --location --request POST 'https://{host}/v3/collect/integration/event/accounts/{account}/profiles/{profile}/datasources/{datasourceId}' --header 'Authorization: Bearer eyJ0***' --header 'Content-Type: application/json' --data-raw '{
  "tealium_event": "page_view",
  "tealium_datasource": "{datasourceId}",
  "page_type": "123",
  "outerObject": {
    "innerobject":"1234"
  },
  "page_name": "kek"
}'
```

#### レスポンスの例

```bash
< HTTP/2 204
< date: Fri, 15 Jul 2022 00:05:23 GMT
< x-amzn-requestid: e3b5bc65-8712-40a3-a87c-9d6bb8df68cf
< x-region: us-east-1
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-amzn-remapped-connection: keep-alive
< x-uuid: fadbdf55-dccb-4241-a9ce-81722fc2a8d9
< x-amz-apigw-id: VSBSnF9OIAMFxXA=
< vary: Origin
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-serverid: uconnect_i-058449c0632b25787
< expires: Fri, 15 Jul 2022 00:05:23 GMT
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< pragma: no-cache
< x-amzn-remapped-date: Fri, 15 Jul 2022 00:05:23 GMT
```

## ステータスコード

以下の表は、TealiumのHTTPレスポンスステータスコードをまとめたものです：

|ステータスコード| 説明|
|---| ---|
|`200 Status OK`| リクエストが成功しました|
|`400 Bad Request`| サーバーがリクエストを理解できません|

`400 Bad Request`ステータスコードは、以下のいずれかが真の場合に発生します：

* JSONキーにピリオドが含まれている、無効である、または1MBを超える
* ファイルタイプパラメータにJSONまたはJavaScript以外の値が含まれている
* `account`、`profile`、および`datalayer_id`の組み合わせが250文字を超える、または制限された文字を含む
* `tealium_account`または`tealium_profile`が欠落している、または誤字がある
* リクエストボディが空です

以下は、必要な`tealium_account`または`tealium_profile`パラメータ値が欠落しているため、`/v3/collect/event`へのGETリクエストに対する`400 Bad Request`レスポンスの例です：

```bash
< HTTP/2 200
< date: Fri, 15 Jul 2022 00:03:05 GMT
< content-type: image/gif
< content-length: 43
< x-error: Missing required tealium_account or tealium_profile param value
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-region: us-west-2
< x-serverid: uconnect_i-0b80d0d9adfb124a2
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< vary: Origin
< pragma: no-cache
< expires: Fri, 15 Jul 2022 00:03:05 GMT
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-uuid: 1d0dd863-dc31-4eb2-b7a0-5b98e3b7fb5b
```

以下は、`/v3/collect/bulk-event`へのPOSTリクエストに対する`400 Bad Request`レスポンスの例です：

```bash
< HTTP/2 400
< date: Fri, 15 Jul 2022 00:01:16 GMT
< content-type: application/json
< content-length: 78
< x-amzn-requestid: 993d950d-cde4-4ee0-9f18-d3e41a3ed5ca
< x-amzn-remapped-content-length: 78
< x-region: us-east-1
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-amzn-remapped-connection: keep-alive
< x-uuid: 59afeed7-abe2-487c-bac1-a96903f4a449
< x-amz-apigw-id: VSAr9HOloAMFQkA=
< vary: Origin
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-serverid: uconnect_i-02ccd81bf59828cde
< expires: Fri, 15 Jul 2022 00:01:16 GMT
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< pragma: no-cache
< x-amzn-remapped-date: Fri, 15 Jul 2022 00:01:16 GMT
<
* Connection #0 to host us-east-1-platform.tealiumapis.com left intact
{ "returnCode" : 1400 , "message" : "Request body must contain 'events' key."}
```