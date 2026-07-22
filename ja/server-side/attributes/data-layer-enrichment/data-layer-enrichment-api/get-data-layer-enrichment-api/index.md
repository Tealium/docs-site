---
title: GETデータレイヤーエンリッチメントパブリックAPI
description: GETデータレイヤーエンリッチメントパブリックAPIを使用して、アクティブな訪問のプロファイルデータを取得します。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/get-data-layer-enrichment-api/
---
## 動作方法

次のGETメソッドを使用して訪問プロファイルを取得します：

```bash
GET https://visitor-service-{REGION}.tealiumiq.com/{ACCOUNT}/{PROFILE}/{VISITOR_ID}
```

地域固有のホストを決定するには、**管理メニュー > サーバーサイド構成 > 地域**にアクセスしてください。その後、[Tealiumの許可されたIPアドレス](https://docs.tealium.com/ip-allow-list/)で地域値を見つけることができます。

訪問IDは、`utag_main`クッキー名前空間の`v_id`キーの値、または`utag.data["cp.utag_main_v_id"]`から見つけることができます。


<blockquote>
提供された訪問IDが無効である場合、または訪問が現在アクティブな訪問を持っていない場合、APIはステータスコード200と空のJSONレスポンスを返します。
</blockquote>


## リクエスト例

```bash
curl https://visitor-service-us-west-2.tealiumiq.com/myaccount/main/015d1de1af41009e41015a38f658b0175002406d00fb3
```

## レスポンス例

```json
   {
        "metrics" : {
            "5117" : 6.0,
            "22" : 6.0
        },
        "dates" : {
            "5111" : 1420223771043
        },
        "properties" : {
            "account" : "myaccount",
            "5123" : "set",
            "profile" : "main"
        },
        "flags" : { "5115" : true } ,
        "current_visit" : {
            "metrics" : {
                "7" : 6.0
            },
            "dates" : {
                "5202" : 1420225387000
            },
            "properties" : {
                "48" : "Chrome",
                "45" : "Mac OS X",
                "44" : "Chrome",
                "47" : "browser",
                "46" : "Mac desktop"
            },
            "flags" : { }
        },
        "badges" : { "5113" : true },
        "audiences" : {
            "myaccount_main_101" : "Sample Audience"
        }
    }
```