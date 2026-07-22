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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

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
|New Relicブラウザアプリケーション|  <ul><li>メトリクスを提供するブラウザアプリケーション。</li><li>アプリケーションがまだNew Relic Insightsに存在しない場合、または作成されない場合は、カスタム名を提供します。</li><li>これはNew Relicシステムにアプリケーションを作成するわけではなく、New Relic Insightsでアプリケーションをクエリする能力を提供します。</li></ul> |
|イベントカテゴリ|  <ul><li>イベントカテゴリ</li></ul> |
|New RelicアプリケーションID|  <ul><li>New RelicアプリケーションID</li></ul> |
|サーバーサイドアプリケーション名|  <ul><li>サーバーサイドアプリケーション名</li></ul> |
|自律システム番号|  <ul><li>自律システム番号</li></ul> |
|自律システム番号の緯度|  <ul><li>自律システム番号の緯度</li></ul> |
|自律システム番号の経度|  <ul><li>自律システム番号の経度</li></ul> |
|自律システム番号の組織|  <ul><li>自律システム番号の組織</li></ul> |
|バックエンド応答時間|  <ul><li>バックエンド応答時間</li></ul> |
|トランザクション名|  <ul><li>トランザクション名</li></ul> |
|市区町村|  <ul><li>市区町村</li></ul> |
|サーバー接続の確立時間|  <ul><li>サーバー接続の確立時間</li></ul> |
|国コード|  <ul><li>国コード</li></ul> |
|デバイスタイプ|  <ul><li>デバイスタイプ</li></ul> |
|トップレベルDNSの解決時間|  <ul><li>トップレベルDNSの解決時間</li></ul> |
|ページの処理時間|  <ul><li>ページの処理時間</li></ul> |
|フロントエンドブラウザ応答時間|  <ul><li>フロントエンドブラウザ応答時間</li></ul> |
|サーバーサイドトランザクションの名前|  <ul><li>サーバーサイドトランザクションの名前</li></ul> |
|ネットワーク待機時間の合計|  <ul><li>ネットワーク待機時間の合計</li></ul> |
|ページのレンダリング時間|  <ul><li>ページのレンダリング時間</li></ul> |
|元のPageView URL|  <ul><li>元のPageView URL</li></ul> |
|サービス開始待ち時間|  <ul><li>サービス開始待ち時間</li></ul> |
|地域コード|  <ul><li>地域コード</li></ul> |
|TLSの構成時間|  <ul><li>TLSの構成時間</li></ul> |
|セッションID|  <ul><li>セッションID</li></ul> |
|ユーザーエージェント名|  <ul><li>ユーザーエージェント名</li></ul> |
|ユーザーエージェントバージョン|  <ul><li>ユーザーエージェントバージョン</li></ul> |
|ユーザーエージェントOS|  <ul><li>ユーザーエージェントOS</li></ul> |
|インタラクションの名前|  <ul><li>インタラクションの名前</li></ul> |
|ページアクションの名前|  <ul><li>ページアクションの名前</li></ul> |
|ブラウザの高さ|  <ul><li>ブラウザの高さ</li></ul> |
|ブラウザの幅|  <ul><li>ブラウザの幅</li></ul> |
|現在のURL|  <ul><li>現在のURL</li></ul> |
|リファラーURL|  <ul><li>リファラーURL</li></ul> |
|ページ要求とPageActionの間の時間|  <ul><li>ページ要求とPageActionの間の時間</li></ul> |
