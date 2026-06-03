---
title: New Relic Mobile コネクタ構成ガイド
description: この記事では、New Relic Mobileコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/new-relic-mobile-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|モバイルアプリケーションメトリクスを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **New RelicアカウントID**
  * New RelicアカウントIDの取得方法については、[New Relic Insights APIキーの登録方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

* **New Relic REST APIキー**
  * REST APIキーは、利用可能なメトリクス、アプリケーション、および他のアカウント情報を取得するために使用されます。
  * New Relic REST APIキーの取得方法については、[New Relic Insights APIキーの登録方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

* **New Relic Insights APIキー**
  * Insights APIキーは、New Relic Insightsにデータを挿入するために使用されます。
  * New Relic Insights APIキーの取得方法については、[New Relic Insights APIキーの登録方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - モバイルアプリケーションメトリクスを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|モバイルアプリケーション|  &lt;ul&gt;&lt;li&gt;メトリクスを提供するブラウザアプリケーション。&lt;/li&gt;&lt;li&gt;アプリケーションがまだNew Relic Insightsに存在しない場合、または作成されない場合は、カスタム名を提供します。&lt;/li&gt;&lt;li&gt;これはNew Relicシステムにアプリケーションを作成するわけではなく、New Relic Insightsでアプリケーションをクエリする能力を提供します。&lt;/li&gt;&lt;/ul&gt; |
|イベントカテゴリ|  &lt;ul&gt;&lt;li&gt;イベントカテゴリ&lt;/li&gt;&lt;/ul&gt; |
|イベントタイプ|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;このデータが保存されるイベントのタイプ。&lt;/li&gt;&lt;li&gt;デフォルト値は **Mobile Event** です&lt;/li&gt;&lt;/ul&gt; |
|アプリケーションビルド番号|  &lt;ul&gt;&lt;li&gt;アプリケーションビルド番号&lt;/li&gt;&lt;/ul&gt; |
|New Relicエージェントバージョン番号|  &lt;ul&gt;&lt;li&gt;New Relicエージェントバージョン番号&lt;/li&gt;&lt;/ul&gt; |
|アプリが位置する都市|  &lt;ul&gt;&lt;li&gt;アプリが位置する都市&lt;/li&gt;&lt;/ul&gt; |
|アプリが位置する国|  &lt;ul&gt;&lt;li&gt;アプリが位置する国&lt;/li&gt;&lt;/ul&gt; |
|アプリが位置する地域|  &lt;ul&gt;&lt;li&gt;アプリが位置する地域&lt;/li&gt;&lt;/ul&gt; |
|デバイスカテゴリ|  &lt;ul&gt;&lt;li&gt;デバイスカテゴリ&lt;/li&gt;&lt;/ul&gt; |
|デバイス製造者|  &lt;ul&gt;&lt;li&gt;デバイス製造者&lt;/li&gt;&lt;/ul&gt; |
|デバイスモデル番号|  &lt;ul&gt;&lt;li&gt;デバイスモデル番号&lt;/li&gt;&lt;/ul&gt; |
|インタラクションの期間|  &lt;ul&gt;&lt;li&gt;インタラクションの期間&lt;/li&gt;&lt;/ul&gt; |
|新規アプリインストール|  &lt;ul&gt;&lt;li&gt;新規アプリインストール&lt;/li&gt;&lt;/ul&gt; |
|最後のアプリケーションインタラクション|  &lt;ul&gt;&lt;li&gt;最後のアプリケーションインタラクション&lt;/li&gt;&lt;/ul&gt; |
|アプリケーションメモリ使用量|  &lt;ul&gt;&lt;li&gt;アプリケーションメモリ使用量&lt;/li&gt;&lt;/ul&gt; |
|ユーザーセッションの期間|  &lt;ul&gt;&lt;li&gt;ユーザーセッションの期間&lt;/li&gt;&lt;/ul&gt; |
|ユーザーセッションID|  &lt;ul&gt;&lt;li&gt;ユーザーセッションID&lt;/li&gt;&lt;/ul&gt; |
|最後のインタラクションからの時間|  &lt;ul&gt;&lt;li&gt;最後のインタラクションからの時間&lt;/li&gt;&lt;/ul&gt; |
|ロードからの時間|  &lt;ul&gt;&lt;li&gt;ロードからの時間&lt;/li&gt;&lt;/ul&gt; |
|バージョンからのアップグレード|  &lt;ul&gt;&lt;li&gt;バージョンからのアップグレード&lt;/li&gt;&lt;/ul&gt; |
|New Relicエージェントバージョン番号|  &lt;ul&gt;&lt;li&gt;New Relicエージェントバージョン番号&lt;/li&gt;&lt;/ul&gt; |
|インタラクションの名前|  &lt;ul&gt;&lt;li&gt;インタラクションの名前&lt;/li&gt;&lt;/ul&gt; |

