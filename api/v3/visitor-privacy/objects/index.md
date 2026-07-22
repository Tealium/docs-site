---
title: Visitor Privacy API objects
description: Visitors are returned as JSON objects.
url: https://docs.tealium.com/api/v3/visitor-privacy/objects/
---
## Visitor fields

Visitors are returned as JSON objects that contain the following fields:

|Object Name| Type| Description|
|---| ---| ---|
|`live`| Boolean|  Set to `true` if the visitor is currently in a live session. |
|`visitor`| object|  The visitor object with sub-objects for each of the attribute data types: <ul><li>Visitor IDs: `secondary_ids : { }`</li><li> Numbers/Array of Numbers:<br> `"metrics" : { }`<br> `"metric_lists" : { }`</li><li>Strings/Array of Strings/Set of Strings: <br>`"properties" : { }`<br> `"property_lists" : { }`<br> `"property_sets" : { }`<br> `"audiences" : { }`</li><li>Booleans/Array of Booleans:<br> `"flags" : { }`<br> `"flag_lists" : { }`</li><li>Dates: `"dates" : { }`</li><li>Badges: `"badges" : { }`</li><li>Tallies: `"metric_sets" : { }`</li></ul>|

## Example Response

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

