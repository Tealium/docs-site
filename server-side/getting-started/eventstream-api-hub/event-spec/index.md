---
title: Event specifications
description: Event specifications represent your data layer in EventStream and provide a way to organize and validate the quality of incoming data.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/event-spec/
---
As mentioned in earlier tutorials, events are identified by the `tealium_event` attribute. The value of this attribute represents the name of the event and its associated specification. The specification also indicates which event attributes are required in the event.

## How it works

Event specifications define and standardize the events you want to collect in your EventStream implementation.

Here&#39;s how it works:

* **Event name and attributes**  
An event specification has a name and a list of required/optional attributes. The name is the value set in the `tealium_event` attribute. For example, an event that tracks when a user performs a search would be represented by `tealium_event=&#34;search&#34;` and would have required attributes `search_term` and `search_results` containing the searched term and the number of results returned respectively.
* **Data sources**  
After you add specifications, they can be associated to data sources. Specs are platform neutral, so a standard event such as `search` should be implemented the same in each platform. However, not all specifications apply to every type of data source. On the **Data Sources** screen, you associate specifications to the data sources that implement them.
* **Get code and installation guide**  
When specifications are associated to a data source, the installation guide automatically includes code samples for each one.
* **Data validation**  
The **Live Events** screen now reflects the quality of your data based on the events that match specifications and if they contain the required attributes.

## Example event specification

![](/images/server-side/eventstream-getting-started-spec.png)

```json
{
    &#34;tealium_event&#34;   : &#34;search&#34;,
    &#34;search_keyword&#34;  : &#34;STRING&#34;,  // the searched term
    &#34;search_results&#34;  : NUMBER,    // number of results
    &#34;product_on_page&#34; : [&#34;STRING&#34;] // array of product strings
}
```

The next tutorial explains how to add an event specification.