---
title: Tealium Collect HTTP APIについて
description: HTTP APIを使用して、HTTPリクエストを送信できる任意のアプリケーションからイベントを送信します。
url: https://docs.tealium.com/ja/api/v3/http-api/about/
---
## 動作原理

Tealium Collect HTTP APIは、データ収集のためのGETおよびPOSTメソッドをサポートする認証済みエンドポイントです。認証されていないエンドポイントについては、[HTTP API v1](/ja/platforms/http-api/)を参照してください。

```
https://collect.tealiumiq.com/v3/collect/event
```

セッションは[訪問スコープ]()属性プロパティに基づいて決定されます。

### 地域およびグローバルエンドポイント

HTTP APIは、アカウントとプロファイルの地域を認識するクロスリージョナルエンドポイントです。

HTTP APIは以下の2つのホストをサポートしています：

* `collect.tealiumiq.com`  
最も近いサーバー（最も低い遅延を持つサーバー）にイベントを送信します。
* `collect-&lt;region&gt;.tealiumiq.com`  
プロファイルの地域のサーバーにイベントを送信します。

認証済みエンドポイントの場合、グローバルエンドポイントは内部的に`collect.tealiumiq.com`に、地域エンドポイントは`collect-&lt;region&gt;.tealiumiq.com`にマッピングされます。

### レート制限

HTTP APIは、最大100イベント/秒のレート制限をサポートしています。

例えば、以下のように送信する場合：

* 1回の呼び出しにつき1イベントの場合、100回/秒を送信できます。
* 1回の呼び出しにつき10イベントの場合、10回/秒を送信できます。

レート制限を超えると、TealiumはHTTP 429レスポンスを返して、リクエストが多すぎることを示します。

イベントの上限を増やす必要がある場合は、Tealiumアカウントマネージャーに連絡してください。

## エンドポイント

さまざまなデータ収集目的のために提供されるエンドポイントは以下の通りです：

### イベント

標準データ収集のためのGETおよびPOSTリクエストをサポートするRESTfulエンドポイントです。

| タイプ | エンドポイント |
|----- | -------- | 
| 認証済みグローバルエンドポイント |  `/v3/collect/event` |
| 認証済み地域エンドポイント | `/v3/collect/regional/event` |

### バルクイベント

複数のイベント（最大10）を単一のリクエストでサポートするPOSTリクエストのRESTfulエンドポイントです。

| タイプ | エンドポイント |
|----- | -------- | 
| 認証済みバルクグローバルエンドポイント | `/v3/collect/bulk-event` |
| 認証済みバルク地域エンドポイント | `/v3/collect/regional/bulk-event` |

### インテグレーション

[incoming webhooks](/ja/server-side/data-sources/webhooks/)によって使用されるRESTfulエンドポイントです。

| タイプ | エンドポイント |
|----- | -------- | 
| 認証済みグローバルエンドポイント |  `/v3/collect/integration/event/accounts/{account}/profiles/{profile}/datasources/{datasourceID}` |
| 認証済み地域エンドポイント | `/v3/collect/regional/integration/event/accounts/{account}/profiles/{profile}/datasources/{datasourceID}` |

## 訪問識別子

以下の組み合わせを使用して訪問を識別します：

* **匿名ID**：訪問を匿名で追跡するために使用されるID（例えば、デバイスやブラウザから）。[既知の訪問](#known-visitors-server-to-server)の場合は、ユーザー識別子に基づいて値を使用します。
* **ユーザー識別子**：訪問が既知の場合に送信されます。特定のデバイスではなくユーザーを識別する値に基づいています。

### 匿名ID

匿名IDは、Tealiumがイベントと訪問の間で訪問を関連付けるために使用する匿名識別子です。この値がGUIDであり、訪問に対して一貫性があることを確認してください。

匿名IDのキー名は`tealium_visitor_id`です。

ビジネスケースに応じて、匿名値または既知のユーザー識別子に基づく値を使用します。

#### 匿名値

|AudienceStream| EventStream|
|---| ---|
| 必須 | N/A |

Tealium iQタグ管理を使用してAPIコールをサーバー間で送信し、匿名訪問プロファイルをエンリッチする場合、`tealium_visitor_id`の値は`utag_main_v_id`クッキーの値と一致する必要があります。utag.jsの組み込み変数についての詳細は、[JavaScript (Web) &gt; Data Layer]()を参照してください。

Adobe LaunchまたはGoogle Tag Managerを使用している場合、値は**TEAL**クッキーの`v`部分と一致する必要があります。

#### 既知の訪問サーバー間

|AudienceStream| EventStream|
|---| ---|
| 必須 | 推奨 |

訪問ID属性（例：`email_address`）の値が存在する既知の訪問のデータを送信する場合、以下の値を`__ACCOUNT_PROFILE__ATTRIBUTE-ID_ATTRIBUTE-VALUE__`の形式で連結します：

* アカウント
* プロファイル
* 訪問ID属性IDおよび値 訪問ID属性IDは、属性リストの属性名の隣または詳細情報内で見つけることができます。詳細については、[属性について]()を参照してください。

例えば、以下の値がある場合：

* アカウント名：`my-account`
* プロファイル：`main`
* 訪問ID属性ID：`7688`
* 訪問ID属性値：`45653454`

連結された値は：

```
&#34;tealium_visitor_id&#34;:&#34;__my-account_main__7688_45653454__&#34;
```

`tealium_visitor_id`が正しくフォーマットされていることを確認してから進めてください。フォーマットが正しくないパラメータはAudienceStreamでの追跡にエラーを引き起こし、適切に追跡されない可能性があります。

例 JSON：

```json
{
    &#34;tealium_account&#34;    : &#34;my-account&#34;,
    &#34;tealium_profile&#34;    : &#34;main&#34;,
    &#34;tealium_event&#34;      : &#34;user_login&#34;,
    &#34;email_address&#34;      : &#34;user@example.com&#34;,
    &#34;tealium_visitor_id&#34; : &#34;__my-account_main__7688_45653454__&#34;
}
```

匿名訪問または既知の訪問を使用する場合でも、APIコールに一貫した`tealium_visitor_id`が含まれていないと、各イベントが新しい訪問を生成し、訪問のスティッチングが不可能になります。

### ユーザー識別子

AudienceStreamを使用する場合、トラッキングコールに既知のユーザー識別子（例：`email_address`または`login_id`）を渡します。

EventStreamを使用していて、ベンダーコネクタにIDを提供する必要がある場合も、ユーザー識別子が必要です。

AudienceStreamでは、これらのユーザー識別子を使用して[訪問ID属性]()を豊かにします。

## 権限要件

* サーバーサイドパブリッシャーの権限

## 認証

すべてのAPIコールを認証するためにはベアラートークンが使用され、APIキーは認証コールでのみ使用されます。ベアラートークンに加えて、認証レスポンスには、後続のサーバーサイドAPIコールで使用する必要がある地域固有のホスト名が含まれています。

APIキーからベアラートークンを生成する方法については、[認証]()を参照してください。