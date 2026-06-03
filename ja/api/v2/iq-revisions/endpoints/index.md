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
curl -H &#39;Authorization: Bearer {token}&#39; \
https://api.tealiumiq.com/v2/manifest/accounts/{account}/profiles/{profile}/revisions
```

### 応答の例

```json
[&#34;201508181719&#34;,
 &#34;201508181718&#34;,
 &#34;201508181717&#34;]
```

リビジョン ID は新しいリビジョンから順に逆時系列でリストされます。

### エラーメッセージ

このタスクの潜在的なエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
| 404 Not Found |  `{&#34;returnCode&#34; : 1240, &#34;message&#34; : &#34;アカウントが見つかりませんでした&#34;}` |
| 404 Not Found | `{&#34;returnCode&#34; : 1250, &#34;message&#34; : &#34;プロファイルが見つかりませんでした&#34;}` |

## リビジョン詳細の取得

GET リビジョン詳細は指定されたリビジョンの詳細を返します。

リビジョンの詳細を取得するには、以下の GET コマンドを使用します：

```bash
GET /v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/details
```

### cURL リクエストの例

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://api.tealiumiq.com/v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/details
```

### 応答の例

```json
{
    &#34;account&#34;: &#34;tealium&#34;,
    &#34;profile&#34;: &#34;profile&#34;,
    &#34;name&#34;: &#34;Full Release - 2016/12/13 19:53&#34;,
    &#34;time_created&#34;: &#34;Tue 2016.12.13 19:54 GMT&#34;,
    &#34;checksums&#34;: {
        &#34;prod&#34;: {
            &#34;manifest.json&#34;: &#34;df8bb8bdb8bc34f9d70d98ff49fdcf53e7f286520747001538b74357418178a2&#34;,
            &#34;bundle.zip&#34;: &#34;9309364527db38cd33538ca239929c3ed89b7b6990e99b4a41d16b50dd519e35&#34;,
            &#34;utag.js&#34;: &#34;3c34236708b14e8fd8a82e5c363d006793fd59fc6f6a6f0367634cf245d16861&#34;,
            &#34;utag.1.js&#34;: &#34;9b911570ac0685a50a3a32ef780a2570b16725779b7336bdbfca2838eea6d216&#34;,
            &#34;utag.2.js&#34;: &#34;0d3cbf8b3d275d181c2140c2eab88ead3c9f2002b5260d9ebd9f23cb7b60de9a&#34;
        }
    },
    &#34;revision_id&#34;: &#34;201612131954&#34;,
    &#34;comment&#34;: &#34;最新の公開&#34;,
    &#34;created_by&#34;: &#34;user@example.com&#34;,
    &#34;targets_published&#34;: [&#34;prod&#34;]
}
```

### エラーメッセージ

このタスクの潜在的なエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|404 Not Found| `{&#34;returnCode&#34; : 1240, &#34;message&#34; : &#34;アカウントが見つかりませんでした&#34; }` |  
|404 Not Found| `{&#34;returnCode&#34; : 1250, &#34;message&#34; : &#34;プロファイルが見つかりませんでした&#34; }` |
|404 Not Found| `{&#34;returnCode&#34; : 1260, &#34;message&#34; : &#34;リビジョンの詳細が存在しません&#34;}` |

## GET リビジョンバンドル

_リビジョンバンドル_ は、ターゲット環境用に公開された JavaScript ファイルの組み合わせを `.zip` ファイルの形で提供します。リビジョンが公開された場合、このエンドポイントでファイルを取得するために `targets_published` の値が使用されます。

```bash
GET /v2/manifest/accounts/{account}/profiles/{profile}/revisions/{revision_id}/environments/{environment}
```

このエンドポイントは最新の公開リビジョンにのみ機能し、以前のリビジョンには機能しません。

### cURL リクエストの例

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
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
|404 Not Found|  `{&#34;returnCode&#34; : 1270, &#34;message&#34; : &#34;要求されたリビジョンバンドルは最新ではありません&#34;}` |
