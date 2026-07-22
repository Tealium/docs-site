---
title: iQ リビジョン API エンドポイント
description: GET iQ リビジョン API は JSON オブジェクトを使用してリビジョンデータを取得します。
url: https://docs.tealium.com/ja/api-v1/iq-revisions/endpoints/
---
これは、[現在の Tealium iQ リビジョン API](https://docs.tealium.com/about-iq-revisions/)の古いバージョンです。

## リビジョンのリスト

リビジョン ID の配列を返します。リビジョン ID は "YYYYMMDDHHMM" の形式のタイムスタンプです。この ID を使用してリビジョンの詳細を取得します。

`GET /v1/accounts/{account}/{profile}/revisions`

### cURL リクエスト

```bash
curl -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/accounts/{account}/{profile}/revisions?utk={token}

```

### 例の応答

```json
["201508181719",
 "201508181718",
 "201508181717"]

```


<blockquote>
リビジョン ID は新しいリビジョンから順に逆時系列でリストされます。
</blockquote>


### エラーメッセージ

**400 NOT FOUND**

```
{
   "returnCode" : 1240,
   "message" : "アカウントが見つかりませんでした"
}

```

```
{
   "returnCode" : 1250,
   "message" : "プロファイルが見つかりませんでした"
}

```

## リビジョンの詳細を取得

リビジョンの詳細を返します。

`GET /v1/accounts/{account}/{profile}/revisions/{revision_id}/details`

### cURL リクエスト

```bash
curl -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/accounts/{account}/{profile}/revisions/{revision_id}/details?utk={token}

```

### 例の応答

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
    "comment": "最新の公開状態",
    "created_by": "user@example.com",
    "targets_published": ["prod"]
}

```

### エラーメッセージ

**404 Not Found**

```
{
   "returnCode" : 1240,
   "message" : "アカウントが見つかりませんでした"
}

```

```
{
   "returnCode" : 1250,
   "message" : "プロファイルが見つかりませんでした"
}

```

```
{
   "returnCode" : 1260,
  "message" : "リビジョンの詳細が存在しません"
}

```

## リビジョンバンドルを取得

_リビジョンバンドル_は、ターゲット環境に公開された JavaScript ファイルのデプロイ可能なコーパスを zip ファイルの形で表します。リビジョンが公開された場合、このエンドポイントでファイルを取得するために `targets_published` の値が使用されます。例えば："prod"。

` GET /v1/accounts/{account}/{profile}/revisions/{revision_id}/{target}`

### cURL リクエスト

```bash
curl -b JSESSION={session_id} \
  http://api.tealiumiq.com/v1/accounts/{account}/{profile}/revisions/{revision_id}/{target}?utk={token} \
  -o utag.zip

```

### 応答

リクエストは以下を含む ".zip" ファイルを返します：

* **utag.js**- メインのローダーファイル
* **utag.\*.js**- ベンダータグファイル。例：`utag.13.js`。
* **utag.sync.js**- (オプション) 同期ローダーファイル
* **mobile.html**- (オプション) モバイルライブラリ構成
* **manifest.json**- この JSON ファイルにはリビジョン詳細エンドポイントによって返された情報と同じ情報が含まれていますが、バンドルの SHA256 は除外されます。

### エラーメッセージ

**400 NOT FOUND**

```
{
   "returnCode" : 1270,
   "message" : "要求されたリビジョンバンドルは最新ではありません"
}

```