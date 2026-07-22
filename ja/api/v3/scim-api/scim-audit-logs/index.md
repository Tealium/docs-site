---
title: SCIM監査ログ
description: SCIM監査ログがユーザープロビジョニングイベントを記録する方法と、コンプライアンス監査およびトラブルシューティングのためにログをエクスポートする方法を学びます。
url: https://docs.tealium.com/ja/api/v3/scim-api/scim-audit-logs/
---
## 動作原理

SCIM監査ログは、作成、更新、パッチ、削除、取得など、すべてのSCIMユーザープロビジョニングイベントを記録します。各ログエントリには、アクションタイプ、結果、対象ユーザーの詳細、イベントをトリガーしたソース、およびトレース用の相関IDが記録されます。

監査ログを使用して、適切なユーザーがプロビジョニングされていることを確認し、プロビジョニング操作の失敗をトラブルシューティングし、コンプライアンス監査のための記録を作成します。

ログは12ヶ月間保持されます。リクエストとレスポンスのペイロードは保存されません。

## ログに記録される内容

以下のSCIM操作が `/scim/v2/Users` でログに記録されます：

| アクション | HTTPメソッド |
| --- | --- |
| ユーザー作成 | `POST` |
| ユーザー更新 | `PUT` |
| ユーザーパッチ | `PATCH` |
| ユーザー取得 | `GET` |
| ユーザー削除 | `DELETE` |

各イベントは結果に関わらず記録されます。失敗した操作は `ERROR` 結果と短いエラーメッセージでログに記録されます。

## UIから監査ログをエクスポート

アカウント管理者およびユーザー管理者は、APIを直接呼び出すことなく監査ログをエクスポートできます。

**権限管理**（プラットフォーム権限）ページで、**監査ログをエクスポート**を選択して、過去12ヶ月間の現在のアカウントのすべての監査ログのCSVをダウンロードします。

**監査ログをエクスポート**ボタンは、新しい権限体験でのみ利用可能です。レガシー権限体験では表示されません。

アカウントにログが存在しない場合はメッセージが表示されます。エクスポートが失敗した場合は、エラーメッセージが表示され、再試行を促すプロンプトが表示されます。

## ログフィールドの参照

各ログエントリには以下のフィールドが含まれます：

| フィールド | 説明 |
| --- | --- |
| `timestamp` | イベントの日時。 |
| `action_type` | 実行されたSCIM操作：`ユーザー作成`、`ユーザー更新`、`ユーザーパッチ`、`ユーザー取得`、または`ユーザー削除`。 |
| `resource_type` | 影響を受けたSCIMリソースのタイプ。`USER`または`GROUP`を返します。 |
| `target_email` | 変更を受けたユーザーのメールアドレス。 |
| `target_first_name` | 対象ユーザーの名。 |
| `target_last_name` | 対象ユーザーの姓。 |
| `target_user_uuid` | 対象ユーザーに割り当てられたTealiumのUUID。 |
| `external_id` | ユーザーのIDプロバイダーの識別子。 |
| `idp_source` | IDプロバイダーの名前。 |
| `http_status` | SCIM操作のHTTPレスポンスコード。 |
| `outcome` | 操作の結果：`SUCCESS`または`ERROR`。 |
| `correlation_id` | リクエストの一意識別子。この値を使用してログ間で特定の操作を追跡します。 |
| `account_name` | Tealiumアカウント名。 |
| `error_message` | 結果が`ERROR`の場合のエラーの短い説明。成功時は空。 |

## 一般的なタスクのためのログのフィルタリング

[GET SCIM Sync Logs API](https://docs.tealium.com/get-scim-sync-logs-api/)は、結果をフィルタリングするためのいくつかのクエリパラメータをサポートしています。以下の例は、一般的なタスクのためのフィルターの使用方法を示しています。

**コンプライアンス監査のためのログのエクスポート（日付範囲）**

特定の期間のすべてのプロビジョニング活動の記録を作成するには、監査に必要な日付範囲に`from`と`to`を構成します：

```bash
curl --location 'https://developer.tealiumapis.com/admin/scim-sync/logs?account={ACCOUNT}&from=2025-01-01T00:00:00Z&to=2025-03-31T23:59:59Z' \
--header 'Authorization: Bearer {TOKEN}'
```

**プロビジョニングの失敗イベントを見つける**

プロビジョニングの失敗を特定するには、`status=ERROR`でフィルタリングします：

```bash
curl --location 'https://developer.tealiumapis.com/admin/scim-sync/logs?account={ACCOUNT}&status=ERROR' \
--header 'Authorization: Bearer {TOKEN}'
```

各結果の`error_message`フィールドは、操作が失敗した理由を説明します。

**特定のリクエストを追跡する**

サポートチケットやアプリケーションログから相関IDを持っている場合、`correlationId`を使用して正確なイベントを取得します：

```bash
curl --location 'https://developer.tealiumapis.com/admin/scim-sync/logs?account={ACCOUNT}&correlationId={CORRELATION_ID}' \
--header 'Authorization: Bearer {TOKEN}'
```