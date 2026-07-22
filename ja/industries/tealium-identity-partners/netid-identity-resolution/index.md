---
title: netID 実装ガイド
description: この記事では、Tealium Identity PartnerとしてnetIDを実装する方法について説明します。
url: https://docs.tealium.com/ja/industries/tealium-identity-partners/netid-identity-resolution/
---
ファーストパーティデータ、例えばnetIDは、正確なリターゲティングとパーソナライゼーションに不可欠です。Tealiumのリアルタイムファーストパーティデータプラットフォームは、これらの識別子をチャネル間で活用し、広告キャンペーンの効果を高めるのに役立ちます。

## 前提条件

* netIDブラウザベースのJavaScript APIへのリクエスト
* Tealium EventStreamまたはAudienceStream

## 動作原理

netIDのシングルサインオン（SSO）および同意管理ソリューションを統合する際、netIDパートナーはnetIDブラウザベースのJavaScript APIへのリクエストを実装する必要があります。APIから返されるプロパティは、ブラウザセッション内でファーストパーティクッキー、`localStorage`、または`sessionStorage`として保持される必要があります。

`tpid`のようなNetIDプロパティは、Tealium iQのクライアントサイドタグと組み合わせて、ウェブページ上の広告技術と統合するために使用できます。

さらに、同じnetIDプロパティはTealium Collectタグによって収集され、EventStreamおよびAudienceStreamの属性として利用可能になります。netIDが訪問属性として保存されると、訪問プロファイルはリアルタイムコネクタを通じて広告ベンダーにアクティブ化することができます。

netIDブラウザベースのJavaScript APIについての詳細は、以下を参照してください：

* [netID: APIから返されるデータポイント](https://developerzone.netid.dev/1.6/cmp/browser-based/#response)
* [netID: レスポンスプロパティの説明](https://developerzone.netid.dev/1.6/cmp/browser-based/#response-properties)

## Tealium iQ

ブラウザに保存されたnetIDプロパティは、データレイヤー（UDOオブジェクト）の一部として取得できます。このデータは、関連する場合にTealium iQのロードルールおよびタグデータマッピングで使用できます。

例えば、netIDの`tpid`パラメータをファーストパーティクッキーとして保持した場合、データレイヤーに新しい変数タイプ**First-Party Cookie**を追加し、**Source**の値をクッキーの名前（例：`netid_tpid`）に構成します。

![](https://docs.tealium.com/images/industries/netid-add-variable.png)

netIDパートナーとして、以下の方法のいずれかを使用して、TealiumデータレイヤーにnetIDのプロパティをキーバリューペアとして含めます：

* **First-Party-Cookie**: ブラウザに`netid_tpid`を[ファーストパーティクッキー](https://docs.tealium.com/platforms/javascript/data-layer/#cookies)として名前`netid_tpid`で保持し、Tealium標準クッキーと並んでデータレイヤーに`cp.`プレフィックスで表示されます：

  ```
  {
    ...,
    "cp.netid_tpid": "Bst040QDNr1nB9JM6sWH0I9__70JEvRyIiKvvd7G0MQLQ",
    ...
  }
  ```

* **Universal Data Object (UDO)**: [UDO変数](https://docs.tealium.com/iq-tag-management/data-layer/data-layer-variables/#udo-variable)を使用して、`utag_data`にnetIDプロパティを明示的に保持します。例えば、ページのUDOに`netid_tpid`としてnetID識別プロパティを追加します：

  ```js
  <script type="text/javascript">
    var utag_data={
        "tealium_event" : "page_view",
        "page_name"     : "product_page",
        "product_id"    : "423543",
        "netid_tpid"    : "12345"
      };
  </script>
  ```

* **イベントの追跡**: [`utag.link()`](https://docs.tealium.com/platforms/javascript/track/#track-events)を使用して、ブラウザベースのJavaScript APIからの成功したnetID認証とレスポンスを追跡し、ペイロードに`netid_tpid`として`netid_tpid`を含めます：

  ```json
  utag.link({
    "tealium_event"     : "netid_login",
    "netid_tpid"        : "12345",
    ...
  });
  ```

## EventStream API

Tealium CollectタグがブラウザのデータレイヤーからnetIDプロパティをキャプチャした後、このデータはイベント属性として処理されます。

これを行うには、`netid_tpid`値をキャプチャするイベント属性を作成します。次の例では、属性はファーストパーティクッキーの値に構成されています：

![](https://docs.tealium.com/images//industries/netid-es-add-attribute.png)

netIDの識別子（`tpid`）は、広告プラットフォームへのファーストパーティ（広告主）IDとしてアクティブ化できます。そのためのコネクタには、以下があります：

* [Adform](https://docs.tealium.com/server-side-connectors/adform-segments-connector/)
* [The Trade Desk](https://docs.tealium.com/server-side-connectors/the-trade-desk-first-party-data-connector/)

### 例

Adformを使用する場合、`netid_tpid`イベント属性をAdformのFirst-Party ID属性にマッピングします：

![](https://docs.tealium.com/images//industries/netid-es-attribute-mapping.png)

## AudienceStream CDP

このデータはイベント属性として処理され、リアルタイム訪問プロファイル上の訪問属性として保存されます。

これを行うには、訪問プロファイルの訪問文字列属性を`netid_tpid`イベント属性値に構成します。次の例では、属性はファーストパーティクッキーの値に構成されています：

![](https://docs.tealium.com/images//industries/netid-as-add-attribute.png)

訪問IDは、netIDを認証方法として使用する訪問のオーディエンスを作成するために使用できます。

![](https://docs.tealium.com/images//industries/netid-as-new-audience.png)

AdformやThe Trade Deskなどの広告プラットフォームへのリアルタイムアクティブ化には、それらのTealiumコネクタを使用します：

* [Adform](https://docs.tealium.com/server-side-connectors/adform-segments-connector/)
* [The Trade Desk](https://docs.tealium.com/server-side-connectors/the-trade-desk-first-party-data-connector/)

## 参考文献

* [netID: ブラウザベースのJavaScript API](https://developerzone.netid.dev/1.6/cmp/browser-based/)
* [Adform: セグメントコネクタ](https://docs.tealium.com/server-side-connectors/adform-segments-connector/)
* [Adform: ファーストパーティIDの使用](https://www.adformhelp.com/hc/en-us/articles/9740579323153-Use-First-Party-IDs-for-Site-Tracking)
* [The Trade Deskファーストパーティデータコネクタ](https://docs.tealium.com/server-side-connectors/the-trade-desk-first-party-data-connector/)
* [Tealiumデータレイヤー](https://docs.tealium.com/iq-tag-management/data-layer/about-the-data-layer/)