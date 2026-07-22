---
title: Event and visitor functions V3
description: This article provides information on event and visitor functions that use the V3 runtime.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/event-visitor-v3/
---
## activate() function

When you create a V3 event or visitor function, the default code is shown in the **Code** tab of the functions code editor. This code contains the `activate()` function and its input parameters.

Event functions have an [`event object`](#event-object) and a [`helper` object](#helper-object).

```js
activate(async ({ event, helper }) => {
  ...
});
```

Visitor functions have a [`visitor` object](#visitor-object), a [`visit` object](#visit-object), and a [`helper` object](#helper-object).

```js
activate(async ({ visitor, visit, helper }) => {
  ...
});
```

The `helper` parameter provides `helper.getAuth()` and `helper.getGlobalVariable()` for getting authorization and retrieving global variables.

Change the code between the first and last lines of the default code to suit your needs.


<blockquote>
Authentication tokens can only be referenced by a function within an HTTP request. If you try to reference the token outside of an HTTP request, the token is replaced by a UUID placeholder.
</blockquote>


## track() function

Functions can use the global `track()` method to send an event to Tealium Collect.

`track()` has two input parameters:

* `data` object: The event data to be sent to Tealium Collect.
* `config` object: (Optional) Contains the following fields:
    * `tealium_account`: The account name.
    * `tealium_profile`: The profile name.
    * `tealium_datasource`: The data source key.  
    If the `tealium_account`, `tealium_profile`, and `tealium_datasource` fields are included in the `data` object, the `config` object is not required.


<blockquote>
Each function invocation can make a maximum of six calls to `track()`.
</blockquote>


The following example shows `track()` called with the `data` and `config` parameters:

```js
track(data, {
            tealium_account: event.account,
            tealium_profile: event.profile,
            tealium_datasource: 'x3p4b7'
        })  
        .then(response => {

        // Code to process the response goes here

        })
```

The following example shows `track()` called with only the `data` parameter:

```js
track(data)  
  .then(response => {

    // Code to process the response goes here

  })
```

For a more detailed example for the `track()` function, see [Send an event to the Tealium Collect HTTP API](https://docs.tealium.com/v3-event-visitor-function-examples/#send-an-event-to-the-tealium-collect-http-api).

## Event object

The `event` data object is available for event functions and contains the event data.


<blockquote>
At the point that event functions run in the data pipeline, modifications to the event data object have no effect on other parts of the system. To modify event data to effect the data pipeline, use either event attribute enrichments or a [data transformation function](https://docs.tealium.com/about-data-transformation-functions/).
</blockquote>


| Property | Data Type | Description |
| --- | --- | --- |
| `account` | string | Tealium account. |
| `data` | object | Data layer, which contains event data. |
| `env` | string | Execution environment. Value can be `qa`, `dev`, or `prod`. |
| `event_id` | string | Tealium event ID. |
| `post_time` | number | Timestamp indicating when the event occurred. |
| `profile` | string | Tealium profile. |
| `useragent` | string | A string that represents the user agent, such as the browser. |
| `visitor_id` | string | Tealium visitor ID. |
| `function getAttributeNameById(id)` | string | Returns a string containing the name of the specified attribute. `id` is a string that specifies the attribute ID. |
| `function getAttributeValueById(id)` | any | Returns the value of the specified attribute. `id` is a string that specifies the attribute ID. |

The `data` object contains the data for the incoming event.

| Property | Type | Description |
| --- | --- | --- |
| `dom` | Object | Standard page data. |
| `firstparty_tealium_cookies` | Object | All the cookies from the browser. |
| `js` | Object | JavaScript variables from the page. |
| `meta` | Object | Data from the meta tags on the web page. |
| `udo` | Object | Universal Data Object that contains the properties of the incoming event. |

### Event object example

The following shows an example of event object data:

```json
{
  "account": "your-account",
  "profile": "main",
  "event_id": "run-test-event-id",
  "visitor_id": "run-test-visitor-id",
  "data": {
    "dom": {
      "viewport_height": 766,
      "referrer": "",
      "viewport_width": 1440,
      "domain": "www.example.com",
      "title": "Home Page",
      "query_string": "q=help",
      "hash": "",
      "url": "https://www.example.com/?q=help",
      "pathname": "/"
    },
    "udo": {
      "tealium_event": "page_view",
      "ut.account": "your-account",
      "ut.visitor_id": "0176cb4f3482110a5ba4702e147b0006d005a065104f2",
      "page_name": "Home Page",
      "ut.event": "view",
      "search_keyword": "help",
      "ut.domain": "example.com",
      "tealium_profile": "main",
      "ut.version": "ut4.46.202006020705",
      "tealium_session_id": "1609910608323",
      "tealium_account": "your-account",
      "ut.profile": "main"
    },
    "firstparty_tealium_cookies": {
      "utag_main__sn": "12",
      "utag_main_dc_visit": "12",
      "utag_main_ses_id": "1609910610822",
      "utag_main_dc_region": "us-east-1",
      "utag_main__st": "1609913306118",
      "utag_main_v_id": "0176cb4f3482110a5ba4702e147b0006d005a065104f2",
      "utag_main__se": "66",
      "utag_main__ss": "0",
      "utag_main_dc_event": "60",
      "utag_main__pn": "5"
    }
  },
  "env": "prod",
  "post_time": 1537305808000
}
```

## Visitor object

The `visitor` data object is available for visitor functions and contains the visitor data.


<blockquote>
At the point that visitor functions run in the data pipeline, modifications to the visitor data object have no effect on other parts of the system. To make modifications to the visitor data object that persist in the system, use visitor attribute enrichments.
</blockquote>


| **Property** | **Data Type** | **Description**  |
| --- | --- | --- |
| `badges` | string[] | Badge attributes. |
| `metrics` | object(key, number) | Number attributes. |
| `properties` | object(key, string) | String attributes. |
| `dates` | object(key, epoch) | Dates attributes in epoch format. |
| `flags` | object(key, boolean) | Boolean attributes. |
| `metrics_sets` | object(key, object(key, number)) | Tally attributes. |
| `property_sets` | object(key, string[]) | Set of strings attributes. |
| `funnels` | object (see example) | Funnel attributes. |
| `sequences` | object (see example) | Timeline attributes. |
| `property_lists` | object(key, string[]) | Array of strings attributes. |
| `metric_lists` | object(key, number[]) | Array of numbers attributes. |
| `flag_lists` | object(key, boolean[]) | Array of booleans attributes. |
| `secondary_ids` | string | User identifiers such as email address, social media ID, or customer ID. |
| `audiences` | string[] | Audiences that the visitor is currently in. |
| `creation_ts` | epoch | Visitor creation timestamp. |
| `new_visitor` | boolean | Indicates whether this is a new visitor. |
| `audiences_joined_at` | number | Timestamps for when the visitor joined audiences. |
| `current_visit` | visit object | Data for the current visit. |
| `function getAttributeNameById(id)` | string | Returns a string containing the name of the specified attribute ID. `id` is a string that contains the attribute ID. |
| `function getAttributeValueById(id)` | any | Returns the value of the specified attribute ID. `id` is a string that contains the attribute ID.

### Visitor object example

The following is an example of `visitor` object data:

```json
{
    "metrics": {
        "Metric 1": 1,
        "Metric 2": 2
    },
    "dates": {
        "Date 1": 1603373790000,
        "Date 2": 1603373522000
    },
    "properties": {
        "profile": "username",
        "visitor_id": "017560818b67001bc185a07f1cd703078003405000b7e",
        "account": "user-account"
    },
    "metrics_sets": {
        "Product Categories Purchased": {
            "Shoes": 1,
            "Pants": 3,
            "Shirts": 7,
            "Shorts": 2
        }
    },
    "sequences": {
        "Hotel Search Timeline": [
            {
                "timestamp": 1681858801598,
                "snapshot": {
                    "Searched Hotel City": "Paradise Island"
                }
            },
            {
                "timestamp": 1681860398985,
                "snapshot": {
                    "Searched Hotel City": "Skokie"
                }
            },
            {
                "timestamp": 1681860423335,
                "snapshot": {
                    "Searched Hotel City": "Las Vegas"
                }
            }
        ]
    },
    "funnels": {
        "Purchase Funnel": {
            "completed": true,
            "steps": {
                "1": {
                    "timestamp": 1636661624226,
                    "snapshot": {
                        "product_name": "Skinny Jeans"
                    }
                },
                "2": {
                    "timestamp": 1636661624227
                },
                "3": {
                    "timestamp": 1636661624228
                },
                "4": {
                    "timestamp": 1636661624229,
                    "snapshot": {
                        "order_id": "0123456789",
                        "order_total": "34.98"
                    }
                }
            }
        }
    },
    "audiences": [
        "Audience 1",
        "Audience 2"
    ],
    "badges": [
        "Badge 1",
        "Badge 2"
    ],
    "creation_ts": 1603373522000,
    "current_visit": {
        "metrics": {
            "Metric 1": 1.3,
            "Metric 2": 6
        },
        "dates": {
            "Date 1": 1603373868000,
            "Date 2": 1603373790000
        },
        "properties": {
            "Property 1": "Chrome",
            "Property 2": "https://URL-for-website "
        },
        "flags": {
            "Flag 1": true,
            "Flag 2": false
        },
        "property_sets": {
            "Property Set 1": [
                "Mac desktop"
            ],
            "Property Set 2": [
                "Chrome"
            ]
        },
        "creation_ts": 1603373790000,
        "total_event_count": 2,
        "events_compressed": false
    },
    "audiences_joined_at": {
        "Audience 1": 1603363523014,
        "Audience 2": 1603363523014
    }
}
```

## Visit object

The `visit` object is available for visitor functions and contains the data for the current visit.


<blockquote>
At the point that visitor functions run in the data pipeline, modifications to the visit data object have no effect on other parts of the system. To make modifications to the visit data object that persist in the system, use visit attribute enrichments.
</blockquote>


| **Property** | **Data Type** | **Description** |
| --- | --- | --- |
| `metrics` | object(key, number) | Number attributes. |
| `properties` | object(key, string) | String attributes. |
| `dates` | object(key, epoch) | Dates attributes in epoch format. |
| `flags` | object(key, boolean) | Boolean attributes. |
| `metrics_sets` | object(key, object(key, number)) | Tally attributes. |
| `property_sets` | object(key, string[]) | Set of strings attributes. |
| `funnels` | object (see example) | Funnel attributes. |
| `sequences` | object (see example) | Timeline attributes. |
| `property_lists` | object(key, string[]) | Array of strings attributes. |
| `metric_lists` | object(key, number[]) | Array of numbers attributes. |
| `flag_lists` | object(key, boolean[]) | Array of booleans attributes. |
| `events_compressed` | boolean | Indicates whether events are compressed. |
| `total_event_count` | number | Total number of events. |
| `creation_ts` | number | Visitor creation timestamp. |
| `function getAttributeNameById(id)` | string | Returns a string containing the name of the specified attribute ID. `id` is a string that contains the attribute ID. |
| `function getAttributeValueById(id)` | any | Returns the value of the specified attribute ID. `id` is a string that contains the attribute ID. |

### Visit object example

The following is an example of `visit` object data:

```json
{
    "metrics": {
        "Metric 1": 1.3,
        "Metric 2": 6
    },
    "dates": {
        "Date 1": 1603373868000,
        "Date 2": 1603373790000
    },
    "properties": {
        "Property 1": "Chrome",
        "Property 2": "https://URL-for-website "
    },
    "flags": {
        "Flag 1": true,
        "Flag 2": false
    },
    "metrics_sets": {
        "Product Categories Purchased": {
            "Shoes": 1,
            "Pants": 3,
            "Shirts": 7,
            "Shorts": 2
        }
    },
    "property_sets": {
        "Property Set 1": [
            "Mac desktop"
        ],
        "Property Set 2": [
            "Chrome"
        ]
    },
    "sequences": {
        "Hotel Search Timeline": [
            {
                "timestamp": 1681858801598,
                "snapshot": {
                    "Searched Hotel City": "Paradise Island"
                }
            },
            {
                "timestamp": 1681860398985,
                "snapshot": {
                    "Searched Hotel City": "Skokie"
                }
            },
            {
                "timestamp": 1681860423335,
                "snapshot": {
                    "Searched Hotel City": "Las Vegas"
                }
            }
        ]
    },
    "funnels": {
        "Purchase Funnel": {
            "completed": true,
            "steps": {
                "1": {
                    "timestamp": 1636661624226,
                    "snapshot": {
                        "product_name": "Skinny Jeans"
                    }
                },
                "2": {
                    "timestamp": 1636661624227
                },
                "3": {
                    "timestamp": 1636661624228
                },
                "4": {
                    "timestamp": 1636661624229,
                    "snapshot": {
                        "order_id": "0123456789",
                        "order_total": "34.98"
                    }
                }
            }
        }
    },
    "creation_ts": 1603373790000,
    "total_event_count": 2,
    "events_compressed": false
}
```

## Helper object

The `helper` object provides the `helper.getGlobalVariable()` and `helper.getAuth()` methods.

### `helper.getGlobalVariable()`

Functions use `helper.getGlobalVariable()` to retrieve global variables.

To retrieve a global variable, pass the key as a parameter: 

```
activate(({ helper }) => {
  console.log(helper.getGlobalVariable("TEST_GLOBAL_VAR"));
});
```

For more information about adding and editing global variables, see [Manage global variables]().

### `helper.getAuth()`

Functions use `helper.getAuth()` to retrieve an authentication that has been added to the function. 

To retrieve an authentication, pass the name of the authentication token as the parameter:

```
activate(({ helper }) => {
    console.log(helper.getAuth("auth_token_name"));
})
```

For information on adding authentication to a function, see [Add authentication to an event or visitor function]().


<blockquote>
Authentication tokens can only be referenced by a function within an HTTP request. If you try to reference the token outside of an HTTP request, the token is replaced by a UUID placeholder.
</blockquote>
