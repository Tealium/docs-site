---
title: Decibel Insightタグ構成ガイド
description: この記事では、Decibel Insightタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/decibel-insight-tag.md/
---
## タグに関するヒント

マッピングを使用すると、アカウントIDの値を動的に上書きしたり、追加のパラメータを構成したりできます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を行います。

* **アカウントID**：DecibelのアカウントID。
* **プロパティID**：（任意）選択したWebサイトの一意のプロパティID。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `da_accountId` | アカウントID |
| `da_propertyId` | プロパティID |
| `collectionRemember` | コレクションの記憶 |
| `collectionStatus` | コレクションのステータス |
| `customer_id` | 顧客ID |
| `order_currency` | 注文通貨 |
| `errorMessage` | エラーメッセージ |
| `errorMessageCssSelector` | エラーメッセージのCSSセレクター |
| `goalName` | 目標名 |
| `goalValue` | 目標値 |
| `httpErrorCode` | HTTPエラーコード |
| `pageRole` | ページの役割 |
| `retentionStatus` | リテンションのステータス |
| `retentionRemember` | リテンションの記憶 |

### ページビュー

| 変数 | 説明 |
|:---------|:------------|
| `pageName` | ページ名 |
| `pageViewParams.title` | タイトル |
| `pageViewParams.queryString` | クエリ文字列 |
| `pageViewParams.fragment` | フラグメント |
| `pageViewParams.waitTime` | 待機時間 |

### イベント

イベントのマッピングの詳細については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `sendApplicationError` | アプリケーションエラーを送信 |
| `sendGoal` | 目標を送信 |
| `sendHTTPError` | HTTPエラーを送信 |
| `setCollection` | コレクションを構成 |
| `setRetention` | リテンションを構成 |
| `trackPageView` | ページビューを追跡 |
| `updateUserId` | ユーザーIDを更新 |

### Eコマース

| 変数 | 説明 |
|:---------|:------------|
| `customer_id`（`_ccustid`を上書き） | 顧客ID |