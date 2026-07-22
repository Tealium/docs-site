---
title: ハイブリッドアプリでのアナリティクスセッションの同期方法
description: このドキュメントでは、ハイブリッドアプリでセッションを同期する方法について説明します。
url: https://docs.tealium.com/ja/platforms/remote-commands/sync-analytics-hybrid-apps/
---
## 概要

ハイブリッドアプリは、ネイティブコード（iOSの場合はObjective-C、Androidの場合はJavaなど）で書かれたコンポーネントと、HTMLとJavaScriptで書かれた1つ以上のWebビューコンポーネントを組み合わせたものです。一般的な使用例は、ネイティブコードのコンポーネントで商品の閲覧を行い、Webビューコンポーネントでチェックアウトや支払い処理を行うショッピングアプリです。

### 問題

ハイブリッドアプリのアナリティクスベンダーにとって、ネイティブコンポーネントとWebビューコンポーネントの間でセッションを追跡することは一般的な課題です。ベンダーが両方のコンポーネントに統合されていても、訪問者はそれぞれに別々のセッション識別子が割り当てられ、ベンダーのレポートではセッション数が過大評価されます。

この問題を解決するには、ネイティブコードとWebビューコンポーネントで情報を共有する必要があります。これらのコンポーネント間で情報を共有するためには、ネイティブコードによってロードされるWebビューのURLにクエリ文字列パラメータを追加する必要があります。このパラメータには、ネイティブコードとWebビューコンポーネントの両方で使用される共有セッションIDが含まれます。

このセッションIDの開始と共有は、Tealium iQの設定とネイティブアプリのカスタムコードを使用して行われます。カスタムリモートコマンドタグは、非表示のWebビューとネイティブコードの間でセッションIDを共有するために使用され、それが可視なWebビューからロードされるウェブサイトに渡されます。

### 解決策

この記事では、Google Analyticsを使用した解決策を示しますが、セッション管理をサポートする他のベンダーにも適用できます。Google Analyticsの解決策では、Tealium iQ SDKでセッションID（`clientId`）を取得し（非表示のWebビューで生成され、リモートコマンドを介してネイティブコードに渡される）、クエリ文字列パラメータを介してハイブリッドアプリのWebビューコンポーネントにセッションIDを渡し、Tealium iQを使用してセッションIDをWebビュー内のウェブサイトで実行されるGoogle Analyticsに戻します。この例では、主にAndroidに焦点を当てますが、iOSのプロセスも同じです。

この解決策の要件は次のとおりです。

1. ネイティブコード
    *  **カスタムリモートコマンド**  
    ネイティブコードで定義されたカスタムコマンドで、カスタムリモートコマンドタグによって呼び出されることができます。これにより、非表示のWebビューがセッションIDをネイティブコードに渡すことができます。
    *  **Webビューのクエリ文字列パラメータ**  
    ハイブリッドアプリのWebビューコンポーネントをロードするURLに、セッションIDが含まれるクエリ文字列パラメータを追加します。
1. モバイルアプリ用のiQプロファイル  
ネイティブアプリを管理するプロファイルには、次の設定が必要です。
    *   **カスタムリモートコマンドタグ** - 非表示のWebビューとネイティブアプリコードの間の通信を容易にするタグ。
    *   `session_id` - カスタムリモートコマンドタグからネイティブコードに渡されるベンダーセッションIDを格納するUDO変数。
    *   **JavaScriptコード拡張** - ベンダーから現在のセッションIDを取得し、それをカスタムリモートコマンドタグに渡すためのJavaScriptコード。
1. モバイルWeb用のiQプロファイル  
ハイブリッドアプリのWebビューコンポーネントには、次のカスタマイズが必要です。
    *   **`session_id`** - WebビューのURLで使用されるクエリ文字列変数で、ネイティブコードからセッションIDを渡します。
    *   **カスタムJavaScript** - セッションIDをベンダータグに渡すためのJavaScriptコード（拡張またはタグテンプレート）。


<blockquote>
この記事では、Android/iOS v5.0以降のTealiumを使用していることを前提としており、アプリを再デプロイする必要があります。
</blockquote>


以下は、ハイブリッドアプリの各コンポーネントに対する解決策の概要です。

<table style="border: 1px solid rgb(237, 237, 237) !important"><thead><tr><td colspan="4" style="text-align: center;"><strong>ハイブリッドアプリ</strong></td></tr></thead><tbody><tr ><th style="border: 1px solid rgb(237, 237, 237) !important;vertical-align: top; text-align: center;text-transform:uppercase;" class="bg-secondary" colspan="2">ネイティブコード<br>コンポーネント</th><td rowspan="3" style="vertical-align: top; text-align: center;border: 1px solid rgb(237, 237, 237) !important">ネイティブコードは、次のURLでWebビューをロードします：<br><code>&session_id=SESSION</code><p>&nbsp;</p></td><th style="vertical-align: top; text-align: center;text-transform:uppercase;" class="bg-secondary">Webビュー<br>コンポーネント</th></tr><tr><td style="vertical-align: top; text-align: center;">iQモバイルプロファイル<br>（非表示のWebビューで実行）</td><td style="border: 1px solid rgb(237, 237, 237) !important;vertical-align: top; text-align: center;">ネイティブコード</td><td style="vertical-align: top; text-align: center;">ウェブサイト用iQプロファイル</td></tr><tr><td style="vertical-align: top;"><p>カスタムリモートコマンド<code>syncSessionId</code>コマンドの設定</p><p>ベンダーからセッションIDを取得するJavaScriptコード拡張</p><p>セッションIDを渡すための<code>utag.link()</code>の呼び出し</p></td><td style="vertical-align: top;border: 1px solid rgb(237, 237, 237) !important"><p>syncSessionIdを同期するためのリモートコマンドのカスタムコード</p><p>セッションID変数をWebビューに渡すためのカスタムコード</p></td><td style="vertical-align: top;"><p>WebビューURLのクエリ文字列変数<code>session_id</code></p><p><code>session_id</code>のデータマッピングを持つベンダータグ</p></td></tr></tbody></table>


## 実装

### リモートコマンドの追加（ネイティブコード）

`addRemoteCommand`メソッドを使用して、カスタムリモートコマンドタグが利用するための新しいコマンドを定義します。これにより、非表示のTealium Webビューがネイティブコード環境のTealiumライブラリにデータを渡すことができます。

#### Android（Javaコード）：


<blockquote>
このコードは完全に機能しますが、このタスクを達成するためのサンプルコードです。ご自身の判断で使用し、ライブアプリにデプロイする前に必ずテストしてください。
</blockquote>


1. `syncSessionId`という新しいリモートコマンドを定義し、渡されたセッションIDの値を`sessionId`というネイティブ変数に格納します。このコードをTealiumの`init`ブロックに配置します（これは通常、ヘルパーファイルになります）：  
    ```java
    // Tealiumの初期化
    Tealium.Config config = Tealium.Config.create(application, "", "", "");
    // 上記のconfigオブジェクトを使用して新しいTealiumインスタンスを作成します
    Tealium inst = Tealium.createInstance(TEALIUM\_INSTANCENAME, config);
    // "syncSessionId"という名前の新しいRemoteCommandをTealiumに登録します
    inst.addRemoteCommand(new RemoteCommand("syncSessionId", "セッションIDを同期します") {
        // onInvokeは、Tealium iQがコマンドをトリガーしたときに呼び出されます
        @Override
        protected void onInvoke(Response response) throws Exception {
            // レスポンスオブジェクトを取得します
            JSONObject resp = response.getRequestPayload();
            // レスポンス内のキー"sessionId"の値をアプリケーションレベルの"gaSessionId"文字列変数に設定します
            // これは、Applicationクラスでこの共有変数を作成したことを前提としています。詳細については、サンプルアプリを参照してください。
            DemoApplication.sessionId = resp.optString("sessionId", null);
        }
    });
    ```
1. Webビューをカスタマイズして、ネイティブコードに格納されたセッション値をクエリ文字列パラメータ`session_id`として追加します。以下は、Webビューが作成され、セッションIDがクエリ文字列パラメータとして渡される例です：  
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

#### iOS（Objective-Cコード）

以下は、同じことをiOSで実現するために必要なObjective-Cコードの一部です。このコードにはWebビューの作成は含まれておらず、出発点として含まれています。

```objc
// インスタンス名を置き換えてください
Tealium *instanceHandle = [Tealium instanceForKey: @"tealium"]; 
[instanceHandle addRemoteCommandID:@"syncSessionId"
   description:@"セッションIDを同期します"
   targetQueue:dispatch_get_main_queue()
 // レスポンスは、Tealium iQで設定したマッピングから生成されます
   responseBlock:^(TEALRemoteCommandResponse * _Nonnull response) {
 // レスポンスオブジェクトからセッションIDを取得します
       NSString *session_id = response.requestPayload[@"sessionId"];
 /* セッションIDを取得したので、後でWebビューを作成するときにアクセスできる場所に保存します。詳細については、Androidコードを参照してください */
}\];
```

### カスタムリモートコマンドタグの追加（モバイルWeb用のiQプロファイル）

iQモバイルプロファイルでは、カスタムリモートコマンドタグを使用して、ネイティブコードで定義したリモートコマンドをトリガーします。このタグにデータマッピングを追加すると、リモートコマンドがそのデータを受け取ります。

モバイルWeb用のiQプロファイルで以下の手順に従ってください。

1. データレイヤーに次のUDO変数を追加します：`session_id`
2. **カスタムリモートコマンド**タグを追加します：  
![](https://docs.tealium.com/images/platforms/remote-commands/sync-analytics1.jpg)
3. **コマンドID**を`syncSessionId`（ネイティブコードで定義したリモートコマンドの名前）に設定します：  
![](https://docs.tealium.com/images/platforms/remote-commands/sync-analytics2.jpg)
4. `session_id`を`sessionId`にマッピングするデータマッピングを追加します。  
![](https://docs.tealium.com/images/platforms/remote-commands/sync-analytics3.jpg)

### ベンダータグの追加（モバイルアプリ用のiQプロファイル）

モバイルアプリのiQプロファイルでは、ベンダータグ（この例ではGoogle Analytics）を使用してセッションを開始し、`utag.link()`を呼び出してカスタムリモートコマンドタグにセッションIDの値を渡します。おそらく、ネイティブアプリのトラッキングの目的で既にこのタグをモバイルプロファイルに追加しているでしょう（多くの人気のあるアナリティクスタグはモバイル対応しています）。

ベンダータグを追加して設定する手順は次のとおりです。

1. ベンダータグを追加します（まだ追加していない場合）。
2. ベンダータグ（Google Analyticsの場合）にスコープが設定されたJavaScriptコード拡張を追加します。以下はその内容です。`UID`をカスタムリモートコマンドタグのUIDに置き換えてください。  
    ```js
    window.setTimeout(function() {
         // ベンダー固有: Google AnalyticsからセッションIDを取得します
         var tracker = window.ga.getByName('tealium_0'); // ページ上にGAトラッカーが1つしかない場合を想定しています
         var clientId = tracker.get('clientId');
         // カスタムリモートコマンドがトリガーされたトラッキングコール
         utag.link({session_id : clientId}, null, ['UID'])
    }, 1000);
    ```
    
この拡張は、タグがロードされるのに十分な時間を与えるために1秒待機し、ベンダーからセッションIDを取得します。その後、`utag.link()`を呼び出してカスタムリモートコマンドタグをトリガーし、パラメータとして`session_id`を渡します。その後、カスタムリモートコマンドタグはそのデータをリモートコマンド`syncSessionId`に渡し、ネイティブコードでそれを後で使用するために保存します。

### ベンダータグの追加（モバイルWeb用のiQプロファイル）

ハイブリッドアプリのWebビューコンポーネントでロードされるウェブサイト用のiQ Webプロファイル（Webプロファイル）では、セッションIDに使用されるクエリ文字列パラメータを検出し、その変数をベンダータグにマッピングします。

セッションIDを同期するためにベンダータグを構成する手順は次のとおりです。

1. ベンダータグを追加します（まだ追加していない場合）。
2. クエリ文字列パラメータのタイプである`session_id`という名前の新しいデータレイヤー変数を追加します。
3. ベンダータグに、`session_id`を`clientId`にマッピングするデータマッピングを追加します（Google Analyticsの場合）。

以上で完了です。上記の手順に従った場合、アプリのWebビューはネイティブアプリと同じセッション識別子を受け取り、ユーザーはGoogle Analyticsの観点からは単一のセッションを使用することになります。

### 結果の検証

上記のコードをデプロイした後、Charles ProxyやFiddlerなどのローカルプロキシを使用して、アプリの出力を表示できます。`www.google-analytics.com`への送信ヒットを検査すると、ネイティブアプリからのヒットとWebビューコンポーネントからのヒットで`cid`パラメータが同じであることを確認できます。

詳細については、[モバイルインストールのトラブルシューティング](https://docs.tealium.com/ja/platforms/getting-started-mobile/troubleshooting/)を参照してください。

ネイティブアプリからの共有セッションID：

![](https://docs.tealium.com/images/platforms/remote-commands/sync-analytics4.png)

インアプリのWebビューからの共有セッションID：

![](https://docs.tealium.com/images/platforms/remote-commands/sync-analytics5.png)

Android Studioプロジェクトとしてサンプルアプリをダウンロード：[GAwebviewDemo.zip](https://docs.tealium.com/images/platforms/remote-commands/GAWebViewDemo.zip)。

## その他の解決策

このガイドでは、Google AnalyticsのセッションIDを同期する方法について説明しましたが、同じ手順をWebtrends、Webtrekk、Adobe Analyticsなどの他のベンダーにも簡単に適用できます。ベンダーによっては、セッションIDを提供するAPIがない場合、クッキーの値を読み取る必要があるかもしれません。

この記事で文書化された解決策は、アナリティクスツールの範囲外でアプリに他の情報を渡すためにも使用できます。カスタムリモートコマンドタグにさらにマッピングを追加することで、1回の呼び出しで複数のパラメータを渡すことも可能ですが、レスポンスオブジェクト内の追加のパラメータを処理するためにネイティブリモートコマンドコードを適応する必要があります。

