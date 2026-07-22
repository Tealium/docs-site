---
title: Install
description: Learn to install Tealium Collect for AMP sites.
url: https://docs.tealium.com/platforms/amp/install/
---## Requirements

* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)

## Install

The `<amp-analytics>` element is an extended AMP component that captures analytic data from an AMP document. AMP analytics provides built-in configuration support for Tealium Collect with the type attribute [`tealiumcollect`](https://amp.dev/documentation/guides-and-tutorials/optimize-and-measure/configure-analytics/analytics-vendors/#tealium-collect).

To install Tealium Collect for AMP sites:

1. Add the script to your page within the `<head>` tags of your HTML document:  

      ```html
      <script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
      ```

2. To add a base installation of Tealium Collect to an AMP page, add the `<amp-analytics>` element within the `<body>` tags of your page as follows:

      ```html
      <amp-analytics type="tealiumcollect">
      <script type="application/json"> {
            "vars": {
              "account": "ACCOUNT",
              "profile": "PROFILE",
              "datasource": "DATASOURCE"
            }
      }     
      </script>
      </amp-analytics>
      ```  
| Parameters | Type | Description |Example |
| --- | --- | --- | --- |
| `account` | `String` |Tealium account name| `"companyXYZ"` |
| `profile` | `String` |Tealium profile name |  `"main"`  |
| `datasource` | `String` | Data source key | `"abc123"` |


## Validation

To verify that that a web page satisfies the AMP HTML specifications, use the [AMP Validator](https://github.com/ampproject/amphtml#the-amp-validator).

1. To turn the validator _on_, add `#development=1` to the end of an AMP page URL.

2. See the browser console to view AMP validation errors, if any.

## Hosted JSON

If you prefer to install Tealium Collect for AMP with hosted JSON (rather than embedded directly in the page) use the `config` attribute to load your AMP configuration from a hosted location:

```html
<amp-analytics type="tealiumcollect" config="https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILE.json" />
```

[Learn more](https://docs.tealium.com/use-case-supplementing-product-data/) about serving remote JSON configuration files for use on an AMP site.

## Full Page Example

This example demonstrates a complete AMP page. This configuration sends standard page view data to Tealium and track button clicks.

```html
<!doctype html>
<html amp lang="en">
  <head>
    <meta charset="utf-8">
    <script async src="https://cdn.ampproject.org/v0.js"></script>
    <script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
    <style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
    <title>Hello, AMPs</title>
    <link rel="canonical" href="http://example.ampproject.org/article-metadata.html">
    <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">
  </head>
  <body>
    <amp-analytics type="tealiumcollect">
    <script type="application/json"> {
      "vars": {
        "account": "ACCOUNT",
        "profile": "PROFILE",
        "datasource": "DATASOURCE"
      },
      "triggers": {
        "custom_click": {
          "on": "click",
          "selector": "#the-button",
          "request": "event",
          "vars": {
            "tealium_event": "custom_click"
          },
          "extraUrlParams": {
            "link_name": "${linkName}"
          }
        }
      },
      "extraUrlParams": {
        "site_section": "Demos"
      }
    }
    </script>
    </amp-analytics>

    <h1 id="header">Welcome to the mobile web.</h1>
    <p>Testing AMP Analytics "tealiumcollect" component.</p>
    <div>
      <button type="button" id="the-button" data-vars-link-name="track">Track</button>
    </div>
  </body>
</html>
```
