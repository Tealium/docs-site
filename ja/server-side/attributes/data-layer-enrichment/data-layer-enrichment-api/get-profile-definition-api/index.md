---
title: GETプロファイル定義API
description: GETプロファイル定義APIを使用して、Tealiumプロファイルからオーディエンスとバッジデータを取得できます。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/get-profile-definition-api/
---
## 動作原理

Data Layer Enrichment Public APIは、IDのみを使用してオーディエンスとバッジデータを返します。訪問データのバッジ名を参照するには、プロファイル定義APIを使用してプロファイルデータをリクエストできます。


<blockquote>
このAPIはデータレイヤーエンリッチメント構成によって制御されます。データレイヤーエンリッチメントが無効になっている場合、APIは`404`レスポンスを返します。詳細については、[サーバーサイドData Layer Enrichmentを有効にする](https://docs.tealium.com/enable-data-layer-enrichment/)を参照してください。
</blockquote>



<blockquote>
プロファイル定義APIはTealiumプロファイルに関連するバッジとオーディエンスデータを返し、特定のユーザーに制限されません。
</blockquote>


プロファイル定義を取得するには、次のGETコマンドを使用します：

```bash
GET https://visitor-service.tealiumiq.com/datacloudprofiledefinitions/{ACCOUNT}/{PROFILE}
```

## 例：リクエスト

```bash
curl https://visitor-service.tealiumiq.com/datacloudprofiledefinitions/myaccount/main/
```
## 例：レスポンス

```json
    {
        "audiences" : [
            {
                "id" : "myaccount_main_101",
                "name" : "サンプルオーディエンス"
            }
        ],
        "badges" : [
            {
                "id" : 5113,
                "name" : "カート放棄者"
            },
            {
                "id" : 32,
                "name" : "未バッジ"
            },
            {
                "id" : 31,
                "name" : "頻繁な訪問"
            },
            {
                "id" : 30,
                "name" : "ファン"
            }
        ]
    }

```