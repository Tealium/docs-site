---
title: Attributes
description: The first step in using AudienceStream is to create attributes. Attributes allow you to define the important characteristics that represent a visitor's habits, preferences, actions, and engagement with your brand. This section will describe the two types of attributes and the different kinds of data they can store.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/attributes/
---
## Visit Attributes

Visit attributes relate to the current visit (or session) of the user. The data stored in these attributes persists for the length of the visit. Some example visit attributes:

* Visit Duration (Number)
* Current Browser (String)
* Current Device (String)
* Page View Count (Number)

## Visitor Attributes

![](https://docs.tealium.com/images/server-side/audiencestream-profile.png)

Visitor attributes relate to the current user. The data stored in these attributes persist for the lifetime of the user. Some example visitor attributes would be:

* Lifetime Order Value (Number)
* First Name (String)
* Birth Date (Date)
* Purchased Brands (Tally)

## Data Types

Both visit and visitor attributes can store the following data types:

* Number and Array of Numbers
* String and Array of Strings
* Boolean and Array of Booleans
* Tally (a number value associated to a specific set of text values)
* Set of Strings (collection of unique text values)
* Date
* Funnel (a multi-step sequence of events)
* Timeline (all occurrences of an event within a time range)

Click **Next** to learn about enrichments and how attributes get their values.