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
| Main Object | object|  The visitor object with sub-objects for each of the attribute data types: <ul><li>Stitched Visitor IDs: `replaces : [ ]`</li><li>Numbers/Array of Numbers: `"metrics" : { }, "metric_lists" : { }`</li><li>Strings/Array of Strings/Set of Strings: `"properties" : { }, "property_lists" : { }, "property_sets" : { }`</li><li>Booleans/Array of Booleans: `"flags" : { }, "flag_lists" : { }`</li><li>Dates: `"dates" : { }`</li><li>Badges: `"badges" : { }`</li><li>Tallies: `"metric_sets" : { }`</li><li>Timelines: `"sequences" : { }`</li><li>Funnels: `"funnels" : { }`</li></ul> |
| `current_visit` | Object|  <ul><li>Last Event `last_event: { }`</li><li>Events `events: [ {}, {}, ...]`</li></ul> |

## JSON file template

```json
// Visitor Record
{
    // Number attributes (Visitor Scope)
    "metrics": {
        "ATTRIBUTE_NAME": NUMERIC_VALUE,
        ...
    },

    // Date attributes (Visitor Scope)
    "dates": {
        "ATTRIBUTE_NAME": UNIX_TIMESTAMP,
        "audience_ACCOUNT_PROFILE_ID_count_ts": UNIX_TIMESTAMP,
        ...
    },

    // String attributes (Visitor Scope)
    "properties": {
        "ATTRIBUTE_NAME": "STRING_VALUE",
        ...
    },

    // Array of Strings attributes (Visitor Scope)
    "property_lists": {
        "ATTRIBUTE_NAME": ["STRING_VALUE", ...],
        ...
    },

    // Set of Strings attributes (Visitor Scope)
    "property_sets": {
        "ATTRIBUTE_NAME": {
            "STRING_VALUE": 1,
            ...
        },
        ...
    },

    // Boolean attributes (Visitor Scope)
    "flags": {
        "ATTRIBUTE_NAME": true|false,
        ...
    },

    // Visitor Stitching
    "replaces": ["45-CHAR-ALPHANUMERIC", "__ACCOUNT_PROFILE__ATTRIBUTE_ID_VALUE__", ...],

    // Audiences
    "audiences": ["AUDIENCE_NAME", ...],

    // Badges
    "badges": ["BADGE_NAME", ...],

    "preloaded": false,

    // Array of Numbers
    "metric_lists": {
        "ATTRIBUTE_NAME": [VALUE, ...],
        ...
    },

    // Tallies (Visitor Scope)
    "metric_sets": {
        "ATTRIBUTE_NAME": {
            "ENTRY_NAME": VALUE,
            ...
        },
        ...
    },
    "creation_ts": UNIX_TIMESTAMP,
    "_id": "GUID",
    "_partition": NUMBER,
    "shard_token": NUMBER,

    // Timelines (Visitor Scope)
    "sequences": {
        "ATTRIBUTE_NAME": [
            {
                "timestamp": UNIX_TIMESTAMP,
                "snapshot": {
                    "ATTRIBUTE_NAME": "STRING_VALUE"
                }
            },
            ...
        ]
    },

    // Funnels (Visitor Scope)
    "funnels": {
        "ATTRIBUTE_NAME": {
            "completed": true|false,
            "steps": {
                "1": {
                    "timestamp": UNIX_TIMESTAMP,
                    "snapshot": {
                        "ATTRIBUTE_NAME": "STRING_VALUE"
                    }
                },
                "2": {
                    "timestamp": UNIX_TIMESTAMP
                },
                ...
            }
        }
    },

    // Current Visit Record
    "current_visit": {
        // Number attributes (Visit scope)
        "metrics": {
            "ATTRIBUTE_NAME": NUMERIC_VALUE,
            ...
        },

        // Date attributes (Visit scope)
        "dates": {
            "ATTRIBUTE_NAME": UNIX_TIMESTAMP,
            ...
            "last_event_ts": UNIX_TIMESTAMP
        },

        // String attributes (Visit scope)
        "properties": {
            "ATTRIBUTE_NAME": "STRING_VALUE",
            ...
        },

        // Boolean attributes (Visitor Scope)
        "flags": {
            "ATTRIBUTE_NAME": true|false,
            ...
        },

        // Events From Current Visit
        "events": [{
            "account": "ACCOUNT",
            "profile": "PROFILE",
            "selector": "2",
            "env": "prod",
            "tags": {
                "TAG_UID": {
                    "executed": true|false,
                    "type": VENDOR_ID,
                    "profile": "PROFILE"
                },
                ...
            }
            "data": {
                // Built-In DOM Variables
                "dom": {
                    "viewport_height": 976,
                    "referrer": "https://www.google.com/",
                    "viewport_width": 1680,
                    "domain": "example.com",
                    "title": "PAGE_TITLE",
                    "query_string": "",
                    "hash": "",
                    "url": "FULL_URL",
                    "pathname": "/"
                },

                // Universal Data Object variables
                "udo": {
                    "UDO_VARIABLE_NAME" : "VALUE",
                    ...
                    "tealium_account": "ACCOUNT",
                    "tealium_datasource": "DATA_SOURCE_KEY",
                    "tealium_environment": "prod",
                    "tealium_event": "view",
                    "tealium_firstparty_visitor_id": "45-CHAR-ALPHANUMERIC",
                    "tealium_library_name": "utag.js",
                    "tealium_library_version": "4.44.0",
                    "tealium_profile": "PROFILE"
                    "tealium_random": "MATH_RANDOM",
                    "tealium_session_id": "UNIX_TIMESTAMP",
                    "tealium_timestamp_epoch": UNIX_TIMESTAMP,
                    "tealium_timestamp_local": "YYYY-MM-DDTHH:MM:SS.mmm",
                    "tealium_timestamp_utc": "2017-10-29T23:10:24.363Z",
                    "tealium_visitor_id": "45-CHAR-ALPHANUMERIC"
                },

                // Javascript Page Variables
                "js": {
                    "VARIABLE_NAME": VALUE,
                    ...
                },

                // Cookies
                "firstparty_tealium_cookies": {
                    "utag_main_v_id": "45-CHAR-ALPHANUMERIC",
                    "COOKIE_NAME" : VALUE,
                    ...
                },

                // Meta Data Variables
                "meta": {
                    "META_TAG_NAME": VALUE,
                    ...
                }
            },
            "type": "LIVE",
            "enrichmentOnly": false,
            "event_id": "GUID",
            "visitor_id": "45-CHAR-ALPHANUMERIC",
            "post_time": UNIX_TIMESTAMP,
            "page_url": {
                "full_url": "URL",
                "scheme": "https",
                "domain": "example.com",
                "path": "/"
            },
            "referrer_url": {
                "full_url": "FULL_URL",
                "scheme": "https",
                "domain": "example.com",
                "path": "/"
            },
            "useragent": "USER_AGENT",
            "client_ip": "IP_ADDRESS",
            "_dctrace": ["COLLECTION_SERVER", ...],
            "new_visitor": true|false
        }],

        // Sets of Strings
        "property_sets": {
            "SET_NAME": ["VALUE", ...],
            ...
        },
        "creation_ts": UNIX_TIMESTAMP,
        "_id": "GUID",
        "shard_token": NUMERIC_VALUE,
        "last_event": {
            "account": "ACCOUNT",
            "profile": "PROFILE",
            "selector": "2",
            "env": "prod",
            "tags": {
                "TAG_UID": {
                    "executed": true|false,
                    "type": VENDOR_ID,
                    "profile": "PROFILE"
                },
                ...
            },
            "data": {
                // Built-In DOM Variables
                "dom": {
                    "viewport_height": 976,
                    "referrer": "https://www.google.com/",
                    "viewport_width": 1680,
                    "domain": "example.com",
                    "title": "PAGE_TITLE",
                    "query_string": "",
                    "hash": "",
                    "url": "FULL_URL",
                    "pathname": "/"
                },
                // Universal Data Object variables
                "udo": {
                    "UDO_VARIABLE_NAME" : "VALUE",
                    ...
                    "tealium_account": "ACCOUNT",
                    "tealium_datasource": "DATA_SOURCE_KEY",
                    "tealium_environment": "prod",
                    "tealium_event": "view",
                    "tealium_firstparty_visitor_id": "45-CHAR-ALPHANUMERIC",
                    "tealium_library_name": "utag.js",
                    "tealium_library_version": "4.44.0",
                    "tealium_profile": "PROFILE"
                    "tealium_random": "MATH_RANDOM",
                    "tealium_session_id": "UNIX_TIMESTAMP",
                    "tealium_timestamp_epoch": UNIX_TIMESTAMP,
                    "tealium_timestamp_local": "YYYY-MM-DDTHH:MM:SS.mmm",
                    "tealium_timestamp_utc": "2017-10-29T23:10:24.363Z",
                    "tealium_visitor_id": "45-CHAR-ALPHANUMERIC"
                },
                // Javascript Page Variables
                "js": {
                    "VARIABLE_NAME": VALUE,
                    ...
                },
                // Cookies
                "firstparty_tealium_cookies": {
                    "utag_main_v_id": "45-CHAR-ALPHANUMERIC",
                    "COOKIE_NAME" : VALUE,
                    ...
                },
                // Meta Data Variables
                "meta": {
                    "META_TAG_NAME": VALUE,
                    ...
                }
            },
            "type": "LIVE",
            "enrichmentOnly": true|false,
            "event_id": "GUID",
            "visitor_id": "45-CHAR-ALPHANUMERIC",
            "post_time": UNIX_TIMESTAMP,
            "page_url": {
                "full_url": "URL",
                "scheme": "https",
                "domain": "example.com",
                "path": "/"
            },
            "referrer_url": {
                "full_url": "FULL_URL",
                "scheme": "https",
                "domain": "example.com",
                "path": "/"
            },
            "useragent": "USER_AGENT",
            "client_ip": "IP_ADDRESS",
            "_dctrace": ["COLLECTION_SERVER", ...],
            "new_visitor": true|false
        },
        "_dc_ttl_": 1800000,
        "total_event_count": 2,
        "events_compressed": false
    },
    "_dctrace": ["COLLECTION_SERVER_ID", ...],
    "new_visitor": true|false,
    "audiences_joined_at": {
        "ACCOUNT_PROFILE_AUDIENCE_ID": {
            "$date": "YYYY-MM-DDTHH:MM:SS.mmmZ"
        },
        ...
    },
    "last_visit_id": "GUID"
},
// Additional Visitor Records
...
```
