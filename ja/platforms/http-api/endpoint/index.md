---
title: エンドポイント仕様
description: この記事では、イベント用HTTP APIを使用してTealium Customer Data Hubにデータを送信する方法について説明します。
url: https://docs.tealium.com/ja/platforms/http-api/endpoint/
---
この記事では、HTTPリクエストを送信するあらゆるアプリケーションで使用される、直接HTTPエンドポイントの仕様について説明します。

## Tealium CollectのURL

Tealium Collectは、次のルートURLにあります。

```bash
https://collect.tealiumiq.com/event
```

## レート制限

Tealium Collect APIでサポートされる最大レート制限は、100リクエスト/秒です。


<blockquote>
ビジネス上、これより高い呼び出し上限が必要な場合は、Tealiumのアカウントマネージャーにお問い合わせください。
</blockquote>


## 標準パラメータ

Tealium Collectでは、各リクエストで次の標準パラメータがサポートされます。

* `tealium_account`：Tealiumアカウントの名前。
* `tealium_profile`：Tealiumプロファイルの名前。デフォルトは**main**です。
* `tealium_datasource`：（オプション）Customer Data Hubのデータソースキー。詳細については、[データソースについて](https://docs.tealium.com/about-data-sources/)を参照してください。
* `tealium_event`：推奨。トラッキングに使用するイベントの名前。
* `tealium_visitor_id`：Customer Data Platform（CDP）では必須。イベントに関連付けられた訪問の一意の識別子（[訪問識別子](#visitor-identifiers)セクションを参照）。データソースによっては、この識別子は訪問が使用しているデバイスに関連付けられた匿名GUID（Globally Unique Identifier）である場合も、訪問の既知のユーザー識別子に基づく場合もあります。
* `tealium_trace_id`：（オプション）[Trace](https://docs.tealium.com/about-trace/)で使用します。

リクエストの形式は、使用するHTTPメソッドによって異なります。以下の例では、プレースホルダー値を次の形式の波括弧で表します：`{VALUE}`。

## カスタムイベントパラメータ

トラッキングの要件に応じて、追加のイベント属性をカスタムパラメータとして送信します。これらのパラメータは、Customer Data Hubでもイベント属性として定義する必要があります。イベント属性の詳細については、[属性について](https://docs.tealium.com/about-attributes/)を参照してください。

## 訪問識別子

訪問のトラッキングでは、次の組み合わせを使用します。

* **匿名ID**：通常、訪問を匿名でトラッキングするために使用するID（デバイスやブラウザから取得したIDなど）。[既知の訪問](#known-visitors-server-to-server)の場合は、ユーザー識別子に基づく値を使用できます。
* **ユーザー識別子**：訪問が既知になった後に送信します。特定のデバイスではなく、ユーザーを識別する値に基づきます。

### 匿名ID

匿名IDは、CDPがイベントや訪問をまたいで訪問を関連付けるために使用する匿名識別子です。この値がGUIDであり、同じ訪問に対して一貫していることを確認してください。また、この値はサーバーサイドプロファイルごとに一意である必要があります。

匿名IDのキー名は`tealium_visitor_id`です。

ビジネスユースケースに応じて、匿名の値または既知のユーザー識別子に基づく値を使用できます。

#### 匿名値

|CDP| Event Streaming|
|---| ---|
| 必須 | 該当なし |

Tag Managementを使用し、匿名訪問プロファイルを拡充するためにサーバー間でAPI呼び出しを送信している場合、`tealium_visitor_id`の値は`utag_main_v_id` Cookieの値と一致する必要があります。utag.jsの組み込み変数の詳細については、[JavaScript（Web）> データレイヤー](https://docs.tealium.com/platforms/javascript/data-layer/)を参照してください。


<blockquote>
Adobe LaunchまたはGoogle Tag Managerを使用している場合、この値は**TEAL** Cookieの`v`部分と一致する必要があります。
</blockquote>


#### 既知の訪問のサーバー間通信

|CDP| Event Streaming|
|---| ---|
| 必須 | 推奨 |

既知の訪問に関するデータを送信する場合（`email_address`などの訪問ID属性に値が存在する場合）、次の項目を連結した値を含めます。

* アカウント
* プロファイル  
プロファイル名を含めることで、`tealium_visitor_id`が各サーバーサイドプロファイルで一意になります。これは、同じ訪問プロファイルが同一リージョン内の複数のサーバーサイドプロファイルに送信される場合に不可欠です。
* 訪問ID属性のIDと値 
<blockquote>
訪問ID属性のIDは、属性リストの属性名の横または展開された詳細内で確認できます。詳細については、[属性について](https://docs.tealium.com/about-attributes/#attribute-ids)を参照してください。
</blockquote>

* `tealium_visitor_id`パラメータの値

たとえば、次の値を使用するとします。

* アカウント名：`my-account`
* プロファイル：`main`
* 訪問ID属性のID：`7688`
* 渡す顧客番号の値：`45653454`

これらの値を次のように連結します。

```
tealium_visitor_id":"__my-account_main__7688_45653454__"
```


<blockquote>
続行する前に、`tealium_visitor_id`が正しい形式であることを確認してください。形式が正しくないパラメータはCDPでエラーを引き起こし、適切にトラッキングされない可能性があります。
</blockquote>


JSONの例：

```json
{
    "tealium_account"    : "my-account",
    "tealium_profile"    : "main",
    "tealium_event"      : "user_login",
    "email_address"      : "user@example.com",
    "customer_number"    : "45653454", 
    "tealium_visitor_id" : "__my-account_main__7688_45653454__"
}
```


<blockquote>
匿名訪問と既知の訪問のどちらを使用する場合でも、API呼び出しに一貫した`tealium_visitor_id`が含まれていないと、イベントごとに新しい訪問と訪問が生成され、訪問のスティッチングができなくなります。
</blockquote>


### ユーザー識別子

CDPを使用する場合、トラッキング呼び出しで既知のユーザー識別子を渡すことができます。たとえば、`email_address`や`login_id`です。

Event Streamingを使用しており、ベンダーコネクタにIDを提供する必要がある場合にも、ユーザー識別子が必要です。

CDPでは、これらのユーザー識別子を使用して[訪問ID属性](https://docs.tealium.com/visitor-id-attribute/)を拡充します。

### 訪問の切り替え

ファーストパーティCookieを使用できない場合、サーバーサイドでは次の優先順位で受信データを使用し、訪問のIDを決定します。

* `TAPID` Cookie（`tealium_thirdparty_visitor_id`とも呼ばれます）
* `tealium_visitor_id`
* `utag_main v_id`（`tealium_firstparty_visitor_id`とも呼ばれます）

CDPでは、使用する訪問プロファイルを決定する際に、`TAPID`内のIDが他のIDより優先されるため、同じデバイス上で複数のユーザーをトラッキングする際に問題が発生する可能性があります。

たとえば、あるユーザーがログインし、そのIDが`TAPID`に追加されると、そのデバイス上のすべての匿名ユーザーからのトラフィックが、そのユーザーに記録されます。匿名Cookieが削除されていない状態で2人目のユーザーがそのデバイスにログインしても、CDPは引き続き最初のユーザーにアクティビティを記録します。訪問が共有スマートテレビや公共のキオスクを使用する場合、訪問プロファイル内のデータが混在する可能性があります。

イベント内の`tealium_visitor_id`値と`tealium_thirdparty_visitor_id`値をエンドポイントで処理する方法を制御するには、次のパラメータを使用します。

| パラメータ | 型 | 説明 |
| -------------------------------------- | ---------- | ----------- |
| `tealium_override_tapid` | string | `tealium_visitor_id`と`tealium_thirdparty_visitor_id`をこの値で上書きします。 |
| `tealium_skip_3rd_party_vid_cookies` | boolean | `TAPID`サードパーティCookieの収集をスキップするには、`true`に構成します。 |
| `tealium_delete_3rd_party_vid_cookies` | boolean | `TAPID`サードパーティCookieを削除するには、`true`に構成します。 |

* `tealium_override_tapid`の値が指定されている場合、`tealium_delete_3rd_party_vid_cookies`パラメータによるCookieの削除は行われません。
* TAPIDから`account/profile`情報を削除した結果、そのCookieが空になる場合は、クライアントからそのCookieを削除するために`set-cookie maxAge=0`が返されます。
## ボットフィルタリング

Tealiumのサーバーサイド製品で収集されるデータの精度を維持するには、サーバーサイドでのボットフィルタリングが不可欠です。

ボットトラフィックとは、サイトまたはアプリへの人間以外によるアクセスを指します。Tealiumのサーバーサイド製品は、各イベントのユーザーエージェントを既知のボットのリストと比較し、ボットトラフィックを自動的に除外します。除外されたイベントは処理されず、使用量にもカウントされません。

詳細およびボットとして認識されるユーザーエージェントの完全なリストについては、[server-side-bot-filtering](https://docs.tealium.com/server-side-bot-filtering/)を参照してください。

## メソッド


<blockquote>
ブラウザーからCollect APIトラフィックを送信する場合、GETメソッドでは、リクエストのHTTPリファラーURLに基づいてページURLが構成されます。このURLには、現在のページのホスト名のみが含まれます。GETメソッドを使用した場合、現在のページのクエリパラメータやパス名は含まれません。この情報を含めるには、POSTメソッドを使用してください。
</blockquote>


### GET

GETメソッドは、指定されたリソースからデータをリクエストするために使用します。エンドポイントのクエリ文字列でキーと値のペアを使用してデータを渡し、HTMLベースの実装との互換性を確保するために、1x1ピクセルの透明なGIFを返します。

curlを使用した例：

```bash
curl -i -X GET "https://collect.tealiumiq.com/event?tealium_account={ACCOUNT}&tealium_profile={PROFILE}&tealium_event=user_login&email_address=user@example.com" 
```

### POST

POSTメソッドは、リソースを作成または更新するためにデータをサーバーへ送信する際に使用します。JSONペイロードをサポートしており、リクエストヘッダーを`Content-Type: application/json`に構成し、ペイロードを有効なJSON文字列としてフォーマットする必要があります。

`user_login`イベントの例：

```javascript
{
    "tealium_account"   : "ACCOUNT",
    "tealium_profile"   : "PROFILE",
    "tealium_event"     : "EVENT_NAME",
    "email_address"     : "EMAIL_ADDRESS"
}
```

curlを使用した例：

```bash
curl -X POST -H 'Content-type: application/json'
--data '{"tealium_account":"{ACCOUNT}","tealium_profile":"{PROFILE}","tealium_event":"user_login","email_address":"user@example.com"}'
https://collect.tealiumiq.com/event
```

## ステータスコード

次の表は、TealiumのHTTPレスポンスステータスコードをまとめたものです。

| ステータスコード | 説明 |
| --- | --- |
| `200 Status OK` | リクエストは成功しました |
| `400 Bad Request` | サーバーがリクエストを理解できません |

次の条件のうち少なくとも1つに該当する場合、`400 Bad Request`ステータスコードが発生します。

- JSONキーにピリオドが含まれている、キーが無効である、またはサイズが1 MBを超えている。
- ファイルタイプパラメータに`json`または`javascript`以外の値が含まれている。
- `account`、`profile`、`datalayer_id`の組み合わせが250文字を超えているか、制限対象の文字が含まれている。
- `tealium_account`または`tealium_profile`が指定されていないか、入力ミスが含まれている。
- リクエスト本文が空である。

次の例は、必須の`tealium_account`または`tealium_profile`パラメータ値が指定されていない場合に、`X-Error`ヘッダーに表示される`400 Bad Request`レスポンスです。

```
> GET /event?tealium_account=jentest-as&tealium_profile=&tealium_visitor_id=sendgeteventhttps@testing.com&tealium_datasource=utc2cj&customer_city=Honolulu&customer_state=Hawaii&Flag=true&Number=45&String=ascent&String_Array=[hello,howareyou,whatsup,yoyoyo]&Number_Array=[2.222,3.000,19.12,28.3]&Flag_Array=[true,false,false,true]&Combo_Array=[1,salutations,2324,world,22jjfssl]&Array_of_Array=[[1,2,3],heyworld]&myvariable=unicorns HTTP/1.1
> Host: qa21-collect.tealiumiq.com
> User-Agent: curl/7.54.0
> Accept: */*
>
< HTTP/1.1 400 Bad Request
< Cache-Control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< Content-Type: application/json
< Date: Wed, 23 Oct 2019 17:10:51 GMT
< Expires: Wed, 23 Oct 2019 17:10:51 GMT
< P3P: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< Pragma: no-cache
< Vary: Origin
< X-Error: Missing required tealium_account or tealium_profile param value
< X-Region: us-east-1
< X-ServerID: uconnect_i-9a157d19
< X-ULVer: 1.0.331-SNAPSHOT
< X-UUID: d4fc78d1-8204-412c-a6cb-57869d2370a7
< Content-Length: 0
< Connection: keep-alive
```

## 例

### HTMLの例

HTML内の`<img>`タグでTealium Collectを参照します。ブラウザーのキャッシュを考慮し、次の例に示すように、ランダムに生成された値を含む追加パラメータであるキャッシュバスターを指定することが重要です。

```javascript
var cb=Math.random()*100000000000;
```

この変数をTealium Collectピクセルのクエリ文字列に追加します。

```html
<img height="1" width="1" style="display:none" src="//collect.tealiumiq.com/event?tealium_account={ACCOUNT}&tealium_profile={PROFILE}&tealium_event=user_login&email_address=user@example.com&cb=' + cb + '"/>
```

### JavaScriptの例

Tealium Collectはクロスドメインリクエストをサポートしているため、次の例に示すように、WebサイトからTealiumのドメインへPOSTリクエストを送信できます。

```javascript
var event = {
    "tealium_account" : "ACCOUNT",
    "tealium_profile" : "PROFILE",
    "tealium_event"   : "EVENT_NAME",
    "email_address"   : "EMAIL_ADDRESS"};
var xhr = new XMLHttpRequest();
xhr.open("POST", "https://collect.tealiumiq.com/event");
xhr.send(JSON.stringify(event));
```

レスポンスヘッダーには、次の内容が含まれます。  

```javascript
Access-Control-Allow-Origin: [http://your_domain.com](http://your_domain.com)
```