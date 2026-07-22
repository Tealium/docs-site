---
title: タグの検証とトラブルシューティング
description: このガイドでは、Tealium iQに実装されたクライアントサイドのタグを検証する方法について説明します。タグが読み込まれ、データが送信されていることを確認するためのいくつかの方法をカバーします。
url: https://docs.tealium.com/ja/iq-tag-management/troubleshooting/validate-tags/
---
## はじめに

ここで説明する検証方法は、Google Chromeをブラウザとして、ベンダー固有のプラグインを使用して行われます。

### ベンダープラグイン

以下のプラグインをGoogle Chromeにダウンロードすることをおすすめします：

* [Google Tag Assistant](https://chrome.google.com/webstore/detail/tag-assistant-by-google/kejbdjndbnbjgmefkgdddjlbokphdefk?hl=ja)
* [Google Analytics Debugger](https://chrome.google.com/webstore/detail/google-analytics-debugger/jnkmfdileelhofjcijamephohjechhna?hl=ja)
* [Facebook Pixel Helper](https://chrome.google.com/webstore/detail/facebook-pixel-helper/fdgfkebogiimcoedlicjlajpkdmockpc?hl=ja)
* [Adobe Analytics Debugger](https://chrome.google.com/webstore/detail/debugger-for-adobe-analyt/bdingoflfadhnjohjaplginnpjeclmof?hl=ja)
* [Tealium Tools](https://docs.tealium.com/tealium-tools-browser-extension/)

### Chrome Developer Tools

Chrome Dev Toolsのチュートリアルを受講して、インターフェースに慣れることをおすすめします：

* [Chrome Dev Toolsチュートリアル](https://www.codeschool.com/courses/discover-devtools)
* [Chrome Dev Toolsドキュメント](https://developers.google.com/web/tools/chrome-devtools/)

## Google Tag Assistantで検証する

以下のリンクは、人気のあるGoogleタグのパラメータについて説明しています：

* [Google Analyticsパラメータチートシート](https://www.cheatography.com/dmpg-tom/cheat-sheets/google-universal-analytics-url-collect-parameters/)
* [Google Analytics Enhanced Ecommerceパラメータチートシート](https://www.cheatography.com/nikalytics/cheat-sheets/enhanced-ecommerce-universal-analytics/)
* [Google Adwordsリマーケティングパラメータ](https://developers.google.com/adwords-remarketing-tag/parameters)
* [Google Adwordsリマーケティングの検証](https://developers.google.com/adwords-remarketing-tag/verification)
* [Google Tag Assistantの詳細](https://support.google.com/analytics/answer/6277313?hl=ja)

Google Tag Assistantを使用して検証する手順は以下の通りです：

1. プラグインをダウンロードした後、Tealiumのタグがインストールされているサイトを開き、Chromeウィンドウの右上隅にあるプラグインアイコンをクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/tag-assistant.png)

1. **すべてのページを検証**を選択し、**完了**をクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-09-41-08.png)

1. プラグインが他のプラグインによってGoogleのタグがブロックされていないかどうかをチェックするために、**許可**をクリックし、プラグインインターフェースに表示されるGoogleのタグをクリックして詳細を確認します。  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-09-44-50.png)

1. Google Analyticsの場合、**ページビューリクエスト**または**イベント**をクリックします。
以下の例は、**ページビューリクエスト**をクリックした場合の結果を示しています。
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-10-00-07.png)

1. それらのいずれかをクリックすると、Googleに送信されるパラメータが表示されます。
**URL**タブをクリックすると、より詳細な表示が表示されます。
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-10-02-02.png)|

1. デフォルトの表示では、フォーマットされていないURLリクエストが表示されます。テーブルボタンをクリックしてフォーマットされた表示に切り替えると、Googleに送信される各パラメータが表示されます。ただし、最初の**メタデータ**タブを表示しても問題ありません。
  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-10-03-53.png)

1. このプラグインを使用して他のGoogleタグを検証することもできます。
例えば、Floodlight、Google Ads、Google Publisher、DFP、Google Trusted Storesなどがあります。

## Google Debuggerで検証する

以下のリンクは、Google Analyticsタグのパラメータについて説明しています：

* [Google Analyticsパラメータチートシート](https://www.cheatography.com/dmpg-tom/cheat-sheets/google-universal-analytics-url-collect-parameters/)
* [Google Analytics Enhanced Ecommerceパラメータチートシート](https://www.cheatography.com/nikalytics/cheat-sheets/enhanced-ecommerce-universal-analytics/)

Google Debuggerを使用して検証する手順は以下の通りです：

1. プラグインをダウンロードした後、Tealiumのタグがインストールされているサイトを開き、Chromeウィンドウの右上隅にあるプラグインアイコンをクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-10-27-20.png)
    [Chrome Developer Tools Console](https://developers.google.com/web/tools/chrome-devtools/console/)にライブ出力が表示されます。
1. イベントやページビューをトリガーすると、コンソールにGoogle Analyticsの出力が表示されます。  
出力には、Google Analyticsに送信される内容が表示されます。  
    ![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-10-28-48.png)|

## Facebook Pixel Helperで検証する

このウィンドウに表示されるイベントは、対話の種類に応じて異なる数が表示されます。これらのイベントとそれに送信できるパラメータについては、[Facebook Events](https://developers.facebook.com/docs/ads-for-websites/pixel-events/v2.11#events)を参照してください。

Facebook Pixel Helperを使用して検証する手順は以下の通りです：

1. プラグインをダウンロードした後、Tealiumのタグがインストールされているサイトを開き、Chromeウィンドウの右上隅にあるプラグインアイコンをクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-11-13-34.png)
1. プラグイン内のイベントを展開すると、以下のようにパラメータが表示されます：  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-11-20-25.png)
1. 検出された各ピクセルタイプを展開して詳細を表示できます。  
この例では、`AddToCart`ピクセルイベントが表示されます：  
表示されるデータはFacebookに送信されるデータです。  
    ![](https://docs.tealium.com/images/iq-tag-management/image-2017-12-28-11-21-53.png)

## Adobe Analytics Debuggerで検証する

Adobe Analyticsデバッガーには、表示されるパラメータがいくつかあります。Adobe Analytics（AppMeasurement）タグのパラメータについては、[Adobe Query Parameters](https://marketing.adobe.com/resources/help/en_US/sc/implement/query_parameters.html)を参照してください。

Adobe Analytics Debuggerを使用して検証する手順は以下の通りです：

1. プラグインをダウンロードした後、Tealiumのタグがインストールされているサイトを開き、Chromeウィンドウの右上隅にあるプラグインアイコンをクリックします。
[Chrome Developer Tools Console](https://developers.google.com/web/tools/chrome-devtools/console/)にライブ出力が表示されます。  
    ![](https://docs.tealium.com/images/iq-tag-management/drapey-tie-neck-top-gap-2017-12-28-11-28-20.png)

1. イベントやページビューをトリガーすると、コンソールにAdobe Analyticsの出力が表示されます。  
このコンソール出力は、各サーバーコールでAdobeに送信されるすべてのデータを表しています。  
    ![](https://docs.tealium.com/images/iq-tag-management/drapey-tie-neck-top-gap-2017-12-28-11-29-46.png)

## Chrome Developer Toolsで検証する

すべてのベンダーが独自のプラグインを持っているわけではありません。その場合は、Chrome Developer Toolsの**Network**タブを使用して、ブラウザからタグによって正常に送信されているかどうかを検証することをおすすめします。

詳細については、[Chrome DevTools Network Analysis](https://developers.google.com/web/tools/chrome-devtools/network-performance/reference)を参照し、ドキュメント内で**View query string parameters**を検索して利用可能なパラメータについて詳しく学びます。

Chrome Developer Toolsを使用して検証する手順は以下の通りです：

1. Tealiumがインストールされているサイトを開きます。
1. Developer Toolsを表示するには、ページを右クリックして**検証**を選択します。  
    ![](https://docs.tealium.com/images/iq-tag-management/chrome-inspect.png)

1. **Network**タブをクリックします。  
この例ではGoogle Analyticsを使用していますが、他のタグでも使用できます。  
    ![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-12-38.png)

1. Tealium iQで、タグの構成部分で**トラッキングID**を見つけてID番号をコピーします。  
    ![](https://docs.tealium.com/images/iq-tag-management/tiq---services-christina-2017-12-28-13-13-14.png)

1. Networkタブがまだ開いている状態で、サイトに戻り、**フィルター**ボックスにID番号を貼り付けます。  
    ![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-13-56.png)

1. **ログを保持する**チェックボックスをクリックし、ページビューやイベントを実行します。  
タグによって送信されるネットワークリクエストが表示されます。  
    ![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-15-15.png)

1. エントリをクリックしてリクエストの詳細を表示します。  
ここには、`Request URL`、`Response Headers`、`Cookies`、`Query Parameters`などの情報がいくつか表示されます。  

<blockquote>
私たちは特に`Request URL`と`Query Parameters`に興味がありますが、他の情報についてはこちらで詳細を確認できます：**Chrome Network Tab**
</blockquote>

![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-15-55.png)
**Request URL**は、ベンダーのサーバーにPOSTまたはGETとして送信されたURL全体です。このURLには、サーバーURLとベンダーが受け取るクエリ文字列パラメータ（データ）が含まれています。  
![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-18-25.png)
**Query String Parameters**は、ベンダーが受け取るパラメータのリスト（サーバーURLは含まれません）です。これはおそらく、ページからベンダーにデータが渡される方法です。  
![](https://docs.tealium.com/images/iq-tag-management/section-page-2017-12-28-13-20-01.png)
以下の例は、Adobe AppMeasurementサーバーコールのQuery String Parametersを示しています：   
![](https://docs.tealium.com/images/iq-tag-management/drapey-tie-neck-top-gap-2017-12-28-13-22-40.png)

## トラブルシューティング

クエリパラメータやプラグインのいずれかに欠落がある場合、自分でトラブルシューティングを試みることがあります。以下の方法を試してみることができます：

* まず、Web CompanionまたはUniversal Tag Monitorを使用して、ページとイベントのトラッキングコールで使用されるデータレイヤー変数を確認します。[詳細を学ぶ](https://docs.tealium.com/ja/platforms/javascript/install/#validate-installation)。
* データレイヤーが不完全な場合、必要な変数を含めるために追加の開発作業が必要になる場合があります。
* データレイヤーが正常で、トラッキングコールも期待どおりに機能しているが、ベンダータグが期待するデータを受け取っていない場合は、次のステップとしてタグのデータマッピングを確認します。データマッピングは、Tealiumに対応するベンダーパラメータに送信するデータレイヤー変数を指示します。[詳細を学ぶ](https://docs.tealium.com/about-data-mappings/)。

