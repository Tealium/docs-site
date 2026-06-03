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

地域固有のホストを決定するには、**管理メニュー &gt; サーバーサイド構成 &gt; 地域**にアクセスしてください。その後、[Tealiumの許可されたIPアドレス]()で地域値を見つけることができます。

訪問IDは、`utag_main`クッキー名前空間の`v_id`キーの値、または`utag.data[&#34;cp.utag_main_v_id&#34;]`から見つけることができます。

提供された訪問IDが無効である場合、または訪問が現在アクティブな訪問を持っていない場合、APIはステータスコード200と空のJSONレスポンスを返します。

## リクエスト例

```bash
curl https://visitor-service-us-west-2.tealiumiq.com/myaccount/main/015d1de1af41009e41015a38f658b0175002406d00fb3
```

## レスポンス例

```json
   {
        &#34;metrics&#34; : {
            &#34;5117&#34; : 6.0,
            &#34;22&#34; : 6.0
        },
        &#34;dates&#34; : {
            &#34;5111&#34; : 1420223771043
        },
        &#34;properties&#34; : {
            &#34;account&#34; : &#34;myaccount&#34;,
            &#34;5123&#34; : &#34;set&#34;,
            &#34;profile&#34; : &#34;main&#34;
        },
        &#34;flags&#34; : { &#34;5115&#34; : true } ,
        &#34;current_visit&#34; : {
            &#34;metrics&#34; : {
                &#34;7&#34; : 6.0
            },
            &#34;dates&#34; : {
                &#34;5202&#34; : 1420225387000
            },
            &#34;properties&#34; : {
                &#34;48&#34; : &#34;Chrome&#34;,
                &#34;45&#34; : &#34;Mac OS X&#34;,
                &#34;44&#34; : &#34;Chrome&#34;,
                &#34;47&#34; : &#34;browser&#34;,
                &#34;46&#34; : &#34;Mac desktop&#34;
            },
            &#34;flags&#34; : { }
        },
        &#34;badges&#34; : { &#34;5113&#34; : true },
        &#34;audiences&#34; : {
            &#34;myaccount_main_101&#34; : &#34;Sample Audience&#34;
        }
    }
```