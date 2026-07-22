---
title: Moments iQ Expertise with AudienceStream example
description: This article provides an example of a Moments iQ experience leading a visitor through expertise assessment and enriching a visitor profile with this information.
url: https://docs.tealium.com/iq-tag-management/moments-iq/audiencestream-example/
---
In the following example, we embed an experience on an electronics site to ask the visitor about their level of expertise. The visitor's response is then enriched in their visitor profile. This helps determine their familiarity with the product line, which can be used to personalize recommendations for additional services and products, such as home installation services, speaker cables, or extended warranties.

## Requirements

This example requires the following:

* Moments iQ.
* Tealium AudienceStream.
* The most recent version of the [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/).

## Step 1: Create tag

The following experience appears on the home page.

[Create a Moments iQ experience](https://docs.tealium.com/manage-moments-iq/#create-a-moments-iq-tag) for the first engagement with the visitor by adding a Tealium Moments iQ tag with the following properties:

* **Title**: `Visitor expertise`
* **Experience Placement**: `Center`
* **Experience Type**: `Embedded`
* **Experience Position**: `After Begin`
* **Redirect Opens Tab**: `False`
* **Header Text**: `Expertise`
* **Main Text**: `Help us to get to know you`
* **Question Text**: `What is your experience level with home theater equipment?`
* **Answer Type**: `Radio button`
* **Answers**: `Professional|Advanced|Basic|None`

Under **Placement Selector**, enter the CSS property where you want the experience to load (for example, `div.col-main`).

### Create load rule

To load the experience only on the home page, create the following rule:


[
  [
    {
      "input": "js.page_type",
      "operator": "equals (ignore case)",
      "filter": "home"
    }
  ] 
]



## Step 2: Create AudienceStream attributes

To configure AudienceStream to enrich attributes with the values from the experiences, use the following steps:

1. If they do not exist already, create the following attributes:
    * **Customer_Expertise** as a string visit attribute that has a rule that stores the value of `momentsiq_answer1`.
1. If they do not exist already, create the following badges:
    * **Beginner** which checks if the value of the **Customer_Expertise** visit attribute is `None`.
    * **Basic** which checks if the value of the **Customer_Expertise** visit attribute is `Basic`.
    * **Advanced** which checks if the value of the **Customer_Expertise** visit attribute is `Advanced`.
    * **Professional** which checks if the value of the **Customer_Expertise** visit attribute is `Professional`.

Since multiple Moments iQ experiences may be created over time, you must ensure that `tealium_event` values from different experiences enrich only the intended attributes.

Update the rule for the `Customer_Expertise` visit attribute to check if `momentsiq_id` matches the UID of the specific experience created in this example. This ensures that only the correct experience updates the `Customer_Expertise` attribute.

In this example, the tag UID is `123`:

![](https://docs.tealium.com/images/early-access/moments-iq/moments-iq-expertise-conditions.png)

## Results

When the visitor loads the home page, the experience is embedded at the beginning of the `div.col-main` element.

![](https://docs.tealium.com/images/moments-iq/momentsiq-example-home-theater.png)

When the customer answers the question, their answer is stored in their visitor profile and they are assigned a badge based on their expertise level.