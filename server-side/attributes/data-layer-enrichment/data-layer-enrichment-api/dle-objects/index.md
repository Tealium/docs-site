---
title: Data Layer Enrichment API objects
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/dle-objects/
---
The Data Layer Enrichment API object has the following properties that correspond to AudienceStream attributes:

|Property| AudienceStream attribute | Description|
|---| ---|---|
|`audiences`|  **Audiences**| Object containing key-value pairs for each audience the user is in, where the key is `ACCOUNT_PROFILE_ID` and the value is the name of the audience. Example:<br> ``` audiences: {     "tealium_main_208" : "Mobile User",     "tealium_main_209" : "DV Attendee" } ``` |
|`badges`|  **Badges**| Object containing key-value pairs for each badge assigned to the user, where the key is `BADGE-ID` and the value is `true`. Example:<br> ``` badges: {     30: true,     128: true,     323: true } ``` |
|`current_visit`|  **Visit Attributes**| Object containing all the relevant visit-scoped attributes. Example:<br>``` current_visit: {     dates: { ... },     flags: { ... }, // boolean attributes     metrics: { ... }, // number attributes     properties: { ... }, // string attributes     property_sets: { ... } // set of string attributes } ``` |
|`dates`|  **Dates**| Object containing key-value pairs where the key is the attribute ID of the data attribute or an audience ID in the form of `audience_account_profile_id_count_ts` and the value is a Unix timestamp. Example:<br> ``` dates: {     9356: 1491233145706,     audience_tealium_main_103_count_ts: 1532722471000 } ``` |
|`flags`|  **Booleans**| Object containing key-value pairs for each Boolean attribute, where the key is`BOOLEAN-ID` and the value is `true` or `false`. Example: <br>``` flags: {     530: true,     6128: false } ``` |
|`flag_lists`|  **Arrays of Booleans**| Object containing key-value pairs, where the key is`BOOLEAN-ID` and the value is an array of Booleans (`true` or `false`). Example:<br> ``` flag_lists: {      620: [true, false, false],     718: [false, true] } ``` |
|`metrics`|  **Numbers**| Object containing key-value pairs for each number attribute, where the key is the attribute ID and the value is numeric. Example:<br> ``` "metrics": {     "5388": 132,     "5390": 113,     "5482": 1,     "5492": 104,     "5500": 1 } ``` |
|`metric_lists`|  **Arrays of Numbers**| Object containing key-value pairs for each number attribute, where the key is the attribute ID and the value is an array of numeric values. Example: <br> ``` `metric_lists: {      432: [15, 248],     519: [61, 47, 962],    674: [9, 16, 21, 53]    },` ``` |
|`metric_sets`|  **Tallies**| Object containing sub-object representing tally attributes where the keys are the ID of the attribute and the value is an object with the contents of the tally. Example: ``` metric_sets: {     57: {         Chrome: 2470,         Firefox: 9,         Safari: 10     } } ``` |
|`properties`|  **Strings**| Object containing key-value pairs where the keys are the IDs of string attributes and the values are the stored values. Example:<br> ``` properties: {     9921: "United States",     9923: "tealium.com" } ``` |
|`property_lists`|  **Arrays of Strings**| Object containing key-value pairs for each string attribute, where the key is the attribute ID and the value is an array of strings. Example:<br> ``` property_lists: {      954: ["North American", "EMEA"],     973: ["Email", "Customer ID", "Phone"] } ``` |
|`property_sets`|  **Sets of Strings**| Object containing key-value pairs where the key is the ID of the attribute and the value is an array of the stored unique values. Example:<br> ``` property_sets: {     7604: ["Social", "Display", "DMP", "CRM"],     7606: ["Personalization", "Analytics", "Email"] } ``` |


## Example response

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
