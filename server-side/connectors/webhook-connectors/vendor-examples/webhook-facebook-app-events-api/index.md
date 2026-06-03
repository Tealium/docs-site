---
title: Webhook Facebook App Events API
description: How to configure the Facebook App Events API using the Webhook - Send Custom Request action with Templates and Template Variables.
url: https://docs.tealium.com/server-side/connectors/webhook-connectors/vendor-examples/webhook-facebook-app-events-api/
---
## Overview

Submit an HTTP request to Facebook to track one or more in-app conversions. Event data is expressed as a JSON encoded string. See the [Facebook App Events API](https://developers.facebook.com/docs/marketing-api/app-event-api/) for more details.

### API call example:

```bash
curl \
  -F &#34;event=CUSTOM_APP_EVENTS&#34; \
  -F &#34;advertiser_id=1111-1111-1111-1111&#34; \
  -F &#34;advertiser_tracking_enabled=1&#34; \
  -F &#34;application_tracking_enabled=1&#34; \
  -F &#34;custom_events=[{\&#34;_eventName\&#34;:\&#34;fb_mobile_purchase\&#34;,
                      \&#34;_valueToSum\&#34;:55.22,
                      \&#34;_logTime\&#34;:1367017882,
                      \&#34;fb_currency\&#34;:\&#34;GBP\&#34;,
                    }]&#34; \
  &#34;https://graph.facebook.com/API_VERSION/APP_ID/activities&#34;
```

The provided curl example (with the `-F` option) implies the request uses a POST method and its body is &#34;multipart/form-data&#34; content type. Let&#39;s break down the whole request into separate components that can be configured in the Webhook.

#### 1. API endpoint/URL

```
https://graph.facebook.com/API_VERSION/APP_ID/activities
```

In the example the URL has placeholder values for the API version and the `APP_ID`. These could probably be hard-coded into the URL, but for demonstration purposes we&#39;ll use a URL Template to create this component using dynamic values.

#### 2. Simple form field values

```
  event = CUSTOM_APP_EVENTS
  advertiser_id = 1111-1111-1111-1111
  advertiser_tracking_enabled = 1
  application_tracking_enabled = 1
```

These key-value pairs are simple form fields that can be mapped using Custom Values in the Body Data section.

#### 3. JSON value

```json
custom_events = [{ &#34;_eventName&#34;  : &#34;fb_mobile_purchase&#34;,
                   &#34;_valueToSum&#34; : 55.22,
                   &#34;_logTime&#34;    : 1367017882,
                   &#34;fb_currency&#34; : &#34;GBP&#34;,
                }]
```

This particular field named `custom_events` has a more complicated value, a JSON string. To recreate this value in the Webhook we&#39;ll use Template Variables and a Template.

## Webhook settings

### Method field

Set to &#34;POST&#34;.

### URL field

Set to `{{url_template}}`.

URL can either be hard coded (with embedded API version and app ID) or template based. The latter approach is taken to allow greater flexibility with data layer attributes. See templates section below.

### Body content type

Select option `multipart/form-data`.

### Body data

Set name/value pairs for each field from the example request. Notice that the value for `custom_events` is the name of the Template we create, `events_template`.

|Facebook Field Names| Custom Value| Comment|
|---| ---| ---|
|`event`| `CUSTOM_APP_EVENTS`|
|`advertiser_id`| `1111-1111-1111-1111`|
|`advertiser_tracking_enabled`|  `1`|
|`application_tracking_enabled`|  `1`|
|`custom_events`| `{{events_template}}`| References the template created below|

Parameter values are custom/static values in this example, but can easily be provided as dynamic Data Layer Attributes.

### Template variables

Set name/value pairs to be referenced and replaced in the Templates.

|Template Variable Name| Type| Value|  Note |
|---| ---| ---| ---|
| `name` |  Custom Value |  `fb_mobile_purchase` |
| `currency` |  Custom Value |  `USD` |
| `logTime` |  [Data Attribute]() |  Current Time |  `1468358987` |
| `eventSums.value` |  [Set of Strings Attribute]() |  FB Event Sums |  The dot-naming convention creates a matching section in the Template. Array value: [0.99, 4.99] |
| `apiVersion` |  Custom Value |  `v2.6 | For use in the URL Template|
| `appId` |  Custom Value |  `123456` | For use in the URL Template|

### Templates

You will create two templates, one for the URL and one for the JSON value to be assigned to the `custom_events` parameter. Notice that the Templates make use of the Template Variables using the curly brackets syntax.

It&#39;s important to understand that this template is based on the &#34;eventSums.value&#34; variable which is populated by a Set of String Attribute. This is an array Attribute so the template will create a section for the prefix of the template variable name we used (in this case &#34;eventSums&#34;).

**url_template**:

```
https://graph.facebook.com/{{apiVersion}}/{{appId}}/activities
```

**events_template**:

```
 [ 
 {{#eventSums}} 
 {     
  &#34;_eventName&#34;  : &#34;{{name}}&#34;,     
  &#34;_valueToSum&#34; : {{value}},     
  &#34;_logTime&#34;    : {{logTime.toTimestamp}},     
  &#34;fb_currency&#34; : &#34;{{currency}}&#34;
}{{#iter.hasNext}}, {{/iter.hasNext}}
 {{/eventSums}} 
 ] 
 ```

### Rendered remplates

The Templates get rendered and their content used wherever they are referenced in the Webhook settings (in this example, the URL and the `custom_events` field in the Body Data).

Notice that the `_valueToSum` parameter receives the values from the Set of Strings attribute.


**url_template**:

```
https://graph.facebook.com/v2.6/12345/activities
```

**events_template**:  

```json
[     
 {         
  &#34;_eventName&#34;  : &#34;fb_mobile_purchase&#34;,         
  &#34;_valueToSum&#34; : 0.99,         
  &#34;_logTime&#34;    : 1468358987,         
  &#34;fb_currency&#34; : &#34;USD&#34;     
  },     
  {         
    &#34;_eventName&#34;  : &#34;fb_mobile_purchase&#34;,         
    &#34;_valueToSum&#34; : 4.99,         
    &#34;_logTime&#34;    : 1468358987,         
    &#34;fb_currency&#34; : &#34;USD&#34;     
  } 
] 
```

