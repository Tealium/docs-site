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
    &#34;cart&#34;: [
        {
            &#34;item&#34;: &#34;2890-17738&#34;,
            &#34;quantity&#34;: &#34;1&#34;,
            &#34;price&#34;: &#34;94.00&#34;,
            &#34;unique_id&#34;: &#34;1233388&#34;
        },
        {
            &#34;item&#34;: &#34;2890-60773&#34;,
            &#34;quantity&#34;: &#34;2&#34;,
            &#34;price&#34;: &#34;133.00&#34;,
            &#34;unique_id&#34;: &#34;7113048&#34;
        },
        {
            &#34;item&#34;: &#34;3414-301727&#34;,
            &#34;quantity&#34;: &#34;3&#34;,
            &#34;price&#34;: &#34;1.99&#34;,
            &#34;unique_id&#34;: &#34;7107457&#34;
        }
    ],
    &#34;order_number&#34;: &#34;830100487001&#34;,
    &#34;discount&#34;: &#34;89.99&#34;,
    &#34;shipping&#34;: &#34;0.00&#34;,
    &#34;user_info&#34;: {
        &#34;email&#34;: &#34;abc.xxx@tealium.com&#34;,
        &#34;details&#34;: {}
    }
}

```

## Action implementation

### Method field

Set to &#34;GET&#34;.

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

Variables are internally translated to JSON and made available to all templates.

#### Resulting JSON structure:

```json
{

  &#34;shipping&#34;: &#34;0.00&#34;,
  &#34;orderNumber&#34;: &#34;830100487001&#34;,
  &#34;userEmail&#34;: &#34;abc.xxx@tealium.com&#34;,
  &#34;cart&#34;: [
    {
      &#34;id&#34;: &#34;7113048&#34;,
      &#34;price&#34;: &#34;1.99&#34;,
      &#34;item&#34;: &#34;3414-301727&#34;,
      &#34;quantity&#34;: &#34;3&#34;
    },
    {
      &#34;id&#34;: &#34;7107457&#34;,
      &#34;price&#34;: &#34;133.00&#34;,
      &#34;item&#34;: &#34;2890-60773&#34;,
      &#34;quantity&#34;: &#34;2&#34;
    },
    {
      &#34;id&#34;: &#34;1233388&#34;,
      &#34;price&#34;: &#34;94.00&#34;,
      &#34;item&#34;: &#34;2890-17738&#34;,
      &#34;quantity&#34;: &#34;1&#34;
    }
  ],
  &#34;projectId&#34;: &#34;6391707&#34;,
  &#34;discount&#34;: &#34;89.99&#34;

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
    &#34;cart&#34;: [
        {{#cart}}
        {
            &#34;item&#34;: &#34;{{item}}&#34;,
            &#34;quantity&#34;: &#34;{{quantity}}&#34;,
            &#34;price&#34;: &#34;{{price}}&#34;,
            &#34;unique_id&#34;: &#34;{{id}}&#34;
        }{{#iter.hasNext}}, {{/iter.hasNext}}
        {{/cart}}
    ],
    &#34;order_number&#34;: &#34;{{orderNumber}}&#34;,
    &#34;discount&#34;: &#34;{{discount}}&#34;,
    &#34;shipping&#34;: &#34;{{shipping}}&#34;,
    &#34;user_info&#34;: {
        &#34;email&#34;: &#34;{{userEmail}}&#34;,
        &#34;details&#34;: {}
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
    &#34;cart&#34;: [
        {
            &#34;item&#34;: &#34;3414-301727&#34;,
            &#34;quantity&#34;: &#34;3&#34;,
            &#34;price&#34;: &#34;1.99&#34;,
            &#34;unique_id&#34;: &#34;7113048&#34;
        },
        {
            &#34;item&#34;: &#34;2890-60773&#34;,
            &#34;quantity&#34;: &#34;2&#34;,
            &#34;price&#34;: &#34;133.00&#34;,
            &#34;unique_id&#34;: &#34;7107457&#34;
        },
        {
            &#34;item&#34;: &#34;2890-17738&#34;,
            &#34;quantity&#34;: &#34;1&#34;,
            &#34;price&#34;: &#34;94.00&#34;,
            &#34;unique_id&#34;: &#34;1233388&#34;
        }
    ],
    &#34;order_number&#34;: &#34;830100487001&#34;,
    &#34;discount&#34;: &#34;89.99&#34;,
    &#34;shipping&#34;: &#34;0.00&#34;,
    &#34;user_info&#34;: {
        &#34;email&#34;: &#34;abc.xxx@tealium.com&#34;,
        &#34;details&#34;: {}
    }
}
```


## Action configuration screenshot

![](/images/server-side/example)
