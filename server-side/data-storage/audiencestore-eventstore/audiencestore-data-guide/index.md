---
title: AudienceStore data guide
description: This article is a summary of the visitor-level attributes that are made available through AudienceStore.
url: https://docs.tealium.com/server-side/data-storage/audiencestore-eventstore/audiencestore-data-guide/
---
AudienceStore provides the most efficient way for collecting and exporting visitor-level data from AudienceStream. Visitor data is compressed into a flattened JSON file and made available for download from Tealium’s Amazon S3 bucket. Each file contains multiple JSON objects representing each visitor record in the audience.

## Create, update, and delete operations on visitor records

* **Visitor record creation**  
Visitor records are created after a session ends. It takes about an hour for the records to appear in DataAccess.

* **Visitor record updates**  
When a visitor revisits a site, the visitor record is updated at the end of the session. If [visitor stitching]() is initiated for a visitor record, the existing profile is temporarily deleted and the stitched profile is re-inserted.

* **Visitor record deletions**  
Visitor records are deleted based on the retention period specified in your contract. Visitor records that have not been updated within the retention period are deleted and cannot be recovered. For example, for a retention period of 30 days, all visitor records that have not been updated in the previous 30 days are deleted.

## Data sent to AudienceStore
                                 
The AudienceStore connector, which sends visitor data to AudienceStore, has a **Send Visitor Data** action, which is used to send visitor record data. If the **Include Current Visit Data** option is selected for this action, the `events` array in the `current_visit` object only includes event attributes that are also defined in AudienceStream (as an attribute or an enrichment).

The following event data attributes are always included in the `events` array:

```
_dc_ttl_
_dctrace
account
consent_*
cp.CONSENTMGR
enrichmentOnly
env
event_id
new_visitor
page_url
post_time
profile
profile_revision
selector
tags
tealium_*
trace_id
type
useragent
visitor_id
```

## Visitor record format

Visitor records (profiles) are stored as JSON objects that contain the following fields:

|Object Name| Type| Description|
|---| ---| ---|
| Main Object | object|  The visitor object with sub-objects for each of the attribute data types: &lt;ul&gt;&lt;li&gt;Stitched Visitor IDs: `replaces : [ ]`&lt;/li&gt;&lt;li&gt;Numbers/Array of Numbers: `&#34;metrics&#34; : { }, &#34;metric_lists&#34; : { }`&lt;/li&gt;&lt;li&gt;Strings/Array of Strings/Set of Strings: `&#34;properties&#34; : { }, &#34;property_lists&#34; : { }, &#34;property_sets&#34; : { }`&lt;/li&gt;&lt;li&gt;Booleans/Array of Booleans: `&#34;flags&#34; : { }, &#34;flag_lists&#34; : { }`&lt;/li&gt;&lt;li&gt;Dates: `&#34;dates&#34; : { }`&lt;/li&gt;&lt;li&gt;Badges: `&#34;badges&#34; : { }`&lt;/li&gt;&lt;li&gt;Tallies: `&#34;metric_sets&#34; : { }`&lt;/li&gt;&lt;li&gt;Timelines: `&#34;sequences&#34; : { }`&lt;/li&gt;&lt;li&gt;Funnels: `&#34;funnels&#34; : { }`&lt;/li&gt;&lt;/ul&gt; |
| `current_visit` | Object|  &lt;ul&gt;&lt;li&gt;Last Event `last_event: { }`&lt;/li&gt;&lt;li&gt;Events `events: [ {}, {}, ...]`&lt;/li&gt;&lt;/ul&gt; |

## JSON file template

```json
// Visitor Record
{
    // Number attributes (Visitor Scope)
    &#34;metrics&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: NUMERIC_VALUE,
        ...
    },

    // Date attributes (Visitor Scope)
    &#34;dates&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: UNIX_TIMESTAMP,
        &#34;audience_ACCOUNT_PROFILE_ID_count_ts&#34;: UNIX_TIMESTAMP,
        ...
    },

    // String attributes (Visitor Scope)
    &#34;properties&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: &#34;STRING_VALUE&#34;,
        ...
    },

    // Array of Strings attributes (Visitor Scope)
    &#34;property_lists&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: [&#34;STRING_VALUE&#34;, ...],
        ...
    },

    // Set of Strings attributes (Visitor Scope)
    &#34;property_sets&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: {
            &#34;STRING_VALUE&#34;: 1,
            ...
        },
        ...
    },

    // Boolean attributes (Visitor Scope)
    &#34;flags&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: true|false,
        ...
    },

    // Visitor Stitching
    &#34;replaces&#34;: [&#34;45-CHAR-ALPHANUMERIC&#34;, &#34;__ACCOUNT_PROFILE__ATTRIBUTE_ID_VALUE__&#34;, ...],

    // Audiences
    &#34;audiences&#34;: [&#34;AUDIENCE_NAME&#34;, ...],

    // Badges
    &#34;badges&#34;: [&#34;BADGE_NAME&#34;, ...],

    &#34;preloaded&#34;: false,

    // Array of Numbers
    &#34;metric_lists&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: [VALUE, ...],
        ...
    },

    // Tallies (Visitor Scope)
    &#34;metric_sets&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: {
            &#34;ENTRY_NAME&#34;: VALUE,
            ...
        },
        ...
    },
    &#34;creation_ts&#34;: UNIX_TIMESTAMP,
    &#34;_id&#34;: &#34;GUID&#34;,
    &#34;_partition&#34;: NUMBER,
    &#34;shard_token&#34;: NUMBER,

    // Timelines (Visitor Scope)
    &#34;sequences&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: [
            {
                &#34;timestamp&#34;: UNIX_TIMESTAMP,
                &#34;snapshot&#34;: {
                    &#34;ATTRIBUTE_NAME&#34;: &#34;STRING_VALUE&#34;
                }
            },
            ...
        ]
    },

    // Funnels (Visitor Scope)
    &#34;funnels&#34;: {
        &#34;ATTRIBUTE_NAME&#34;: {
            &#34;completed&#34;: true|false,
            &#34;steps&#34;: {
                &#34;1&#34;: {
                    &#34;timestamp&#34;: UNIX_TIMESTAMP,
                    &#34;snapshot&#34;: {
                        &#34;ATTRIBUTE_NAME&#34;: &#34;STRING_VALUE&#34;
                    }
                },
                &#34;2&#34;: {
                    &#34;timestamp&#34;: UNIX_TIMESTAMP
                },
                ...
            }
        }
    },

    // Current Visit Record
    &#34;current_visit&#34;: {
        // Number attributes (Visit scope)
        &#34;metrics&#34;: {
            &#34;ATTRIBUTE_NAME&#34;: NUMERIC_VALUE,
            ...
        },

        // Date attributes (Visit scope)
        &#34;dates&#34;: {
            &#34;ATTRIBUTE_NAME&#34;: UNIX_TIMESTAMP,
            ...
            &#34;last_event_ts&#34;: UNIX_TIMESTAMP
        },

        // String attributes (Visit scope)
        &#34;properties&#34;: {
            &#34;ATTRIBUTE_NAME&#34;: &#34;STRING_VALUE&#34;,
            ...
        },

        // Boolean attributes (Visitor Scope)
        &#34;flags&#34;: {
            &#34;ATTRIBUTE_NAME&#34;: true|false,
            ...
        },

        // Events From Current Visit
        &#34;events&#34;: [{
            &#34;account&#34;: &#34;ACCOUNT&#34;,
            &#34;profile&#34;: &#34;PROFILE&#34;,
            &#34;selector&#34;: &#34;2&#34;,
            &#34;env&#34;: &#34;prod&#34;,
            &#34;tags&#34;: {
                &#34;TAG_UID&#34;: {
                    &#34;executed&#34;: true|false,
                    &#34;type&#34;: VENDOR_ID,
                    &#34;profile&#34;: &#34;PROFILE&#34;
                },
                ...
            }
            &#34;data&#34;: {
                // Built-In DOM Variables
                &#34;dom&#34;: {
                    &#34;viewport_height&#34;: 976,
                    &#34;referrer&#34;: &#34;https://www.google.com/&#34;,
                    &#34;viewport_width&#34;: 1680,
                    &#34;domain&#34;: &#34;example.com&#34;,
                    &#34;title&#34;: &#34;PAGE_TITLE&#34;,
                    &#34;query_string&#34;: &#34;&#34;,
                    &#34;hash&#34;: &#34;&#34;,
                    &#34;url&#34;: &#34;FULL_URL&#34;,
                    &#34;pathname&#34;: &#34;/&#34;
                },

                // Universal Data Object variables
                &#34;udo&#34;: {
                    &#34;UDO_VARIABLE_NAME&#34; : &#34;VALUE&#34;,
                    ...
                    &#34;tealium_account&#34;: &#34;ACCOUNT&#34;,
                    &#34;tealium_datasource&#34;: &#34;DATA_SOURCE_KEY&#34;,
                    &#34;tealium_environment&#34;: &#34;prod&#34;,
                    &#34;tealium_event&#34;: &#34;view&#34;,
                    &#34;tealium_firstparty_visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
                    &#34;tealium_library_name&#34;: &#34;utag.js&#34;,
                    &#34;tealium_library_version&#34;: &#34;4.44.0&#34;,
                    &#34;tealium_profile&#34;: &#34;PROFILE&#34;
                    &#34;tealium_random&#34;: &#34;MATH_RANDOM&#34;,
                    &#34;tealium_session_id&#34;: &#34;UNIX_TIMESTAMP&#34;,
                    &#34;tealium_timestamp_epoch&#34;: UNIX_TIMESTAMP,
                    &#34;tealium_timestamp_local&#34;: &#34;YYYY-MM-DDTHH:MM:SS.mmm&#34;,
                    &#34;tealium_timestamp_utc&#34;: &#34;2017-10-29T23:10:24.363Z&#34;,
                    &#34;tealium_visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;
                },

                // Javascript Page Variables
                &#34;js&#34;: {
                    &#34;VARIABLE_NAME&#34;: VALUE,
                    ...
                },

                // Cookies
                &#34;firstparty_tealium_cookies&#34;: {
                    &#34;utag_main_v_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
                    &#34;COOKIE_NAME&#34; : VALUE,
                    ...
                },

                // Meta Data Variables
                &#34;meta&#34;: {
                    &#34;META_TAG_NAME&#34;: VALUE,
                    ...
                }
            },
            &#34;type&#34;: &#34;LIVE&#34;,
            &#34;enrichmentOnly&#34;: false,
            &#34;event_id&#34;: &#34;GUID&#34;,
            &#34;visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
            &#34;post_time&#34;: UNIX_TIMESTAMP,
            &#34;page_url&#34;: {
                &#34;full_url&#34;: &#34;URL&#34;,
                &#34;scheme&#34;: &#34;https&#34;,
                &#34;domain&#34;: &#34;example.com&#34;,
                &#34;path&#34;: &#34;/&#34;
            },
            &#34;referrer_url&#34;: {
                &#34;full_url&#34;: &#34;FULL_URL&#34;,
                &#34;scheme&#34;: &#34;https&#34;,
                &#34;domain&#34;: &#34;example.com&#34;,
                &#34;path&#34;: &#34;/&#34;
            },
            &#34;useragent&#34;: &#34;USER_AGENT&#34;,
            &#34;client_ip&#34;: &#34;IP_ADDRESS&#34;,
            &#34;_dctrace&#34;: [&#34;COLLECTION_SERVER&#34;, ...],
            &#34;new_visitor&#34;: true|false
        }],

        // Sets of Strings
        &#34;property_sets&#34;: {
            &#34;SET_NAME&#34;: [&#34;VALUE&#34;, ...],
            ...
        },
        &#34;creation_ts&#34;: UNIX_TIMESTAMP,
        &#34;_id&#34;: &#34;GUID&#34;,
        &#34;shard_token&#34;: NUMERIC_VALUE,
        &#34;last_event&#34;: {
            &#34;account&#34;: &#34;ACCOUNT&#34;,
            &#34;profile&#34;: &#34;PROFILE&#34;,
            &#34;selector&#34;: &#34;2&#34;,
            &#34;env&#34;: &#34;prod&#34;,
            &#34;tags&#34;: {
                &#34;TAG_UID&#34;: {
                    &#34;executed&#34;: true|false,
                    &#34;type&#34;: VENDOR_ID,
                    &#34;profile&#34;: &#34;PROFILE&#34;
                },
                ...
            },
            &#34;data&#34;: {
                // Built-In DOM Variables
                &#34;dom&#34;: {
                    &#34;viewport_height&#34;: 976,
                    &#34;referrer&#34;: &#34;https://www.google.com/&#34;,
                    &#34;viewport_width&#34;: 1680,
                    &#34;domain&#34;: &#34;example.com&#34;,
                    &#34;title&#34;: &#34;PAGE_TITLE&#34;,
                    &#34;query_string&#34;: &#34;&#34;,
                    &#34;hash&#34;: &#34;&#34;,
                    &#34;url&#34;: &#34;FULL_URL&#34;,
                    &#34;pathname&#34;: &#34;/&#34;
                },
                // Universal Data Object variables
                &#34;udo&#34;: {
                    &#34;UDO_VARIABLE_NAME&#34; : &#34;VALUE&#34;,
                    ...
                    &#34;tealium_account&#34;: &#34;ACCOUNT&#34;,
                    &#34;tealium_datasource&#34;: &#34;DATA_SOURCE_KEY&#34;,
                    &#34;tealium_environment&#34;: &#34;prod&#34;,
                    &#34;tealium_event&#34;: &#34;view&#34;,
                    &#34;tealium_firstparty_visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
                    &#34;tealium_library_name&#34;: &#34;utag.js&#34;,
                    &#34;tealium_library_version&#34;: &#34;4.44.0&#34;,
                    &#34;tealium_profile&#34;: &#34;PROFILE&#34;
                    &#34;tealium_random&#34;: &#34;MATH_RANDOM&#34;,
                    &#34;tealium_session_id&#34;: &#34;UNIX_TIMESTAMP&#34;,
                    &#34;tealium_timestamp_epoch&#34;: UNIX_TIMESTAMP,
                    &#34;tealium_timestamp_local&#34;: &#34;YYYY-MM-DDTHH:MM:SS.mmm&#34;,
                    &#34;tealium_timestamp_utc&#34;: &#34;2017-10-29T23:10:24.363Z&#34;,
                    &#34;tealium_visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;
                },
                // Javascript Page Variables
                &#34;js&#34;: {
                    &#34;VARIABLE_NAME&#34;: VALUE,
                    ...
                },
                // Cookies
                &#34;firstparty_tealium_cookies&#34;: {
                    &#34;utag_main_v_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
                    &#34;COOKIE_NAME&#34; : VALUE,
                    ...
                },
                // Meta Data Variables
                &#34;meta&#34;: {
                    &#34;META_TAG_NAME&#34;: VALUE,
                    ...
                }
            },
            &#34;type&#34;: &#34;LIVE&#34;,
            &#34;enrichmentOnly&#34;: true|false,
            &#34;event_id&#34;: &#34;GUID&#34;,
            &#34;visitor_id&#34;: &#34;45-CHAR-ALPHANUMERIC&#34;,
            &#34;post_time&#34;: UNIX_TIMESTAMP,
            &#34;page_url&#34;: {
                &#34;full_url&#34;: &#34;URL&#34;,
                &#34;scheme&#34;: &#34;https&#34;,
                &#34;domain&#34;: &#34;example.com&#34;,
                &#34;path&#34;: &#34;/&#34;
            },
            &#34;referrer_url&#34;: {
                &#34;full_url&#34;: &#34;FULL_URL&#34;,
                &#34;scheme&#34;: &#34;https&#34;,
                &#34;domain&#34;: &#34;example.com&#34;,
                &#34;path&#34;: &#34;/&#34;
            },
            &#34;useragent&#34;: &#34;USER_AGENT&#34;,
            &#34;client_ip&#34;: &#34;IP_ADDRESS&#34;,
            &#34;_dctrace&#34;: [&#34;COLLECTION_SERVER&#34;, ...],
            &#34;new_visitor&#34;: true|false
        },
        &#34;_dc_ttl_&#34;: 1800000,
        &#34;total_event_count&#34;: 2,
        &#34;events_compressed&#34;: false
    },
    &#34;_dctrace&#34;: [&#34;COLLECTION_SERVER_ID&#34;, ...],
    &#34;new_visitor&#34;: true|false,
    &#34;audiences_joined_at&#34;: {
        &#34;ACCOUNT_PROFILE_AUDIENCE_ID&#34;: {
            &#34;$date&#34;: &#34;YYYY-MM-DDTHH:MM:SS.mmmZ&#34;
        },
        ...
    },
    &#34;last_visit_id&#34;: &#34;GUID&#34;
},
// Additional Visitor Records
...
```
