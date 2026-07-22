---
title: iQリビジョンオブジェクト
description: リビジョンはJSONオブジェクトとして返されます。
url: https://docs.tealium.com/ja/api-v1/iq-revisions/data-objects/
---
これは、[現在のTealium iQリビジョンAPI](https://docs.tealium.com/about-iq-revisions/)の古いバージョンです。

リビジョンは、以下のフィールドを含むJSONオブジェクトとして返されます：

|名前| タイプ| 説明|
|---| ---| ---|
|revision_id| 文字列| リビジョンのタイムスタンプ、`YYYYMMDDHHMMSS`の形式の文字列として表されます。|
|created_by| メール| リビジョンを作成したユーザーのメール。|
|comment| 文字列| ユーザーが残したコメント。|
|targets_published| 配列| 使用された公開ターゲットの環境名の配列。|
|name| 文字列| リビジョンに付けられた名前。|
|time_created| 文字列| 作成時間の文字列表現。例："Tue 2016.12.13 19:54 GMT"。|
|account| 文字列| リビジョンのアカウント名。|
|profile| 文字列| リビジョンのプロファイル名。|
|checksums| オブジェクト| `targets_published`の各値はこのオブジェクトのキーで、その値はそのターゲットに公開された各JavaScriptファイルのチェックサム値を含むオブジェクトです。例：``` "targets_published" : ["dev"], "checksums" : {     "dev": {         "manifest.json" : "<CHECKSUM HERE>",         "bundle.zip"    : "<CHECKSUM HERE>",         "utag.js"       : "<CHECKSUM HERE>",         "utag.1.js"     : "<CHECKSUM HERE>"     } } ``` |

## 例のレスポンス

```json
{
    "account": "tealium",
    "profile": "main",
    "name": "Full Release - 2016/12/13 19:53",
    "time_created": "Tue 2016.12.13 19:54 GMT",
    "checksums": {
        "prod": {
            "manifest.json": "df8bb8bdb8bc34f9d70d98ff49fdcf53e7f286520747001538b74357418178a2",
            "bundle.zip": "9309364527db38cd33538ca239929c3ed89b7b6990e99b4a41d16b50dd519e35",
            "utag.sync.js": "7cdc832b67612bb053f2e4a91ea9eab2aeb4bd26bae9668cbf5bb58bb6a2e9a1",
            "utag.js": "3c34236708b14e8fd8a82e5c363d006793fd59fc6f6a6f0367634cf245d16861",
            "utag.1.js": "9b911570ac0685a50a3a32ef780a2570b16725779b7336bdbfca2838eea6d216"
        }
    },
    "revision_id": "201612131954",
    "comment": "up to date publish",
    "created_by": "user@example.com",
    "targets_published": ["prod"]
}
```