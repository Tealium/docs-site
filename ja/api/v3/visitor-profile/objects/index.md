---
title: ビジタープロファイルAPIオブジェクト
description: ビジターはJSONオブジェクトとして返されます。
url: https://docs.tealium.com/ja/api/v3/visitor-profile/objects/
---
## ビジターフィールド

ビジターは、以下のフィールドを含むJSONオブジェクトとして返されます：

|オブジェクト名| タイプ| 説明|
|---| ---| ---|
|`live`| Boolean|  ビジターが現在ライブセッション中である場合は`true`に構成します。 |
|`visitor`| object|  属性データタイプごとのサブオブジェクトを持つビジターオブジェクト：&lt;ul&gt;&lt;li&gt;ビジターID： `secondary_ids : { }`&lt;/li&gt;&lt;li&gt; 数値/数値の配列：&lt;br&gt; `&#34;metrics&#34; : { }`&lt;br&gt; `&#34;metric_lists&#34; : { }`&lt;/li&gt;&lt;li&gt;文字列/文字列の配列/文字列のセット：&lt;br&gt;`&#34;properties&#34; : { }`&lt;br&gt; `&#34;property_lists&#34; : { }`&lt;br&gt; `&#34;property_sets&#34; : { }`&lt;br&gt; `&#34;audiences&#34; : { }`&lt;/li&gt;&lt;li&gt;ブール値/ブール値の配列：&lt;br&gt; `&#34;flags&#34; : { }`&lt;br&gt; `&#34;flag_lists&#34; : { }`&lt;/li&gt;&lt;li&gt;日付： `&#34;dates&#34; : { }`&lt;/li&gt;&lt;li&gt;バッジ： `&#34;badges&#34; : { }`&lt;/li&gt;&lt;li&gt;集計： `&#34;metric_sets&#34; : { }`&lt;/li&gt;&lt;li&gt;タイムライン： `&#34;sequences&#34; : { }`&lt;/li&gt;&lt;li&gt;ファネル： `&#34;funnels&#34; : { }`&lt;/li&gt;&lt;/ul&gt;|

## 例のレスポンス

```json
{&#34;live&#34;: false,
    &#34;visitor&#34;: {
        &#34;metrics&#34;: {
            &#34;Weeks since first visit&#34;: 0.14,
            &#34;Total referred visits&#34;: 11,
            &#34;Lifetime visit count&#34;: 12,
            &#34;Average visit duration in minutes&#34;: 0.36,
            &#34;Lifetime event count&#34;: 35,
            &#34;Total time spent on site in minutes&#34;: 4.27,
            &#34;Total direct visits&#34;: 1
        },
        &#34;dates&#34;: {
            &#34;Last visit&#34;: 1521217490000,
            &#34;last_visit_start_ts&#34;: 1521217490000,
            &#34;First visit&#34;: 1521134626000
        },
        &#34;properties&#34;: {
            &#34;Lifetime browser versions used (favorite)&#34;: &#34;Chrome&#34;,
            &#34;Lifetime browser types used (favorite)&#34;: &#34;Chrome&#34;,
            &#34;profile&#34;: &#34;main&#34;,
            &#34;Lifetime devices used (favorite)&#34;: &#34;Mac desktop&#34;,
            &#34;Lifetime platforms used (favorite)&#34;: &#34;browser&#34;,
            &#34;Last event URL&#34;: &#34;http://www.tealium.com/&#34;,
            &#34;account&#34;: &#34;tealium&#34;,
            &#34;Lifetime operating systems used (favorite)&#34;: &#34;Mac OS X&#34;
        },
        &#34;flags&#34;: {
            &#34;Returning visitor&#34;: true
        },
        &#34;funnels&#34;: {
            &#34;fake_funnel&#34;: {
                &#34;completed&#34;: true,
                &#34;fake_title&#34;: {
                    &#34;timestamp&#34;: 1655303842639,
                    &#34;snapshot&#34;: {
                        &#34;fake_string&#34;: &#34;fake_string&#34;,
                        &#34;Average visits per week&#34;: 1.0
                    }
                }
            },
            &#34;pii_funnel&#34;: {
                &#34;completed&#34;: true,
                &#34;step2&#34;: {
                    &#34;timestamp&#34;: 1655303842639,
                    &#34;snapshot&#34;: {
                        &#34;pii_string&#34;: &#34;Example string&#34;,
                        &#34;First visit&#34;: 1655303836000,
                        &#34;Last event URL&#34;: &#34;http://172.16.3.15:8000/datacloudtest.html&#34;
                    }
                },
                &#34;step1&#34;: {
                    &#34;timestamp&#34;: 1655303842639,
                    &#34;snapshot&#34;: {
                        &#34;pii_string&#34;: &#34;Example string&#34;
                    }
                }
            }
        },
        &#34;sequences&#34;: {
            &#34;fake_timeline&#34;: [
                {
                    &#34;timestamp&#34;: 1655303842639,
                    &#34;snapshot&#34;: {}
                },
                {
                    &#34;timestamp&#34;: 1655303842642,
                    &#34;snapshot&#34;: {}
                },
                {
                    &#34;timestamp&#34;: 1655303842652,
                    &#34;snapshot&#34;: {}
                },
                {
                    &#34;timestamp&#34;: 1655303842654,
                    &#34;snapshot&#34;: {}
                },
                {
                    &#34;timestamp&#34;: 1655303842665,
                    &#34;snapshot&#34;: {}
                }
            ]
        },
        &#34;audiences&#34;: [
            &#34;fake_visitors&#34;
        ],
        &#34;badges&#34;: [&#34;Unbadged&#34;],
        &#34;metric_sets&#34;: {
            &#34;Lifetime operating systems used&#34;: {
                &#34;Mac OS X&#34;: 12
            },
            &#34;Lifetime devices used&#34;: {
                &#34;Mac desktop&#34;: 12
            },
            &#34;Lifetime browser versions used&#34;: {
                &#34;Chrome&#34;: 12
            },
            &#34;Lifetime browser types used&#34;: {
                &#34;Chrome&#34;: 12
            },
            &#34;Lifetime platforms used&#34;: {
                &#34;browser&#34;: 12
            }
        }
    }
}
```