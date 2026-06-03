---
title: GETプロファイル定義API
description: GETプロファイル定義APIを使用すると、Tealiumプロファイルから視聴者とバッジのデータを取得できます。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/get-profile-definition-api/
---
## 仕組み

Data Layer Enrichment Public APIは、IDのみを使用して視聴者とバッジのデータを返します。訪問データのバッジの名前を参照するには、Profile Definition APIを使用してプロファイルデータをリクエストできます。

プロファイル定義APIは、Tealiumプロファイルに関連するバッジと視聴者のデータを返し、特定のユーザーに制限されません。

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
        &#34;audiences&#34; : [
            {
                &#34;id&#34; : &#34;myaccount_main_101&#34;,
                &#34;name&#34; : &#34;Sample Audience&#34;
            }
        ],
        &#34;badges&#34; : [
            {
                &#34;id&#34; : 5113,
                &#34;name&#34; : &#34;Cart abandoner&#34;
            },
            {
                &#34;id&#34; : 32,
                &#34;name&#34; : &#34;Unbadged&#34;
            },
            {
                &#34;id&#34; : 31,
                &#34;name&#34; : &#34;Frequent visitor&#34;
            },
            {
                &#34;id&#34; : 30,
                &#34;name&#34; : &#34;Fan&#34;
            }
        ]
    }

```

