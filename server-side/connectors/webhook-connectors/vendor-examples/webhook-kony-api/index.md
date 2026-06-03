---
title: Webhook - Kony API
description: How to configure an advanced Webhook - Send Custom Request action using Template Variables for Kony API
url: https://docs.tealium.com/server-side/connectors/webhook-connectors/vendor-examples/webhook-kony-api/
---
## Overview

Submit an http request to Kony with a list of subscriber IDs and name &amp;amp; value pairs. Whole request body is a JSON message.

## Vendor requirements

### Sample JSON message:

```json
{
    &#34;messageRequest&#34;: {
        &#34;appId&#34;: &#34;IceMobile&#34;,
        &#34;global&#34;: {},
        &#34;messages&#34;: {
            &#34;message&#34;: {
                &#34;content&#34;: {
                    &#34;priorityService&#34;: &#34;false&#34;,
                    &#34;data&#34;: &#34;Message Body&#34;,
                    &#34;mimeType&#34;: &#34;text/plain&#34;
                },
                &#34;overrideMessageId&#34;: 0,
                &#34;startTimestamp&#34;: 0,
                &#34;expiryTimestamp&#34;: 0,
                &#34;subscribers&#34;: {
                    &#34;subscriber&#34;: [
                        {
                            &#34;ksid&#34;: &#34;95784&#34;
                        },
                        {
                            &#34;ksid&#34;: &#34;97899&#34;
                        }
                    ]
                },
                &#34;platformSpecificProps&#34;: {
                    &#34;iphone&#34;: {
                        &#34;badge&#34;: 0,
                        &#34;customData&#34;: {
                            &#34;key&#34;: [
                                {
                                    &#34;name&#34;: &#34;trip_type&#34;,
                                    &#34;content&#34;: &#34;o&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;o&#34;,
                                    &#34;content&#34;: &#34;LAX&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;d&#34;,
                                    &#34;content&#34;: &#34;NRT&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;dd&#34;,
                                    &#34;content&#34;: &#34;2016-01-09&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;rd&#34;,
                                    &#34;content&#34;: &#34;2016-01-20&#34;
                                }
                            ]
                        }
                    }
                },
                &#34;type&#34;: &#34;PUSH&#34;
            }
        }
    }
}

```

#### Notes

* Subscribers array is dynamic and can contain one or more subscriber IDs.
* &#34;customData&#34; key array is dynamic and can contain one or more name and content objects.

## Action implementation

### Method field

Set to `POST`.

### URL field

Set to PutsReq bucket URL.

Consult Kony API documentation for a URL. A PutsReq URL is adequate to demonstrate a general implementation here.

### Body content type

Select option `application/json`.

### Body data

Select `Body` option and provide a template reference.

|Name| Value|
|---| ---|
|`Body`| `{{json_template}}`|

### Template variables

Set name and value pairs to be referenced and replaced in templates.

|Name| Value| Note|
|---| ---| ---|
|`subscribers.ksid`| Kony Sub IDs| Set of Strings attribute|
|`customData.name`| Kony Data Names| Set of Strings attribute|
|`customData.content`| Kony Data Contents| Set of Strings attribute|

Variables are internally translated to JSON and made available to all templates.

#### Resulting JSON structure:

```json
{
    &#34;subscribers&#34;: [
        {
            &#34;ksid&#34;: &#34;sub-id-1&#34;
        },
        {
            &#34;ksid&#34;: &#34;sub-id-2&#34;
        }
    ],
    &#34;customData&#34;: [
        {
            &#34;name&#34;: &#34;name-1&#34;,
            &#34;content&#34;: &#34;Content A&#34;
        },
        {
            &#34;name&#34;: &#34;name-2&#34;,
            &#34;content&#34;: &#34;Content B&#34;
        },
        {
            &#34;name&#34;: &#34;name-3&#34;,
            &#34;content&#34;: &#34;Content C&#34;
        }
    ]
}

```

### Templates

`json_template`  

```json
{
    &#34;messageRequest&#34;: {
        &#34;appId&#34;: &#34;IceMobile&#34;,
        &#34;global&#34;: {},
        &#34;messages&#34;: {
            &#34;message&#34;: {
                &#34;content&#34;: {
                    &#34;priorityService&#34;: &#34;false&#34;,
                    &#34;data&#34;: &#34;Message Body&#34;,
                    &#34;mimeType&#34;: &#34;text/plain&#34;
                },
                &#34;overrideMessageId&#34;: 0,
                &#34;startTimestamp&#34;: 0,
                &#34;expiryTimestamp&#34;: 0,
                &#34;subscribers&#34;: {
                    &#34;subscriber&#34;: [
                        {{#subscribers}}
                        {
                            &#34;ksid&#34;: &#34;{{ksid}}&#34;
                        }{{#iter.hasNext}}, {{/iter.hasNext}}
                        {{/subscribers}}
                    ]
                },
                &#34;platformSpecificProps&#34;: {
                    &#34;iphone&#34;: {
                        &#34;badge&#34;: 0,
                        &#34;customData&#34;: {
                            &#34;key&#34;: [
                                {{#customData}}
                                {
                                    &#34;name&#34;: &#34;{{name}}&#34;,
                                    &#34;content&#34;: &#34;{{content}}&#34;
                                }{{#iter.hasNext}}, {{/iter.hasNext}}
                                {{/customData}}
                            ]
                        }
                    }
                },
                &#34;type&#34;: &#34;PUSH&#34;
            }
        }
    }
}
```

### Templates Rendered

Internally template gets rendered and its content injected where referenced.

`json_template`  

```json
{
    &#34;messageRequest&#34;: {
        &#34;appId&#34;: &#34;IceMobile&#34;,
        &#34;global&#34;: {},
        &#34;messages&#34;: {
            &#34;message&#34;: {
                &#34;content&#34;: {
                    &#34;priorityService&#34;: &#34;false&#34;,
                    &#34;data&#34;: &#34;Message Body&#34;,
                    &#34;mimeType&#34;: &#34;text/plain&#34;
                },
                &#34;overrideMessageId&#34;: 0,
                &#34;startTimestamp&#34;: 0,
                &#34;expiryTimestamp&#34;: 0,
                &#34;subscribers&#34;: {
                    &#34;subscriber&#34;: [
                        {
                            &#34;ksid&#34;: &#34;sub-id-1&#34;
                        },
                        {
                            &#34;ksid&#34;: &#34;sub-id-2&#34;
                        }
                    ]
                },
                &#34;platformSpecificProps&#34;: {
                    &#34;iphone&#34;: {
                        &#34;badge&#34;: 0,
                        &#34;customData&#34;: {
                            &#34;key&#34;: [
                                {
                                    &#34;name&#34;: &#34;name-1&#34;,
                                    &#34;content&#34;: &#34;Content A&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;name-2&#34;,
                                    &#34;content&#34;: &#34;Content B&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;name-3&#34;,
                                    &#34;content&#34;: &#34;Content C&#34;
                                }
                            ]
                        }
                    }
                },
                &#34;type&#34;: &#34;PUSH&#34;
            }
        }
    }
}
```

## Action configuration screenshot

![](/images/server-side/example)
