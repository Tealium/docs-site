---
title: Tealium Collectタグの追加と構成
description: この記事では、データレイヤーのエンリッチメントを有効にするためにTealium Collectタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/tealium-collect-dle/
---
詳細な手順については、[Tealium Collectタグ構成ガイド](https://docs.tealium.com/tealium-collect-tag/)を参照してください。


<blockquote>
この構成はTealium iQでクライアントサイド属性同期を有効にします。データレイヤーエンリッチメントAPIおよびプロファイル定義APIは、別のサーバーサイド構成によって制御されます。詳細については、[サーバーサイドデータレイヤーエンリッチメントを有効にする](https://docs.tealium.com/enable-data-layer-enrichment/)を参照してください。
</blockquote>


![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-tealiumcollecttagconfiguration.png)

## データエンリッチメントの頻度

Tealium Collectタグを構成してデータレイヤーエンリッチメントを有効にするには、属性情報でデータレイヤーをどのくらいの頻度で更新するかを決定する必要があります。こちらがオプションです：

* **なし**（デフォルト）
  * データレイヤーエンリッチメントは行われません。
* **まれ**
  * データレイヤーエンリッチメントは訪問（セッション）ごとに1回行われます。
  * 取得した顧客データはローカル保存に保存され、セッション中の後続のトラッキングコールで使用されます。
* **頻繁**（推奨）
  * データレイヤーエンリッチメントはすべてのトラッキングコールで行われます。セッション中に変更された顧客データは、リアルタイムでユニバーサルデータオブジェクト（UDO）に反映されます。  
  
<blockquote>
このオプションはページごとに追加のHTTPリクエストを発生させます。
</blockquote>


## ロードルールの選択

Tealium Collectタグについては、デフォルトの**すべてのページでロード**ルールを選択したままにすることをお勧めします。データレイヤーに必要な属性が含まれるように、最も関連性の高いデータでそれを満たしてください。

### Tealium iQでAudienceStream属性を使用する

AudienceStream属性はTealium iQでインポートされた変数として扱われます。これらの変数は編集または削除することはできません。AudienceStream属性を削除または変更するには、AudienceStreamプロファイルで変更を行います。属性は[プロファイルライブラリ](https://docs.tealium.com/about-profile-libraries/)にはインポートできず、通常のプロファイルにのみインポートできます。

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-editaudiencestreamvariables.png)

### どのAudienceStream属性タイプがインポートされますか？

以下の属性タイプがTealium iQにインポートされ、データレイヤーで利用可能になります：

* バッジ
* 数値
* 文字列
* ブール値
* 日付  


<blockquote>
日付属性はデータレイヤーにインポートされ、UDOで表示されますが、ロードルールやタグマッピングで使用することはできません。
</blockquote>


## ロードルールの構築

サポートされている属性を使用してロードルールを作成できます。以下のルール演算子がバッジのロードルールで利用可能です。

* **バッジが割り当てられている**  
訪問にバッジ属性が割り当てられている場合は`True`です。  
      ![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-badgeisorisnotassigned.png)
* **バッジが割り当てられていない**  
訪問にバッジ属性が割り当てられていない場合は`False`です。


<blockquote>
AudienceStreamから属性を削除すると、Tealium iQのデータレイヤースクリーンから自動的に削除されます。ただし、削除された属性を参照するロードルールは自動的に更新されません。削除された属性をまだ参照しているロードルールを手動で更新する必要があります。
</blockquote>


## コールバック関数

データレイヤーエンリッチメントリクエストは、レスポンスに基づいてコードを実行することができるコールバックメソッド`window.tealium_enrichment()`を提供します。

コールバック関数を使用するには、次のコードを含む[JavaScript Code extension](https://docs.tealium.com/advanced-javascript-code-extension/)をPre Loaderにスコープする必要があります：

```js
window.tealium_enrichment = function(data) {
    console.log("Data Layer Enrichment Callback");
    // ここにコードを記述...
};
```