---
title: Webhook Krux（非推奨）
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/vendor-examples/webhook-krux-deprecated/
---
Krux Webhookは非推奨の機能であり、[Salesforce Audience Studio Connector]()に置き換えられました。

----

前提条件:

* [Webhook Send Custom Action]()

この記事では、AudienceStream Webhook Connectorを使用してKruxにオーディエンスデータを送信する方法について説明します。

## 概要

このソリューションは、iQおよびCustomer Data Hubの以下のコンポーネントを組み合わせています:

* iQ内のKruxタグ
* iQ内のPersist Data Value拡張機能
* Customer Data Hub内のVisitor Attribute
* Customer Data Hub内のWebhook

## iQタグ管理

### Kruxコントロールタグを追加

iQタグ管理タグマーケットプレイスからKruxコントロールタグを追加します。Kruxから提供されたKrux Configuration IDでタグを構成します。

![](/images/server-side/kruxtag.png)

### KruxユーザーIDでCookieを構成

Webhookコネクタを通じて送信するユーザーをKruxユーザーと照合するために、Kruxコントロールタグによって生成されたKruxオブジェクトからKruxユーザーIDを抽出する必要があります。Kruxオブジェクトの命名規則はクライアントごとに異なります。ユーザーIDを抽出するコードは `Krux.ns.CLIENT(&#39;get&#39;, &#39;user&#39;)` のようになります。ここで、CLIENTはあなたのKruxクライアント名です。このオブジェクトの命名規則についてはKrux担当者に尋ねるか、[Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/) Consoleで `Krux.ns` と入力して結果のオブジェクトを調べることができます。

Kruxクライアント名を取得したら、以下の手順でKruxユーザーIDをCookieに保存します:

1. Tealium iQタグ管理の[Data Layer]()に2つの変数を追加します。
    * `krux_id` を [UDO Variable]()のタイプで
    * `utag_main_krux_id` を [First Party Cookie]()のタイプで

1. [Set Data Values Extension]()を追加して、上記の拡張機能から`krux_id`にKruxオブジェクトユーザーIDを抽出します。この拡張機能の**実行**を「タグの後」に構成します。これにより、KruxコントロールタグがKruxオブジェクトを作成する機会を与えます。
    この拡張機能の条件を、`utag_main_krux_id`クッキーがまだ構成されていない場合にのみ変数を構成するように構成します。
  
    ![](/images/server-side/krux-set-data-values)

1. [Persist Data Value Extension]()を追加して、上記の拡張機能から`krux_id`をクッキーに保存します。
このクッキーを保存する条件を、`krux_id`変数が入力され、最初に構成された値を保持するように構成します。

![](/images/server-side/krux-persist)

## Customer Data Hub

### KruxユーザーIDでVisitor Attributeを構成

&#34;Krux ID&#34;という名前のVisitorスコープのString Attributeを作成します。この属性を`utag_main_krux_id`クッキーから取得します。

![](/images/server-side/krux-id-attribute.png)

### Krux HTTP API Webhookを追加

このセクションでは、[Webhook Send Custom Request Action]()を使用してKruxコネクタを作成するために必要なパラメータを定義します。

ベンダー文書: [Krux Mobile HTTP API](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API)

* **Method**: GET
* **URL**: `https://beacon.krxd.net/pixel.gif&amp;amp;tech_browser_lang=en`
* **URLパラメータ**:
|Mapped Attribute| Kruxパラメータ| 説明|
|---| ---| ---|
|&amp;lt;Custom Value&amp;gt;| _kpid| パブリッシャーUUID（Krux提供）|
|&amp;lt;Custom Value&amp;gt;| _kcp_d| ドメイン（Krux提供）|
|&amp;lt;Custom Value&amp;gt;| _kcp_s| サイト（Krux提供）|
|Krux ID| _kuid| Krux ID Visitor Attribute|
|&amp;lt;Custom Value&amp;gt;| _kua_&amp;lt;krux_user attribute_name&amp;gt;|  Kruxで構成されたカスタムユーザー属性。例: _kua_cartAbandoner) |

![](/images/server-side/connector.png)
