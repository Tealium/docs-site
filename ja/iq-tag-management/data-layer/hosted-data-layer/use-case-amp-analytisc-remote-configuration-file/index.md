---
title: ユースケース - AMPアナリティクスリモート構成ファイル
url: https://docs.tealium.com/ja/iq-tag-management/data-layer/hosted-data-layer/use-case-amp-analytisc-remote-configuration-file/
---
このセクションでは、ホストされたデータレイヤーがAMPアナリティクスの実装のためのリモートJSON構成ファイルを提供するためにどのように使用できるかを示すユースケースを説明します。

[Tealium for AMP]/platforms/amp/)の実装について詳しくはこちらをご覧ください。

## 前提条件

* 特定のタグを実行したいAMPサイト

## AMPアナリティクスにリモートJSONファイルを提供する

AMPアナリティクス構成のためのリモートJSONファイルを提供するための次の手順を使用します：

1. **AMP構成を特定する**  
amp-analytics構成は、あなたのベンダーまたはイベントトラッキングのニーズに特化しています。  
詳細情報については、[AMP Analytics](https://www.ampproject.org/docs/analytics/analytics_amp)のドキュメンテーションを参照してください。  
AMP Analytics JSON構成の例：  
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

1. **ホストされたデータレイヤーJSONファイルをアップロードする**  
AMP構成ファイルは任意の名前を持つことができ、例えばamp.analytics.config.jsonなどです。このユースケースでは、アップロードされたファイルのデータレイヤーIDはamp.analytics.configです。ファイルがHosted Data Layer APIを使用してアップロードされると、次の場所で利用可能になります：  
    ```
    https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/amp.analytics.config.json
    ```

1. **AMPページにタグを付ける**  
新しいホストされたデータレイヤーJSONファイルは、`amp-analytics`タグを使用してAMPページで参照できます：  
    ```
    &lt;amp-analytics config=&#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/amp.analytics.config.json&#34;&gt;
    ```
