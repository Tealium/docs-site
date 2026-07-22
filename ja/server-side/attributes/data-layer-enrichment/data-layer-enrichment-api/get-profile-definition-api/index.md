---
title: GETプロファイル定義API
description: GETプロファイル定義APIを使用すると、Tealiumプロファイルから視聴者とバッジのデータを取得できます。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/get-profile-definition-api/
---
## 仕組み

Data Layer Enrichment Public APIは、IDのみを使用して視聴者とバッジのデータを返します。訪問データのバッジの名前を参照するには、Profile Definition APIを使用してプロファイルデータをリクエストできます。


<blockquote>
プロファイル定義APIは、Tealiumプロファイルに関連するバッジと視聴者のデータを返し、特定のユーザーに制限されません。
</blockquote>


以下のGETコマンドを使用してプロファイル定義を取得します：

```bash
GET https://visitor-service.tealiumiq.com/datacloudprofiledefinitions/{ACCOUNT}/{PROFILE}
```

## リクエスト例

```bash
curl https://visitor-service.tealiumiq.com/datacloudprofiledefinitions/myaccount/main/
```
## レスポンス例

```json
    {
        "audiences" : [
            {
                "id" : "myaccount_main_101",
                "name" : "Sample Audience"
            }
        ],
        "badges" : [
            {
                "id" : 5113,
                "name" : "Cart abandoner"
            },
            {
                "id" : 32,
                "name" : "Unbadged"
            },
            {
                "id" : 31,
                "name" : "Frequent visitor"
            },
            {
                "id" : 30,
                "name" : "Fan"
            }
        ]
    }

```

