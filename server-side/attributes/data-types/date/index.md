---
title: Date Attribute
description: The date attribute stores the timestamp of an event.
url: https://docs.tealium.com/server-side/attributes/data-types/date/
---
## How it works

Use the date attribute to store important timestamps such as `First Purchase Date`, `Last Checkout Date`, or `Last Visit Date`.

The date attribute is available for the event, visit, and visitor scopes.

![](/images/server-side/attribute-scopes-table-all.png)

## Date formatter

To convert a string attribute to a date, use the date formatter. Select the timestamp components from the date format panel that match the string values. For example, a string value such as `01/31/2020` can be converted to a date using a format of `MM/dd/yyyy`.

Date and time string patterns:

| Symbol | Description                       | Example Values         |
|--------|-----------------------------------|------------------------|
| G      | Era designator                    | BC, AD                 |
| y      | Year (2 or 4 digits)              | 12, 2012 (use `yy` or `yyyy`) |
| M      | Month in year (length depends on M&#39;s count) | MM, MMM, MMMMM      |
| d      | Day in month (length depends on d&#39;s count)  | d, dd    |
| h      | Hour of day, 1-12 (AM/PM)              | hh        |
| H      | Hour of day, 0-23                      | HH        |
| m      | Minute in hour, 0-59                   | mm        |
| s      | Second in minute, 0-59                 | ss        |
| S      | Millisecond in second, 0-999           | SSS       |
| a      | AM/PM marker                           | AM, PM    |
| z      | Time Zone                              | PST, EST  |
| Z      | RFC 822 Time Zone                      | -0800, &#43;0530   |
| &#39;      | Escape for text delimiter    |         |
| &#39;      | Single quote                 |         |

For more information, see [Oracle: SimpleDateFormat Java Class](https://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html).

 If the string includes a `T`, include single quotes before and after the `T` in the expression. For example, a `2024-08-22T10:24:58.905` string uses the expression `yyyy-MM-dd&#39;T&#39;HH:mm:ss.SSS`. Omitting the quotes, such as using `yyyy-MM-ddTHH:mm:ss.SSS`, results in a parsing error. 

### Collect date values as string attributes

It is a best practice to collect date values as string event attributes and then use an enrichment to convert them to a date visitor attribute. This approach minimizes the risk of errors caused by incorrect formats, which could disrupt data collection and processing in downstream database systems. Importing as a string ensures greater flexibility and data integrity, especially when handling diverse date formats.  

#### Example

To capture a signup date as a string and enrich a date attribute, use the following steps:

1. Create the `Signup Date` event attribute as a string, such as `&#34;2023-10-15&#34;`.
1. Create the `Signup Date` visitor attribute as a date.  
1. Use the [Set Date enrichment](#set-date) on the visitor attribute to convert the string into a date attribute using the format `yyyy-MM-dd`.  

### Size Limits

The size of a each date attribute is limited to the following range:

* Minimum: `-292275055-05-16T16:47:04.192Z`
* Maximum: `&#43;292278994-08-17T07:12:55.807Z`

These attributes are also limited by the maximum size of the profile after encryption and compression (400 KB).

## Enrichments

### Capture date

The **Capture Date** enrichment sets the attribute to the current timestamp at the time of an event condition. This enrichment is available for event, visit, and visitor attributes.

For example, to capture the Last Purchase Date, use this enrichment with a rule that identifies a purchase event.

**Attribute Name:** Last Purchase Date

* **Starting Value**: `&#34;&#34;`
* **Enriched With**:
* **Resulting Value**: `1491233145706`

### Set date

The **Set date** enrichment sets the attribute to the value of another attribute. If the other attribute is a string, use the [Date Formatter](#date-formatter) to convert it to a date. This enrichment is available for event, visit, and visitor attributes.

**Attribute Name**: Last Purchase Date

* **Starting Value**: `&#34;&#34;`
* **Enriched with String**: `01/04/2019`
* **Using Format**: `dd/MM/yyyy` (This format specifies the day, month, and year order for parsing the string.)

When you use the **Set date** enrichment to set an EventStream date from another date attribute (EventStream or AudienceStream), you can use a placeholder for the format string. For example, in the **Set Date** enrichment, set the following:
* **Set date to**: The date attribute you want to set the value to. In this example,`date_of_birth`.
* **with date format**: Enter any placeholder, for example, `x`.

![](/images/server-side/attributes/set_date_enrichment_example.png)

### Remove date

The **Remove date** enrichment erases the value of a date attribute. This enrichment is available for event, visit, and visitor attributes.

**Attribute Name**: Last Visit Date

* **Starting Value**: `1491233145706`
* **Resulting Value**: (Removed)

### Convert from date format

The **Convert from date format** enrichment sets the value based on an expected date format of incoming values. This enrichment is used to convert string values sent from the Collect tag or HTTP API. Use the [Date Formatter](#date-formatter) to convert the string value to a date. This enrichment is available for event attributes.
