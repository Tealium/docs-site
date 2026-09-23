---
title: 制限データについて
description: 制限データは、機密データを含む属性を識別するプロパティです。
url: https://docs.tealium.com/ja/server-side/attributes/restricted-data/
---
## 制限データとは何ですか？

制限データは、以下のデータを含む属性を指します：

* ✔ プライベートまたは個人的な情報
* ✔ プライバシー法によって保護されている
* ✔ アクセスが制御されている

デフォルトでは、属性は制限されておらず、さまざまな宛先に流れることがあります。属性には**制限データ**という構成があり、これにより一部のプロセスでデータがCustomer Data Hubから送信されるのを防ぎます。属性のエンリッチメントは影響を受けません。

## 制限属性の特定

左のナビゲーションパネルのフィルターを使用して、リストしたい属性のタイプを選択できます。制限データを持つ属性を特定するには、**制限データ**チェックボックスをクリックします。

![](https://docs.tealium.com/images/server-side/restricted-attributes-filter.png)

属性の詳細を編集する際、適用される場合にはプロパティセクションに**制限データ**フィールドが表示されます。属性を制限データとしてマークしたい場合は、このボックスをチェックします。

![](https://docs.tealium.com/images/server-side/restricted-attributes-checkbox-example.png)

## 制限属性

制限データの構成は、以下のサービスに適用されます：

* **EventStoreおよびEventDB**  
デフォルトでは、制限属性はイベントフィードから省略されます。この動作は各フィードの構成で変更できます。
<blockquote>
データソースとしてイベントフィードを使用するコネクタは、イベントフィードの構成に関わらず常に制限属性を受け取ります。
</blockquote>

* **Data Layer Enrichment**  
デフォルトでは、制限属性はAudienceStreamを使用したデータレイヤーエンリッチメントでページ上のデータレイヤーに返される訪問属性から省略されます。Tealium Collectタグが最新の訪問プロファイルを要求すると、AudienceStreamは制限されていない属性を返します。この動作は変更できません。
* **Context API**  
デフォルトでは、制限属性はエンジンのレスポンスに含めることができません。認証を要求するように構成されたエンジンは、エンジン構成で**Allow PII**が有効になっている場合、制限属性を含めることができます。詳細については、[Manage Context API engines](https://docs.tealium.com/context-api-manage-engines/)を参照してください。

制限データの構成は、以下のサービスには適用されません：

* **AudienceStoreおよびAudienceDB**  
デフォルトでは、制限属性は常に含まれます。AudienceDBに送信されるか、AudienceStoreコネクタを使用してエクスポートされるかに関わらず、この動作は変更できません。
* **Connectors（Webhookを含む）**  
デフォルトでは、制限属性は常に含まれます。マッピングを通じてベンダーに送信されるか、訪問プロファイルの一部として送信されるかに関わらず、この動作は変更できません。

<blockquote>
コネクタリクエストに1つ以上の制限属性が含まれている場合、警告メッセージが表示されます。
</blockquote>


## まとめ

* 属性を制限データとしてマークすることで、選択したTealiumサービスへの送信を防ぎます。
* EventStore、EventDB、Data Layer Enrichment、およびContext APIはデフォルトで制限データを尊重します。
* 認証を要求するContext APIエンジンは、**Allow PII**が有効になっている場合、制限属性を含めることができます。
* AudienceStore、AudienceDB、およびConnectorsは制限データを尊重しません。
* 制限属性はすべてのエンリッチメントで利用可能です。