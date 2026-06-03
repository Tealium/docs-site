---
title: LaunchDarklyオーディエンスコホーティングコネクタ設定ガイド
description: この記事では、LaunchDarklyオーディエンスコホーティングコネクタの設定方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/launchdarkly-audience-cohorting/
---
## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| セグメントにメンバーを追加 | ✓ | ✗ |
| セグメントからメンバーを削除 | ✓ | ✗ |

## 設定

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の設定を行います：

* **クライアントサイドID**  
（必須）メトリックイベント環境のクライアントサイドID。クライアントサイドIDは、[LaunchDarklyアカウント設定ページ](https://app.launchdarkly.com/settings/members)の**プロジェクト**タブで**環境**の下にあります。
* **アクセストークン**  
（必須）アクセストークンは、`importEventData`アクションを許可するロールを持つ必要があります。LaunchDarklyは、この権限を持つ専用のアクセストークンの使用を強く推奨します。詳細については、LaunchDarklyのドキュメンテーション内の[パーソナルAPIアクセストークンのスコープ設定](https://docs.launchdarkly.com/home/account-security/api-access-tokens#scoping-personal-api-access-tokens)と[環境](https://docs.launchdarkly.com/home/organize/environments?q=environment)を参照してください。
* **セグメント名**  
（必須）データを送信したいLaunchDarklyのセグメント名。
* **セグメントID**  
（必須）LaunchDarklyのセグメントの一意の識別子。
* **セグメントの説明**  
LaunchDarklyで提供されるセグメントの説明。
* **URLオーバーライド**  
（テスト目的のみ）アクションのURLをオーバーライドできます。

## アクション

以下のセクションでは、各アクションのサポートされるパラメータをリストします。

### セグメントにメンバーを追加

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| メンバーID | 訪問者のLaunchDarkly ID。 |
| HTTPリクエストセッションID | セッションIDを送信したい場合は、このオプションを選択します。デフォルトではセッションIDは送信されません。 |

#### メンバーパラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 姓 | 訪問者の姓。 |
| 名 | 訪問者の名前。 |
| メール | 訪問者のメールアドレス。 |
| 電話番号 | 訪問者の電話番号。 |

### セグメントからメンバーを削除

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| メンバーID | 訪問者のLaunchDarkly ID。|
| HTTPリクエストセッションID | セッションIDを送信したい場合は、このオプションを選択します。デフォルトではセッションIDは送信されません。 |
