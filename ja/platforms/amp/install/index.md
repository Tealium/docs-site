---
title: インストール
description: Tealium CollectをAMPサイトにインストールする方法を学びます。
url: https://docs.tealium.com/ja/platforms/amp/install/
---## 要件

* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## インストール

`<amp-analytics>`要素は、AMPドキュメントから分析データをキャプチャする拡張AMPコンポーネントです。AMP分析は、タイプ属性[`tealiumcollect`](https://amp.dev/documentation/guides-and-tutorials/optimize-and-measure/configure-analytics/analytics-vendors/#tealium-collect)を使用してTealium Collectの組み込み構成サポートを提供します。

AMPサイトのTealium Collectをインストールするには：

1. スクリプトをHTMLドキュメントの`<head>`タグ内のページに追加します：

      ```html
      <script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
      ```

2. Tealium Collectの基本インストールをAMPページに追加するには、以下のようにページの`<body>`タグ内に`<amp-analytics>`要素を追加します：

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
| パラメータ | タイプ | 説明 |例 |
| --- | --- | --- | --- |
| `account` | `String` |Tealiumアカウント名| `"companyXYZ"` |
| `profile` | `String` |Tealiumプロファイル名 |  `"main"`  |
| `datasource` | `String` | データソースキー | `"abc123"` |


## 検証

ウェブページがAMP HTML仕様を満たしていることを確認するには、[AMP Validator](https://github.com/ampproject/amphtml#the-amp-validator)を使用します。

1. バリデータを_オン_にするには、AMPページのURLの末尾に`#development=1`を追加します。

2. ブラウザのコンソールを見て、AMP検証エラーがある場合は確認します。

## ホストされたJSON

ページに直接埋め込むのではなく、ホストされたJSONを使用してTealium Collect for AMPをインストールすることを希望する場合は、`config`属性を使用してAMP構成をホストされた場所からロードします：

```html
<amp-analytics type="tealiumcollect" config="https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILE.json" />
```

AMPサイトでリモートJSON構成ファイルを提供する方法について[詳しく学ぶ](https://docs.tealium.com/use-case-supplementing-product-data/)。

## フルページの例

この例は、完全なAMPページを示しています。この構成は、標準的なページビューデータをTealiumに送信し、ボタンのクリックを追跡します。

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
