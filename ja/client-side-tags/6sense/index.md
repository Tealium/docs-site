---
title: 6senseタグ
description: この記事では、6senseタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/6sense/
---
6senseは、購入者の身元、ニーズ、購入時期を完全に可視化し、マーケティングチームと営業チームを支援します。

## タグに関するヒント

マッピングを使用して、以下を行います。

* 標準構成値を上書きする。
* カスタムパラメータと属性を構成する。
* 特定のタグについてのみイベントを追跡するには、**手動追跡タグ**（例：`['A', 'BUTTON']`）をマッピングする。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、以下の構成を行います。

* **イベントトラッキング顧客トークン**：自動イベントトラッキングを有効にします。6senseのカスタマーサクセスマネージャーから提供されます。
* **Identity API組織トークン**：Company Identity APIを有効にします。6senseのカスタマーサクセスマネージャーから提供されます。
* **検出時にイベントをトリガー**：`Yes`を選択すると、タグの検出時にコールバック関数が呼び出されます。返されたJSONオブジェクトを渡す`utag.link`をトリガーします。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|   `customer_token` | 文字列 | イベントトラッキング顧客トークン |
|   `org_token` | 文字列 | Identity API組織トークン |
|  `trackedTags`  | 配列 | 手動追跡タグ |
| `setEndpoint` | 文字列 | エンドポイント |
|  `setWhitelistFields`  | 配列 | ホワイトリストフィールド |
|  `setCustomMetatags`  | 配列 | カスタムメタタグ |
| `setPageAttributes.param` | 文字列 | ページ属性 |
|   `setThirdPartyValues.vendor` | 文字列 | サードパーティ分析 |
| `enableCompanyDetails`  | ブール値 | データ取得を有効化 |
|  `enableEventTracking`  | ブール値 | イベントトラッキングを有効化 |
|  `triggerEvent`  | ブール値 | 検出時にイベントをトリガー |