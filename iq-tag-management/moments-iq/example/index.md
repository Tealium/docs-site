---
title: Moments iQ Expertise example
description: This article provides an example of Moments iQ experience leading a visitor through expertise assessment.
url: https://docs.tealium.com/iq-tag-management/moments-iq/example/
---
In the following example, we embed an experience on an electronics site to ask the visitor what their level of expertise is. This helps you determine the level of comfort the visitor has with the product line, which you might use for suggesting additional services and products such as home installation services or additional accessories like speaker cable or extended warranties.

## Requirements

This example requires the following:

* Moments iQ.

## Step 1 Create tag

The following experience appears on the home page.

[Create a Moments iQ experience]() for the first engagement with the visitor by adding a Tealium Moments iQ tag with the following properties:

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
      &#34;input&#34;: &#34;js.page_type&#34;,
      &#34;operator&#34;: &#34;equals (ignore case)&#34;,
      &#34;filter&#34;: &#34;home&#34;
    }
  ] 
]


For the purposes of this example, assume that the tag UID is `123`.

## Step 2: Store the answer

To personalize the visitor experience using the visitor responses to Moments iQ experiences, you need to store the visitor&#39;s responses. Because this example uses only client-side functionality and the visitor&#39;s web browser, use a Persist data values extension to store the values in a cookie.

In the following example, we are storing the value in the cookie `MomentsiQExp123` for as long as the visitor&#39;s browser is set to store cookies:

![](/images/early-access/moments-iq/manage-moments-persist-data-value.png)

Be sure to add a condition to the extension so that it runs only when the `momentsiq_submit` event occurs. In this case, we check for `momentsiq_id` to equal `123`.

You can access the data from the cookie through a JavaScript extension as `b[&#34;MomentsiQExp123&#34;,&#34;momentsiq_answer1&#34;]` or through the `MomentsiQExp123` cookie variable.

For more information, see [Persist data value extension]().

## Results

When the visitor loads the home page, the home page embeds the experience after the beginning of the `div.col-main` element.

![](/images/moments-iq/momentsiq-example-home-theater.png)