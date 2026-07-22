---
title: 訪問プライバシーAPIオブジェクト
description: 訪問はJSONオブジェクトとして返されます。
url: https://docs.tealium.com/ja/api/v3/visitor-privacy/objects/
---
## 訪問フィールド

訪問は、以下のフィールドを含むJSONオブジェクトとして返されます：

|オブジェクト名| タイプ| 説明|
|---| ---| ---|
|`live`| Boolean|  訪問が現在ライブセッション中である場合は`true`に構成します。 |
|`visitor`| object|  属性データタイプごとのサブオブジェクトを持つ訪問オブジェクト：<ul><li>訪問ID：`secondary_ids : { }`</li><li> 数値/数値の配列：<br> `"metrics" : { }`<br> `"metric_lists" : { }`</li><li>文字列/文字列の配列/文字列のセット：<br>`"properties" : { }`<br> `"property_lists" : { }`<br> `"property_sets" : { }`<br> `"audiences" : { }`</li><li>ブール値/ブール値の配列：<br> `"flags" : { }`<br> `"flag_lists" : { }`</li><li>日付：`"dates" : { }`</li><li>バッジ：`"badges" : { }`</li><li>集計：`"metric_sets" : { }`</li></ul>|

## 例のレスポンス

```json
{
    "live": false,
    "visitor": {
        "metrics": {
            "Weeks since first visit": 0.14,
            "Total referred visits": 11,
            "Lifetime visit count": 12,
            "Average visit duration in minutes": 0.36,
            "Lifetime event count": 35,
            "Total time spent on site in minutes": 4.27,
            "Total direct visits": 1
        },
        "dates": {
            "Last visit": 1521217490000,
            "last_visit_start_ts": 1521217490000,
            "First visit": 1521134626000
        },
        "properties": {
            "Lifetime browser versions used (favorite)": "Chrome",
            "Lifetime browser types used (favorite)": "Chrome",
            "profile": "main",
            "Lifetime devices used (favorite)": "Mac desktop",
            "Lifetime platforms used (favorite)": "browser",
            "Last event URL": "http://www.tealium.com/",
            "account": "tealium",
            "Lifetime operating systems used (favorite)": "Mac OS X"
        },
        "flags": {
            "Returning visitor": true
        },
        "badges": ["Unbadged"],
        "metric_sets": {
            "Lifetime operating systems used": {
                "Mac OS X": 12
            },
            "Lifetime devices used": {
                "Mac desktop": 12
            },
            "Lifetime browser versions used": {
                "Chrome": 12
            },
            "Lifetime browser types used": {
                "Chrome": 12
            },
            "Lifetime platforms used": {
                "browser": 12
            }
        }
    }
}

```