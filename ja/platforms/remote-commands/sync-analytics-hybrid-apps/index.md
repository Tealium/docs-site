---
title: ハイブリッドアプリでアナリティクスセッションを同期する方法
description: このドキュメントでは、ハイブリッドアプリでセッションを同期する方法について説明します。
url: https://docs.tealium.com/ja/platforms/remote-commands/sync-analytics-hybrid-apps/
---
## 概要

ハイブリッドアプリは、iOS向けのObjective-CやAndroid向けのJavaなどのネイティブコードで記述されたコンポーネントと、HTMLおよびJavaScriptで記述された1つ以上のWebViewコンポーネントを組み合わせたものです。一般的なユースケースとして、商品の閲覧にはネイティブコードのコンポーネントを使用し、チェックアウトと決済処理にはWebViewコンポーネントを使用するショッピングアプリがあります。

### 問題

ハイブリッドアプリにおいてアナリティクスベンダーが直面する一般的な課題は、ネイティブコンポーネントとWebViewコンポーネントの間でセッションを追跡できるようにすることです。ベンダーが両方のコンポーネントに統合されている場合でも、訪問にはそれぞれで異なるセッション識別子が割り当てられるため、ベンダーのレポートではセッション数が実際より多く表示されます。

この問題を解決するには、ネイティブコンポーネントとWebViewコンポーネントの間で情報を共有する必要があります。これらのコンポーネント間で情報を共有するには、ネイティブコードによって読み込まれるWebViewのURLにクエリ文字列パラメータを追加します。このパラメータには、ネイティブコンポーネントとWebViewコンポーネントの両方で使用される共有セッションIDが含まれます。

このセッションIDの生成と共有は、タグ管理での構成と、ネイティブアプリ内のカスタムコードによって実現します。カスタムリモートコマンドタグにより、非表示のWebViewとネイティブコードの間でセッションIDを共有できます。その後、そのIDは、表示されているWebViewから読み込まれるWebサイトに渡されます。

### 解決策

この記事ではGoogle Analyticsを使用してこの解決策を説明しますが、セッション管理をサポートするすべてのベンダーに適用できます。Google Analytics向けの解決策では、タグ管理SDKでセッションID（`clientId`）を取得し（非表示のWebViewで生成し、リモートコマンドを介してネイティブコードに渡します）、クエリ文字列パラメータを介してハイブリッドアプリのWebViewコンポーネントに渡します。次に、タグ管理を使用して、WebView内のWebサイトで実行されているGoogle AnalyticsにセッションIDを渡します。この例では主にAndroidを取り上げますが、iOSでも手順は同じです。

この解決策には、次の要件があります。

1. ネイティブコード
    *  **カスタムリモートコマンド**  
    カスタムリモートコマンドタグから呼び出される、ネイティブコード内で定義されたカスタムコマンドです。これにより、非表示のWebViewからネイティブコードにセッションIDを渡すことができます。
    *  **WebViewのクエリ文字列パラメータ**  
    セッションIDを含むクエリ文字列パラメータを、ハイブリッドアプリのWebViewコンポーネントを読み込むURLに追加します。
1. モバイルアプリ用のiQプロファイル  
ネイティブアプリを管理するプロファイルには、次の構成が必要です。
    *   **カスタムリモートコマンドタグ** - 非表示のWebViewとネイティブアプリのコード間の通信を可能にするタグです。
    *   `session_id` - カスタムリモートコマンドタグからネイティブコードに渡されるベンダーのセッションIDを保存するためのUDO変数です。
    *   **JavaScriptコード拡張機能** - ベンダーから現在のセッションIDを取得し、カスタムリモートコマンドタグに渡すためのJavaScriptコードです。
1. モバイルWeb用のiQプロファイル  
ハイブリッドアプリのWebViewコンポーネント用iQプロファイルには、次のカスタマイズが必要です。
    *   **`session_id`** - ネイティブコードからセッションIDを渡すために、WebViewのURLで使用されるクエリ文字列変数です。
    *   **カスタムJavaScript** - セッションIDをベンダータグに渡すためのJavaScriptコード（拡張機能またはタグテンプレート）です。


<blockquote>
この記事では、Tealium for Android/iOS v5.0以降を使用していることを前提としており、アプリの再デプロイが必要です。
</blockquote>


ハイブリッドアプリの各コンポーネントにおける解決策の概要は、次のとおりです。

<table style="border: 1px solid rgb(237, 237, 237) !important"><thead><tr><td colspan="4" style="text-align: center;"><strong>ハイブリッドアプリ</strong></td></tr></thead><tbody><tr ><th style="border: 1px solid rgb(237, 237, 237) !important;vertical-align: top; text-align: center;text-transform:uppercase;" class="bg-secondary" colspan="2">ネイティブコード<br>コンポーネント</th><td rowspan="3" style="vertical-align: top; text-align: center;border: 1px solid rgb(237, 237, 237) !important">ネイティブコードは、次のパラメータを含むURLでWebViewを読み込みます。<br><code>&session_id=SESSION</code><p>&nbsp;</p></td><th style="vertical-align: top; text-align: center;text-transform:uppercase;" class="bg-secondary">WebView<br>コンポーネント</th></tr><tr><td style="vertical-align: top; text-align: center;">iQモバイルプロファイル<br>（非表示のWebViewで実行）</td><td style="border: 1px solid rgb(237, 237, 237) !important;vertical-align: top; text-align: center;">ネイティブコード</td><td style="vertical-align: top; text-align: center;">Webサイト用のiQプロファイル</td></tr><tr><td style="vertical-align: top;"><p>カスタムリモートコマンド<code>syncSessionId</code>を構成</p><p>ベンダーからセッションIDを取得するJavaScriptコード拡張機能</p><p>セッションIDを渡してカスタムリモートコマンドをトリガーする<code>utag.link()</code>の呼び出し</p></td><td style="vertical-align: top;border: 1px solid rgb(237, 237, 237) !important"><p>syncSessionIdへのリモート呼び出しを処理するカスタムコード</p><p>セッションID変数をWebViewに渡すカスタムコード</p></td><td style="vertical-align: top;"><p>WebViewのURLから取得するクエリ文字列変数<code>session_id</code></p><p><code>session_id</code>用のデータマッピングを含むベンダータグ</p></td></tr></tbody></table>


## 実装

### リモートコマンドを追加する（ネイティブコード）

カスタムリモートコマンドタグで使用する新しいコマンドを定義するには、`addRemoteCommand`メソッドを使用します。これにより、非表示のTealium WebViewからネイティブコード環境のTealiumライブラリにデータを渡すことができます。

#### Android（Javaコード）：


<blockquote>
このコードは完全に機能しますが、このタスクを実行する方法を示すための単なるサンプルです。ご自身で適切に判断し、実稼働アプリにコードをデプロイする前には必ずテストしてください。
</blockquote>


1. 渡されたセッションIDの値を`sessionId`というネイティブ変数に保存する、`syncSessionId`という新しいリモートコマンドを定義します。このコードをTealiumの`init`ブロック内（通常はヘルパーファイル内）に配置します。  
    ```java
    // initialize Tealium
    Tealium.Config config = Tealium.Config.create(application, "", "", "");
    // create a new Tealium instance with the above config object
    Tealium inst = Tealium.createInstance(TEALIUM\_INSTANCENAME, config);
    // register a new RemoteCommand with Tealium called "syncGASession"
    inst.addRemoteCommand(new RemoteCommand("syncSessionId", "Syncs the Analytics Session ID") {
        // onInvoke will be called when Tag Management triggers the command
        @Override
        protected void onInvoke(Response response) throws Exception {
            // grab the response object
            JSONObject resp = response.getRequestPayload();
            // set the application-level "gaSessionId" String variable to the value of the key "sessionId" in the response
            // assumes you created this shared variable in your Application class. See sample app for details.
            DemoApplication.sessionId = resp.optString("sessionId", null);
        }
    });
    ```
1. ネイティブコードに保存されているセッション値を使用して、クエリ文字列パラメータ`session_id`を追加するようにWebViewをカスタマイズします。次の例では、WebViewを作成し、セッションIDをクエリ文字列パラメータとして渡しています。  
    ```java
    public class WebviewActivity extends AppCompatActivity {
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_webview);
            webview mywebview = (webview) findViewById(R.id.webview);
            mywebview.clearCache(true);
            mywebview.getSettings().setJavaScriptEnabled(true);
            mywebview.loadUrl("https://solutions.tealium.net/hosted/cpr/mobile_ga_demo.html?session_id=" + DemoApplication.sessionId);
        }
    }
    ```
#### iOS（Objective-C コード）

iOS で同じことを実現するために必要な、同等の Objective-C コードの一部を以下に示します。このコードには WebView の作成処理は含まれておらず、実装の開始点として提供されています。

```objc
// replace with your instance name
Tealium *instanceHandle = [Tealium instanceForKey: @"tealium"]; 
[instanceHandle addRemoteCommandID:@"syncSessionId"
   description:@"Syncs the Session ID"
   targetQueue:dispatch_get_main_queue()
 // response is generated from the mappings set up in Tag Management
   responseBlock:^(TEALRemoteCommandResponse * _Nonnull response) {
 // grab the Session ID from the response object
       NSString *session_id = response.requestPayload[@"sessionId"];
 /* now that you have the session ID, store it somewhere you can 
 access it later on when you create your webview. See Android code
 for an example */
}\];
```

### カスタムリモートコマンドタグを追加する（モバイル Web 用の iQ プロファイル）

モバイル用の iQ プロファイルで、カスタムリモートコマンドタグを使用して、ネイティブコードで定義したリモートコマンドをトリガーします。このタグにデータマッピングを追加すると、リモートコマンドがそのデータを受信します。

モバイル Web 用の iQ プロファイルで、次の手順を実行します。

1. データレイヤーに次の UDO 変数を追加します：`session_id`
2. **Custom Remote Command**タグを追加します：  
![](https://docs.tealium.com/images/platforms/remote-commands/sync-analytics1.jpg)
3. **Command ID**を`syncSessionId`（ネイティブコードで定義したリモートコマンドの名前）に構成します：  
![](https://docs.tealium.com/images/platforms/remote-commands/sync-analytics2.jpg)
4. `session_id`から`sessionId`へのデータマッピングを追加します。  
![](https://docs.tealium.com/images/platforms/remote-commands/sync-analytics3.jpg)

### ベンダータグを追加する（モバイルアプリ用の iQ プロファイル）

モバイルアプリ用の iQ プロファイルでは、ベンダータグ（この例では Google Analytics）を使用してセッションを開始し、`utag.link()`の呼び出しによってセッション ID の値をカスタムリモートコマンドタグに渡します。一般的な分析タグの多くはモバイルに対応しているため、ネイティブアプリのトラッキング用として、このタグはすでにモバイルプロファイルに追加されている可能性があります。

ベンダータグを追加して構成するには、次の手順を実行します。

1. ベンダータグをまだ追加していない場合は、追加します。
2. 次の内容を含む JavaScript Code 拡張機能を追加し、適用範囲をベンダータグ（Google Analytics）に構成します。`UID`をカスタムリモートコマンドタグの UID に置き換えます。  
    ```js
    window.setTimeout(function() {
         // Vendor Specific: Retrieve a session ID from Google Analytics
         var tracker = window.ga.getByName('tealium_0'); // assumes you only have one GA tracker on the page
         var clientId = tracker.get('clientId');
         // A tracking call picked up custom remote command
         utag.link({session_id : clientId}, null, ['UID'])
    }, 1000);
    ```
    
この拡張機能は、タグが読み込まれるのに十分な時間を確保するために 1 秒間待機してから、ベンダーからセッション ID を取得します。次に、`session_id`をパラメータとして渡して`utag.link()`を呼び出し、カスタムリモートコマンドタグをトリガーします。その後、カスタムリモートコマンドタグがそのデータをリモートコマンド`syncSessionId`に渡し、ネイティブコードが後で使用できるように保存します。

### ベンダータグを追加する（モバイル Web 用の iQ プロファイル）

iQ Web プロファイル（ハイブリッドアプリの WebView コンポーネントに読み込まれる Web サイトで使用するプロファイル）で、セッション ID に使用されるクエリ文字列パラメータを検出するための新しいデータレイヤー変数を定義し、その変数をベンダータグにマッピングします。

セッション ID を同期するようにベンダータグを構成するには、次の手順を実行します。

1. ベンダータグをまだ追加していない場合は、追加します。
2. クエリ文字列パラメータ型の`session_id`という名前の新しいデータレイヤー変数を追加します。
3. ベンダータグで、`session_id`から`clientId`（この例では Google Analytics 固有）へのデータマッピングを追加します。

これで完了です。上記のすべての手順を実行していれば、アプリ内の WebView はネイティブアプリと同じセッション識別子を受信し、ユーザーは単一のセッションを使用するようになります（Google Analytics の観点において）。

### 結果を検証する

上記のコードをデプロイした後、Charles Proxy や Fiddler などのローカルプロキシを使用して、アプリからの出力を確認できます。`www.google-analytics.com`への送信ヒットを調べることで、ネイティブアプリから送信されたヒットと WebView コンポーネントから送信されたヒットで、`cid`パラメータが同じであることを確認できます。

詳細については、[モバイルインストールのトラブルシューティング](https://docs.tealium.com/ja/platforms/getting-started-mobile/troubleshooting/)を参照してください。

ネイティブアプリから共有されたセッション ID：

![](https://docs.tealium.com/images/platforms/remote-commands/sync-analytics4.png)

アプリ内 WebView から共有されたセッション ID：

![](https://docs.tealium.com/images/platforms/remote-commands/sync-analytics5.png)

サンプルアプリを Android Studio プロジェクトとしてダウンロードしてください：[GAwebviewDemo.zip](https://docs.tealium.com/images/platforms/remote-commands/GAWebViewDemo.zip)。

## その他のソリューション

このガイドでは、Google Analytics のセッション ID を同期する方法について説明していますが、同じ手順を Webtrends、Webtrekk、Adobe Analytics などの他のベンダーにも簡単に応用できます。ベンダーによっては、セッション ID を提供する API がない場合に Cookie の値を読み取る必要があります。

この記事で説明したソリューションは、分析ツールの範囲外にあるその他の情報をアプリに渡すためにも使用できます。カスタムリモートコマンドタグにマッピングを追加することで、一度に複数のパラメータを渡すことも可能ですが、レスポンスオブジェクト内の追加パラメータを処理できるように、ネイティブのリモートコマンドコードを変更する必要があります。