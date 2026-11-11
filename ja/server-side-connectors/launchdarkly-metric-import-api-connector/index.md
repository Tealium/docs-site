---
title: LaunchDarkly Metric Import API コネクタ構成ガイド
description: この記事では、LaunchDarkly Metric Import API コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/launchdarkly-metric-import-api-connector/
---
## API 情報

このコネクタは、次のベンダー API を使用します。

* API 名: LaunchDarkly API
* API バージョン: 20240415
* API エンドポイント: `https://events.launchdarkly.com`
* ドキュメント: [LaunchDarkly API](https://docs.launchdarkly.com/home/creating-experiments/import-metric-events)

## バッチ処理の上限

このコネクタは、ベンダーへの大量のデータ転送に対応するため、リクエストをバッチ処理します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数: 10000
* 最も古いリクエストからの最大経過時間: 10 分
* リクエストの最大サイズ: 10 MB

## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| メトリクスを実験機能に送信 | ✗ | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **会社名**  
 （必須）LaunchDarkly に登録されている会社名。
* **プロジェクトキー**  
 （必須）メトリクスイベント環境のプロジェクトキー。LaunchDarkly のアカウント構成で、［Projects］>［Environments］の順に移動してプロジェクトキーを確認します。
* **環境キー**  
（必須）メトリクスイベントが関連付けられている環境の環境キー。LaunchDarkly の[アカウント](https://app.launchdarkly.com/settings/members)構成ページにある［Projects］タブの［Environments］で確認できます。
* **アクセストークン**  
（必須）アクセストークンには、`importEventData`アクションを許可するロールが必要です。LaunchDarkly では、この権限を持つ専用のアクセストークンを使用することを強く推奨しています。詳細については、[個人 API トークンのスコープ構成](https://docs.launchdarkly.com/home/account-security/api-access-tokens#scoping-personal-api-access-tokens)および[環境アクション](https://docs.launchdarkly.com/home/members/role-actions#environment-actions?q=import)を参照してください。

## アクション

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメーターとオプションを構成する方法について説明します。

### メトリクスを実験機能に送信

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| キー | （必須）メトリクスを識別します。LaunchDarkly メトリクスのイベント名は、この値と一致する必要があります。 |
| 作成日時 | イベントが作成された時刻を示す Unix ミリ秒単位のタイムスタンプ。 |
| メトリクス値 | メトリクスの値。数値メトリクスでは必須です。コンバージョンメトリクスでは任意です。コンバージョンメトリクスにこの値を指定した場合、LaunchDarkly は無視します。 |
| コンテキストキー | 1 つ以上のプロパティを持ち、各メトリクスイベントコンテキストのコンテキストキーを`<contextKind>: <contextKey>`形式で列挙する JSON オブジェクト。たとえば、実験でユーザーコンテキストを使用する場合、次の kind/key ペアを使用できます：`"user": "user-key-123abc"`。<br>各コンテキストの kind と key は、実験で使用されるフラグを評価する LaunchDarkly SDK に提供された、対応するコンテキストの kind/key ペアと一致する必要があります。<br>コンテキスト kind の使用方法について詳しくは、[ランダム化単位](https://docs.launchdarkly.com/home/creating-experiments/allocation#randomization-units)を参照してください。 |