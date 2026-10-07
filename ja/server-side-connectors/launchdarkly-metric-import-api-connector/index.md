---
title: LaunchDarkly メトリックインポートAPIコネクタ構成ガイド
description: この記事では、LaunchDarkly メトリックインポートAPIコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/launchdarkly-metric-import-api-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：LaunchDarkly API
* APIバージョン：20240415
* APIエンドポイント：`https://events.launchdarkly.com`
* ドキュメント：[LaunchDarkly API](https://docs.launchdarkly.com/home/creating-experiments/import-metric-events)

## バッチ制限
このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：10000
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：10 MB

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| 実験機能へのメトリック送信 | ✗ | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動して、新しいコネクタを追加します。コネクタの追加方法についての一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **会社名**  
 (必須) LaunchDarklyでの会社名。
* **プロジェクトキー**  
 (必須) メトリックイベント環境のプロジェクトキー。LaunchDarklyアカウント構成 > プロジェクト > 環境でプロジェクトキーを探します。
* **環境キー**  
(必須) メトリックイベントに関連する環境の環境キー。LaunchDarkly [アカウント](https://app.launchdarkly.com/settings/members)構成ページのプロジェクトタブの環境でこれらを見つけます。
* **アクセストークン**  
(必須) `importEventData`アクションを許可するロールを持つアクセストークンが必要です。LaunchDarklyは、この権限を持つ専用のアクセストークンの使用を強く推奨します。詳細については、[個人APIトークンの範囲指定](https://docs.launchdarkly.com/home/account-security/api-access-tokens#scoping-personal-api-access-tokens)および[環境アクション](https://docs.launchdarkly.com/home/members/role-actions#environment-actions?q=import)を参照してください。

## アクション

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### 実験機能へのメトリック送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| キー | (必須) メトリックを識別します。LaunchDarklyのメトリックのイベント名はこの値と一致する必要があります。 |
| 作成日 | イベントが作成された時のタイムスタンプ、Unixミリ秒単位。 |
| メトリック値 | メトリックの値。数値メトリックには必須です。変換メトリックにはオプションです。変換メトリックにこの値が提供されてもLaunchDarklyは無視します。 |
| コンテキストキー | メトリックイベントコンテキストのコンテキストキーをリストする1つ以上のプロパティを持つJSONオブジェクト。たとえば、実験がユーザーコンテキストを使用する場合、次の種類/キーペアがあるかもしれません：`"user": "user-key-123abc"`。<br>各コンテキストの種類とキーは、実験で使用されるフラグを評価するLaunchDarkly SDKに提供される対応するコンテキストの種類/キーペアと一致する必要があります。<br>コンテキストの種類の使用についての詳細は、[ランダム化ユニット](https://docs.launchdarkly.com/home/creating-experiments/allocation#randomization-units)を参照してください。 |