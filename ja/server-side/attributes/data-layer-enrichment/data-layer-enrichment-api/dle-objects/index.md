---
title: データレイヤーエンリッチメントAPIオブジェクト
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/dle-objects/
---
データレイヤーエンリッチメントAPIオブジェクトには、AudienceStream属性に対応する以下のプロパティがあります：

|プロパティ| AudienceStream属性 | 説明|
|---| ---|---|
|`audiences`|  **Audiences**| ユーザーが所属する各オーディエンスのキーと値のペアを含むオブジェクトで、キーは `ACCOUNT_PROFILE_ID` で、値はオーディエンスの名前です。例：&lt;br&gt; ``` audiences: {     &#34;tealium_main_208&#34; : &#34;Mobile User&#34;,     &#34;tealium_main_209&#34; : &#34;DV Attendee&#34; } ``` |
|`badges`|  **Badges**| ユーザーに割り当てられた各バッジのキーと値のペアを含むオブジェクトで、キーは `BADGE-ID` で、値は `true` です。例：&lt;br&gt; ``` badges: {     30: true,     128: true,     323: true } ``` |
|`current_visit`|  **Visit Attributes**| 関連する訪問スコープの属性をすべて含むオブジェクト。例：&lt;br&gt;``` current_visit: {     dates: { ... },     flags: { ... }, // boolean attributes     metrics: { ... }, // number attributes     properties: { ... }, // string attributes     property_sets: { ... } // set of string attributes } ``` |
|`dates`|  **Dates**| キーがデータ属性の属性IDまたは `audience_account_profile_id_count_ts` 形式のオーディエンスIDで、値がUnixタイムスタンプであるキーと値のペアを含むオブジェクト。例：&lt;br&gt; ``` dates: {     9356: 1491233145706,     audience_tealium_main_103_count_ts: 1532722471000 } ``` |
|`flags`|  **Booleans**| 各ブール属性のキーと値のペアを含むオブジェクトで、キーは`BOOLEAN-ID`で、値は `true` または `false` です。例: &lt;br&gt;``` flags: {     530: true,     6128: false } ``` |
|`flag_lists`|  **Arrays of Booleans**| キーと値のペアを含むオブジェクトで、キーは`BOOLEAN-ID`で、値はブール値（`true` または `false`）の配列です。例:&lt;br&gt; ``` flag_lists: {      620: [true, false, false],     718: [false, true] } ``` |
|`metrics`|  **Numbers**| 各数値属性のキーと値のペアを含むオブジェクトで、キーは属性IDで、値は数値です。例:&lt;br&gt; ``` &#34;metrics&#34;: {     &#34;5388&#34;: 132,     &#34;5390&#34;: 113,     &#34;5482&#34;: 1,     &#34;5492&#34;: 104,     &#34;5500&#34;: 1 } ``` |
|`metric_lists`|  **Arrays of Numbers**| 各数値属性のキーと値のペアを含むオブジェクトで、キーは属性IDで、値は数値の配列です。例: &lt;br&gt; ``` `metric_lists: {      432: [15, 248],     519: [61, 47, 962],    674: [9, 16, 21, 53]    },` ``` |
|`metric_sets`|  **Tallies**| キーが属性のIDで、値が集計の内容を持つオブジェクトであるサブオブジェクトを含むオブジェクト。例: ``` metric_sets: {     57: {         Chrome: 2470,         Firefox: 9,         Safari: 10     } } ``` |
|`properties`|  **Strings**| キーが文字列属性のIDで、値が保存された値であるキーと値のペアを含むオブジェクト。例:&lt;br&gt; ``` properties: {     9921: &#34;United States&#34;,     9923: &#34;tealium.com&#34; } ``` |
|`property_lists`|  **Arrays of Strings**| 各文字列属性のキーと値のペアを含むオブジェクトで、キーは属性IDで、値は文字列の配列です。例:&lt;br&gt; ``` property_lists: {      954: [&#34;North American&#34;, &#34;EMEA&#34;],     973: [&#34;Email&#34;, &#34;Customer ID&#34;, &#34;Phone&#34;] } ``` |
|`property_sets`|  **Sets of Strings**| キーが属性のIDで、値が保存された一意の値の配列であるキーと値のペアを含むオブジェクト。例:&lt;br&gt; ``` property_sets: {     7604: [&#34;Social&#34;, &#34;Display&#34;, &#34;DMP&#34;, &#34;CRM&#34;],     7606: [&#34;Personalization&#34;, &#34;Analytics&#34;, &#34;Email&#34;] } ``` |


## 例のレスポンス

```json
{
  &#34;metrics&#34;: {
    &#34;5601&#34;: 10.0,
    &#34;5972&#34;: 75.0,
    &#34;5603&#34;: 7.0
  },
  &#34;dates&#34;: {
    &#34;6229&#34;: 1544032032053,
    &#34;5416&#34;: 1695422086000
  },
  &#34;properties&#34;: {
    &#34;58&#34;: &#34;Mac OS X&#34;,
    &#34;56&#34;: &#34;Chrome&#34;,
    &#34;60&#34;: &#34;browser&#34;,
    &#34;5402&#34;: &#34;email&#34;
  },
  &#34;flags&#34;: {
    &#34;5905&#34;: true,
    &#34;5477&#34;: true,
    &#34;5420&#34;: true,
    &#34;40008&#34;: true
  },
  &#34;property_sets&#34;: {
    &#34;7606&#34;: [&#34;Personalization&#34;, &#34;Analytics&#34;, &#34;CRM&#34;, &#34;Email&#34;],
    &#34;7604&#34;: [&#34;Social&#34;, &#34;Display&#34;, &#34;Personalization&#34;, &#34;DMP&#34;, &#34;CRM&#34;]
  },
  &#34;metric_sets&#34;: {
    &#34;59&#34;: {
      &#34;Mac OS X&#34;: 7949.0,
      &#34;Android&#34;: 4.0,
      &#34;iOS&#34;: 1.0
    },
    &#34;57&#34;: {
      &#34;Chrome&#34;: 7947.0,
      &#34;Firefox&#34;: 9.0,
      &#34;Safari&#34;: 11.0
    }
  },
  &#34;property_lists&#34;: {
    &#34;66964&#34;: [&#34;analytics&#34;, &#34;marketing&#34;, &#34;personalization&#34;],
    &#34;67245&#34;: [&#34;search&#34;, &#34;email&#34;, &#34;social&#34;, &#34;big_data&#34;, &#34;misc&#34;, &#34;mobile&#34;, &#34;monitoring&#34;, &#34;crm&#34;]
  },
  &#34;current_visit&#34;: {},
  &#34;last_visit_id&#34;: &#34;bcead68bf2d7426c15cb8aa85163473edfac0a0768ff880542f256e5858193f0&#34;,
  &#34;badges&#34;: {
    &#34;24935&#34;: true,
    &#34;8879&#34;: true,
    &#34;5447&#34;: true
  },
  &#34;audiences&#34;: {
    &#34;example_main_193&#34;: &#34;Has Email&#34;,
    &#34;example_main_158&#34;: &#34;Platform - Android Users&#34;,
    &#34;example_main_208&#34;: &#34;Mobile User&#34;,
    &#34;example_main_164&#34;: &#34;Video Viewers (3&#43;)&#34;
  }
}
```