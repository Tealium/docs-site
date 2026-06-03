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
curl -i -X GET &#39;https://{host}/v3/collect/event?tealium_account={account}&amp;tealium_profile={profile}&amp;tealium_event=user_login&amp;email_address=user@example.com&#39;
--header &#39;Authorization: Bearer eyJ0**&#39;
```

#### レスポンスの例

```bash
&lt; HTTP/2 200
&lt; date: Fri, 15 Jul 2022 00:08:50 GMT
&lt; content-type: image/gif
&lt; content-length: 43
&lt; x-amzn-requestid: 03bb378a-2619-4440-9d5a-c1e7d0e8d2ae
&lt; x-amzn-remapped-content-length: 43
&lt; x-region: us-east-1
&lt; x-acc: {account}:{profile}:2:event
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-amzn-remapped-connection: keep-alive
&lt; x-uuid: f513ef4b-5870-4fa4-b908-38c5e12bf3e4
&lt; x-amz-apigw-id: VSBy2Fu6oAMFezA=
&lt; vary: Origin
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-serverid: uconnect_i-0182b50695a2297ec
&lt; expires: Fri, 15 Jul 2022 00:08:50 GMT
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; x-tid: f513ef4b58704fa4b90838c5e12bf3e4
&lt; pragma: no-cache
&lt; x-amzn-remapped-date: Fri, 15 Jul 2022 00:08:50 GMT
```

## POSTメソッド

POSTメソッドはJSONペイロードをサポートしており、リクエストヘッダーには`Content-Type: application/json`を構成し、ペイロードは有効なJSON文字列としてフォーマットする必要があります。

### `/event`の例

#### cURLリクエストの例

```bash
curl --location --request POST &#39;https://{host}/v3/collect/event&#39; --header &#39;Authorization: Bearer eyJ0eXA***&#39; --header &#39;Content-Type: application/json&#39; --data-raw &#39;{
&#34;tealium_account&#34;: &#34;{account}&#34;,
&#34;tealium_datasource&#34;: &#34;abc123&#34;,
&#34;tealium_profile&#34;: &#34;{profile}&#34;,
&#34;tealium_event&#34;: &#34;page_view&#34;,
&#34;page_type&#34;: &#34;123&#34;,
&#34;page_name&#34;: &#34;testName&#34;
}&#39;
```

#### レスポンスの例

```bash
&lt; HTTP/2 200
&lt; date: Fri, 15 Jul 2022 00:08:03 GMT
&lt; content-type: application/json
&lt; content-length: 0
&lt; x-amzn-requestid: ad5c154f-3053-4991-9a60-45b35745eba7
&lt; x-region: us-east-1
&lt; x-acc: {account}:main:2:event
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-amzn-remapped-connection: keep-alive
&lt; x-uuid: 1d6b9c12-16c3-44a9-95c9-78afeabaf8e0
&lt; x-amz-apigw-id: VSBroH24oAMFXpQ=
&lt; vary: Origin
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-serverid: uconnect_i-0a95ad51791af67ac
&lt; expires: Fri, 15 Jul 2022 00:08:03 GMT
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; x-tid: abc123_071422_1
&lt; pragma: no-cache
&lt; x-amzn-remapped-date: Fri, 15 Jul 2022 00:08:03 GMT
```

### `/bulk-event`の例

#### cURLリクエストの例

```bash
curl --location --request POST &#39;https://{host}/v3/collect/bulk-event&#39; \
--header &#39;Authorization: Bearer eyJ0eXAi***&#39; \
--header &#39;Content-Type: application/json&#39; \
--data-raw &#39;{
    &#34;shared&#34;: {
      &#34;tealium_account&#34;: &#34;{account}&#34;,
      &#34;tealium_profile&#34;: &#34;{profile}&#34;,
      &#34;tealium_environment&#34;: &#34;prod&#34;,
      &#34;tealium_datasource&#34;: &#34;{datasource}&#34;,
      &#34;tealium_visitor_id&#34;: &#34;abc123_071222_1&#34;
    },
    &#34;events&#34;: [
      {
        &#34;page_name&#34;: &#34;test1&#34;,
        &#34;tealium_event&#34;: &#34;page_view&#34;
      },
      {
        &#34;page_name&#34;: &#34;test2&#34;,
        &#34;tealium_event&#34;: &#34;page_view&#34;
      }
    ]
}&#39;
```

#### レスポンスの例

```bash
&lt; HTTP/2 200
&lt; date: Fri, 15 Jul 2022 00:07:37 GMT
&lt; content-type: application/json
&lt; content-length: 0
&lt; x-amzn-requestid: 11f79456-cdb8-4ccc-8cc7-e8a54db79414
&lt; x-region: us-east-1
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-amzn-remapped-connection: keep-alive
&lt; x-uuid: 7277c009-f9f5-47a2-9fe6-61f05c98e6fd
&lt; x-amz-apigw-id: VSBnlEqkIAMFbFA=
&lt; vary: Origin
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-serverid: uconnect_i-01e68ac980b602444
&lt; expires: Fri, 15 Jul 2022 00:07:37 GMT
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; pragma: no-cache
&lt; x-amzn-remapped-date: Fri, 15 Jul 2022 00:07:37 GMT
```

### `/integration/event`の例

#### cURLリクエストの例

```bash
curl --location --request POST &#39;https://{host}/v3/collect/integration/event/accounts/{account}/profiles/{profile}/datasources/{datasourceId}&#39; --header &#39;Authorization: Bearer eyJ0***&#39; --header &#39;Content-Type: application/json&#39; --data-raw &#39;{
  &#34;tealium_event&#34;: &#34;page_view&#34;,
  &#34;tealium_datasource&#34;: &#34;{datasourceId}&#34;,
  &#34;page_type&#34;: &#34;123&#34;,
  &#34;outerObject&#34;: {
    &#34;innerobject&#34;:&#34;1234&#34;
  },
  &#34;page_name&#34;: &#34;kek&#34;
}&#39;
```

#### レスポンスの例

```bash
&lt; HTTP/2 204
&lt; date: Fri, 15 Jul 2022 00:05:23 GMT
&lt; x-amzn-requestid: e3b5bc65-8712-40a3-a87c-9d6bb8df68cf
&lt; x-region: us-east-1
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-amzn-remapped-connection: keep-alive
&lt; x-uuid: fadbdf55-dccb-4241-a9ce-81722fc2a8d9
&lt; x-amz-apigw-id: VSBSnF9OIAMFxXA=
&lt; vary: Origin
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-serverid: uconnect_i-058449c0632b25787
&lt; expires: Fri, 15 Jul 2022 00:05:23 GMT
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; pragma: no-cache
&lt; x-amzn-remapped-date: Fri, 15 Jul 2022 00:05:23 GMT
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
&lt; HTTP/2 200
&lt; date: Fri, 15 Jul 2022 00:03:05 GMT
&lt; content-type: image/gif
&lt; content-length: 43
&lt; x-error: Missing required tealium_account or tealium_profile param value
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-region: us-west-2
&lt; x-serverid: uconnect_i-0b80d0d9adfb124a2
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; vary: Origin
&lt; pragma: no-cache
&lt; expires: Fri, 15 Jul 2022 00:03:05 GMT
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-uuid: 1d0dd863-dc31-4eb2-b7a0-5b98e3b7fb5b
```

以下は、`/v3/collect/bulk-event`へのPOSTリクエストに対する`400 Bad Request`レスポンスの例です：

```bash
&lt; HTTP/2 400
&lt; date: Fri, 15 Jul 2022 00:01:16 GMT
&lt; content-type: application/json
&lt; content-length: 78
&lt; x-amzn-requestid: 993d950d-cde4-4ee0-9f18-d3e41a3ed5ca
&lt; x-amzn-remapped-content-length: 78
&lt; x-region: us-east-1
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-amzn-remapped-connection: keep-alive
&lt; x-uuid: 59afeed7-abe2-487c-bac1-a96903f4a449
&lt; x-amz-apigw-id: VSAr9HOloAMFQkA=
&lt; vary: Origin
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-serverid: uconnect_i-02ccd81bf59828cde
&lt; expires: Fri, 15 Jul 2022 00:01:16 GMT
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; pragma: no-cache
&lt; x-amzn-remapped-date: Fri, 15 Jul 2022 00:01:16 GMT
&lt;
* Connection #0 to host us-east-1-platform.tealiumapis.com left intact
{ &#34;returnCode&#34; : 1400 , &#34;message&#34; : &#34;Request body must contain &#39;events&#39; key.&#34;}
```