---
title: エンドポイント仕様
description: この記事では、イベント用のHTTP APIを使用してTealium Customer Data Hubにデータを送信する方法について説明します。
url: https://docs.tealium.com/ja/platforms/http-api/endpoint/
---
この記事では、HTTPリクエストを送信する任意のアプリケーションで使用される直接HTTPエンドポイントの仕様について説明します。

## Tealium Collect URL

Tealium Collectは以下のルートURLに位置しています：

```bash
https://collect.tealiumiq.com/event
```

## レート制限

Tealium Collect APIは、最大100リクエスト/秒のレート制限をサポートしています。

ビジネスニーズがより高い呼び出し制限を必要とする場合は、Tealiumアカウントマネージャーに連絡してください。

## 標準パラメータ

Tealium Collectは、各リクエストに以下の標準パラメータをサポートしています：

* `tealium_account`: あなたのTealiumアカウントの名前。
* `tealium_profile`: あなたのTealiumプロファイルの名前。デフォルトは**main**です。
* `tealium_datasource`: オプション。Customer Data Hubからのデータソースキー。詳細については、[データソースについて]()を参照してください。
* `tealium_event`: 推奨。トラッキング目的のイベント名。
* `tealium_visitor_id`: AudienceStream用に必須。イベントに関連付けられた訪問の一意の識別子（[訪問識別子](#visitor-identifiers)セクションを参照）。データのソースによっては、この識別子は訪問が使用しているデバイスに関連付けられた匿名のGUID（グローバル一意識別子）であるか、訪問の既知のユーザー識別子に基づいている場合があります。
* `tealium_trace_id`: オプション。[Trace]()で使用します。

リクエストの形式は使用されるHTTPメソッドによって異なります。以下の例では、プレースホルダー値は次の形式で中括弧で表されています：`{VALUE}`。

## カスタムイベントパラメータ

追跡ニーズに応じて、追加のイベント属性はカスタムパラメータとして送信されます。これらのパラメータもCustomer Data Hubでイベント属性として定義する必要があります。イベント属性についての詳細は、[属性について]()を参照してください。

## 訪問識別子

AudienceStreamは、以下の組み合わせを使用して訪問を追跡します：

* **匿名ID**: 訪問を匿名で追跡するために通常使用されるID（例えば、デバイスやブラウザから）。[既知の訪問](#known-visitors-server-to-server)の場合、ユーザー識別子に基づいた値を使用できます。
* **ユーザー識別子**: 訪問が既知の場合に送信されます。特定のデバイスではなく、ユーザーを識別する値に基づいています。

### 匿名ID

匿名IDは、AudienceStreamが訪問をイベントや訪問間で関連付けるために使用する匿名識別子です。この値はGUIDであり、訪問に対して一貫性がある必要があります。この値は、サーバーサイドプロファイルごとに一意でなければなりません。

匿名IDのキー名は`tealium_visitor_id`です。

ビジネスケースに応じて、匿名値または既知のユーザー識別子に基づいた値を使用できます。

#### 匿名値

|AudienceStream| EventStream|
|---| ---|
| 必須 | N/A |

Tealium Tag Managementを使用してAPIコールをサーバー間で送信し、匿名訪問プロファイルをエンリッチする場合、`tealium_visitor_id`の値は`utag_main_v_id`クッキーの値と一致する必要があります。utag.jsの組み込み変数についての詳細は、[JavaScript (Web) &gt; Data Layer]()を参照してください。

Adobe LaunchまたはGoogle Tag Managerを使用している場合、値は**TEAL**クッキーの`v`部分と一致する必要があります。

#### 既知の訪問サーバー間

|AudienceStream| EventStream|
|---| ---|
| 必須 | 推奨 |

訪問ID属性（例えば`email_address`）の値が存在する場合に既知の訪問のデータを送信するとき、以下のものを連結して含めます：

* アカウント
* プロファイル  
プロファイル名を含めることで、`tealium_visitor_id`が各サーバーサイドプロファイルに固有であることを確実にします。これは、同じ訪問プロファイルが地域内の複数のサーバーサイドプロファイルに送信される場合に重要です。
* 訪問ID属性IDと値 訪問ID属性IDは、属性リストの属性名の隣または展開された詳細内で見つけることができます。詳細については、[属性について]()を参照してください。
* `tealium_visitor_id`パラメータ内の値

例えば、以下の値の場合：

* アカウント名：`my-account`
* プロファイル：`main`
* 訪問ID属性ID：`7688`
* 伝えたい顧客番号の値：`45653454`

これらの値を以下の方法で連結します：

```
tealium_visitor_id&#34;:&#34;__my-account_main__7688_45653454__&#34;
```

 `tealium_visitor_id`が正しくフォーマットされていることを確認してから進めてください。フォーマットが正しくないパラメータはAudienceStreamでエラーを引き起こし、適切に追跡されない可能性があります。

例 JSON：

```json
{
    &#34;tealium_account&#34;    : &#34;my-account&#34;,
    &#34;tealium_profile&#34;    : &#34;main&#34;,
    &#34;tealium_event&#34;      : &#34;user_login&#34;,
    &#34;email_address&#34;      : &#34;user@example.com&#34;,
    &#34;customer_number&#34;    : &#34;45653454&#34;, 
    &#34;tealium_visitor_id&#34; : &#34;__my-account_main__7688_45653454__&#34;
}
```

匿名訪問であっても既知の訪問であっても、APIコールに一貫した`tealium_visitor_id`が含まれていない場合、各イベントは新しい訪問を生成し、訪問のスティッチングが不可能になります。

### ユーザー識別子

AudienceStreamを使用する場合、トラッキングコールに既知のユーザー識別子（例えば、`email_address`や`login_id`）を渡すことができます。

ユーザー識別子は、EventStreamを使用してベンダーコネクタにIDを提供する必要がある場合にも必要です。

AudienceStreamでは、これらのユーザー識別子は[訪問ID属性]()をエンリッチするために使用されます。

### 訪問の切り替え

ファーストパーティクッキーが利用できない場合、サーバーサイドは次の優先順位で受信データを使用して訪問のIDを決定します：

* `TAPID`クッキー、別名`tealium_thirdparty_visitor_id`
* `tealium_visitor_id`
* `utag_main v_id`、別名`tealium_firstparty_visitor_id`

AudienceStreamは、訪問プロファイルを使用するために`TAPID`のIDを他のIDより優先するため、同じデバイス上の複数のユーザーを追跡する際に問題を引き起こす可能性があります。

たとえば、ユーザーがログインしてそのIDが`TAPID`に追加された場合、そのデバイスのすべての匿名ユーザーのトラフィックはそのユーザーに記録されます。別のユーザーがそのデバイスにログインした場合、匿名クッキーがクリアされていないと仮定すると、AudienceStreamは引き続き最初のユーザーにアクティビティを記録します。訪問が共有スマートテレビや公共のキオスクを使用する場合、これにより訪問プロファイルのデータが汚染される可能性があります。

エンドポイントがイベント内の`tealium_visitor_id`および`tealium_thirdparty_visitor_id`値を処理する方法を制御するためのパラメータを以下に示します：

| パラメータ                              | タイプ       | 説明 |
| -------------------------------------- | ---------- | ----------- |
| `tealium_override_tapid`               | 文字列     |  この値で`tealium_visitor_id`および`tealium_thirdparty_visitor_id`を上書きします。           |
| `tealium_skip_3rd_party_vid_cookies`   | ブール値    |  `TAPID`サードパーティクッキーの収集をスキップするには`true`に構成します。          |
| `tealium_delete_3rd_party_vid_cookies` | ブール値    |  `TAPID`サードパーティクッキーを削除するには`true`に構成します。           |

* `tealium_override_tapid`値は、`tealium_delete_3rd_party_vid_cookies`パラメータがクッキーを削除するのを防ぎます。
* TAPIDから`account/profile`情報を削除するとそのクッキーが空になる場合、クライアントからそのクッキーを削除するために`set-cookie maxAge=0`が返されます。
## ボットフィルタリング

Tealiumのサーバーサイド製品を通じて収集されたデータの正確性を維持するためには、サーバーサイドのボットフィルタリングが不可欠です。

ボットトラフィックとは、サイトやアプリへの非人間による訪問を指します。Tealiumのサーバーサイド製品は、各イベントのユーザーエージェントを既知のボットのリストと比較することにより、ボットトラフィックを自動的にフィルタリングします。フィルタリングされたイベントは処理されず、使用量にはカウントされません。

ボットとして認識されるユーザーエージェントの完全なリストについては、を参照してください。

## 方法

 ブラウザからCollect APIトラフィックを送信する場合、GETメソッドはリクエストのHTTPリファラーURLに基づいてページURLを構成し、これには現在のページのホスト名のみが含まれます。GETメソッドでは、現在のページのクエリパラメーターやパス名は含まれません。この情報を含めるには、POSTメソッドを使用してください。

### GET

GETメソッドは、指定されたリソースからデータを要求するために使用されます。エンドポイントのクエリ文字列にキーと値のペアを使用してデータを渡し、HTMLベースの実装と互換性を持たせるために1x1の透明GIFを返します。

curlを使用した例：

```bash
curl -i -X GET &#34;https://collect.tealiumiq.com/event?tealium_account={ACCOUNT}&amp;tealium_profile={PROFILE}&amp;tealium_event=user_login&amp;email_address=user@example.com&#34;
```

### POST

POSTメソッドは、データをサーバーに送信してリソースを作成/更新するために使用されます。リクエストヘッダーを`Content-Type: application/json`に構成し、ペイロードを有効なJSON文字列としてフォーマットする必要があります。

`user_login`イベントの例：

```javascript
{
    &#34;tealium_account&#34;   : &#34;ACCOUNT&#34;,
    &#34;tealium_profile&#34;   : &#34;PROFILE&#34;,
    &#34;tealium_event&#34;     : &#34;EVENT_NAME&#34;,
    &#34;email_address&#34;     : &#34;EMAIL_ADDRESS&#34;
}
```

curlを使用した例：

```bash
curl -X POST -H &#39;Content-type: application/json&#39;
--data &#39;{&#34;tealium_account&#34;:&#34;{ACCOUNT}&#34;,&#34;tealium_profile&#34;:&#34;{PROFILE}&#34;,&#34;tealium_event&#34;:&#34;user_login&#34;,&#34;email_address&#34;:&#34;user@example.com&#34;}&#39;
https://collect.tealiumiq.com/event
```

## ステータスコード

以下の表は、TealiumのHTTPレスポンスステータスコードをまとめたものです：

| ステータスコード | 説明 |
| --- | --- |
| `200 Status OK` | リクエストは成功しました |
| `400 Bad Request` | サーバーがリクエストを理解できません |

`400 Bad Request`ステータスコードは、以下のいずれかが真である場合に発生します：

- JSONキーにピリオドが含まれている、無効である、または1MBを超える。
- ファイルタイプパラメーターに`json`または`javascript`以外の値が含まれている。
- `account`、`profile`、および`datalayer_id`の組み合わせが250文字を超えるか、制限された文字を含んでいる。
- `tealium_account`または`tealium_profile`が欠落しているか、誤植がある。
- リクエストボディが空です。

必要な`tealium_account`または`tealium_profile`パラメータ値が欠落している場合の`400 Bad Request`レスポンスの例を、`X-Error`ヘッダーで示します：

```
&gt; GET /event?tealium_account=jentest-as&amp;tealium_profile=&amp;tealium_visitor_id=sendgeteventhttps@testing.com&amp;tealium_datasource=utc2cj&amp;customer_city=Honolulu&amp;customer_state=Hawaii&amp;Flag=true&amp;Number=45&amp;String=ascent&amp;String_Array=[hello,howareyou,whatsup,yoyoyo]&amp;Number_Array=[2.222,3.000,19.12,28.3]&amp;Flag_Array=[true,false,false,true]&amp;Combo_Array=[1,salutations,2324,world,22jjfssl]&amp;Array_of_Array=[[1,2,3],heyworld]&amp;myvariable=unicorns HTTP/1.1
&gt; Host: qa21-collect.tealiumiq.com
&gt; User-Agent: curl/7.54.0
&gt; Accept: */*
&gt;
&lt; HTTP/1.1 400 Bad Request
&lt; Cache-Control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; Content-Type: application/json
&lt; Date: Wed, 23 Oct 2019 17:10:51 GMT
&lt; Expires: Wed, 23 Oct 2019 17:10:51 GMT
&lt; P3P: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; Pragma: no-cache
&lt; Vary: Origin
&lt; X-Error: Missing required tealium_account or tealium_profile param value
&lt; X-Region: us-east-1
&lt; X-ServerID: uconnect_i-9a157d19
&lt; X-ULVer: 1.0.331-SNAPSHOT
&lt; X-UUID: d4fc78d1-8204-412c-a6cb-57869d2370a7
&lt; Content-Length: 0
&lt; Connection: keep-alive
```

## 例

### HTMLの例

Tealium Collectは、HTML内の`&lt;img&gt;`タグで参照されます。ブラウザキャッシュのため、ランダムに生成された値を含む追加パラメーターであるキャッシュバスターを含めることが重要です。以下の例を参照してください：

```javascript
var cb=Math.random()*100000000000;
```

この変数はTealium Collectピクセルのクエリ文字列に追加されます：

```html
&lt;img height=&#34;1&#34; width=&#34;1&#34; style=&#34;display:none&#34; src=&#34;//collect.tealiumiq.com/event?tealium_account={ACCOUNT}&amp;tealium_profile={PROFILE}&amp;tealium_event=user_login&amp;email_address=user@example.com&amp;cb=&#39; &#43; cb &#43; &#39;&#34;/&gt;
```

### JavaScriptの例

Tealium Collectはクロスドメインリクエストをサポートしており、以下の例のように、あなたのウェブサイトから私たちのドメインへPOSTを送信することができます：

```javascript
var event = {
    &#34;tealium_account&#34; : &#34;ACCOUNT&#34;,
    &#34;tealium_profile&#34; : &#34;PROFILE&#34;,
    &#34;tealium_event&#34;   : &#34;EVENT_NAME&#34;,
    &#34;email_address&#34;   : &#34;EMAIL_ADDRESS&#34;};
var xhr = new XMLHttpRequest();
xhr.open(&#34;POST&#34;, &#34;https://collect.tealiumiq.com/event&#34;);
xhr.send(JSON.stringify(event));
```

レスポンスヘッダーには以下が含まれます：

```javascript
Access-Control-Allow-Origin: [http://your_domain.com](http://your_domain.com)
```
