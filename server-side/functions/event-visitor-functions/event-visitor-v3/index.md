---
title: Event and visitor functions V3
description: This article provides information on event and visitor functions that use the V3 runtime.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/event-visitor-v3/
---
## activate() function

When you create a V3 event or visitor function, the default code is shown in the **Code** tab of the functions code editor. This code contains the `activate()` function and its input parameters.

Event functions have an [`event object`](#event-object) and a [`helper` object](#helper-object).

```js
activate(async ({ event, helper }) =&gt; {
  ...
});
```

Visitor functions have a [`visitor` object](#visitor-object), a [`visit` object](#visit-object), and a [`helper` object](#helper-object).

```js
activate(async ({ visitor, visit, helper }) =&gt; {
  ...
});
```

The `helper` parameter provides `helper.getAuth()` and `helper.getGlobalVariable()` for getting authorization and retrieving global variables.

Change the code between the first and last lines of the default code to suit your needs.

Authentication tokens can only be referenced by a function within an HTTP request. If you try to reference the token outside of an HTTP request, the token is replaced by a UUID placeholder.

## track() function

Functions can use the global `track()` method to send an event to Tealium Collect.

`track()` has two input parameters:

* `data` object: The event data to be sent to Tealium Collect.
* `config` object: (Optional) Contains the following fields:
    * `tealium_account`: The account name.
    * `tealium_profile`: The profile name.
    * `tealium_datasource`: The data source key.  
    If the `tealium_account`, `tealium_profile`, and `tealium_datasource` fields are included in the `data` object, the `config` object is not required.

Each function invocation can make a maximum of six calls to `track()`.

The following example shows `track()` called with the `data` and `config` parameters:

```js
track(data, {
            tealium_account: event.account,
            tealium_profile: event.profile,
            tealium_datasource: &#39;x3p4b7&#39;
        })  
        .then(response =&gt; {

        // Code to process the response goes here

        })
```

The following example shows `track()` called with only the `data` parameter:

```js
track(data)  
  .then(response =&gt; {

    // Code to process the response goes here

  })
```

For a more detailed example for the `track()` function, see [Send an event to the Tealium Collect HTTP API]().

## Event object

The `event` data object is available for event functions and contains the event data.

At the point that event functions run in the data pipeline, modifications to the event data object have no effect on other parts of the system. To modify event data to effect the data pipeline, use either event attribute enrichments or a [data transformation function]().

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
  &#34;account&#34;: &#34;your-account&#34;,
  &#34;profile&#34;: &#34;main&#34;,
  &#34;event_id&#34;: &#34;run-test-event-id&#34;,
  &#34;visitor_id&#34;: &#34;run-test-visitor-id&#34;,
  &#34;data&#34;: {
    &#34;dom&#34;: {
      &#34;viewport_height&#34;: 766,
      &#34;referrer&#34;: &#34;&#34;,
      &#34;viewport_width&#34;: 1440,
      &#34;domain&#34;: &#34;www.example.com&#34;,
      &#34;title&#34;: &#34;Home Page&#34;,
      &#34;query_string&#34;: &#34;q=help&#34;,
      &#34;hash&#34;: &#34;&#34;,
      &#34;url&#34;: &#34;https://www.example.com/?q=help&#34;,
      &#34;pathname&#34;: &#34;/&#34;
    },
    &#34;udo&#34;: {
      &#34;tealium_event&#34;: &#34;page_view&#34;,
      &#34;ut.account&#34;: &#34;your-account&#34;,
      &#34;ut.visitor_id&#34;: &#34;0176cb4f3482110a5ba4702e147b0006d005a065104f2&#34;,
      &#34;page_name&#34;: &#34;Home Page&#34;,
      &#34;ut.event&#34;: &#34;view&#34;,
      &#34;search_keyword&#34;: &#34;help&#34;,
      &#34;ut.domain&#34;: &#34;example.com&#34;,
      &#34;tealium_profile&#34;: &#34;main&#34;,
      &#34;ut.version&#34;: &#34;ut4.46.202006020705&#34;,
      &#34;tealium_session_id&#34;: &#34;1609910608323&#34;,
      &#34;tealium_account&#34;: &#34;your-account&#34;,
      &#34;ut.profile&#34;: &#34;main&#34;
    },
    &#34;firstparty_tealium_cookies&#34;: {
      &#34;utag_main__sn&#34;: &#34;12&#34;,
      &#34;utag_main_dc_visit&#34;: &#34;12&#34;,
      &#34;utag_main_ses_id&#34;: &#34;1609910610822&#34;,
      &#34;utag_main_dc_region&#34;: &#34;us-east-1&#34;,
      &#34;utag_main__st&#34;: &#34;1609913306118&#34;,
      &#34;utag_main_v_id&#34;: &#34;0176cb4f3482110a5ba4702e147b0006d005a065104f2&#34;,
      &#34;utag_main__se&#34;: &#34;66&#34;,
      &#34;utag_main__ss&#34;: &#34;0&#34;,
      &#34;utag_main_dc_event&#34;: &#34;60&#34;,
      &#34;utag_main__pn&#34;: &#34;5&#34;
    }
  },
  &#34;env&#34;: &#34;prod&#34;,
  &#34;post_time&#34;: 1537305808000
}
```

## Visitor object

The `visitor` data object is available for visitor functions and contains the visitor data.

At the point that visitor functions run in the data pipeline, modifications to the visitor data object have no effect on other parts of the system. To make modifications to the visitor data object that persist in the system, use visitor attribute enrichments.

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
    &#34;metrics&#34;: {
        &#34;Metric 1&#34;: 1,
        &#34;Metric 2&#34;: 2
    },
    &#34;dates&#34;: {
        &#34;Date 1&#34;: 1603373790000,
        &#34;Date 2&#34;: 1603373522000
    },
    &#34;properties&#34;: {
        &#34;profile&#34;: &#34;username&#34;,
        &#34;visitor_id&#34;: &#34;017560818b67001bc185a07f1cd703078003405000b7e&#34;,
        &#34;account&#34;: &#34;user-account&#34;
    },
    &#34;metrics_sets&#34;: {
        &#34;Product Categories Purchased&#34;: {
            &#34;Shoes&#34;: 1,
            &#34;Pants&#34;: 3,
            &#34;Shirts&#34;: 7,
            &#34;Shorts&#34;: 2
        }
    },
    &#34;sequences&#34;: {
        &#34;Hotel Search Timeline&#34;: [
            {
                &#34;timestamp&#34;: 1681858801598,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Paradise Island&#34;
                }
            },
            {
                &#34;timestamp&#34;: 1681860398985,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Skokie&#34;
                }
            },
            {
                &#34;timestamp&#34;: 1681860423335,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Las Vegas&#34;
                }
            }
        ]
    },
    &#34;funnels&#34;: {
        &#34;Purchase Funnel&#34;: {
            &#34;completed&#34;: true,
            &#34;steps&#34;: {
                &#34;1&#34;: {
                    &#34;timestamp&#34;: 1636661624226,
                    &#34;snapshot&#34;: {
                        &#34;product_name&#34;: &#34;Skinny Jeans&#34;
                    }
                },
                &#34;2&#34;: {
                    &#34;timestamp&#34;: 1636661624227
                },
                &#34;3&#34;: {
                    &#34;timestamp&#34;: 1636661624228
                },
                &#34;4&#34;: {
                    &#34;timestamp&#34;: 1636661624229,
                    &#34;snapshot&#34;: {
                        &#34;order_id&#34;: &#34;0123456789&#34;,
                        &#34;order_total&#34;: &#34;34.98&#34;
                    }
                }
            }
        }
    },
    &#34;audiences&#34;: [
        &#34;Audience 1&#34;,
        &#34;Audience 2&#34;
    ],
    &#34;badges&#34;: [
        &#34;Badge 1&#34;,
        &#34;Badge 2&#34;
    ],
    &#34;creation_ts&#34;: 1603373522000,
    &#34;current_visit&#34;: {
        &#34;metrics&#34;: {
            &#34;Metric 1&#34;: 1.3,
            &#34;Metric 2&#34;: 6
        },
        &#34;dates&#34;: {
            &#34;Date 1&#34;: 1603373868000,
            &#34;Date 2&#34;: 1603373790000
        },
        &#34;properties&#34;: {
            &#34;Property 1&#34;: &#34;Chrome&#34;,
            &#34;Property 2&#34;: &#34;https://URL-for-website &#34;
        },
        &#34;flags&#34;: {
            &#34;Flag 1&#34;: true,
            &#34;Flag 2&#34;: false
        },
        &#34;property_sets&#34;: {
            &#34;Property Set 1&#34;: [
                &#34;Mac desktop&#34;
            ],
            &#34;Property Set 2&#34;: [
                &#34;Chrome&#34;
            ]
        },
        &#34;creation_ts&#34;: 1603373790000,
        &#34;total_event_count&#34;: 2,
        &#34;events_compressed&#34;: false
    },
    &#34;audiences_joined_at&#34;: {
        &#34;Audience 1&#34;: 1603363523014,
        &#34;Audience 2&#34;: 1603363523014
    }
}
```

## Visit object

The `visit` object is available for visitor functions and contains the data for the current visit.

At the point that visitor functions run in the data pipeline, modifications to the visit data object have no effect on other parts of the system. To make modifications to the visit data object that persist in the system, use visit attribute enrichments.

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
    &#34;metrics&#34;: {
        &#34;Metric 1&#34;: 1.3,
        &#34;Metric 2&#34;: 6
    },
    &#34;dates&#34;: {
        &#34;Date 1&#34;: 1603373868000,
        &#34;Date 2&#34;: 1603373790000
    },
    &#34;properties&#34;: {
        &#34;Property 1&#34;: &#34;Chrome&#34;,
        &#34;Property 2&#34;: &#34;https://URL-for-website &#34;
    },
    &#34;flags&#34;: {
        &#34;Flag 1&#34;: true,
        &#34;Flag 2&#34;: false
    },
    &#34;metrics_sets&#34;: {
        &#34;Product Categories Purchased&#34;: {
            &#34;Shoes&#34;: 1,
            &#34;Pants&#34;: 3,
            &#34;Shirts&#34;: 7,
            &#34;Shorts&#34;: 2
        }
    },
    &#34;property_sets&#34;: {
        &#34;Property Set 1&#34;: [
            &#34;Mac desktop&#34;
        ],
        &#34;Property Set 2&#34;: [
            &#34;Chrome&#34;
        ]
    },
    &#34;sequences&#34;: {
        &#34;Hotel Search Timeline&#34;: [
            {
                &#34;timestamp&#34;: 1681858801598,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Paradise Island&#34;
                }
            },
            {
                &#34;timestamp&#34;: 1681860398985,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Skokie&#34;
                }
            },
            {
                &#34;timestamp&#34;: 1681860423335,
                &#34;snapshot&#34;: {
                    &#34;Searched Hotel City&#34;: &#34;Las Vegas&#34;
                }
            }
        ]
    },
    &#34;funnels&#34;: {
        &#34;Purchase Funnel&#34;: {
            &#34;completed&#34;: true,
            &#34;steps&#34;: {
                &#34;1&#34;: {
                    &#34;timestamp&#34;: 1636661624226,
                    &#34;snapshot&#34;: {
                        &#34;product_name&#34;: &#34;Skinny Jeans&#34;
                    }
                },
                &#34;2&#34;: {
                    &#34;timestamp&#34;: 1636661624227
                },
                &#34;3&#34;: {
                    &#34;timestamp&#34;: 1636661624228
                },
                &#34;4&#34;: {
                    &#34;timestamp&#34;: 1636661624229,
                    &#34;snapshot&#34;: {
                        &#34;order_id&#34;: &#34;0123456789&#34;,
                        &#34;order_total&#34;: &#34;34.98&#34;
                    }
                }
            }
        }
    },
    &#34;creation_ts&#34;: 1603373790000,
    &#34;total_event_count&#34;: 2,
    &#34;events_compressed&#34;: false
}
```

## Helper object

The `helper` object provides the `helper.getGlobalVariable()` and `helper.getAuth()` methods.

### `helper.getGlobalVariable()`

Functions use `helper.getGlobalVariable()` to retrieve global variables.

To retrieve a global variable, pass the key as a parameter: 

```
activate(({ helper }) =&gt; {
  console.log(helper.getGlobalVariable(&#34;TEST_GLOBAL_VAR&#34;));
});
```

For more information about adding and editing global variables, see [Manage global variables]().

### `helper.getAuth()`

Functions use `helper.getAuth()` to retrieve an authentication that has been added to the function. 

To retrieve an authentication, pass the name of the authentication token as the parameter:

```
activate(({ helper }) =&gt; {
    console.log(helper.getAuth(&#34;auth_token_name&#34;));
})
```

For information on adding authentication to a function, see [Add authentication to an event or visitor function]().

Authentication tokens can only be referenced by a function within an HTTP request. If you try to reference the token outside of an HTTP request, the token is replaced by a UUID placeholder.