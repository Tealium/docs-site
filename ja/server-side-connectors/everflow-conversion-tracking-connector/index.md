---
title: Everflowコンバージョントラッキングコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでEverflowコンバージョントラッキングコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/everflow-conversion-tracking-connector/
---## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|広告主のコンバージョンを送信| ✓| ✓|
|広告主のポストコンバージョンイベントを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **Everflow Network ID**：コンバージョントラッキングエンドポイントのサブドメインとなるネットワークIDを入力します。例：[https://MY_NETWORK_ID.servecvr.com](https://MY_NETWORK_ID.servecvr.com)。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 広告主のコンバージョンを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|トランザクションID|  &lt;ul&gt;&lt;li&gt;ランディングページから取得したEverflowによって追跡された一意のクリックIDを渡します。&lt;/li&gt;&lt;li&gt;詳細については、[Everflowサポート](https://help.everflow.io/support/solutions/articles/22000221125-advertiser-conversion-tracking-postback-url)を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 広告主のポストコンバージョンイベントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|トランザクションID|  &lt;ul&gt;&lt;li&gt;ランディングページから取得したEverflowによって追跡された一意のクリックIDを渡します。&lt;/li&gt;&lt;li&gt;詳細については、[Everflowヘルプデスク](https://help.everflow.io/support/solutions/articles/22000221125-advertiser-conversion-tracking-postback-url)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|イベントデータ|  &lt;ul&gt;&lt;li&gt;オファービューで利用可能な**event\_id**を含むポストコンバージョンイベントを追跡するためのイベントデータを追加します。&lt;/li&gt;&lt;/ul&gt; |
