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
    "purchases": [
        {
            "item": "Golden gadget",
            "price": 25.50,
            "transaction_id": "f029342"
        },
        {
            "item": "Different gadget",
            "price": 17.75,
            "transaction_id": "f029342"
        }
    ],
    "transactions": [
        {
            "id": "f029342",
            "items": 2,
            "total": 43.25
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

Select "Body" option and provide a template reference.

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


<blockquote>
Variables are internally translated to JSON and made available to all templates.
</blockquote>


#### Resulting JSON structure:

```json
{
  "purchases": [
    {
      "price": "17.75",
      "item": "Different gadget"
    },
    {
      "price": "25.50",
      "item": "Golden gadget"
    }
  ],
  "apiVersion": "3.0",
  "transactionId": "f029342",
  "transactionItemCount": "2",
  "transactionTotalPrice": "43.25",
  "projectId": "98765"
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
    "purchases": [
        {{#purchases}}
        {
            "item": "{{item}}",
            "price": {{price}},
            "transaction_id": "{{transactionId}}"
        }{{#iter.hasNext}}, {{/iter.hasNext}}
        {{/purchases}}
    ],
    "transactions": [
        {
            "id": "{{transactionId}}",
            "items": {{transactionItemCount}},
            "total": {{transactionTotalPrice}}
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
    "purchases": [
        {
            "item": "Different gadget",
            "price": 17.75,
            "transaction_id": "f029342"
        },
        {
            "item": "Golden gadget",
            "price": 25.50,
            "transaction_id": "f029342"
        }
    ],
    "transactions": [
        {
            "id": "f029342",
            "items": 2,
            "total": 43.25
        }
    ]
}
```


## Action configuration screenshot

![](https://docs.tealium.com/images/server-side/example)
