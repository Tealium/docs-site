---
title: Adobe Launch用Tealiumデータエンリッチメント拡張機能
description: Adobe Experience Platform Launch用Tealiumデータレイヤーエンリッチメント拡張機能について学びましょう。
url: https://docs.tealium.com/ja/platforms/adobe-launch/data-enrichment-extension/
---
Tealium Data Enrichment拡張機能は、Tealium AudienceStreamのサーバーサイド属性を取得し、データレイヤーに注入します。

Tealium Data Enrichment拡張機能をインストールするには、以下の手順を使用します：

1. Adobe Extension Catalogで**Tealium Data Enrichment**拡張機能を検索します。
1. **Install**ボタンをクリックして拡張機能を追加します。
1. **Tealium Data Enrichment**のための**Rule and Action**を追加します。
1. インストールされた拡張機能にカーソルを合わせて**Configure**をクリックし、次のオプションを構成します：
      * **Tealium Account**：（必須）あなたのTealiumアカウント名。
      * **Tealium Profile**：（必須）あなたのTealiumプロファイル名。
      * **Endpoint**：（オプション）デフォルトのエンドポイントを独自のカスタムファーストパーティエンドポイント（例：`https://visitor-service.collect.example.co.uk`）で上書きします。
1. Adobe Launchでローカル保存のデータを読み取るデータエレメントを追加します。詳細については、[Adobe: Data Elements](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements)を参照してください。

[data layer enrichment object]()は、`localStorage`の`teal_adobe_enrichment_data`キーの下に保存されます。このキーを取得すると、データレイヤーエンリッチメントオブジェクトが返されます。

次の例では、`localStorage`からデータレイヤーエンリッチメントオブジェクトを取得し、すべてのオーディエンスを配列に保存します：

```javascript
var dle_object = JSON.parse(localStorage.getItem(
   &#34;teal_adobe_enrichment_data&#34;));

var data = {audiences: []};
if (dle_object.audiences) {
  for (var id in dle_object.audiences) {
    if (dle_object.audiences.hasOwnProperty(id)) {
     data.audiences.push(id);
    }
  }
}
```

データレイヤーエンリッチメントオブジェクトにネストされた値が含まれている場合、Tealium Collectエンドポイントに送信される前に自動的にフラット化されます。

詳細については、[Adobe: Adobe Experience Platform Launch object reference](https://experienceleague.adobe.com/docs/launch/using/reference/client-side-info/launch-object-reference.html?lang=en#buildinfo)を参照してください。