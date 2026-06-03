---
title: Webhook - Keen.io API
description: How to configure an advanced Webhook - Send Custom Request action using Template Variables for Keen.io API
url: https://docs.tealium.com/server-side/connectors/webhook-connectors/vendor-examples/webhook-keenio-api/
---

## Overview

Submit an http request to Keen.io to record multiple purchase events for a single transaction. Whole request body is a JSON message.

## Vendor requirements

Documentation: [Keen IO Data Collection API](https://keen.io/docs/data-collection/)

Request URL

```
https://api.keen.io/API_VERSION/projects/PROJECT_ID/events

```

### API request body example:

```json
{
    &#34;purchases&#34;: [
        {
            &#34;item&#34;: &#34;Golden gadget&#34;,
            &#34;price&#34;: 25.50,
            &#34;transaction_id&#34;: &#34;f029342&#34;
        },
        {
            &#34;item&#34;: &#34;Different gadget&#34;,
            &#34;price&#34;: 17.75,
            &#34;transaction_id&#34;: &#34;f029342&#34;
        }
    ],
    &#34;transactions&#34;: [
        {
            &#34;id&#34;: &#34;f029342&#34;,
            &#34;items&#34;: 2,
            &#34;total&#34;: 43.25
        }
    ]
}

```

## Action implementation

### Method field

Set to `POST`.

### URL field

Set to `{{url_template}}`.

URL can either be hard coded (with embedded api version and project ID) or template based. The latter approach is taken to allow greater flexibility with data layer attributes. See templates section below.

### Body content type

Select option `application/json`.

### Body data

Select &#34;Body&#34; option and provide a template reference.

|Name| Value|
|---| ---|
|Body| `{{json_template}}`|

### Template variables

Set name and value pairs to be referenced and replaced in templates. Variable values are custom values in this example, but can easily be provided as dynamic data layer attributes.

|Name| Value| Note|
|---| ---| ---|
|`transactionId`| `f029342`|
|`transactionItemCount`| `2`|
|`transactionTotalPrice`| `43.25`|
|`purchases.item`| Keen.io Purchase Items| Set of Strings attribute|
|`purchases.price`| Keen.io Purchase Prices| Set of Strings attribute|
|`apiVersion`| `3.0`|
|`projectId`| `987.65`|

Variables are internally translated to JSON and made available to all templates.

#### Resulting JSON structure:

```json
{
  &#34;purchases&#34;: [
    {
      &#34;price&#34;: &#34;17.75&#34;,
      &#34;item&#34;: &#34;Different gadget&#34;
    },
    {
      &#34;price&#34;: &#34;25.50&#34;,
      &#34;item&#34;: &#34;Golden gadget&#34;
    }
  ],
  &#34;apiVersion&#34;: &#34;3.0&#34;,
  &#34;transactionId&#34;: &#34;f029342&#34;,
  &#34;transactionItemCount&#34;: &#34;2&#34;,
  &#34;transactionTotalPrice&#34;: &#34;43.25&#34;,
  &#34;projectId&#34;: &#34;98765&#34;
}

```

### Templates

`url_template`

```
https://api.keen.io/{{apiVersion}}/projects/{{projectId}}/events
```

`json_template`   

```json
{
    &#34;purchases&#34;: [
        {{#purchases}}
        {
            &#34;item&#34;: &#34;{{item}}&#34;,
            &#34;price&#34;: {{price}},
            &#34;transaction_id&#34;: &#34;{{transactionId}}&#34;
        }{{#iter.hasNext}}, {{/iter.hasNext}}
        {{/purchases}}
    ],
    &#34;transactions&#34;: [
        {
            &#34;id&#34;: &#34;{{transactionId}}&#34;,
            &#34;items&#34;: {{transactionItemCount}},
            &#34;total&#34;: {{transactionTotalPrice}}
        }
    ]
}
 ```


### Templates rendered

Internally templates get rendered (see below) and their content injected where referenced. For example: URL field and Body.

`url_template`

```
https://api.keen.io/3.0/projects/98765/events
```

`json_template`

```json
{
    &#34;purchases&#34;: [
        {
            &#34;item&#34;: &#34;Different gadget&#34;,
            &#34;price&#34;: 17.75,
            &#34;transaction_id&#34;: &#34;f029342&#34;
        },
        {
            &#34;item&#34;: &#34;Golden gadget&#34;,
            &#34;price&#34;: 25.50,
            &#34;transaction_id&#34;: &#34;f029342&#34;
        }
    ],
    &#34;transactions&#34;: [
        {
            &#34;id&#34;: &#34;f029342&#34;,
            &#34;items&#34;: 2,
            &#34;total&#34;: 43.25
        }
    ]
}
```


## Action configuration screenshot

![](/images/server-side/example)
