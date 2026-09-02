---
title: Adobe Target タグ構成ガイド
description: この記事では、Adobe Target タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-target/
---
Adobe Target は、マーケターがオンラインコンテンツやオファーを顧客にとってより関連性の高いものにし続けるために必要な機能を提供します。これにより、より高いコンバージョンが期待できます。

## タグのヒント

* このテンプレートには utag のバージョン v4.26 以上が必要です。`utag.js` テンプレートの更新についての詳細は、ナレッジベースの記事 [utag.js の最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470) を参照してください。
* Adobe Experience Cloud ID サービスを使用する場合は、このタグの**前に** Adobe Experience Cloud ID サービスタグを追加してください。
* [Adobe Target Extension](https://docs.tealium.com/adobe-target-extension/) をこのタグに適用してください。
* **タイムアウト** 構成は、Target サーバーが応答していない場合の安全策です。最適なパフォーマンスのために、この値を 5000 ms 未満に構成しないでください。
* このタグではアンバンドリングはサポートされていません。**バンドルフラグ** を `No` に構成しても、`Yes` に上書きされます。
* `getOffers` から受け取ったレスポンスオブジェクトは `u.offersReceived` 配列に格納されます。

### getOffers レスポンスオブジェクトの例

`getOffers` からのレスポンスの内容は以下のようになります：

```
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "anytown",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "countryname"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

このレスポンスは `u.offersResponse` 配列に格納されます。その後、`u.applyOffers()` 関数が呼び出され、`u.offersResponse` 配列を解析し、解析された各オファーを Adobe Target の `aaplyOffers()` メソッドに渡します。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加してください。タグの追加方法についての詳細は、[タグの管理](https://docs.tealium.com/manage-tags/) を参照してください。

タグを追加する際には、以下の構成を構成してください：

* **コードバージョン**: 使用する Adobe Target のバージョン。詳細については、[Adobe Target バージョンの詳細](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/target-atjs-versions.html) を参照してください。
* **クライアントコード**: クライアント名（例：`mycompany` in the `mycompany.tt.omtrdc.net`）
* **タイムアウト**: この値を `5000` 以上に構成してください。これは、Target サーバーからの応答を待つ時間（ミリ秒単位）です。
* **Adobe Org ID**: Adobe Target と Site Catalyst での訪問トラッキングに使用されます。`mbox.js` の `var imsOrgId = 'XXXXXXXXXXXXXXXXXXXXXXXX@AdobeOrg'` で見つかります。
* **ライブラリエンドポイントパス**: ライブラリ呼び出しのパス変数（通常は変更の必要はありません）。
* **オーサリングスクリプトURL**: ターゲットコンテンツをオーサリングする場合は、オーサリングスクリプトの URL を入力してください（例：`//cdn.tt.omtrdc.net/cdn/target-vec.j`）。
* **グローバル mbox の自動作成**: グローバルに隠された mbox を自動的に作成するかどうか。他の場所で mbox を実装している場合は、これを `false` に構成してください。
* **グローバル mbox 名**: Adobe は通常 `target-global-mbox` をグローバルに隠された mbox の名前として使用します。このタグは自動的に mboxCreate を呼び出してこの mbox を作成します。

## 読み込みルール

すべてのページでタグを読み込むか、タグが読み込まれる条件を構成してください。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/) を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/) を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `config.clientCode` | | クライアントコード。  |
|  `config.imsOrgId` | |  Adobe 組織 ID。  |
|  `config.serverDomain` | | サーバードメイン。Adobe Target リクエストが送信されるドメイン。  |
|  `config.crossDomain` | | クロスドメインを有効にする。  |
|  `config.timeout` | | Target タイムアウト。  |
|  `config.globalMboxName` | | グローバル Mbox 名。  |
|  `config.globalMboxAutoCreate` | Boolean | グローバル Mbox 作成を有効にする。  |
| `config.endpoint` | | ライブラリエンドポイントパス。  | 
| `config.defaultContentHiddenStyle` | | デフォルトのコンテンツ非表示スタイル。  | 
| `config.defaultContentVisibleStyle` | | デフォルトのコンテンツ表示スタイル。  | 
| `config.bodyHiddenStyle` | | BODY 要素を隠す際に使用するスタイル。デフォルト値は `body{opacity:0}` です。 | 
|  `config.bodyHidingEnabled` | Boolean | BODY 隠しを有効にする。この構成を有効にすると、ウィンドウのちらつきを防ぐために BODY 要素が隠されます。 |
| `config.deviceIdLifetime` | Number | デバイス ID の寿命。  | 
| `config.sessionIdLifetime` | Number | セッション ID の寿命。  | 
| `config.selectorsPollingTimeout` | Number | セレクターのポーリングタイムアウト。  | 
|  `config.visitorApiTimeout` | Number | 訪問 API のタイムアウト。  |
|  `config.overrideMboxEdgeServer` | | Mbox エッジサーバーのオーバーライドを有効にする。  |
|  `config.overrideMboxEdgeServerTimeout` | Number | Mbox エッジサーバーのオーバーライドタイムアウト。  |
|  `config.optoutEnabled` | Boolean | オプトアウトを有効にする。  |
| `config.optinEnabled` | Boolean | オプトインを有効にする。  | 
| `config.secureOnly` | Boolean | セキュアなリクエストのみ。  | 
| `config.pageLoadEnabled` | Boolean | ページ読み込みを有効にする。  | 
|  `config.viewsEnabled` | Boolean | ビューを有効にする。  |
| `config.authoringScriptUrl` | | オーサリングスクリプト URL  | 
|`config.decisioningMethod` | | 決定方法。  |
| `config.aepSandboxId` | String | Aep サンドボックス ID。 |
| `config.aepSandboxName` | String | Aep サンドボックス名。 |

### トラックイベント

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `evt.mbox` |String | Mbox 名。  | 
|  `evt.selector` |String |CSS セレクター。  |
|  `evt.type` |String |HTML イベントタイプ。  |
| `evt.preventDefault` |Boolean |デフォルトの動作を防ぐ。  | 
| `evt.params` | Object | Mbox パラメータ。   |
| `evt.params.###` | String | カスタム mbox パラメータ。`###` をパラメータ名に置き換えてください（例：`evt.params.param1`）。  | 
| `evt.timeout` | Integer | タイムアウト。   | 
|  `evt.success` | Function | 成功関数。  |
|  `evt.error` | Function | エラー関数。  |

### パラメータ

パラメータ変数名の `###` はプレースホルダーです。カスタムパラメータ名で置き換えてください。たとえば、現在のページのすべての mbox に `param1` というパラメータを渡すには、変数を `targetPageParams.param1` にマッピングします。

| 変数 | 説明 |
|:---------|:------------|
| `mboxParams.###` | `###` をパラメータ名に置き換えてください（例：`mboxParams.param1`）。 |
| `targetPageParamsAll.###` | すべての mbox に渡されるカスタムパラメータ。`###` をパラメータ名に置き換えてください（例：`targetPageParamsAll.param1`）。 |
|  `targetPageParams.###` | グローバル mbox に渡されるカスタムパラメータ。`###` をパラメータ名に置き換えてください（例：`targetPageParams.param1`）。 |
| `targetPageParams.at_property` | Adobe Target ワークスペースプロパティトークン。 |


### 複数のオファーとSPA

| 変数 | 説明 |
|:---------|:------------|
|  `request_type`  | [prefetchまたはexecute] オファー取得リクエストタイプ |
| `offers.fetchViews` |すべてのビューを取得 |
|  `offers.consumerId` |消費者ID |
|  `offers.timeout` |リクエストタイムアウト |
| `offers.id.tntId` |リクエストID - tntId |
|  `offers.id.thirdPartyId` |リクエストID - thirdPartyId |
|  `offers.id.marketingCloudVisitorId` |リクエストID - marketingCloudVisitorId |
|  `offers.experienceCloud.analytics.logging` |Adobe Analytics統合 - ロギングタイプ |
|  `offers.views`  | ビュー配列 - 配列 |
|  `offers.pageLoad`  | PageLoadオブジェクト - オブジェクト |
|  `offers.mboxes`  | Mboxes配列 |
|  `offers.decisioningMethod` |意思決定方法 |
|  `selector`  | CSSセレクター - 配列 |
| `offersResponse` |レスポンスオブジェクト |
| `viewName` |ビュー名 |
|  `countPage`  | インプレッション数を増やす - ブール値 |