---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/amp/track/
---
## Track Views

The base installation makes a tracking call every time a user opens or changes a screen in your AMP site.

To customize the data layer used for this tracking, add the [extra URL Params](https://amp.dev/documentation/components/amp-analytics/?format=websites#extra-url-params) block `extraUrlParams` with key-value pairs for your variables:

```html
<amp-analytics type="tealiumcollect">
<script type="application/json">
{
  "vars": {
    "account": "ACCOUNT",
    "profile": "PROFILE",
    "datasource": "DATASOURCE"
  },
  "extraUrlParams": {
    "example_param1": "abc",
    "example_param2": 123
  }
}     
</script>
</amp-analytics>
```

| Parameters | Type | Description |Example |
| --- | --- | --- | --- |
| `account` | `String` |Tealium account name | `"companyXYZ"` |
| `profile` | `String` |Tealium profile name | `"main"`  |
| `datasource` | `String` | Data source key  | `"abc123"` |


## Track Events

The `triggers` configuration object defines which events to track. A trigger is define as a key-value pair of trigger name and configuration. Trigger names are alphanumeric strings and the configuration determines the targets of the events.

The following is an example of a trigger:

```json
"triggers": {
  "trigger_name": {
    "on": "VALUE",
    "selector": "VALUE",
    "request": "VALUE",
    "vars": {
      "tealium_event": "VALUE"
    }
    "extraUrlParams": {
      "extra_var": "${extraVar}"
    }
  }
}
```

AMP supports the following [`amp-analytics` triggers](https://www.ampproject.org/docs/reference/components/amp-analytics#triggers).


## Dynamic Tracking Variables

For the event types `visible` and `click` (used in the `on` property), dynamic tracking variables are passed using HTML5 elemental attributes in the format `data-vars-*`. Variables passed this way are converted to camel-case naming.

For example, the property `data-vars-link-name="register"` becomes the variable `${linkName}` that is referenced in the `extraUrlParams` block of your trigger.

```json
"triggers": {
  "custom_click": {
    "on": "click",
    "selector": "#the-button",
    "request": "event",
    "vars": {
      "tealium_event": "custom_click"
    }
    "extraUrlParams": {
      "link_name": "${linkName}"
    }
  }
}
```

AMP supports the following [`amp-analytics` extra URL params](https://amp.dev/documentation/components/amp-analytics/?referrer=ampproject.org#extra-url-params).

The button's HTML example:

```html
<span id="the-button" data-vars-link-name="register">
Button Text
</span>
```
