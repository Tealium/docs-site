---
title: データレイヤーエンリッチメントAPIオブジェクト
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/dle-objects/
---
データレイヤーエンリッチメントAPIオブジェクトには、顧客データプラットフォーム（CDP）の属性に対応する次のプロパティがあります。

|プロパティ| CDP属性 | 説明|
|---| ---|---|
|`audiences`| **オーディエンス**| ユーザーが属する各オーディエンスのキーと値のペアを含むオブジェクトです。キーは`ACCOUNT_PROFILE_ID`、値はオーディエンス名です。例：<br> ``` audiences: {     "tealium_main_208" : "Mobile User",     "tealium_main_209" : "DV Attendee" } ``` |
|`badges`| **バッジ**| ユーザーに割り当てられた各バッジのキーと値のペアを含むオブジェクトです。キーは`BADGE-ID`、値は`true`です。例：<br> ``` badges: {     30: true,     128: true,     323: true } ``` |
|`current_visit`| **訪問属性**| 関連するすべての訪問スコープ属性を含むオブジェクトです。例：<br>``` current_visit: {     dates: { ... },     flags: { ... }, // boolean attributes     metrics: { ... }, // number attributes     properties: { ... }, // string attributes     property_sets: { ... } // set of string attributes } ``` |
|`dates`| **日付**| キーと値のペアを含むオブジェクトです。キーはデータ属性の属性ID、または`audience_account_profile_id_count_ts`形式のオーディエンスIDで、値はUnixタイムスタンプです。例：<br> ``` dates: {     9356: 1491233145706,     audience_tealium_main_103_count_ts: 1532722471000 } ``` |
|`flags`| **ブール値**| 各ブール属性のキーと値のペアを含むオブジェクトです。キーは`BOOLEAN-ID`、値は`true`または`false`です。例：<br>``` flags: {     530: true,     6128: false } ``` |
|`flag_lists`| **ブール値の配列**| キーと値のペアを含むオブジェクトです。キーは`BOOLEAN-ID`、値はブール値（`true`または`false`）の配列です。例：<br> ``` flag_lists: {      620: [true, false, false],     718: [false, true] } ``` |
|`metrics`| **数値**| 各数値属性のキーと値のペアを含むオブジェクトです。キーは属性ID、値は数値です。例：<br> ``` "metrics": {     "5388": 132,     "5390": 113,     "5482": 1,     "5492": 104,     "5500": 1 } ``` |
|`metric_lists`| **数値の配列**| 各数値属性のキーと値のペアを含むオブジェクトです。キーは属性ID、値は数値の配列です。例：<br> ``` `metric_lists: {      432: [15, 248],     519: [61, 47, 962],    674: [9, 16, 21, 53]    },` ``` |
|`metric_sets`| **集計**| 集計属性を表すサブオブジェクトを含むオブジェクトです。キーは属性ID、値は集計の内容を持つオブジェクトです。例： ``` metric_sets: {     57: {         Chrome: 2470,         Firefox: 9,         Safari: 10     } } ``` |
|`properties`| **文字列**| キーと値のペアを含むオブジェクトです。キーは文字列属性のID、値は保存されている値です。例：<br> ``` properties: {     9921: "United States",     9923: "tealium.com" } ``` |
|`property_lists`| **文字列の配列**| 各文字列属性のキーと値のペアを含むオブジェクトです。キーは属性ID、値は文字列の配列です。例：<br> ``` property_lists: {      954: ["North American", "EMEA"],     973: ["Email", "Customer ID", "Phone"] } ``` |
|`property_sets`| **文字列のセット**| キーと値のペアを含むオブジェクトです。キーは属性ID、値は保存されている一意の値の配列です。例：<br> ``` property_sets: {     7604: ["Social", "Display", "DMP", "CRM"],     7606: ["Personalization", "Analytics", "Email"] } ``` |


## レスポンスの例

```json
{
  "metrics": {
    "5601": 10.0,
    "5972": 75.0,
    "5603": 7.0
  },
  "dates": {
    "6229": 1544032032053,
    "5416": 1695422086000
  },
  "properties": {
    "58": "Mac OS X",
    "56": "Chrome",
    "60": "browser",
    "5402": "email"
  },
  "flags": {
    "5905": true,
    "5477": true,
    "5420": true,
    "40008": true
  },
  "property_sets": {
    "7606": ["Personalization", "Analytics", "CRM", "Email"],
    "7604": ["Social", "Display", "Personalization", "DMP", "CRM"]
  },
  "metric_sets": {
    "59": {
      "Mac OS X": 7949.0,
      "Android": 4.0,
      "iOS": 1.0
    },
    "57": {
      "Chrome": 7947.0,
      "Firefox": 9.0,
      "Safari": 11.0
    }
  },
  "property_lists": {
    "66964": ["analytics", "marketing", "personalization"],
    "67245": ["search", "email", "social", "big_data", "misc", "mobile", "monitoring", "crm"]
  },
  "current_visit": {},
  "last_visit_id": "bcead68bf2d7426c15cb8aa85163473edfac0a0768ff880542f256e5858193f0",
  "badges": {
    "24935": true,
    "8879": true,
    "5447": true
  },
  "audiences": {
    "example_main_193": "Has Email",
    "example_main_158": "Platform - Android Users",
    "example_main_208": "Mobile User",
    "example_main_164": "Video Viewers (3+)"
  }
}
```