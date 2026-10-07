---
title: LaunchDarkly オーディエンスコホーティングコネクタ構成ガイド
description: この記事では、LaunchDarkly オーディエンスコホーティングコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/launchdarkly-audience-cohorting/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：LaunchDarkly API
* APIバージョン：20240415
* APIエンドポイント：`https://app.launchdarkly.com`
* ドキュメント：[LaunchDarkly API](https://docs.launchdarkly.com/)

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| セグメントへのメンバー追加 | ✓ | ✗ |
| セグメントからのメンバー削除 | ✓ | ✗ |

## 構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **クライアントサイドID**  
（必須）メトリックイベント環境のクライアントサイドID。クライアントサイドIDは、[LaunchDarklyアカウント構成ページ](https://app.launchdarkly.com/settings/members)の**環境**タブで見つけることができます。
* **アクセストークン**  
（必須）`importEventData`アクションを許可するロールが必要です。LaunchDarklyは、この権限を持つ専用のアクセストークンの使用を強く推奨します。詳細については、LaunchDarklyのドキュメントの[個人APIアクセストークンのスコープ構成](https://docs.launchdarkly.com/home/account-security/api-access-tokens#scoping-personal-api-access-tokens)および[環境](https://docs.launchdarkly.com/home/organize/environments?q=environment)を参照してください。
* **セグメント名**  
（必須）データを送信したいLaunchDarklyのセグメント名。
* **セグメントID**  
（必須）LaunchDarkly内のセグメントの一意の識別子。
* **セグメント説明**  
LaunchDarklyで提供されるセグメントの説明。
* **URLオーバーライド**  
（テスト目的のみ）アクションのURLをオーバーライドすることができます。

## アクション

以下のセクションでは、各アクションのサポートされるパラメータをリストします。

### セグメントへのメンバー追加

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| メンバーID | 訪問のLaunchDarkly ID。 |
| HTTPリクエストセッションID | セッションIDを送信する場合はこのオプションを選択します。デフォルトではセッションIDは送信されません。 |

#### メンバーパラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 姓 | 訪問の姓。 |
| 名 | 訪問の名。 |
| メール | 訪問のメールアドレス。 |
| 電話番号 | 訪問の電話番号。 |

### セグメントからのメンバー削除

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| メンバーID | 訪問のLaunchDarkly ID。|
| HTTPリクエストセッションID | セッションIDを送信する場合はこのオプションを選択します。デフォルトではセッションIDは送信されません。 |