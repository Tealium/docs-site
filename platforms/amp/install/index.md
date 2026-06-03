---
title: Install
description: Learn to install Tealium Collect for AMP sites.
url: https://docs.tealium.com/platforms/amp/install/
---## Requirements

* [Tealium Customer Data Hub account]()

## Install

The `&lt;amp-analytics&gt;` element is an extended AMP component that captures analytic data from an AMP document. AMP analytics provides built-in configuration support for Tealium Collect with the type attribute [`tealiumcollect`](https://amp.dev/documentation/guides-and-tutorials/optimize-and-measure/configure-analytics/analytics-vendors/#tealium-collect).

To install Tealium Collect for AMP sites:

1. Add the script to your page within the `&lt;head&gt;` tags of your HTML document:  

      ```html
      &lt;script async custom-element=&#34;amp-analytics&#34; src=&#34;https://cdn.ampproject.org/v0/amp-analytics-0.1.js&#34;&gt;&lt;/script&gt;
      ```

2. To add a base installation of Tealium Collect to an AMP page, add the `&lt;amp-analytics&gt;` element within the `&lt;body&gt;` tags of your page as follows:

      ```html
      &lt;amp-analytics type=&#34;tealiumcollect&#34;&gt;
      &lt;script type=&#34;application/json&#34;&gt; {
            &#34;vars&#34;: {
              &#34;account&#34;: &#34;ACCOUNT&#34;,
              &#34;profile&#34;: &#34;PROFILE&#34;,
              &#34;datasource&#34;: &#34;DATASOURCE&#34;
            }
      }     
      &lt;/script&gt;
      &lt;/amp-analytics&gt;
      ```  
| Parameters | Type | Description |Example |
| --- | --- | --- | --- |
| `account` | `String` |Tealium account name| `&#34;companyXYZ&#34;` |
| `profile` | `String` |Tealium profile name |  `&#34;main&#34;`  |
| `datasource` | `String` | Data source key | `&#34;abc123&#34;` |


## Validation

To verify that that a web page satisfies the AMP HTML specifications, use the [AMP Validator](https://github.com/ampproject/amphtml#the-amp-validator).

1. To turn the validator _on_, add `#development=1` to the end of an AMP page URL.

2. See the browser console to view AMP validation errors, if any.

## Hosted JSON

If you prefer to install Tealium Collect for AMP with hosted JSON (rather than embedded directly in the page) use the `config` attribute to load your AMP configuration from a hosted location:

```html
&lt;amp-analytics type=&#34;tealiumcollect&#34; config=&#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILE.json&#34; /&gt;
```

[Learn more]() about serving remote JSON configuration files for use on an AMP site.

## Full Page Example

This example demonstrates a complete AMP page. This configuration sends standard page view data to Tealium and track button clicks.

```html
&lt;!doctype html&gt;
&lt;html amp lang=&#34;en&#34;&gt;
  &lt;head&gt;
    &lt;meta charset=&#34;utf-8&#34;&gt;
    &lt;script async src=&#34;https://cdn.ampproject.org/v0.js&#34;&gt;&lt;/script&gt;
    &lt;script async custom-element=&#34;amp-analytics&#34; src=&#34;https://cdn.ampproject.org/v0/amp-analytics-0.1.js&#34;&gt;&lt;/script&gt;
    &lt;style amp-boilerplate&gt;body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}&lt;/style&gt;&lt;noscript&gt;&lt;style amp-boilerplate&gt;body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}&lt;/style&gt;&lt;/noscript&gt;
    &lt;title&gt;Hello, AMPs&lt;/title&gt;
    &lt;link rel=&#34;canonical&#34; href=&#34;http://example.ampproject.org/article-metadata.html&#34;&gt;
    &lt;meta name=&#34;viewport&#34; content=&#34;width=device-width,minimum-scale=1,initial-scale=1&#34;&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;amp-analytics type=&#34;tealiumcollect&#34;&gt;
    &lt;script type=&#34;application/json&#34;&gt; {
      &#34;vars&#34;: {
        &#34;account&#34;: &#34;ACCOUNT&#34;,
        &#34;profile&#34;: &#34;PROFILE&#34;,
        &#34;datasource&#34;: &#34;DATASOURCE&#34;
      },
      &#34;triggers&#34;: {
        &#34;custom_click&#34;: {
          &#34;on&#34;: &#34;click&#34;,
          &#34;selector&#34;: &#34;#the-button&#34;,
          &#34;request&#34;: &#34;event&#34;,
          &#34;vars&#34;: {
            &#34;tealium_event&#34;: &#34;custom_click&#34;
          },
          &#34;extraUrlParams&#34;: {
            &#34;link_name&#34;: &#34;${linkName}&#34;
          }
        }
      },
      &#34;extraUrlParams&#34;: {
        &#34;site_section&#34;: &#34;Demos&#34;
      }
    }
    &lt;/script&gt;
    &lt;/amp-analytics&gt;

    &lt;h1 id=&#34;header&#34;&gt;Welcome to the mobile web.&lt;/h1&gt;
    &lt;p&gt;Testing AMP Analytics &#34;tealiumcollect&#34; component.&lt;/p&gt;
    &lt;div&gt;
      &lt;button type=&#34;button&#34; id=&#34;the-button&#34; data-vars-link-name=&#34;track&#34;&gt;Track&lt;/button&gt;
    &lt;/div&gt;
  &lt;/body&gt;
&lt;/html&gt;
```
