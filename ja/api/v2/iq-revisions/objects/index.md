---
title: iQリビジョンオブジェクト
description: リビジョンはJSONオブジェクトとして返されます。
url: https://docs.tealium.com/ja/api/v2/iq-revisions/objects/
---## 利用可能なフィールド

| パラメータ | タイプ | 説明 |
|---|---|---|
| `revision_id` | 文字列 | リビジョンのタイムスタンプを`YYYYMMDDHHMMSS`の形式の文字列として表現したもの。 |
| `created_by` | メール | リビジョンを作成したユーザーのメール。 |
| `comment` | 文字列 | リビジョンが作成された時点でユーザーが残したコメント。 |
| `targets_published` | 配列 | 使用された公開ターゲットの環境名の配列。 |
| `name` | 文字列 | リビジョンに付けられた名前。 |
| `time_created` | 文字列 | 作成時間の文字列表現、例： `Tue 2017.12.13 19:54 GMT`。 |
| `account` | 文字列 | リビジョンのアカウント名。 |
| `profile` | 文字列 | リビジョンのプロファイル名。 |
| `checksums` | オブジェクト | `targets_published`の値は`checksums`オブジェクトのキーファクターです。値には、そのターゲットに公開されたJavaScriptファイルごとの`checksums`値が含まれます。|


## 例のレスポンス

```json
{
    "account": "tealium",
    "profile": "main",
    "name": "Full Release - 2025/01/02 19:53",
    "time_created": "Thu 2025.01.02 19:53 GMT",
    "checksums": {
        "prod": {
            "manifest.json": "df8bb8bdb8bc34f9d70d98ff49fdcf53e7f286520747001538b74357418178a2",
            "bundle.zip": "9309364527db38cd33538ca239929c3ed89b7b6990e99b4a41d16b50dd519e35",
            "utag.sync.js": "7cdc832b67612bb053f2e4a91ea9eab2aeb4bd26bae9668cbf5bb58bb6a2e9a1",
            "utag.js": "3c34236708b14e8fd8a82e5c363d006793fd59fc6f6a6f0367634cf245d16861",
            "utag.1.js": "9b911570ac0685a50a3a32ef780a2570b16725779b7336bdbfca2838eea6d216",
            "utag.v.js": "31fd720e49c140f869999210c239f3cf89fd7ad0e7fd88b7b7af75612479cbcc",
            "mobile.html": "c5e99a1378a590ddf42bbc810d7c941ee98cfd0611abc1bf439d649cdb000bf7"
        }
    },
    "revision_id": "201712131954",
    "comment": "up to date publish",
    "created_by": "user@example.com",
    "targets_published": ["prod"]
}
```