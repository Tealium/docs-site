---
title: Adobe Launch向けTealium Data Enrichment拡張機能
description: Adobe Experience Platform Launch向けTealium Data Layer Enrichment拡張機能について説明します。
url: https://docs.tealium.com/ja/platforms/adobe-launch/data-enrichment-extension/
---
Tealium Data Enrichment拡張機能は、サーバー側の訪問属性と訪問属性をデータレイヤーに挿入します。

Tealium Data Enrichment拡張機能をインストールするには、次の手順を実行します。

1. Adobe Extension Catalogで**Tealium Data Enrichment**拡張機能を検索します。
1. **Install**ボタンをクリックして拡張機能を追加します。
1. **Tealium Data Enrichment**用の**Rule and Action**を追加します。
1. インストール済みの拡張機能にカーソルを合わせて**Configure**をクリックし、次のオプションを構成します。
      * **Tealium Account**：（必須）Tealiumアカウント名。
      * **Tealium Profile**：（必須）Tealiumプロファイル名。
      * **Endpoint**：（任意）デフォルトのエンドポイントを、`https://visitor-service.collect.example.co.uk`などの独自のカスタムファーストパーティエンドポイントで上書きします。
1. Adobe Launchにデータ要素を追加し、ローカル保存内のデータを読み取ります。詳細については、[Adobe：データ要素](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements)を参照してください。

[データレイヤーエンリッチメントオブジェクト](https://docs.tealium.com/configure-data-layer-enrichment-iq/)は、`teal_adobe_enrichment_data`キーを使用して`localStorage`に保存されます。このキーを取得すると、データレイヤーエンリッチメントオブジェクトが返されます。

次の例では、`localStorage`からデータレイヤーエンリッチメントオブジェクトを取得し、すべてのオーディエンスを配列に格納します。

```javascript
var dle_object = JSON.parse(localStorage.getItem(
   "teal_adobe_enrichment_data"));

var data = {audiences: []};
if (dle_object.audiences) {
  for (var id in dle_object.audiences) {
    if (dle_object.audiences.hasOwnProperty(id)) {
     data.audiences.push(id);
    }
  }
}
```


<blockquote>
データレイヤーエンリッチメントオブジェクトにネストされた値が含まれている場合、Tealium Collectエンドポイントに送信される前に自動的にフラット化されます。
</blockquote>


詳細については、[Adobe：Adobe Experience Platform Launchオブジェクトリファレンス](https://experienceleague.adobe.com/docs/launch/using/reference/client-side-info/launch-object-reference.html?lang=en#buildinfo)を参照してください。