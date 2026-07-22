---
title: SCIM同期ログの取得
description: Get SCIM Sync Logs APIは、SCIMユーザーの同期ログを取得します。
url: https://docs.tealium.com/ja/api/v3/scim-api/get-scim-sync-logs-api/
---
## 動作方法

SCIM同期ログを取得するにはGETメソッドを使用します：

```bash
GET /admin/scim-sync/logs
```

## 認証

すべてのAPI呼び出しにはJSESSIONID値が使用され、APIキーは使用されません。APIキーは認証呼び出しでのみ使用されます。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## GET操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `account`| 文字列 | 必須 | アカウントの一意の識別子です。 |
| `utk` | 文字列 | 必須 | 認証用のユーザートークンです。 |
| `from` | 文字列 | 任意 | ログの時間範囲の開始です。ISO 8601形式。デフォルト値は30日前です。 |
| `to` | 文字列 | 任意 | ログの時間範囲の終了です。ISO 8601形式。デフォルト値は現在の日付と時刻です。 |
| `status` | 文字列 | 任意 | 同期の状態です。例えば、`SUCCESS`や`ERROR`です。 |
| `action` | 文字列 | 任意 | 同期中に行われたアクションです。例えば：`User OOO`, `User Patch`, `User Update`, `User Creation`, `User Deletion`, `User Retrieval`です。 |
| `source` | 文字列 | 任意 | 同期リクエストのソースです。例えば、`SCIM_API`です。 |
| `userEmail` | 文字列 | 任意 | ユーザーのメールアドレスです。この値は大文字小文字を区別しない部分文字列です。 |
| `correlationId` | 文字列 | 任意 | リクエストの相関IDです。 |
| `format` | 文字列 | 任意 | 応答形式です。許可される値は`csv`と`json`です。デフォルト値は`csv`です。 |
| `limit` | 文字列 | 任意 | 返されるログエントリの最大数です。デフォルト値は`1000`で、最大値は`5000`です。 |

### 例 cURLリクエスト

```bash
curl --location --request GET 'https://my.tealiumiq.com/urest/admin/scim-sync/logs?account={ACCOUNT}&from=2023-10-01T00:00:00Z&to=2023-10-31T23:59:59Z&limit=100&format=json&utk=01234567890012345678901234567890'
```

### 例 応答

 

| timestamp	| action_type	| resource_type	| target_email| 	target_first_name	| target_last_name| 	target_user_uuid	| external_id	idp_source| 	http_status	| outcome	| correlation_id	| account_name	| error_message| 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
| 2025-10-13 23:01:15.684Z|	User Creation|	USER	| 	test.userXZ4@example.com	| 	Test	| 	User	| |  | 409| 	ERROR	| a211d118-f6db-49ec-8a85-05f46742954d	| 	admin1	| 	アカウントに既に存在するユーザーです。|
| 2025-10-13 22:51:57.472Z|	User Patch	| 	USER	| 	test.userxz4@example.com		|  |	User	| aa580e7f-569c-460e-b7e0-a73416161949	|	|	200	|SUCCESS	|019f36c9-3018-418c-b877-41450d845fca	| admin1	|
| 2025-10-13 22:51:53.201Z|	User Patch		| USER	| 	test.userxz4@example.com|	john | 	User	|aa580e7f-569c-460e-b7e0-a73416161949		| |	200	| SUCCESS	| 10120449-3901-4889-b18c-aedeed1a7d88 |	admin1	|
| 2025-10-13 22:47:00.753Z|	User Patch	| USER	| 	test.userxz4@example.com	|john| 	User	| aa580e7f-569c-460e-b7e0-a73416161949	|		| 200	| SUCCESS	| 0e79ebfd-76f0-40f9-8e6e-20f105b53e46| 	admin1	|
| 2025-10-13 22:46:54.604Z|	User Update	| USER	| 	| | | aa580e7f-569c-460e-b7e0-a73416161949		| 	| 	400	| ERROR |	c9f40bc4-62da-4d10-8fe5-08fddf4686cd	| admin1	| userNameが必要です。 |



### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `400 Bad Request: "message": "Account parameter is required."` |
| 401 | `400 Bad Request: "message": "Authentication failed"` |
| 403 | `403 Forbidden "message": "Unauthorized access."` |
| 405 | `405 Invalid Method "message": "Method is not allowed on this endpoint. Allowed methods: GET."`|
| 500 | `500 Internal Server Error "message": "Error processing json for extension - account {ACCOUNT}"`|