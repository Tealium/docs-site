---
title: Event Specifications: Data Quality
description: After you define event specifications, Live Events displays the quality of your incoming data.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/data-quality/
---
The color-coded bars in the chart are segmented according to the validation of the event specifications against your data.

![](https://docs.tealium.com/images/server-side/getting-started-eventstream-live-events-all-filters.png)

Live Events with event spec validation:

* **Valid (Green)**  
Valid events satisfy the requirements of an event specification. The event has a known value for the `tealium_event` attribute and contains all the required attributes.

* **Invalid (Red)**  
Invalid events match an event specification, but do not contain the required attributes. The event has a known value for the `tealium_event` attribute, but the required attributes are either missing or contain unexpected values.

* **No Spec (Blue)**  
Events marked as **No Spec** do not have a matching event specification. The event does not have the `tealium_event` attribute or the value does not have a corresponding event specification.

Click any of the filters to toggle those values on or off and adjust the display of the chart.

This concludes the basics of getting installed and set up with a data layer. The next tutorial demonstrates how to create actionable event feeds.
