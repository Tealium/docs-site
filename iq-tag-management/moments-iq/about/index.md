---
title: About Moments iQ
description: This document explains Moments iQ on the Tealium platform.
url: https://docs.tealium.com/iq-tag-management/moments-iq/about/
---
## Requirements

Moments iQ requires the following product:

* Tealium iQ Tag Management

To integrate Moments iQ with server-side products, you need the following:

* Tealium AudienceStream or Tealium EventStream
* The most recent version of the [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/)

To use AudienceStream variables in Moments iQ rules and dynamic text in Moments iQ experiences, you need one of the following:

* [Data Layer Enrichment](https://docs.tealium.com/data-layer-enrichment/) enabled
* Moments API

## About Moments iQ

Moments iQ lets you create an embedded or modal experience on your website that collects preferences (zero-party data) in real time directly from your visitors. Zero-party data is information that you collect directly from a customer, while first-party data is inferred from visitor activity, such as their browsing activity on your site and their purchases. With this data, you can better understand what your visitors want, their current intentions, and how they want to be seen by your brand, without the need for additional tools. If you enrich visitor profiles with this data, you can create more robust and accurate audiences that let you engage with your customers in a more meaningful way that fosters an open and trusted relationship with your brand.

The following example collects information about a visitor's job function:

![](https://docs.tealium.com/images/moments-iq/moments-iq-example.png)

## Features

Moments iQ provides the following features: 

* **Easy installation**  
Add the Moments iQ Experiences tag from the tag marketplace and configure the questions, answers, and styles. Moments iQ configuration is bundled with your existing installation of our JavaScript library (`utag.js`). No additional code on your site is necessary.
* **Real-time data collection**  
With built-in tracking, user responses are instantly available in the data layer. This data can be used to personalize the user experience, enrich visitor profiles, and be sent to any vendor system.
* **Precision targeting**  
Determine when, where, and to whom an experience is displayed by leveraging load rules, visitor data and event listeners.
* **Custom style and appearance**  
Use simple configurations or CSS to match the look and feel of your site to provide your visitors with a seamless modal or embedded experience. You can also position the experience anywhere on a page or you can pop up the experience in a styled modal window.
* **Multiple question formats**  
Supports radio buttons, checkboxes, and text box answers.
* **Privacy by design**  
Data is collected, transformed, and sent appropriately through built-in tracking calls based on the visitor’s consent preferences.
* **Seamless integration**  
Send the event data to AudienceStream to enhance visitor profiles, assign badges, or update audience membership to trigger connectors.

## Steps

Moments iQ is set up through the following screens in the [Moments iQ tag](https://docs.tealium.com/manage-moments-iq/):

* **Tag configuration**: Configure the experience's position and appearance on the page.
* **Load rules and event listeners**: Set the conditions to determine when, where, and to whom an experience is displayed.
* **Data mapping**: Advanced settings to set and override prompt styling or configuration.

## Events

When the visitor submits or closes the experience, the browser sends a `utag.track` call with the relevant data for your tags and extensions to process.

Moments iQ events use the following variables:

| Variable | Type | Description | Example |
| -------- | ---- | ----------- | ------- |
| `tealium_event` | String | The event will contain one of the following values:<ul><li>`momentsiq_close`: If the visitor closed the window, usually with the close button.</li><li>`momentsiq_submit`: If the visitor clicked the submit button, whether they answered the question or not.</li></ul> | `momentsiq_close` |
| `momentsiq_question1` | String | The question asked in the experience. | `What is your favorite color?` |
| `momentsiq_questions_answered` | String | This variable only appears if the visitor closed the experience without submitting. The value will either be blank or contain any selection or text they entered before closing the experience. This variable lets you filter out incomplete values to avoid contaminating your data. | `"test1"` |
| `momentsiq_question1_type` | String | If the visitor clicked the primary button, the type of question (`checkbox`, `text`, or `radio`) | `radio` |
| `momentsiq_id` |  Number | The tag UID. | `34` | 
| `momentsiq_answer1` | String |  If the visitor clicked the primary button, the answer or answers that the visitor entered or selected. Multiple answers are separated by the pipe (&#124;) character. | `Red` |


### Examples

The following example is the event for a radio button experience with a submitted answer:

```json
{
  "tealium_event": "momentsiq_submit",
  "momentsiq_id": "54",
  "momentsiq_question1_type": "radio",
  "momentsiq_question1": "What is your favorite color?",
  "momentsiq_answer1": "Blue"
}
```

The following example is the event for a checkbox experience with multiple answers submitted:

```json
{
  "tealium_event": "momentsiq_submit",
  "momentsiq_id": "55",
  "momentsiq_question1_type": "checkbox",
  "momentsiq_question1": "What is your favorite color?",
  "momentsiq_answer1": "Blue|Purple"
}
```

The following example is the event for an experience that the visitor closed before answering or submitting:

```json
{
  "tealium_event" : "momentsiq_close",
  "momentsiq_questions_answered": "",
  "momentsiq_id"  : "56"
}
```

The following example is the event for an experience that loaded and the value of the **Track On Load** setting is `True`:

```json
{
  "tealium_event" : "momentsiq_view",
  "momentsiq_id"  : "56"
}
```

For a basic example of a Moments iQ experience, see [Moments iQ example](https://docs.tealium.com/moments-iq-expertise-example/).