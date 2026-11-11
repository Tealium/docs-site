---
title: LaunchDarkly オーディエンスコホーティングコネクタ構成ガイド
description: この記事では、LaunchDarkly オーディエンスコホーティングコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/launchdarkly-audience-cohorting/
---
## API 情報

このコネクタは、次のベンダー API を使用します。

* API 名: LaunchDarkly API
* API バージョン: 20240415
* API エンドポイント: `https://app.launchdarkly.com`
* ドキュメント: [LaunchDarkly API](https://docs.launchdarkly.com/)

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| セグメントにメンバーを追加 | ✓ | ✗ |
| セグメントからメンバーを削除 | ✓ | ✗ |

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の項目を構成します。

* **クライアント側 ID**  
（必須）メトリクスイベント環境のクライアント側 ID。[LaunchDarkly アカウント構成ページ](https://app.launchdarkly.com/settings/members)の **Projects** タブにある **Environments** で確認できます。
* **アクセストークン**  
（必須）アクセストークンには、`importEventData` アクションを許可するロールが必要です。LaunchDarkly では、この権限を持つ専用のアクセストークンを使用することを強く推奨しています。詳細については、LaunchDarkly ドキュメントの[個人用 API アクセストークンのスコープ構成](https://docs.launchdarkly.com/home/account-security/api-access-tokens#scoping-personal-api-access-tokens)および[環境](https://docs.launchdarkly.com/home/organize/environments?q=environment)を参照してください。
* **セグメント名**  
（必須）データの送信先となる LaunchDarkly のセグメント名。
* **セグメント ID**  
（必須）LaunchDarkly のセグメントを一意に識別する ID。
* **セグメントの説明**  
LaunchDarkly で指定されたセグメントの説明。
* **URL のオーバーライド**  

コネクタを構成したら、**Done** をクリックします。
（テスト目的のみ）アクションの URL をオーバーライドできます。

## アクション

次のセクションでは、各アクションでサポートされているパラメーターについて説明します。

### セグメントにメンバーを追加

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| メンバー ID | 訪問の LaunchDarkly ID。 |
| HTTP リクエストセッション ID | セッション ID を送信する場合は、このオプションを選択します。デフォルトでは、セッション ID は送信されません。 |

#### メンバーパラメーター

| **パラメーター** | **説明** |
| --- | --- |
| 姓 | 訪問の姓。 |
| 名 | 訪問の名。 |
| メールアドレス | 訪問のメールアドレス。 |
| 電話番号 | 訪問の電話番号。 |

### セグメントからメンバーを削除

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| メンバー ID | 訪問の LaunchDarkly ID。|
| HTTP リクエストセッション ID | セッション ID を送信する場合は、このオプションを選択します。デフォルトでは、セッション ID は送信されません。 |