---
title: Timeline Attribute
description: This article describes the timeline attribute and how to use it.
url: https://docs.tealium.com/server-side/attributes/data-types/timeline/
---
## How it works

The timeline attribute records a list of events over a specified time period. A captured event generates an entry in the timeline that contains captured attribute values and a timestamp. The timestamp can be the time of the event or a date/time provided by another attribute. Timestamps are recorded in Unix/Epoch format.

The timeline attribute is available in the visit and visitor scopes.

![](https://docs.tealium.com/images/server-side/screenshot-2019-11-11-at-1.26.28-pm.png)

### Size limits

Timeline attributes are limited to a maximum of 100 entries. If a timeline reaches this limit, the earliest entries are discarded (First-In, First-Out). For example, if a timeline contains 100 entries, and a new entry is added, the first entry is deleted.

The maximum time period of a timeline is 365 days.

Timeline attributes are also limited by the maximum size of the profile after encryption and compression (400 KB).

## Capture attribute data

In addition to the timestamp of the event, you can also capture the value of one or more attributes when the event occurs. Captured attribute values provide more information about the event when it occurred. Numbers and tallies are the only useful attribute types to capture because only those attribute types can be aggregated using enrichments.

For example, to track the order total for each purchase, capture the attribute `order_total` in a purchase timeline.


<blockquote>
Verify timelines by viewing the latest visitor profile in [Trace](https://docs.tealium.com/about-trace/).
</blockquote>


## Expiration of entries

Entries in a timeline can be set to expire after a set number of days. This expiration only applies to entries within the timeline and not the timeline attribute itself. The expiration period is evaluated at the start of each visit. If an entry is older than the expiration time, it is removed from the timeline.

Timelines work well with numbers because numeric entries are easily used to create a rolling sum or a rolling average value based on the timeline entries.

## Best practices

Timelines are limited to 100 entries. Like any attributes, they contribute to the maximum visitor profile size of [400KB compressed](https://docs.tealium.com/about-attributes/#storage-capacity-limits).

To use timeline attributes efficiently, we recommend the following:

* Do not store information in the timeline longer than required. Set an expiration date for timeline entries.
* Do not store other attributes in a timeline unless you have a specialized use case, such as sending the timeline entries to AudienceStore or another connector. You can store most attribute types in a timeline, but only numbers and tallies can be enriched onto other AudienceStream attributes from a timeline. For example, you can get the sum of a number from entries in the timeline, or aggregate a tally from entries in a timeline. Although you can store other attribute types, there are no enrichments to aggregate the values you store. 
<blockquote>
Storing other attributes in a timeline entry increases the visitor profile size.
</blockquote>

* You can minimize the number of entries in a timeline, and the number of timelines in total, by using them strategically.
  * To efficiently count events using a timeline attribute, increment visit numbers when the target event occurs and store the visit number in the timeline at the end of the visit.
  * To get an overall count at the beginning of the visit, use a sum enrichment to add the visits in the timeline attribute and store them in a number attribute. You can then increment this number during the visit to keep it completely up to date. 
  * If you store several numbers over the same time period, store them all in a single timeline.

## Enrichments

### Update timeline

Use this enrichment to record an entry in a timeline. To add this enrichment, click **Create an Entry** and select **Update Timeline**.

Choose one of the following options for recording the timestamp of the entry:

* **Time of event received (default)**  
The timestamp of the entry is set automatically when the event occurs.
* **Based on date**  
The timestamp of the entry is set to the value of another attribute. If you choose a string attribute, you must also use the [date formatter](https://docs.tealium.com/date-attribute/) to create a date/time pattern that matches the expected value.

To capture attribute values in the entry, select an attribute from the drop-down list and click **Add Attribute**. The added attribute is displayed as a captured attribute. Repeat this step for each attribute to capture in the entry.

#### Example

**Attribute Name**: Orders Last 60 days  
**Captured Attributes:** `order_subtotal` and `order_total`  

**Example JSON Data**:

```json
"Orders Last 60 Days" : [
  {
    "timestamp" : 1576862494000,
    "snapshot" : {
      "order_total" : 44.00,
      "order_subtotal" : 38.00
    }
  },
  {
    "timestamp" : 1577640094000,
    "snapshot" : {
      "order_total" : 100.00,
      "order_subtotal" : 95.00
    }
  },
  {
    "timestamp" : 1578849694000,
    "snapshot": {
      "order_total" : 60.00,
      "order_subtotal" : 59.00
    }
  }
]
```

### Set expiration for timeline events

Use this enrichment to determine when an entry should be removed from the timeline based on the number of days since it was recorded. Each entry that is older than the expiration setting is removed from the timeline automatically. The expiration of timeline entries is evaluated at the beginning of a visit.


<blockquote>
The expiration does not apply to the timeline itself, only to the entries within it.
</blockquote>

