---
title: Use Case — AMP Analytics Remote Configuration File
url: https://docs.tealium.com/iq-tag-management/data-layer/hosted-data-layer/use-case-amp-analytisc-remote-configuration-file/
---
This section illustrates a use case that shows how hosted data layer can be used to serve a remote JSON configuration file for an implementation of AMP Analytics.

Learn more about implementing [Tealium for AMP]/platforms/amp/).

## Prerequisites

* An AMP site where you want to run certain tags

## Serve a remote JSON file to AMP analytics

Use the following steps to serve a remote JSON file for an AMP Analytics configuration:

1. **Identify your AMP configuration**  
The amp-analytics configuration is specific to your vendor or event tracking needs.  
For additional information, see the [AMP Analytics](https://www.ampproject.org/docs/analytics/analytics_amp) documentation.  
AMP Analytics JSON configuration example:  
    ```json
        {
          &#34;requests&#34;: {
            &#34;pageview&#34;: &#34;https://example.com/analytics?url=${canonicalUrl}&amp;title=${title}&amp;acct=${account}&#34;
          },
          &#34;vars&#34;: {
            &#34;account&#34;: &#34;A0123456789&#34;
          },
          &#34;triggers&#34;: {
            &#34;trackPageview&#34;: {
              &#34;on&#34;: &#34;visible&#34;,
              &#34;request&#34;: &#34;pageview&#34;
            },
            &#34;links&#34;: {
              &#34;on&#34;: &#34;click&#34;,
              &#34;selector&#34;: &#34;.tracked-links-selector&#34;,
              &#34;request&#34;: &#34;event&#34;
            }
          }
        }
    ```

1. **Upload hosted data layer JSON file**  
Your AMP configuration file can have any name, for example amp.analytics.config.json. In this use case, the data layer ID for the uploaded file is amp.analytics.config. Once the file is uploaded using the Hosted Data Layer API, it will then be available at the following location:  
    ```
    https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/amp.analytics.config.json
    ```

1. **Tag your AMP page**  
The new hosted data layer JSON file can be referenced in your AMP pages using the `amp-analytics` tag:  
    ```
    &lt;amp-analytics config=&#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/amp.analytics.config.json&#34;&gt;
    ```
