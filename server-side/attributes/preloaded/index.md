---
title: Preloaded attributes
description: This article describes preloaded attributes.
url: https://docs.tealium.com/server-side/attributes/preloaded/
---
## How it works

For your convenience, AudienceStream and EventStream contain a set of preloaded event, visit, and visitor attributes. Each attribute is configured to collect statistical information that can help you determine useful information about each visitor or visit. These attributes do not require additional data beyond the standard event data from the [Tealium Collect tag]().

 Preloaded attributes cannot be modified, but you can duplicate them and modify the copy. The duplicate contains all of the enrichments and rules from the original. 

## Visitor attributes

| Visitor attributes |  ID |  Type |  Description|  Enrichments |
|-----|-----|-----|-----|-----|
|Average visit duration in minutes| 26 | Number  | The average visit duration in minutes.| Set ratio `Average visit duration in minutes` to `Total time spent on site in minutes` divided by `Lifetime visit count` when visit ended. |
|Average visits per week| 29 | Number | Average visits per week.| Set ratio  `Average visits per week` to `Lifetime visit count` divided by `Weeks since first visit` when new visit if `Weeks since first visit` is greater than or equal to `1`. |
|Fan| 30|  Badge| The visitor has visited more than two times and has more direct visits than referrals.| Assign `Fan` badge to visitor when new visit if `Total direct visits` is greater than `Total referred visits`. |
|First visit| 23 | Date | The date of the first visit.| Set `First visit_copy` to  `Last event timestamp` when new visitor. |
|Frequent visitor|  31 | Badge| The visitor has averages two or more visits a week.| Remove `Frequent visitor` badge from visitor when new visit if `Average visits per week` is less than `2` and assign `Frequent visitor` to visitor when new visit if `Average visits per week` is greater than or equal to `2`. |
|Last event URL | 17 | String | The last event URL for the visitor. | Set string `Last event URL` to `Current URL` when any event. |
|Last visit | 24 | Date | The date of the last visit.| Set `Last visit` to Last event timestamp when visit ended. |
|Lifetime browser types used| 57 | Tally| A tally of how many times each type of browser is used.| For tally `Lifetime browser types used` increment all values by `1` if found in `Active browser types` when visit ended. |
|Lifetime browser types used (favorite)|  56 | String | The favorite item out of the Lifetime browser types used attribute.| Automatically generated from Lifetime browser types used. |
|Lifetime browser versions used | 63 | Tally| A tally of browser versions used.| For tally `Lifetime browser versions used` increment all values by `1` if found in `Active browser versions` when visit ended. |
|Lifetime browser versions used (favorite)| 62 | String | The favorite out of the Lifetime browser versions used attribute.| Automatically generated from Lifetime browser versions used.|
|Lifetime devices used| 55 | Tally | A tally of devices used| For tally `Lifetime devices used` increment all values by `1` if found in `Active devices` when visit ended. | 
|Lifetime devices used (favorite) | 54 | String | The favorite item out of the Lifetime devices used attribute.| Automatically generated from Lifetime devices used.|
|Lifetime event count | 22 | Number | The total number of events triggered by user.| Increment number `Lifetime event count` by `1` when any event. |
|Lifetime operating systems used| 59 | Tally |A tally of operating systems used.| For tally `Lifetime operating systems used` increment all values by `1` if found in `Active operating systems` when visit ended. |
|Lifetime operating systems used (favorite) | 58 | String|  The favorite item out of the Lifetime operating systems used attribute| Automatically generated from Lifetime operating systems used. |
|Lifetime platforms used |61 | Tally| A tally of platforms used.| For tally `Lifetime platforms used` increment all values by `1` if found in `Active platforms` when visit ended. |
|Lifetime platforms used (favorite) | 60 | String | The favorite item out of the Lifetime platforms used attribute.| Automatically generated from Lifetime platforms used.|
|Lifetime visit count | 21  |Number | Total number of times user has visited site.| &lt;ul&gt;&lt;li&gt;Set ratio `Average visit duration in minutes` to `Total time spent on site in minutes` divided by `Lifetime visit count` when visit ended.&lt;/li&gt;&lt;li&gt;Set ratio `Average visits per week` to `Lifetime visit count` divided by `Weeks since first visit` when new visit if `Weeks since first visit` is greater than or equal to `1`.&lt;/li&gt;&lt;/ul&gt; |
|Returning visitor| 27 | Boolean| The visitor is a returning visitor.| Set `Returning visitor` to `true` when new visit `Lifetime visit count` is greater than `1`. |
|Total direct visits| 15 | Number | The total number of direct visits.| Increment number `Total direct visits` by `1` when new visit if `Referring URL` is empty or `Referring URL` equals `Current URL`. |
|Total referred visits |16 | Number | The total number of referred visits.| Increment number `Total referred visits` by `1` when new visit if `Referring URL` is not empty and `Referring URL` does not equal `Current URL`.|
|Total time spent on site in minutes| 25|  Number | The sum of the duration of all user visits.| Increment number `Total time spent on site in minutes` by `Visit duration ` when visit ended. |
|Unbadged|  32|  Badge| The visitor has not been assigned any badges. | Assign `Unbadged` badge to visitor when new visitor. |
|Weeks since first visit| 28|  Number| The number of weeks elapsed since first visit.| Set ratio `Average visits per week` to `Lifetime visit count` divided by `Weeks since first visit` when new visit if `Weeks since first visit` is greater than or equal to `1`. |

## Visit attributes

| Visit attributes |  ID |  Type |  Description| Enrichments|
|-----|-----|-----|-----|-----|
|Active browser type |44 | String|  The browser actively being used by the visitor.| &lt;ul&gt;&lt;li&gt;Set string `Active browser version` to `Active browser type` when any event if `User Agent` does not contain `Firefox` and `User Agent` does not contain `Safari` and `User Agent` does not contain `MSIE` and `User Agent` does not contain `Edg` and `User Agent` does not contain Opera.&lt;/li&gt;&lt;li&gt;Set string `Active browser version` to `Active browser type` when any event `User Agent` is `Chrome`.&lt;/li&gt;&lt;li&gt;Set string `Active browser version` to `Active browser type` when any event `User Agent` is `Firefox`.&lt;/li&gt;&lt;li&gt;Set string `Active browser version` to `Active browser type` when any event `User Agent` is `Opera`.&lt;/li&gt;&lt;li&gt;For `Set of Strings` Active browser types add `Active browser type` when any event.&lt;/li&gt;&lt;/ul&gt; |
|Active browser types  |49  |Set of strings|  A deduplicated list of browser types used this visit.| For tally `Lifetime browser types used` increment all values by `1` if found in `Active browser types when visit ended.` |
|Active browser version| 48|  String|  The browser version actively being used by the visitor.| For set of strings `Active browser versions` add `Active browser version` when any event. |
|Active browser versions| 53|  Set of strings|  A deduplicated list of browser versions this visit.| For tally `Lifetime browser versions used` increment all values by `1` if found in `Active browser versions` when visit ended. |
|Active device| 46|  String|  The device actively being used by the visitor.| For set of strings `Active devices` add `Active device` when any visit. |
|Active devices|  51|  Set of strings|  A deduplicated list of devices this visit.| For tally `Lifetime devices used` increment all values by `1` if found in `Active devices` when visit ended. |
|Active operating system| 45|  String|  The operating system actively being used by the visitor.| For set of strings `Active operating systems` add `Active operating system` when any event. |
|Active operating systems|  50|  Set of strings|  A deduplicated list of operating systems.|  For tally `Lifetime operating systems used` increment all values by `1`  if found in `Active operating systems` when visit ended. |
|Active platform| 47|  String|  The platform actively being used by the visitor.| For set of strings `Active platforms` add `Active platform` when any event. |
|Active platforms|  52|  Set of strings|  A deduplicated list of active platforms.| For tally `Lifetime platforms used` increment all values by `1` if found in `Active platforms` when visit ended. |
|Direct visit|  14|  Boolean| The user navigated directly to the site.| Set boolean `Direct visit` to `true` when new visit if `Referring URL` is empty or `Referring URL` equals `Current URL`. |
|Entry URL| 5| String|  The URL of the first page visited.| Set string `Entry URL` to `Current URL` when new visit. |
|Event count| 7| Number| The total number of events in this visit.| Increment Number `Event count` by `1` when any event. |
|Exit URL|  6| String|  The URL of the last page visited.| Set string `Exit URL` to `Current URL` when visit ended. |
|Referred visit|  13 | Boolean| The user was referred from another site.| Set boolean `Referred visit` to `true` when new visit if `Referring URL` is not empty and `Referring URL` does not equal `Current URL`. |
|Visit duration|  12|  Number|  The duration of this visit.| Increment number `Total time spent on site in minutes` by `Visit duration` when visit ended. |
|Visit end| 11|  Date|  The end date of this visit.| Set number `Visit duration` to be the difference between `Visit end` and `Visit start` in minutes when any event.|
|Visit start| 10|  Date|  The start date of this visit.| Set number `Visit duration` to be the difference between `Visit end` and `Visit start` in minutes when any event. |

## Event attributes

| Event attributes |  ID |  Type |  Description|  Enrichments|
|-----|-----|-----|-----|-----|
|Client IP|74|String|The IPv4 address of the visitor.| |
|Client IPv6|83|String|The IPv6 address of the visitor. The visitor must have an IPv6 address and their network infrastructure must be able to transmit the address. For more information, see [Support for IPv6](#support-for-ipv6).| |
|Current URL|4|String|The URL of the current page. | &lt;ul&gt;&lt;li&gt;Set string `Entry URL` to `Current URL` when new visit.&lt;/li&gt;&lt;li&gt;Set string `Exit URL` to `Current URL` when visit ended.&lt;/li&gt;&lt;li&gt;Set string `Last event URL` to `Current URL` when any event.&lt;/li&gt;&lt;/ul&gt; |
|Domain|35|String|The domain of the current page.| |
|event_name|64|String|This attribute is deprecated; use `tealium_event` instead.|
|Last event timestamp|8|String|The timestamp of the last event.| &lt;ul&gt;&lt;li&gt;Set date `Visit start` to `Last event timestamp` when new visit.&lt;/li&gt;&lt;li&gt;Set date `Visit end` to `Last event timestamp` when any event.&lt;/li&gt;&lt;li&gt;Set date `First visit` to `Last event timestamp` when new visitor.&lt;/li&gt;&lt;li&gt;Set date `Last visit` to `Last event timestamp` when visit ended.&lt;/li&gt;&lt;/ul&gt;|
|Page Title|38|String|The title of the current page.| |
|Pathname|36|String|The pathname of the current page.| |
|platform|40|String|The platform of the client.| |
|Query String|37|String|The query string of the current page.| |
|Referring URL|3|String|The URL of the previous page.| |
|tealium_account|66|String|The account name.| |
|tealium_datasource|70|String|The Data Source Key.| |
|tealium_environment|67|String|The publishing environment.| |
|tealium_event|75|String|The Tealium event name (either `view` or `link`).| |
|tealium_event_type|78|String| The type of Tealium event being dispatched (either `view` or `event`).| |
|tealium_firstparty_visitor_id|76|String| The visitor ID provided by the first-party cookie.| |
|tealium_library_name|68|String|The library name.| |
|tealium_library_version|69|String|The version of the library.| |
|tealium_profile|79|String|The account profile.| |
|tealium_random|65|Number|This value is a random number that the platform generated for each event. The expected value is 16 numeric digits. This value is prepended with zeroes if it is less than 16 digits.| |
|tealium_session_id|71|Number|This value is the epoch timestamp of when the first page view, event, or library finished starting up (in milliseconds). This value resets if there is no activity for 30 minutes on the web. | |
|tealium_thirdparty_visitor_id|77|String|The visitor ID provided by the third-party cookie.| |
|tealium_timestamp_epoch|73|Number|This value is when the event occurred, in seconds. If event was queued, this value is the time that the event originally occurred.| |
|tealium_visitor_id|72|String|This value is the generated UUID, which is case sensitive on AudienceStream. This value was formerly `tealium_vid` in `vdata` calls.| |
|User Agent|2|String|The user agent string.| |

### Support for IPv6

This section shows which components support IPv6 and how to set a fallback when the IPv6 address is not available.

**Tag hostnames**

| Hostname | IPv4 Support | IPv6 Support |
|----------|--------------|--------------|
| `tags.tiqcdn.com` | ✓ | ✓ |
| `tags.tiqcdn.cn` | ✓ | ✓ |
| `tags-eu.tiqcdn.com` | ✓ | ✗ |

**First-party domains**

IPv6 support for first-party domains depends on when the configuration was created:  

* Configurations created before the release of the first-party domain feature support IPv6.  
* Configurations created through the product UI after the feature was released do not support IPv6 by default. To enable IPv6, add an AAAA DNS record that points to the same distribution as the domain&#39;s A record.

**Other components**

The following components do not support IPv6:  

* Tealium Collect tag and Collect HTTP API (`collect.tealiumiq.com` and `collect-&lt;region&gt;.tealiumiq.com`)  
* First-party Collect domains  
* Tealium v1, v2, and v3 APIs (`platform.tealiumapis.com`)  
* Connectors and external file imports  

To create an attribute that uses the IPv4 address as a fallback when the IPv6 address is not available, see the [Setting Fallbacks When Using IPv6](https://support.tealiumiq.com/en/support/solutions/articles/36000521207) knowledge base article.

## Examples

The following examples demonstrate how you can use preloaded attributes:

* Use the **Frequent visitor** badge to create an audience, and then action that audience with a connector to send email to those visitors that says &#34;Thank you for being a regular visitor.&#34;
* Use the **Lifetime operating systems used (favorite)** attribute to change the placement of specific downloads on a page, making more relevant apps appear first.
* Use **Total Direct Visits** and **Total Referred Visits** to calculate the ratio of  direct to referred visits for a visitor to understand each visitor or visit.
