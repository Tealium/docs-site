---
title: Decibel Insightタグ設定ガイド
description: この記事では、Decibel Insightタグの設定方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/decibel-insight-tag.md/
---
## タグのヒント

マッピングを使用して、アカウントIDの値を動的に上書きしたり、追加のパラメータを設定したりします。

## タグの設定

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の設定を行います：

* **アカウントID**： DecibelのアカウントID。
* **プロパティID**： (オプション) 選択したウェブサイトの一意のプロパティID。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を設定します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数 | 説明 |
|:---------|:------------|
|  `da_accountId` |アカウントID  |
|  `da_propertyId` |プロパティID  |
|  `collectionRemember` |コレクションリメンバー  |
|  `collectionStatus` |コレクションステータス  |
|  `customer_id` |カスタマーID  |
|  `order_currency` |注文通貨  |
|  `errorMessage` |エラーメッセージ  |
| `errorMessageCssSelector` |エラーメッセージCSSセレクタ  | 
| `goalName` |ゴール名  | 
|  `goalValue` |ゴール値  |
|  `httpErrorCode` |HTTPエラーコード  |
|  `pageRole` |ページロール  |
|  `retentionStatus` |リテンションステータス  |
| `retentionRemember` |リテンションリメンバー  | 

### ページビュー

| 変数 | 説明 |
|:---------|:------------|
| `pageName` | ページ名| 
| `pageViewParams.title` | タイトル| 
| `pageViewParams.queryString` | クエリストリング| 
| `pageViewParams.fragment` | フラグメント| 
| `pageViewParams.waitTime` | 待ち時間| 

### イベント

イベントマッピングの作成についての詳細は、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `sendApplicationError` | アプリケーションエラーの送信 |
| `sendGoal` | ゴールの送信 |
| `sendHTTPError` | HTTPエラーの送信 |
| `setCollection` | コレクションの設定 |
| `setRetention` | リテンションの設定 |
| `trackPageView` | ページビューの追跡 |
| `updateUserId` | ユーザーIDの更新 |

### E-コマース

|  変数 |説明 |
|:---------|:------------|
|  `customer_id` (Overrides `_ccustid`) |カスタマーID  |

