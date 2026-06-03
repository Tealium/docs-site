---
title: New Relicブラウザコネクタ構成ガイド
description: この記事では、New Relicブラウザコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/new-relic-browser-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ブラウザアプリケーションメトリクスを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **New RelicアカウントID**
  * New RelicアカウントIDの取得方法については、[New Relic Insights APIキーの登録方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

* **New Relic REST APIキー**
  * REST APIキーは、利用可能なメトリクス、アプリケーション、その他のアカウント情報を取得するために使用されます。
  * New Relic REST APIキーの取得方法については、[New Relic Insights APIキーの登録方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

* **New Relic Insights APIキー**
  * Insights APIキーは、New Relic Insightsにデータを挿入するために使用されます。
  * New Relic Insights APIキーの取得方法については、[New Relic Insights APIキーの登録方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ブラウザアプリケーションメトリクスを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|New Relicブラウザアプリケーション|  &lt;ul&gt;&lt;li&gt;メトリクスを提供するブラウザアプリケーション。&lt;/li&gt;&lt;li&gt;アプリケーションがまだNew Relic Insightsに存在しない場合、または作成されない場合は、カスタム名を提供します。&lt;/li&gt;&lt;li&gt;これはNew Relicシステムにアプリケーションを作成するわけではなく、New Relic Insightsでアプリケーションをクエリする能力を提供します。&lt;/li&gt;&lt;/ul&gt; |
|イベントカテゴリ|  &lt;ul&gt;&lt;li&gt;イベントカテゴリ&lt;/li&gt;&lt;/ul&gt; |
|New RelicアプリケーションID|  &lt;ul&gt;&lt;li&gt;New RelicアプリケーションID&lt;/li&gt;&lt;/ul&gt; |
|サーバーサイドアプリケーション名|  &lt;ul&gt;&lt;li&gt;サーバーサイドアプリケーション名&lt;/li&gt;&lt;/ul&gt; |
|自律システム番号|  &lt;ul&gt;&lt;li&gt;自律システム番号&lt;/li&gt;&lt;/ul&gt; |
|自律システム番号の緯度|  &lt;ul&gt;&lt;li&gt;自律システム番号の緯度&lt;/li&gt;&lt;/ul&gt; |
|自律システム番号の経度|  &lt;ul&gt;&lt;li&gt;自律システム番号の経度&lt;/li&gt;&lt;/ul&gt; |
|自律システム番号の組織|  &lt;ul&gt;&lt;li&gt;自律システム番号の組織&lt;/li&gt;&lt;/ul&gt; |
|バックエンド応答時間|  &lt;ul&gt;&lt;li&gt;バックエンド応答時間&lt;/li&gt;&lt;/ul&gt; |
|トランザクション名|  &lt;ul&gt;&lt;li&gt;トランザクション名&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;市区町村&lt;/li&gt;&lt;/ul&gt; |
|サーバー接続の確立時間|  &lt;ul&gt;&lt;li&gt;サーバー接続の確立時間&lt;/li&gt;&lt;/ul&gt; |
|国コード|  &lt;ul&gt;&lt;li&gt;国コード&lt;/li&gt;&lt;/ul&gt; |
|デバイスタイプ|  &lt;ul&gt;&lt;li&gt;デバイスタイプ&lt;/li&gt;&lt;/ul&gt; |
|トップレベルDNSの解決時間|  &lt;ul&gt;&lt;li&gt;トップレベルDNSの解決時間&lt;/li&gt;&lt;/ul&gt; |
|ページの処理時間|  &lt;ul&gt;&lt;li&gt;ページの処理時間&lt;/li&gt;&lt;/ul&gt; |
|フロントエンドブラウザ応答時間|  &lt;ul&gt;&lt;li&gt;フロントエンドブラウザ応答時間&lt;/li&gt;&lt;/ul&gt; |
|サーバーサイドトランザクションの名前|  &lt;ul&gt;&lt;li&gt;サーバーサイドトランザクションの名前&lt;/li&gt;&lt;/ul&gt; |
|ネットワーク待機時間の合計|  &lt;ul&gt;&lt;li&gt;ネットワーク待機時間の合計&lt;/li&gt;&lt;/ul&gt; |
|ページのレンダリング時間|  &lt;ul&gt;&lt;li&gt;ページのレンダリング時間&lt;/li&gt;&lt;/ul&gt; |
|元のPageView URL|  &lt;ul&gt;&lt;li&gt;元のPageView URL&lt;/li&gt;&lt;/ul&gt; |
|サービス開始待ち時間|  &lt;ul&gt;&lt;li&gt;サービス開始待ち時間&lt;/li&gt;&lt;/ul&gt; |
|地域コード|  &lt;ul&gt;&lt;li&gt;地域コード&lt;/li&gt;&lt;/ul&gt; |
|TLSの構成時間|  &lt;ul&gt;&lt;li&gt;TLSの構成時間&lt;/li&gt;&lt;/ul&gt; |
|セッションID|  &lt;ul&gt;&lt;li&gt;セッションID&lt;/li&gt;&lt;/ul&gt; |
|ユーザーエージェント名|  &lt;ul&gt;&lt;li&gt;ユーザーエージェント名&lt;/li&gt;&lt;/ul&gt; |
|ユーザーエージェントバージョン|  &lt;ul&gt;&lt;li&gt;ユーザーエージェントバージョン&lt;/li&gt;&lt;/ul&gt; |
|ユーザーエージェントOS|  &lt;ul&gt;&lt;li&gt;ユーザーエージェントOS&lt;/li&gt;&lt;/ul&gt; |
|インタラクションの名前|  &lt;ul&gt;&lt;li&gt;インタラクションの名前&lt;/li&gt;&lt;/ul&gt; |
|ページアクションの名前|  &lt;ul&gt;&lt;li&gt;ページアクションの名前&lt;/li&gt;&lt;/ul&gt; |
|ブラウザの高さ|  &lt;ul&gt;&lt;li&gt;ブラウザの高さ&lt;/li&gt;&lt;/ul&gt; |
|ブラウザの幅|  &lt;ul&gt;&lt;li&gt;ブラウザの幅&lt;/li&gt;&lt;/ul&gt; |
|現在のURL|  &lt;ul&gt;&lt;li&gt;現在のURL&lt;/li&gt;&lt;/ul&gt; |
|リファラーURL|  &lt;ul&gt;&lt;li&gt;リファラーURL&lt;/li&gt;&lt;/ul&gt; |
|ページ要求とPageActionの間の時間|  &lt;ul&gt;&lt;li&gt;ページ要求とPageActionの間の時間&lt;/li&gt;&lt;/ul&gt; |
