---
title: LaunchDarklyメトリックインポートAPIコネクタ設定ガイド
description: この記事では、LaunchDarklyメトリックインポートAPIコネクタの設定方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/launchdarkly-metric-import-api-connector/
---
## API情報

このコネクタは、以下のベンダーAPIを使用します：

* API名：LaunchDarkly API
* APIバージョン：v2
* APIエンドポイント：`https://events.launchdarkly.com`
* ドキュメンテーション：[LaunchDarkly API](https://docs.launchdarkly.com/home/creating-experiments/import-metric-events)

## バッチ制限
このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション]()を参照してください。リクエストは、以下のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数：10000
* 最も古いリクエストからの最大時間：10分
* リクエストの最大サイズ：10 MB

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| 実験機能にメトリクスを送信 | ✗ | ✓ |

## 設定の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の設定を構成します：

* **会社名**  
 必須。LaunchDarklyでのあなたの会社の名前。
* **プロジェクトキー**  
 必須。メトリックイベント環境のプロジェクトキー。LaunchDarklyアカウント設定 &gt; プロジェクト &gt; 環境でプロジェクトキーを探します。
* **環境キー**  
必須。メトリックイベントが関連する環境の環境キー。これらはLaunchDarkly [アカウント](https://app.launchdarkly.com/settings/members)設定ページのプロジェクトタブの環境で見つけることができます。
* **アクセストークン**  
必須。アクセストークンは、`importEventData`アクションを許可するロールを持つ必要があります。LaunchDarklyは、この権限を持つ専用のアクセストークンの使用を強く推奨します。詳細については、[パーソナルAPIトークンのスコープ設定](https://docs.launchdarkly.com/home/account-security/api-access-tokens#scoping-personal-api-access-tokens)と[環境アクション](https://docs.launchdarkly.com/home/members/role-actions#environment-actions?q=import)を参照してください。

## アクション

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの設定方法について説明します。

### 実験機能にメトリクスを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| キー | 必須。あなたのメトリックを識別します。LaunchDarklyメトリックのイベント名は、この値と一致する必要があります。 |
| 作成日 | イベントが作成されたタイムスタンプ、Unixミリ秒。 |
| メトリック値 | メトリックの値。数値メトリックには必須、変換メトリックにはオプションです。変換メトリックに対してこの値が提供された場合、LaunchDarklyはこの値を無視します。 |
| コンテキストキー | メトリックイベントコンテキストの各コンテキストキーをリストする1つ以上のプロパティを持つJSONオブジェクト。形式は`&lt;contextKind&gt;: &lt;contextKey&gt;`です。例えば、あなたの実験がユーザーコンテキストで動作する場合、次のような種類/キーのペアがあるかもしれません：`&#34;user&#34;: &#34;user-key-123abc&#34;`。&lt;br&gt;各コンテキストの種類とキーは、あなたの実験で使用されるフラグを評価するためにLaunchDarkly SDKに提供される対応するコンテキストの種類/キーのペアと一致する必要があります。&lt;br&gt;コンテキスト種類の使用についての詳細は、[ランダム化ユニット](https://docs.launchdarkly.com/home/creating-experiments/allocation#randomization-units)を参照してください。 |
