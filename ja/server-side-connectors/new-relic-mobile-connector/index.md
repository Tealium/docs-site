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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

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
|モバイルアプリケーション|  <ul><li>メトリクスを提供するブラウザアプリケーション。</li><li>アプリケーションがまだNew Relic Insightsに存在しない場合、または作成されない場合は、カスタム名を提供します。</li><li>これはNew Relicシステムにアプリケーションを作成するわけではなく、New Relic Insightsでアプリケーションをクエリする能力を提供します。</li></ul> |
|イベントカテゴリ|  <ul><li>イベントカテゴリ</li></ul> |
|イベントタイプ|  <ul><li>オプション</li><li>このデータが保存されるイベントのタイプ。</li><li>デフォルト値は **Mobile Event** です</li></ul> |
|アプリケーションビルド番号|  <ul><li>アプリケーションビルド番号</li></ul> |
|New Relicエージェントバージョン番号|  <ul><li>New Relicエージェントバージョン番号</li></ul> |
|アプリが位置する都市|  <ul><li>アプリが位置する都市</li></ul> |
|アプリが位置する国|  <ul><li>アプリが位置する国</li></ul> |
|アプリが位置する地域|  <ul><li>アプリが位置する地域</li></ul> |
|デバイスカテゴリ|  <ul><li>デバイスカテゴリ</li></ul> |
|デバイス製造者|  <ul><li>デバイス製造者</li></ul> |
|デバイスモデル番号|  <ul><li>デバイスモデル番号</li></ul> |
|インタラクションの期間|  <ul><li>インタラクションの期間</li></ul> |
|新規アプリインストール|  <ul><li>新規アプリインストール</li></ul> |
|最後のアプリケーションインタラクション|  <ul><li>最後のアプリケーションインタラクション</li></ul> |
|アプリケーションメモリ使用量|  <ul><li>アプリケーションメモリ使用量</li></ul> |
|ユーザーセッションの期間|  <ul><li>ユーザーセッションの期間</li></ul> |
|ユーザーセッションID|  <ul><li>ユーザーセッションID</li></ul> |
|最後のインタラクションからの時間|  <ul><li>最後のインタラクションからの時間</li></ul> |
|ロードからの時間|  <ul><li>ロードからの時間</li></ul> |
|バージョンからのアップグレード|  <ul><li>バージョンからのアップグレード</li></ul> |
|New Relicエージェントバージョン番号|  <ul><li>New Relicエージェントバージョン番号</li></ul> |
|インタラクションの名前|  <ul><li>インタラクションの名前</li></ul> |

