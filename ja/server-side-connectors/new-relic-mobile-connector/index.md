---
title: New Relic Mobileコネクタ構成ガイド
description: この記事では、New Relic Mobileコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/new-relic-mobile-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|モバイルアプリケーションの指標を送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します。

* **New RelicアカウントID**
  * New RelicアカウントIDを取得する方法については、[New Relic Insights APIキーを登録する方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

* **New Relic REST APIキー**
  * REST APIキーは、利用可能な指標、アプリケーション、およびその他のアカウント情報を取得するために使用されます。
  * New Relic REST APIキーを取得する方法については、[New Relic Insights APIキーを登録する方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

* **New Relic Insights APIキー**
  * Insights APIキーは、New Relic Insightsにデータを挿入するために使用されます。
  * New Relic Insights APIキーを取得する方法については、[New Relic Insights APIキーを登録する方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - モバイルアプリケーションの指標を送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|モバイルアプリケーション|  <ul><li>指標を提供するブラウザアプリケーション。</li><li>アプリケーションがまだNew Relic Insightsに存在しない場合は、カスタム名を指定してください。指定しない場合、作成されません。</li><li>これによってNew Relicシステム内にアプリケーションが作成されることはありませんが、New Relic Insightsでアプリケーションをクエリできるようになります。</li></ul> |
|イベントカテゴリ|  <ul><li>イベントカテゴリ</li></ul> |
|イベントタイプ|  <ul><li>（任意）このデータを保存するイベントのタイプ。</li><li>デフォルト値は**モバイルイベント**です。</li></ul> |
|アプリケーションのビルド番号|  <ul><li>アプリケーションのビルド番号</li></ul> |
|New Relicエージェントのバージョン番号|  <ul><li>New Relicエージェントのバージョン番号</li></ul> |
|アプリが所在する都市|  <ul><li>アプリが所在する都市</li></ul> |
|アプリが所在する国|  <ul><li>アプリが所在する国</li></ul> |
|アプリが所在する地域|  <ul><li>アプリが所在する地域</li></ul> |
|デバイスカテゴリ|  <ul><li>デバイスカテゴリ</li></ul> |
|デバイスメーカー|  <ul><li>デバイスメーカー</li></ul> |
|デバイスのモデル番号|  <ul><li>デバイスのモデル番号</li></ul> |
|インタラクション時間|  <ul><li>インタラクション時間</li></ul> |
|アプリの新規インストール|  <ul><li>アプリの新規インストール</li></ul> |
|最後のアプリケーションインタラクション|  <ul><li>最後のアプリケーションインタラクション</li></ul> |
|アプリケーションのメモリ使用量|  <ul><li>アプリケーションのメモリ使用量</li></ul> |
|ユーザーセッション時間|  <ul><li>ユーザーセッション時間</li></ul> |
|ユーザーセッションID|  <ul><li>ユーザーセッションID</li></ul> |
|最後のインタラクションからの経過時間|  <ul><li>最後のインタラクションからの経過時間</li></ul> |
|読み込みからの経過時間|  <ul><li>読み込みからの経過時間</li></ul> |
|アップグレード前のバージョン|  <ul><li>アップグレード前のバージョン</li></ul> |
|New Relicエージェントのバージョン番号|  <ul><li>New Relicエージェントのバージョン番号</li></ul> |
|インタラクション名|  <ul><li>インタラクション名</li></ul> |