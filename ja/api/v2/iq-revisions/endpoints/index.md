---
title: iQ リビジョン API エンドポイント
description: GET iQ リビジョン API は JSON オブジェクトを使用してリビジョンデータを取得します。
url: https://docs.tealium.com/ja/api/v2/iq-revisions/endpoints/
---
## GET リビジョン

GET リビジョンはリビジョン ID の配列を返します。リビジョン ID は `YYYYMMDDHHMM` の形式のタイムスタンプです。この ID を使用してリビジョンの詳細を取得します。

リビジョンをリストするには、以下の GET コマンドを使用します：

```bash
GET /v2/manifest/accounts/{account}/profiles/{profile}/revisions
```

### cURL リクエストの例

```bash
curl -H 'Authorization: Bearer {token}' \
https://api.tealiumiq.com/v2/manifest/accounts/{account}/profiles/{profile}/revisions
```

### 応答の例

```json
["201508181719",
 "201508181718",
 "201508181717"]
```


<blockquote>
リビジョン ID は新しいリビジョンから順に逆時系列でリストされます。
</blockquote>


### エラーメッセージ

このタスクの潜在的なエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
| 404 Not Found |  `{"returnCode" : 1240, "message" : "アカウントが見つかりませんでした"}` |
| 404 Not Found | `{"returnCode" : 1250, "message" : "プロファイルが見つかりませんでした"}` |

## リビジョン詳細の取得

GET リビジョン詳細は指定されたリビジョンの詳細を返します。

リビジョンの詳細を取得するには、以下の GET コマンドを使用します：

```bash
GET /v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/details
```

### cURL リクエストの例

```bash
curl -H 'Authorization: Bearer {token}' \
https://api.tealiumiq.com/v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/details
```

### 応答の例

```json
{
    "account": "tealium",
    "profile": "profile",
    "name": "Full Release - 2016/12/13 19:53",
    "time_created": "Tue 2016.12.13 19:54 GMT",
    "checksums": {
        "prod": {
            "manifest.json": "df8bb8bdb8bc34f9d70d98ff49fdcf53e7f286520747001538b74357418178a2",
            "bundle.zip": "9309364527db38cd33538ca239929c3ed89b7b6990e99b4a41d16b50dd519e35",
            "utag.js": "3c34236708b14e8fd8a82e5c363d006793fd59fc6f6a6f0367634cf245d16861",
            "utag.1.js": "9b911570ac0685a50a3a32ef780a2570b16725779b7336bdbfca2838eea6d216",
            "utag.2.js": "0d3cbf8b3d275d181c2140c2eab88ead3c9f2002b5260d9ebd9f23cb7b60de9a"
        }
    },
    "revision_id": "201612131954",
    "comment": "最新の公開",
    "created_by": "user@example.com",
    "targets_published": ["prod"]
}
```

### エラーメッセージ

このタスクの潜在的なエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|404 Not Found| `{"returnCode" : 1240, "message" : "アカウントが見つかりませんでした" }` |  
|404 Not Found| `{"returnCode" : 1250, "message" : "プロファイルが見つかりませんでした" }` |
|404 Not Found| `{"returnCode" : 1260, "message" : "リビジョンの詳細が存在しません"}` |

## GET リビジョンバンドル

_リビジョンバンドル_ は、ターゲット環境用に公開された JavaScript ファイルの組み合わせを `.zip` ファイルの形で提供します。リビジョンが公開された場合、このエンドポイントでファイルを取得するために `targets_published` の値が使用されます。

```bash
GET /v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/environments/{environment}
```

このエンドポイントは最新の公開リビジョンにのみ機能し、以前のリビジョンには機能しません。

### cURL リクエストの例

```bash
curl -H 'Authorization: Bearer {token}' \
https://api.tealiumiq.com/v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/environments/{environment}
--output distro.zip
```

### 応答の例

cURL コマンドの応答は、以下の個々のファイルを含む `.zip` ファイルの返却です：

| ファイル名| 内容|
|---| ---|
| `utag.js`| メインのローダーファイル|
| `utag.*.js`|  ベンダータグファイル、例えば `utag.13.js`|
| `utag.sync.js`| (オプション) 同期ローダーファイルを含む |
| `mobile.html `| (オプション) モバイルライブラリ構成を含む |
| `manifest.json`|  リビジョン詳細エンドポイントによって返される情報を含む JSON ファイル。注: バンドルの SHA256 は含まれていません。|

### エラーメッセージ

このタスクの潜在的なエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|404 Not Found|  `{"returnCode" : 1270, "message" : "要求されたリビジョンバンドルは最新ではありません"}` |
