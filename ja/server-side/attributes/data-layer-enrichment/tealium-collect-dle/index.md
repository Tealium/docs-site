---
title: Tealium Collectタグの追加と構成
description: この記事では、データレイヤーエンリッチメントを有効にするためのTealium Collectタグの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/tealium-collect-dle/
---
詳しい手順については、[Tealium Collectタグ構成ガイド](https://docs.tealium.com/tealium-collect-tag/)を参照してください。


<blockquote>
この構成により、タグ管理でクライアント側の属性同期が有効になります。Data Layer Enrichment APIとProfile Definition APIは、別のサーバー側構成によって制御されます。詳細については、[サーバー側のデータレイヤーエンリッチメントの有効化](https://docs.tealium.com/enable-data-layer-enrichment/)を参照してください。
</blockquote>


![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-tealiumcollecttagconfiguration.png)

## データエンリッチメントの頻度

データレイヤーエンリッチメントを有効にするようTealium Collectタグを構成するには、属性情報でデータレイヤーを更新する頻度を決定する必要があります。次のオプションがあります。

* **なし**（デフォルト）
  * データレイヤーエンリッチメントは実行されません。
* **低頻度**
  * データレイヤーエンリッチメントは、訪問（セッション）ごとに1回実行されます。
  * 取得した顧客データはローカル保存に保存され、セッション中の後続のトラッキング呼び出しで使用されます。
* **高頻度**（推奨）
  * データレイヤーエンリッチメントは、トラッキング呼び出しごとに実行されます。セッション中に変更された顧客データは、Universal Data Object（UDO）にリアルタイムで反映されます。  
  
<blockquote>
このオプションを選択すると、ページごとに追加のHTTPリクエストが発生します。
</blockquote>


## ロードルールの選択

Tealium Collectタグでは、デフォルトの**すべてのページで読み込む**ロードルールを選択したままにすることをお勧めします。データレイヤーに必要な属性が含まれるようにするため、最も関連性の高いデータを構成してください。

### タグ管理でのCustomer Data Platform（CDP）属性の使用

タグ管理では、CDP属性はインポートされた変数として扱われます。これらの変数は編集または削除できません。CDP属性を削除または変更するには、CDPプロファイルで変更してください。属性を[プロファイルライブラリ](https://docs.tealium.com/about-profile-libraries/)にインポートすることはできず、通常のプロファイルにのみインポートできます。

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-editaudiencestreamvariables.png)

### インポートされるCDP属性タイプ

次の属性タイプがタグ管理にインポートされ、データレイヤーで使用できるようになります。

* バッジ
* 数値
* 文字列
* ブール値
* 日付  


<blockquote>
日付属性はデータレイヤーにインポートされ、UDOに表示されます。ただし、ロードルールやタグマッピングでは使用できません。
</blockquote>


## ロードルールの作成

サポートされている属性を使用して、ロードルールを作成できます。ロードルール内のバッジでは、次のルール演算子を使用できます。

* **バッジが割り当てられている**  
バッジ属性が訪問に割り当てられている場合は`True`です。  
      ![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-badgeisorisnotassigned.png)
* **バッジが割り当てられていない**  
バッジ属性が訪問に割り当てられていない場合は`False`です。


<blockquote>
CDPから属性を削除すると、タグ管理のデータレイヤー画面からも自動的に削除されます。ただし、削除された属性を参照するロードルールは自動的には更新されません。削除された属性を引き続き参照しているロードルールは、手動で更新する必要があります。
</blockquote>


## コールバック関数

データレイヤーエンリッチメントリクエストには、レスポンスに基づいてコードを実行できるコールバックメソッド`window.tealium_enrichment()`が用意されています。

コールバック関数を使用するには、次のコードを使用して、スコープをPre Loaderに構成した[JavaScriptコード拡張機能](https://docs.tealium.com/advanced-javascript-code-extension/)を作成します。

```js
window.tealium_enrichment = function(data) {
    console.log("Data Layer Enrichment Callback");
    // Your code here...
};
```