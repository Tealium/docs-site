---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/amp/track/
---
## Track Views

The base installation makes a tracking call every time a user opens or changes a screen in your AMP site.

To customize the data layer used for this tracking, add the [extra URL Params](https://amp.dev/documentation/components/amp-analytics/?format=websites#extra-url-params) block `extraUrlParams` with key-value pairs for your variables:

```html
&lt;amp-analytics type=&#34;tealiumcollect&#34;&gt;
&lt;script type=&#34;application/json&#34;&gt;
{
  &#34;vars&#34;: {
    &#34;account&#34;: &#34;ACCOUNT&#34;,
    &#34;profile&#34;: &#34;PROFILE&#34;,
    &#34;datasource&#34;: &#34;DATASOURCE&#34;
  },
  &#34;extraUrlParams&#34;: {
    &#34;example_param1&#34;: &#34;abc&#34;,
    &#34;example_param2&#34;: 123
  }
}     
&lt;/script&gt;
&lt;/amp-analytics&gt;
```

| Parameters | Type | Description |Example |
| --- | --- | --- | --- |
| `account` | `String` |Tealium account name | `&#34;companyXYZ&#34;` |
| `profile` | `String` |Tealium profile name | `&#34;main&#34;`  |
| `datasource` | `String` | Data source key  | `&#34;abc123&#34;` |


## Track Events

The `triggers` configuration object defines which events to track. A trigger is define as a key-value pair of trigger name and configuration. Trigger names are alphanumeric strings and the configuration determines the targets of the events.

The following is an example of a trigger:

```json
&#34;triggers&#34;: {
  &#34;trigger_name&#34;: {
    &#34;on&#34;: &#34;VALUE&#34;,
    &#34;selector&#34;: &#34;VALUE&#34;,
    &#34;request&#34;: &#34;VALUE&#34;,
    &#34;vars&#34;: {
      &#34;tealium_event&#34;: &#34;VALUE&#34;
    }
    &#34;extraUrlParams&#34;: {
      &#34;extra_var&#34;: &#34;${extraVar}&#34;
    }
  }
}
```

AMP supports the following [`amp-analytics` triggers](https://www.ampproject.org/docs/reference/components/amp-analytics#triggers).


## Dynamic Tracking Variables

For the event types `visible` and `click` (used in the `on` property), dynamic tracking variables are passed using HTML5 elemental attributes in the format `data-vars-*`. Variables passed this way are converted to camel-case naming.

For example, the property `data-vars-link-name=&#34;register&#34;` becomes the variable `${linkName}` that is referenced in the `extraUrlParams` block of your trigger.

```json
&#34;triggers&#34;: {
  &#34;custom_click&#34;: {
    &#34;on&#34;: &#34;click&#34;,
    &#34;selector&#34;: &#34;#the-button&#34;,
    &#34;request&#34;: &#34;event&#34;,
    &#34;vars&#34;: {
      &#34;tealium_event&#34;: &#34;custom_click&#34;
    }
    &#34;extraUrlParams&#34;: {
      &#34;link_name&#34;: &#34;${linkName}&#34;
    }
  }
}
```

AMP supports the following [`amp-analytics` extra URL params](https://amp.dev/documentation/components/amp-analytics/?referrer=ampproject.org#extra-url-params).

The button&#39;s HTML example:

```html
&lt;span id=&#34;the-button&#34; data-vars-link-name=&#34;register&#34;&gt;
Button Text
&lt;/span&gt;
```
