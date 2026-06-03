---
title: Data Layer Enrichment API objects
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/dle-objects/
---
The Data Layer Enrichment API object has the following properties that correspond to AudienceStream attributes:

|Property| AudienceStream attribute | Description|
|---| ---|---|
|`audiences`|  **Audiences**| Object containing key-value pairs for each audience the user is in, where the key is `ACCOUNT_PROFILE_ID` and the value is the name of the audience. Example:&lt;br&gt; ``` audiences: {     &#34;tealium_main_208&#34; : &#34;Mobile User&#34;,     &#34;tealium_main_209&#34; : &#34;DV Attendee&#34; } ``` |
|`badges`|  **Badges**| Object containing key-value pairs for each badge assigned to the user, where the key is `BADGE-ID` and the value is `true`. Example:&lt;br&gt; ``` badges: {     30: true,     128: true,     323: true } ``` |
|`current_visit`|  **Visit Attributes**| Object containing all the relevant visit-scoped attributes. Example:&lt;br&gt;``` current_visit: {     dates: { ... },     flags: { ... }, // boolean attributes     metrics: { ... }, // number attributes     properties: { ... }, // string attributes     property_sets: { ... } // set of string attributes } ``` |
|`dates`|  **Dates**| Object containing key-value pairs where the key is the attribute ID of the data attribute or an audience ID in the form of `audience_account_profile_id_count_ts` and the value is a Unix timestamp. Example:&lt;br&gt; ``` dates: {     9356: 1491233145706,     audience_tealium_main_103_count_ts: 1532722471000 } ``` |
|`flags`|  **Booleans**| Object containing key-value pairs for each Boolean attribute, where the key is`BOOLEAN-ID` and the value is `true` or `false`. Example: &lt;br&gt;``` flags: {     530: true,     6128: false } ``` |
|`flag_lists`|  **Arrays of Booleans**| Object containing key-value pairs, where the key is`BOOLEAN-ID` and the value is an array of Booleans (`true` or `false`). Example:&lt;br&gt; ``` flag_lists: {      620: [true, false, false],     718: [false, true] } ``` |
|`metrics`|  **Numbers**| Object containing key-value pairs for each number attribute, where the key is the attribute ID and the value is numeric. Example:&lt;br&gt; ``` &#34;metrics&#34;: {     &#34;5388&#34;: 132,     &#34;5390&#34;: 113,     &#34;5482&#34;: 1,     &#34;5492&#34;: 104,     &#34;5500&#34;: 1 } ``` |
|`metric_lists`|  **Arrays of Numbers**| Object containing key-value pairs for each number attribute, where the key is the attribute ID and the value is an array of numeric values. Example: &lt;br&gt; ``` `metric_lists: {      432: [15, 248],     519: [61, 47, 962],    674: [9, 16, 21, 53]    },` ``` |
|`metric_sets`|  **Tallies**| Object containing sub-object representing tally attributes where the keys are the ID of the attribute and the value is an object with the contents of the tally. Example: ``` metric_sets: {     57: {         Chrome: 2470,         Firefox: 9,         Safari: 10     } } ``` |
|`properties`|  **Strings**| Object containing key-value pairs where the keys are the IDs of string attributes and the values are the stored values. Example:&lt;br&gt; ``` properties: {     9921: &#34;United States&#34;,     9923: &#34;tealium.com&#34; } ``` |
|`property_lists`|  **Arrays of Strings**| Object containing key-value pairs for each string attribute, where the key is the attribute ID and the value is an array of strings. Example:&lt;br&gt; ``` property_lists: {      954: [&#34;North American&#34;, &#34;EMEA&#34;],     973: [&#34;Email&#34;, &#34;Customer ID&#34;, &#34;Phone&#34;] } ``` |
|`property_sets`|  **Sets of Strings**| Object containing key-value pairs where the key is the ID of the attribute and the value is an array of the stored unique values. Example:&lt;br&gt; ``` property_sets: {     7604: [&#34;Social&#34;, &#34;Display&#34;, &#34;DMP&#34;, &#34;CRM&#34;],     7606: [&#34;Personalization&#34;, &#34;Analytics&#34;, &#34;Email&#34;] } ``` |


## Example response

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
