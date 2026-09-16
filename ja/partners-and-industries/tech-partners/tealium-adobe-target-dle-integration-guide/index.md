---
title: Tealium + Adobe Target 統合ガイド
description: データレイヤーのエンリッチメントを使用して、Adobe Targetに訪問データを注入し、クライアントサイドでのパーソナライゼーションを実現します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-adobe-target-dle-integration-guide/
---
## 概要

このガイドを使用して、Tealiumからの訪問オーディエンス、バッジ、およびプロパティを使用してAdobe Targetのエクスペリエンスをパーソナライズします。この統合はセッション中にクライアントサイドで実行され、サーバーサイドのコネクタは必要ありません。データレイヤーのエンリッチメント（DLE）により、訪問データがブラウザで利用可能になり、Adobe Targetの`dataProviders`フックを使用して、`at.js`が起動する前にmboxリクエストにそのデータを渡すことができます。

## 要件

この統合には以下が必要です：

* Tealium CDPプロファイルがアクティブであり、訪問および訪問属性が定義されていること。
* Tealiumタグ管理の公開構成でDLEが有効になっていること。詳細については、[データレイヤーのエンリッチメントを有効にする](https://docs.tealium.com/enable-data-layer-enrichment/)を参照してください。
* DLEが有効になっているすべてのページにTealium Collectタグがデプロイされていること。詳細については、[Tealium Collectタグを追加および構成する](https://docs.tealium.com/tealium-collect-tag/)を参照してください。
* Tealiumタグ管理でデータレイヤー変数として訪問属性が同期されていること。
* `at.js` 2.xを使用してAdobe Targetがデプロイされていること。


<blockquote>
`dataProviders`は`at.js` 1.3以降で利用可能です。このガイドは`at.js` 2.xを使用しており、`mbox.js`の実装には適用されません。
</blockquote>


## 動作原理

DLEがアクティブな場合、Tealium Collectタグは非同期で訪問プロファイルをフェッチし、`tealium_va`というキーの下に`localStorage`に保存します。保存された値は、`audiences`および`badges`オブジェクトを含む文字列化されたJSONオブジェクトで、属性IDによってキーが付けられた`properties`オブジェクトです。

`at.js`は`targetGlobalSettings`内に`dataProviders`構成フックをサポートしています。各`dataProviders`エントリは`name`、`version`、および`provider(callback)`を持つオブジェクトです。Adobe Targetはグローバルmboxリクエストの前にプロバイダーを実行し、コールバックに渡されたキーバリューペアをリクエストにマージします。

統合は、`tealium_va`を読み取り、それを解析し、フラット化されたキーバリューパラメーターをコールバックに渡すデータプロバイダーオブジェクトを登録します。Adobe Targetはこれらのパラメーターをmboxコールに追加してからリクエストを送信します。


<blockquote>
DLEは訪問プロファイルを非同期でフェッチします。新しい訪問の最初のページビューでは、`at.js`が起動するときに`tealium_va`が空の可能性があります。訪問データは2ページ目のビューから、またはSPAルートの変更後に利用可能になります。
</blockquote>


## データプロバイダーの追加

次のJavaScriptは`localStorage`から`tealium_va`を読み取り、データプロバイダーを登録します。プレースホルダー属性IDをAudienceStreamの文字列属性IDに置き換えてください。このコードは`at.js`が読み込まれる前に実行する必要があります。

```javascript
window.targetGlobalSettings = window.targetGlobalSettings || {};
window.targetGlobalSettings.dataProviders = window.targetGlobalSettings.dataProviders || [];

window.targetGlobalSettings.dataProviders.push({
  name: "tealium-dle",
  version: "1.0.0",
  provider: function(callback) {
    var tealiumTargetData = {};
    var attributeIdMap = {
      tealium_ltv: "ATTRIBUTE_ID_FOR_CUSTOMER_LTV",
      profile_tealium_lifecycle: "ATTRIBUTE_ID_FOR_LIFECYCLE_STAGE"
    };

    try {
      var dleString = localStorage.getItem("tealium_va");

      if (dleString) {
        var dleObject = JSON.parse(dleString);
        var audienceNames = dleObject.audiences ? Object.keys(dleObject.audiences).map(function(key) {
          return dleObject.audiences[key];
        }) : [];
        var badgeIds = dleObject.badges ? Object.keys(dleObject.badges) : [];

        if (audienceNames.length > 0) {
          tealiumTargetData["profile.tealium_audiences"] = audienceNames.join("|");
        }

        if (badgeIds.length > 0) {
          tealiumTargetData["profile.tealium_badges"] = badgeIds.join("|");
        }

        if (dleObject.properties) {
          if (dleObject.properties[attributeIdMap.tealium_ltv]) {
            tealiumTargetData.tealium_ltv = dleObject.properties[attributeIdMap.tealium_ltv];
          }
          if (dleObject.properties[attributeIdMap.profile_tealium_lifecycle]) {
            tealiumTargetData["profile.tealium_lifecycle"] = dleObject.properties[attributeIdMap.profile_tealium_lifecycle];
          }
        }
      }
    } catch (e) {
      console.error("Adobe Target Data Provider: Error parsing Tealium DLE data", e);
    }

    callback(tealiumTargetData);
  }
});
```

スニペットを次のいずれかのオプションを使用してデプロイします。

* **直接ページ配置**  
ページの`<head>`内、`at.js`を読み込む`<script>`タグの上にスニペットを追加します。
* **Tealium iQ Pre-Loader拡張機能**  
**Pre Loader**にスコープされた[JavaScript Code拡張機能](https://docs.tealium.com/javascript-code-extension/)を作成し、拡張機能エディタにスニペットを貼り付け、変更を保存して公開します。このオプションはコードをTealium内で管理します。

## パラメータータイプについて

Adobe Targetはmboxリクエストで2種類のパラメーターをサポートしています。タイプはTargetが値を保持する期間とターゲティングに利用可能な場所を決定します。

**プロファイルパラメーター**は`profile.`プレフィックスを使用します。Adobe Targetはプロファイルパラメーターを訪問のTargetプロファイルにセッション間で永続的に保存します。プロファイルパラメーター値は、`localStorage`がクリアされても利用可能です。長期的なターゲティングを駆動するオーディエンスやバッジにプロファイルパラメーターを使用します。例えば`profile.tealium_audiences`や`profile.tealium_badges`です。

**Mboxパラメーター**はプレフィックスがありません。Adobe Targetはmboxパラメーターを現在のページまたはmboxコールのみで評価します。頻繁に変更される値や現在のページビューにのみ適用される値にmboxパラメーターを使用します。例えば`tealium_ltv`です。

Adobe TargetはmboxコールでネストされたJSONを受け入れません。DLEオブジェクトからのすべての値を直接のキーバリュー文字列ペアにフラット化してから、`dataProviders`コールバックに渡します。複数値フィールドはパイプ(`|`)またはカンマ区切りで結合します。

## 関連情報

* [データレイヤーのエンリッチメントについて](https://docs.tealium.com/about-data-layer-enrichment/)
* [データレイヤーのエンリッチメントを有効にする](https://docs.tealium.com/enable-data-layer-enrichment/)
* [Tealium Collectタグを追加および構成する](https://docs.tealium.com/tealium-collect-tag/)
* [Adobe Targetタグ構成ガイド](https://docs.tealium.com/adobe-target-tag/)
* [Adobe Targetコネクタ](https://docs.tealium.com/adobe-target-connector/): 次のセッションのパーソナライゼーションやオフラインプロファイル更新にはサーバーサイドコネクタを使用します。セッション中の次ページのパーソナライゼーションには、このDLEパターンを使用します。