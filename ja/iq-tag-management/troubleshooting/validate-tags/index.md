---
title: タグの検証とトラブルシューティング
description: このガイドでは、Tealium iQに実装されたクライアントサイドタグの検証方法について説明します。タグがロードされ、データが送信されていることを確認するためのいくつかの方法をカバーします。
url: https://docs.tealium.com/ja/iq-tag-management/troubleshooting/validate-tags/
---
## はじめに

ここで取り上げる検証方法は、ブラウザとしてGoogle Chromeを使用し、ベンダー固有のプラグインを使用して実行されます。

### ベンダープラグイン

Google Chrome用の以下のプラグインをダウンロードすることをお勧めします：

* [Google Tag Assistant](https://chrome.google.com/webstore/detail/tag-assistant-by-google/kejbdjndbnbjgmefkgdddjlbokphdefk?hl=en)
* [Google Analytics Debugger](https://chrome.google.com/webstore/detail/google-analytics-debugger/jnkmfdileelhofjcijamephohjechhna?hl=en)
* [Facebook Pixel Helper](https://chrome.google.com/webstore/detail/facebook-pixel-helper/fdgfkebogiimcoedlicjlajpkdmockpc?hl=en)
* [Adobe Analytics Debugger](https://chrome.google.com/webstore/detail/debugger-for-adobe-analyt/bdingoflfadhnjohjaplginnpjeclmof?hl=en)
* [Tealium Tools](https://docs.tealium.com/tealium-tools-browser-extension/)

### Chrome Developer Tools

Chrome Dev Toolsのインターフェースに慣れるためのチュートリアルを受講することをお勧めします：

* [Chrome Dev Tools Tutorial](https://www.codeschool.com/courses/discover-devtools)
* [Chrome Dev Tools Documentation](https://developers.google.com/web/tools/chrome-devtools/)

## Google Tag Assistantを使用して検証する

以下のリストは、人気のあるGoogleタグのパラメータについて説明するリンクを提供します：

* [Google Analytics Parameters Cheat Sheet](https://www.cheatography.com/dmpg-tom/cheat-sheets/google-universal-analytics-url-collect-parameters/)
* [Google Analytics Enhanced Ecommerce Parameters Cheat Sheet](https://www.cheatography.com/nikalytics/cheat-sheets/enhanced-ecommerce-universal-analytics/)
* [Google Adwords Remarketing Parameters](https://developers.google.com/adwords-remarketing-tag/parameters)
* [Google Adwords Remarketing Verification](https://developers.google.com/adwords-remarketing-tag/verification)
* [More About Google Tag Assistant](https://support.google.com/analytics/answer/6277313?hl=en)

Google Tag Assistantを使用して検証するための次の手順を使用します：

1. プラグインをダウンロードした後、Tealiumタグがインストールされているサイトを開き、Chromeウィンドウの右上隅にあるプラグインアイコンをクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/tag-assistant.png)

1. **Validate All Pages** を選択し、**Done** をクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-09-41-08.png)

1. プラグインが他のプラグインによってGoogleタグがブロックされているかどうかをチェックすることを許可するために **Allow** をクリックし、プラグインインターフェースに表示されるGoogleタグの詳細を表示するために任意のGoogleタグをクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-09-44-50.png)

1. Google Analyticsの場合、**Pageview Requests** または **Events** をクリックします。
次の例は、**Pageview Requests** をクリックしたときに表示される結果を示しています。
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-10-00-07.png)

1. これらのいずれかをクリックすると、Googleに送信されたパラメータが表示されます。
**URLs** タブをクリックすると、より詳細なビューが提供されます。
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-10-02-02.png)|

1. デフォルトビューは整形されていないURLリクエストを表示します。整形されたビューに切り替えるには、テーブルボタンをクリックします。
これにより、Googleに送信された各パラメータを確認できます。ただし、最初の **Metadata** タブを表示しても問題ありません。
  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-10-03-53.png)

1. このプラグインを使用して他のGoogleタグを検証することもできます。
いくつかの例は、Floodlight、Google Ads、Google Publisher、DFP、Google Trusted Storesです。

## Google Debuggerを使用して検証する

以下のリストは、Google Analyticsタグのパラメータについて説明するリンクを提供します：

* [Google Analytics Parameters Cheat Sheet](https://www.cheatography.com/dmpg-tom/cheat-sheets/google-universal-analytics-url-collect-parameters/)
* [Google Analytics Enhanced Ecommerce Parameters Cheat Sheet](https://www.cheatography.com/nikalytics/cheat-sheets/enhanced-ecommerce-universal-analytics/)

Google Debuggerを使用して検証するための次の手順を使用します：

1. プラグインをダウンロードした後、Tealiumタグがインストールされているサイトを開き、Chromeウィンドウの右上隅にあるプラグインアイコンをクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-10-27-20.png)
    [Chrome Developer Tools Console](https://developers.google.com/web/tools/chrome-devtools/console/)にライブ出力が表示されます。
1. イベントとページビューをトリガーすると、コンソールにGoogle Analyticsの出力が表示されます。  
出力には、Google Analyticsに送信されている内容が表示されます。  
    ![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-10-28-48.png)|

## Facebook Pixel Helperを使用して検証する

このウィンドウには、インタラクションのタイプに応じて表示されるイベントがいくつかあります。これらのイベントとそれぞれに送信できるパラメータについて学ぶには、[Facebook Events](https://developers.facebook.com/docs/ads-for-websites/pixel-events/v2.11#events)にアクセスしてください。

Facebook Pixel Helperを使用して検証するための次の手順を使用します：

1. プラグインをダウンロードした後、Tealiumタグがインストールされているサイトを開き、Chromeウィンドウの右上隅にあるプラグインアイコンをクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-11-13-34.png)
1. プラグイン内でイベントを展開すると、パラメータが次のように表示されます：  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-11-20-25.png)
1. 検出された各ピクセルタイプを展開して詳細を表示することができます。  
この例では、`AddToCart` ピクセルイベントが表示されています：  
表示されるデータは、Facebookに送信されたデータです。  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-11-21-53.png)

## Adobe Analytics Debuggerを使用して検証する

Adobe Analyticsデバッガーに表示されるパラメータはいくつかあります。Adobe Analytics（AppMeasurement）タグのパラメータについて詳しく知るには、[Adobe Query Parameters](https://experienceleague.adobe.com/en/docs/analytics/implementation/validate/query-parameters)にアクセスしてください。

Adobe Analytics Debuggerを使用して検証するための次の手順を使用します：

1. プラグインをダウンロードした後、Tealiumタグがインストールされているサイトを開き、Chromeウィンドウの右上隅にあるプラグインアイコンをクリックします。
[Chrome Developer Tools Console](https://developers.google.com/web/tools/chrome-devtools/console/)にライブ出力が表示されます。  
    ![](https://docs.tealium.com/images/iq-tag-management/drapey-tie-neck-top-gap-2017-12-28-11-28-20.png)

1. イベントとページビューをトリガーすると、コンソールにAdobe Analyticsの出力が表示されます。  
このコンソール出力は、各サーバーコールでAdobeに送信されるすべてのデータを表しています。  
    ![](https://docs.tealium.com/images/iq-tag-management/drapey-tie-neck-top-gap-2017-12-28-11-29-46.png)
## Chrome 開発者ツールを使用した検証

すべてのベンダーが独自のプラグインを持っているわけではありません。この場合、ブラウザからタグによってリクエストが正常に送信されていることを検証するために、Chrome 開発者ツールの **ネットワーク** タブを使用することをお勧めします。

詳細については、[Chrome DevTools ネットワーク分析](https://developers.google.com/web/tools/chrome-devtools/network-performance/reference)を参照し、ドキュメントで **クエリ文字列パラメータの表示** を検索して、利用可能なパラメータについてさらに学んでください。

Chrome 開発者ツールを使用して検証するための手順は以下の通りです：

1. Tealiumがインストールされているサイトを開きます。
1. 開発者ツールを表示するには、ページを右クリックして **検証** を選択します。  
    ![](https://docs.tealium.com/images/iq-tag-management/chrome-inspect.png)

1. **ネットワーク** タブをクリックします。  
この例ではGoogle Analyticsを使用していますが、任意のタグを使用できます。  
    ![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-12-38.png)

1. Tealium iQで、タグの構成部分にある **トラッキングID** を見つけ、ID番号をコピーします。  
    ![](https://docs.tealium.com/images/iq-tag-management/tiq---services-christina-2017-12-28-13-13-14.png)

1. ネットワークタブが開いているサイトに戻り、**フィルター** ボックスにID番号を貼り付けます。  
    ![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-13-56.png)

1. **ログを保持** チェックボックスをクリックし、ページビューやイベントの実行を開始します。  
タグによって送信されるネットワークリクエストが表示されます。  
    ![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-15-15.png)

1. エントリをクリックしてリクエストの詳細を表示します。  
ここでは、`Request URL`、`Response Headers`、`Cookies`、`Query Parameters` など、いくつかの情報セクションが表示されます。  

<blockquote>
私たちは `Request URL` と `Query Parameters` に最も関心がありますが、ここで他の情報も見つけることができます：**Chrome Network Tab**
</blockquote>

![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-15-55.png)
**Request URL** は、POSTまたはGETでベンダーのサーバーに送信された完全なURLです。このURLには、サーバーのURLとベンダーが受け取るクエリ文字列パラメータ（データ）が含まれています。  
![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-18-25.png)
**クエリ文字列パラメータ** は、ベンダーが受け取るパラメータ（サーバーのURLを含まない）のリストです。これは、ページからベンダーへデータが渡される方法です。  
![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-20-01.png)
次の例は、Adobe AppMeasurementサーバーコールからのクエリ文字列パラメータを示しています：  
![](https://docs.tealium.com/images/iq-tag-management/drapey-tie-neck-top-gap-2017-12-28-13-22-40.png)

## トラブルシューティング

クエリパラメータやプラグインに何かが欠けている場合があります。自分でトラブルシューティングを試みたい場合は、次のことを試すことができます：

* 最初に、Web CompanionまたはUniversal Tag Monitorを使用して、ページおよびイベントトラッキングコールで使用されるデータレイヤー変数を確認します。[詳細を学ぶ](https://docs.tealium.com/ja/platforms/javascript/install/#validate-installation)。
* データレイヤーが不完全な場合は、必要な変数を含めるために追加の開発作業が必要になる場合があります。
* データレイヤーが正しく見え、トラッキングコールが期待通りに機能しているが、ベンダータグが期待するデータを受け取っていない場合は、タグのデータマッピングを確認することが次のステップです。データマッピングは、Tealiumがどのデータレイヤー変数を対応するベンダーパラメータに送信するかを指示します。[詳細を学ぶ]().