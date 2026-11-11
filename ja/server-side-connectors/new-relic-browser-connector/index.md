---
title: New Relic Browserコネクタ構成ガイド
description: この記事では、New Relic Browserコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/new-relic-browser-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|ブラウザアプリケーションのメトリクスを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の項目を構成します。

* **New RelicアカウントID**
  * New RelicアカウントIDの取得方法については、[New Relic Insights APIキーを登録する方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

* **New Relic REST APIキー**
  * REST APIキーは、利用可能なメトリクス、アプリケーション、およびその他のアカウント情報を取得するために使用します。
  * New Relic REST APIキーの取得方法については、[New Relic Insights APIキーを登録する方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

* **New Relic Insights APIキー**
  * Insights APIキーは、New Relic Insightsにデータを挿入するために使用します。
  * New Relic Insights APIキーの取得方法については、[New Relic Insights APIキーを登録する方法](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/inserting-custom-events-insights-api#register/)を参照してください。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - ブラウザアプリケーションのメトリクスを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|New Relic Browserアプリケーション| <ul><li>メトリクスの提供対象となるブラウザアプリケーション。</li><li>アプリケーションがまだNew Relic Insightsに存在しない場合は、カスタム名を指定してください。指定しないと作成されません。</li><li>これによってNew Relicシステム内にアプリケーションが作成されることはありませんが、New Relic Insightsでアプリケーションをクエリできるようになります。</li></ul> |
|イベントカテゴリ| <ul><li>イベントカテゴリ</li></ul> |
|New RelicアプリケーションID| <ul><li>New RelicアプリケーションID</li></ul> |
|サーバーサイドアプリケーション名| <ul><li>サーバーサイドアプリケーション名</li></ul> |
|自律システム番号| <ul><li>自律システム番号</li></ul> |
|自律システム番号の緯度| <ul><li>自律システム番号の緯度</li></ul> |
|自律システム番号の経度| <ul><li>自律システム番号の経度</li></ul> |
|自律システム番号の組織| <ul><li>自律システム番号の組織</li></ul> |
|バックエンド応答時間| <ul><li>バックエンド応答時間</li></ul> |
|トランザクション名| <ul><li>トランザクション名</li></ul> |
|市区町村| <ul><li>市区町村</li></ul> |
|サーバー接続の確立時間| <ul><li>サーバー接続の確立時間</li></ul> |
|国コード| <ul><li>国コード</li></ul> |
|デバイスタイプ| <ul><li>デバイスタイプ</li></ul> |
|トップレベルDNSの名前解決時間| <ul><li>トップレベルDNSの名前解決時間</li></ul> |
|ページ処理時間| <ul><li>ページ処理時間</li></ul> |
|フロントエンドブラウザ応答時間| <ul><li>フロントエンドブラウザ応答時間</li></ul> |
|サーバーサイドトランザクション名| <ul><li>サーバーサイドトランザクション名</li></ul> |
|ネットワークの合計待機時間| <ul><li>ネットワークの合計待機時間</li></ul> |
|ページのレンダリング時間| <ul><li>ページのレンダリング時間</li></ul> |
|元のページビューURL| <ul><li>元のページビューURL</li></ul> |
|サービス開始までの待機時間| <ul><li>サービス開始までの待機時間</li></ul> |
|地域コード| <ul><li>地域コード</li></ul> |
|TLSの構成時間| <ul><li>TLSの構成時間</li></ul> |
|セッションID| <ul><li>セッションID</li></ul> |
|ユーザーエージェント名| <ul><li>ユーザーエージェント名</li></ul> |
|ユーザーエージェントのバージョン| <ul><li>ユーザーエージェントのバージョン</li></ul> |
|ユーザーエージェントのOS| <ul><li>ユーザーエージェントのOS</li></ul> |
|インタラクション名| <ul><li>インタラクション名</li></ul> |
|ページアクション名| <ul><li>ページアクション名</li></ul> |
|ブラウザの高さ| <ul><li>ブラウザの高さ</li></ul> |
|ブラウザの幅| <ul><li>ブラウザの幅</li></ul> |
|現在のURL| <ul><li>現在のURL</li></ul> |
|参照元URL| <ul><li>参照元URL</li></ul> |
|ページのリクエストからページアクションまでの時間| <ul><li>ページのリクエストからページアクションまでの時間</li></ul> |