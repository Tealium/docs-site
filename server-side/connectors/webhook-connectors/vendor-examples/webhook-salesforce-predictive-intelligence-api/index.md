---
title: Webhook Salesforce Predictive Intelligence API
description: How to configure an advanced Webhook - Send Custom Request action using Template Variables for Salesforce Predictive Intelligence API
url: https://docs.tealium.com/server-side/connectors/webhook-connectors/vendor-examples/webhook-salesforce-predictive-intelligence-api/
---

## Overview

Submit an http request to Salesforce Predictive Intelligence (formerly iGoDigital) to record a change to user’s shopping cart. Shopping cart is expressed as JSON URL parameter.

## Vendor requirements

### API request example:

```
https://nova.collect.igodigital.com/c2/6391707/track_conversion?payload={.......}]
```

URL parameter `payload` value is JSON:

```json
{
    "cart": [
        {
            "item": "2890-17738",
            "quantity": "1",
            "price": "94.00",
            "unique_id": "1233388"
        },
        {
            "item": "2890-60773",
            "quantity": "2",
            "price": "133.00",
            "unique_id": "7113048"
        },
        {
            "item": "3414-301727",
            "quantity": "3",
            "price": "1.99",
            "unique_id": "7107457"
        }
    ],
    "order_number": "830100487001",
    "discount": "89.99",
    "shipping": "0.00",
    "user_info": {
        "email": "abc.xxx@tealium.com",
        "details": {}
    }
}

```

## Action implementation

### Method field

Set to "GET".

### URL field

Set to `{{url_template}}`.

URL can either be hard coded (with embedded project ID) or template based. The latter approach is taken to allow greater flexibility with data layer attributes. See templates section below.

### URL parameters

|Name| Value|
|---| ---|
|`payload`| `{{json_template}}`|

### Template Variables

Set name and value pairs to be referenced and replaced in templates. Variable values are custom values in this example, but can easily be provided as dynamic data layer attributes.

|Name| Value| Note|
|---| ---| ---|
|`projectId`| `6391707`|
|`cart.item`| PredictIntel Cart Items| [Set of Strings attribute]()|
|`cart.quantity`| PredictIntel Cart Quantities| Set of Strings attribute|
|`cart.price`| PredictIntel Cart Prices| Set of Strings attribute|
|`cart.id`| PredictIntel Cart IDs| Set of Strings attribute|
|`orderNumber`| `830100487001`|
|`discount`| `89.99`|
|`shipping`| `0.00`|
|`userEmail`| `abc.xxx@tealium.com`|


<blockquote>
Variables are internally translated to JSON and made available to all templates.
</blockquote>


#### Resulting JSON structure:

```json
{

  "shipping": "0.00",
  "orderNumber": "830100487001",
  "userEmail": "abc.xxx@tealium.com",
  "cart": [
    {
      "id": "7113048",
      "price": "1.99",
      "item": "3414-301727",
      "quantity": "3"
    },
    {
      "id": "7107457",
      "price": "133.00",
      "item": "2890-60773",
      "quantity": "2"
    },
    {
      "id": "1233388",
      "price": "94.00",
      "item": "2890-17738",
      "quantity": "1"
    }
  ],
  "projectId": "6391707",
  "discount": "89.99"

}

```

### Templates

`url_template` 

```
https://nova.collect.igodigital.com/c2/{{projectId}}/track_conversion
```

`json_template` 

```json
{
    "cart": [
        {{#cart}}
        {
            "item": "{{item}}",
            "quantity": "{{quantity}}",
            "price": "{{price}}",
            "unique_id": "{{id}}"
        }{{#iter.hasNext}}, {{/iter.hasNext}}
        {{/cart}}
    ],
    "order_number": "{{orderNumber}}",
    "discount": "{{discount}}",
    "shipping": "{{shipping}}",
    "user_info": {
        "email": "{{userEmail}}",
        "details": {}
    }
}
```

### Templates rendered

Internally templates get rendered (see below) and their content injected where referenced. For example: URL field and URL parameter.

`url_template` 

```
https://nova.collect.igodigital.com/c2/6391707/track_conversion
```

`json_template` 

```json
{
    "cart": [
        {
            "item": "3414-301727",
            "quantity": "3",
            "price": "1.99",
            "unique_id": "7113048"
        },
        {
            "item": "2890-60773",
            "quantity": "2",
            "price": "133.00",
            "unique_id": "7107457"
        },
        {
            "item": "2890-17738",
            "quantity": "1",
            "price": "94.00",
            "unique_id": "1233388"
        }
    ],
    "order_number": "830100487001",
    "discount": "89.99",
    "shipping": "0.00",
    "user_info": {
        "email": "abc.xxx@tealium.com",
        "details": {}
    }
}
```


## Action configuration screenshot

![](https://docs.tealium.com/images/server-side/example)
