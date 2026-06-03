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
|`visitor`| object|  The visitor object with sub-objects for each of the attribute data types: &lt;ul&gt;&lt;li&gt;Visitor IDs: `secondary_ids : { }`&lt;/li&gt;&lt;li&gt; Numbers/Array of Numbers:&lt;br&gt; `&#34;metrics&#34; : { }`&lt;br&gt; `&#34;metric_lists&#34; : { }`&lt;/li&gt;&lt;li&gt;Strings/Array of Strings/Set of Strings: &lt;br&gt;`&#34;properties&#34; : { }`&lt;br&gt; `&#34;property_lists&#34; : { }`&lt;br&gt; `&#34;property_sets&#34; : { }`&lt;br&gt; `&#34;audiences&#34; : { }`&lt;/li&gt;&lt;li&gt;Booleans/Array of Booleans:&lt;br&gt; `&#34;flags&#34; : { }`&lt;br&gt; `&#34;flag_lists&#34; : { }`&lt;/li&gt;&lt;li&gt;Dates: `&#34;dates&#34; : { }`&lt;/li&gt;&lt;li&gt;Badges: `&#34;badges&#34; : { }`&lt;/li&gt;&lt;li&gt;Tallies: `&#34;metric_sets&#34; : { }`&lt;/li&gt;&lt;/ul&gt;|

## Example Response

```json
{
    &#34;live&#34;: false,
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

