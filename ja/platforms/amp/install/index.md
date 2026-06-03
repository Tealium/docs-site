---
title: インストール
description: Tealium CollectをAMPサイトにインストールする方法を学びます。
url: https://docs.tealium.com/ja/platforms/amp/install/
---## 要件

* [Tealium Customer Data Hubアカウント]()

## インストール

`&lt;amp-analytics&gt;`要素は、AMPドキュメントから分析データをキャプチャする拡張AMPコンポーネントです。AMP分析は、タイプ属性[`tealiumcollect`](https://amp.dev/documentation/guides-and-tutorials/optimize-and-measure/configure-analytics/analytics-vendors/#tealium-collect)を使用してTealium Collectの組み込み構成サポートを提供します。

AMPサイトのTealium Collectをインストールするには：

1. スクリプトをHTMLドキュメントの`&lt;head&gt;`タグ内のページに追加します：

      ```html
      &lt;script async custom-element=&#34;amp-analytics&#34; src=&#34;https://cdn.ampproject.org/v0/amp-analytics-0.1.js&#34;&gt;&lt;/script&gt;
      ```

2. Tealium Collectの基本インストールをAMPページに追加するには、以下のようにページの`&lt;body&gt;`タグ内に`&lt;amp-analytics&gt;`要素を追加します：

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
| パラメータ | タイプ | 説明 |例 |
| --- | --- | --- | --- |
| `account` | `String` |Tealiumアカウント名| `&#34;companyXYZ&#34;` |
| `profile` | `String` |Tealiumプロファイル名 |  `&#34;main&#34;`  |
| `datasource` | `String` | データソースキー | `&#34;abc123&#34;` |


## 検証

ウェブページがAMP HTML仕様を満たしていることを確認するには、[AMP Validator](https://github.com/ampproject/amphtml#the-amp-validator)を使用します。

1. バリデータを_オン_にするには、AMPページのURLの末尾に`#development=1`を追加します。

2. ブラウザのコンソールを見て、AMP検証エラーがある場合は確認します。

## ホストされたJSON

ページに直接埋め込むのではなく、ホストされたJSONを使用してTealium Collect for AMPをインストールすることを希望する場合は、`config`属性を使用してAMP構成をホストされた場所からロードします：

```html
&lt;amp-analytics type=&#34;tealiumcollect&#34; config=&#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILE.json&#34; /&gt;
```

AMPサイトでリモートJSON構成ファイルを提供する方法について[詳しく学ぶ]()。

## フルページの例

この例は、完全なAMPページを示しています。この構成は、標準的なページビューデータをTealiumに送信し、ボタンのクリックを追跡します。

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
