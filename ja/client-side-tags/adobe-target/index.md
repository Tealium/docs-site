---
title: Adobe Targetタグ構成ガイド
description: この記事では、Adobe Targetタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-target/
---
Adobe Targetは、オンラインコンテンツやオファーを顧客にとってより関連性の高いものへ継続的に改善し、コンバージョンを向上させるために必要な機能をマーケターに提供します。

## タグに関するヒント

* このテンプレートには、utagバージョンv4.26以降が必要です。`utag.js`テンプレートの更新について詳しくは、ナレッジベースの記事「[utag.jsを最新バージョンに更新するためのベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)」を参照してください。
* Adobe Experience Cloud ID Serviceを使用する場合は、このタグの**前に**Adobe Experience Cloud ID Serviceタグを追加してください。
* [Adobe Target拡張機能](https://docs.tealium.com/adobe-target-extension/)のスコープをこのタグに構成してください。
* **Timeout**構成は、Targetサーバーが応答しない場合に備えたフェイルセーフです。最適なパフォーマンスを得るため、この値を5000ミリ秒未満に構成しないでください。
* このタグではバンドル解除はサポートされていません。**Bundle Flag**を`No`に構成した場合、その値は`Yes`で上書きされます。
* `getOffers`から受信したレスポンスオブジェクトは、`u.offersReceived`配列に格納されます。

### getOffersレスポンスオブジェクトの例

`getOffers`から返されるレスポンスの内容は、次のようになります。

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

このレスポンスは`u.offersResponse`配列に格納されます。次に、`u.applyOffers()`関数が呼び出されて`u.offersResponse`配列が解析され、解析された各オファーを渡すためにAdobe Targetの`aaplyOffers()`メソッドが呼び出されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **Code Version**：使用するAdobe Targetのバージョン。詳しくは、[Adobe Targetのバージョン詳細](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/target-atjs-versions.html)を参照してください。
* **Client Code**：クライアント名（たとえば、`mycompany.tt.omtrdc.net`の`mycompany`）。
* **Timeout**：この値を`5000`以上に構成します。Targetサーバーが応答していないと判断するまで、Targetからのレスポンスを待機する時間（ミリ秒単位）です。
* **Adobe Org ID**：Adobe TargetとSite Catalystにまたがる訪問トラッキングで使用します。`mbox.js`内の`var imsOrgId = 'XXXXXXXXXXXXXXXXXXXXXXXX@AdobeOrg'`で確認できます。
* **Library Endpoint Path**：ライブラリ呼び出し内のパス変数です（通常、変更する必要はありません）。
* **Authoring Script URL**：ターゲットコンテンツを作成する場合は、オーサリングスクリプトのURLを入力します（例：`//cdn.tt.omtrdc.net/cdn/target-vec.j`）。
* **Auto Create Global mbox**：グローバルに非表示となるmboxを自動的に作成するかどうかを指定します。mboxを別の場所で実装する場合にのみ、これを`false`に構成してください。
* **Global mbox Name**：Adobeでは通常、グローバルに非表示となるmboxの名前として`target-global-mbox`を使用します。このタグはmboxCreateを自動的に呼び出して、このmboxを作成します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳しくは、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `config.clientCode` | | クライアントコード。 |
| `config.imsOrgId` | | Adobe組織ID。 |
| `config.serverDomain` | | サーバードメイン。Adobe Targetリクエストの送信先となるドメイン。 |
| `config.crossDomain` | | クロスドメインを有効にします。 |
| `config.timeout` | | Targetのタイムアウト。 |
| `config.globalMboxName` | | グローバルMbox名。 |
| `config.globalMboxAutoCreate` | Boolean | グローバルMboxの作成を有効にします。 |
| `config.endpoint` | | ライブラリエンドポイントのパス。 |
| `config.defaultContentHiddenStyle` | | コンテンツを非表示にするデフォルトのスタイル。 |
| `config.defaultContentVisibleStyle` | | コンテンツを表示するデフォルトのスタイル。 |
| `config.bodyHiddenStyle` | | bodyを非表示にするスタイル。BODY要素を非表示にするときに使用するスタイルです。デフォルト値は`body{opacity:0}`です。 |
| `config.bodyHidingEnabled` | Boolean | bodyの非表示を有効にします。この構成を有効にすると、画面のちらつきを防ぐためにBODY要素が非表示になります。 |
| `config.deviceIdLifetime` | Number | デバイスIDの有効期間。 |
| `config.sessionIdLifetime` | Number | セッションIDの有効期間。 |
| `config.selectorsPollingTimeout` | Number | セレクターのポーリングタイムアウト。 |
| `config.visitorApiTimeout` | Number | Visitor APIのタイムアウト。 |
| `config.overrideMboxEdgeServer` | | Mbox Edge Serverのオーバーライドを有効にします。 |
| `config.overrideMboxEdgeServerTimeout` | Number | Mbox Edge Serverのオーバーライドのタイムアウト。 |
| `config.optoutEnabled` | Boolean | オプトアウトを有効にします。 |
| `config.optinEnabled` | Boolean | オプトインを有効にします。 |
| `config.secureOnly` | Boolean | セキュアなリクエストのみに限定します。 |
| `config.pageLoadEnabled` | Boolean | ページ読み込みを有効にします。 |
| `config.viewsEnabled` | Boolean | ビューを有効にします。 |
| `config.authoringScriptUrl` | | オーサリングスクリプトのURL。 |
| `config.decisioningMethod` | | 意思決定方法。 |
| `config.aepSandboxId` | String | AEPサンドボックスID。 |
| `config.aepSandboxName` | String | AEPサンドボックス名。 |

### イベントのトラッキング

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `evt.mbox` | String | Mbox名。 |
| `sevt.elector` | String | CSSセレクター。 |
| `evt.type` | String | HTMLイベントタイプ。 |
| `evt.preventDefault` | Boolean | prevent defaultを使用します。 |
| `evt.params` | Object | Mboxパラメーター。 |
| `evt.params.###` | String | カスタムmboxパラメーター。`###`をパラメーター名に置き換えます（例：`evt.params.param1`）。 |
| `evt.timeout` | Integer | タイムアウト。 |
| `evt.success` | Function | 成功時に実行する関数。 |
| `evt.error` | Function | エラー時に実行する関数。 |

### パラメーター

パラメーター変数名の`###`はプレースホルダーです。カスタムパラメーター名に置き換えてください。たとえば、`param1`という名前のパラメーターを現在のページ上のすべてのmboxに渡すには、変数を`targetPageParams.param1`にマッピングします。

| 変数 | 説明 |
|:---------|:------------|
| `mboxParams.###` | `###`をパラメーター名に置き換えます（例：`mboxParams.param1`）。 |
| `targetPageParamsAll.###` | すべてのmboxに渡されるカスタムパラメーター。`###`をパラメーター名に置き換えます（例：`targetPageParamsAll.param1`）。 |
| `targetPageParams.###` | グローバルmboxに渡されるカスタムパラメーター。`###`をパラメーター名に置き換えます（例：`targetPageParams.param1`）。 |
| `targetPageParams.at_property` | Adobe Targetワークスペースのプロパティトークン。 |
### 複数のオファーとSPA

| 変数 | 説明 |
|:---------|:------------|
| `request_type` | ［prefetchまたはexecute］オファー取得リクエストタイプ |
| `offers.fetchViews` | すべてのビューを取得 |
| `offers.consumerId` | コンシューマーID |
| `offers.timeout` | リクエストタイムアウト |
| `offers.id.tntId` | リクエストID - tntId |
| `offers.id.thirdPartyId` | リクエストID - thirdPartyId |
| `offers.id.marketingCloudVisitorId` | リクエストID - marketingCloudVisitorId |
| `offers.experienceCloud.analytics.logging` | Adobe Analytics統合 - ログタイプ |
| `offers.views` | ビュー配列 - 配列 |
| `offers.pageLoad` | PageLoadオブジェクト - オブジェクト |
| `offers.mboxes` | Mbox配列 |
| `offers.decisioningMethod` | 判定方法 |
| `selector` | CSSセレクター - 配列 |
| `offersResponse` | レスポンスオブジェクト |
| `viewName` | ビュー名 |
| `countPage` | インプレッション数を増加 - ブール値 |