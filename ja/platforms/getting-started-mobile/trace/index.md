---
title: トレース
description: デバッグにトレースを使用する方法について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/
---
[トレース](https://docs.tealium.com/manage-traces/)は、イベントストリーミングおよび顧客データプラットフォーム（CDP）の構成をテスト、検査するためのツールです。トレースを使用すると、訪問のワークフローをキャプチャし、イベントと顧客データがリアルタイムで処理される様子を確認できます。

## モバイルトレースツール

### サポートされるプラットフォーム

モバイルトレースツールでは、次のプラットフォームがサポートされています。

* [Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/)
* [iOS（Swift v2.x）](https://docs.tealium.com/ja/platforms/ios-swift/)



<blockquote>
一括イベントにトレースを追加しないでください。<br>本番データを監視するための永続的なパラメータとしてトレースを追加しないでください。
</blockquote>


### 仕組み

モバイルトレースツールでは、デバイスでスキャン可能なQRコードを提供することでトレース機能をエンリッチメントし、Tealium Mobile SDKから送信されるイベントをすばやく確認できるようにします。

ツールで**トレースを開始**をクリックすると、Tealiumプラットフォームのセッションごとに1回、新しいトレースを開始するたびにQRコードがメインブラウザーウィンドウへ自動的に挿入されます。

QRコードは、プラットフォーム（[Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/)）ごとに生成されます。モバイルデバイスのカメラで該当するQRコードをスキャンした後、QRコードのリンクをクリックしてアプリを起動し、トレースパラメータをTealium SDKに渡します。Tealium SDKはトレースIDを（その他のパラメータとともに）受信し、現在のセッションのデータレイヤーに挿入します。

その後のすべてのイベントは、セッションを終了するかトレースから退出するまで、トレースセッションに記録されます。

次の図は、この仕組みを示しています。

![](https://docs.tealium.com/images/platforms/getting-started-mobile/trace-tool-overview.png)

### インストール

このツールを使用するには、次の手順を実行します。

1. 使用するブラウザーに[Tealium Toolsブラウザー拡張機能](https://docs.tealium.com/tealium-tools-browser-extension/)をインストールします。
1. インストールが完了したら、Tealium Tools拡張機能を開きます。
1. **ツールカタログ**タブをクリックします。
1. **モバイルトレースツール**をクリックします。

![](https://docs.tealium.com/images/platforms/getting-started-mobile/mobile-trace-tool.png)

### URLスキーム

モバイルトレースツールを使用するには、モバイルアプリで処理されるURLを確認し、URLスキームを構成します。

QRコードによるトレース機能は、URLからアプリを起動し、特定のクエリパラメータをリッスンします。URLからアプリを直接起動するには、特定のドメインを処理するようにアプリが登録されている必要があります。

通常、ほとんどのアプリはすでに特定のURLを処理するように構成されています。たとえば、Webサイトのドメインが[https://mycompany.com](https://mycompany.com)の場合、アプリはこのドメインのハンドラーとして登録されます。アプリがユーザーのデバイスにインストールされている場合、ブラウザー内ではなくアプリでリンクを開くようユーザーに求めるメッセージが表示されます。


<blockquote>
一部のアプリでは、`http`や`https`の代わりに`mycompanyapp://`などのカスタムURLスキームが登録されています。これらもモバイルトレースツールで使用できます。
</blockquote>


アプリを起動するURLスキームを確認したら、モバイルトレースツールの入力フィールドに入力します。必要に応じてAndroidとiOSで異なるスキームを使用できますが、通常は両方のプラットフォームで同じスキームを使用します。

![](https://docs.tealium.com/images/platforms/getting-started-mobile/trace-tool.png)

各URLスキームの横にある**保存**をクリックし、ブラウザーの`localStorage`に構成を保存します。必要に応じて青い鉛筆アイコンをクリックし、URLスキームを編集します。

### トレースの開始

トレースを開始する前に、Tealiumのサーバーサイドプラットフォームを使用していることを確認してください。モバイルトレースツールで**トレースを開始**をクリックして新しいトレースを開始し、モバイルトレース用QRコードをトレースウィンドウに追加します。

![](https://docs.tealium.com/images/platforms/getting-started-mobile/trace-tool-start.png)

トレースを開始した後、以降のセッションでは必要ないため、Tealium ToolsのUIを閉じます。

以降のトレースはTealiumから直接開始します。新しいトレースを開始するたびに、QRコードが自動的に更新されます。デバイスのカメラでQRコードをスキャンし、リンクをクリックしてアプリを起動すると、トレースが自動的に開始されます。トレースへの参加後にアプリで生成されたTealiumイベントは、すべてトレースセッションに記録されます。

![](https://docs.tealium.com/images/platforms/getting-started-mobile/trace-qr-code.png)

### トレースからの退出

トレースセッションを終了せずに退出した場合、そのトレースセッションの履歴を失うことなく、別のデバイスから同じトレースに再参加できます。

トレースから退出するには、次の手順を実行します。

1. トレースUIで**トレースから退出**チェックボックスを選択します。
1. デバイスのカメラでもう一度QRコードをスキャンします。
1. リンクをクリックし、デバイスをトレースセッションから退出させます。

### 訪問の終了（顧客データプラットフォーム（CDP））

CDPで「訪問の終了」アクションをテストするには、訪問のセッションを即座に終了するシグナルが必要です。そうしない場合、セッションが通常どおり期限切れになるまで待つ必要があります。

モバイルトレースツールで**訪問セッションを終了**チェックボックスを選択すると、SDKに`kill_visitor_session`イベントを送信させるパラメータがQRコードに追加され、セッションが即座に終了します。

![](https://docs.tealium.com/images/platforms/getting-started-mobile/trace-end-visit.png)

## Charles Proxy

Charles Web Debugging Proxyを使用して、Mobile SDKおよびTealium Collectタグを使用するアプリケーションからトレースを開始します。

### 要件

* [Charles Proxy](https://www.charlesproxy.com)
* [Tealiumサーバーサイドアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

### セットアップ

コンピューター上のCharlesを経由してトラフィックをプロキシするようモバイルデバイスを構成するには、[Android](https://docs.tealium.com/ja/platforms/android-kotlin/charles-proxy-android)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/charles-proxy-iosdevice)デバイス向けの手順に従ってください。

### リライトの使用

Charlesをプロキシとして使用してアプリケーションを実行し、ネットワークトラフィックを`teal`でフィルタリングします。リクエストを右クリックし、**URLをコピー**を選択します。

Charlesのメニューから**ツール > リライト**を選択し、**リライト構成**ダイアログを開きます。

ロケーションを追加するには、次の手順を実行します。

1. **リライトを有効化**チェックボックスを選択し、**ロケーション**リストの下にある**追加**をクリックします。
1. **名前**フィールドに`Add Trace ID`と入力し、**追加**をクリックしてロケーションを追加します。
1. ロケーションの各フィールドに必要な情報を入力し、**ホスト**にCollectタグのURLを入力します。
      
<blockquote>
**ロケーションを編集**ダイアログボックスの外側をクリックすると、Charlesが追加のURLコンポーネントを自動的に判別します。
</blockquote>

1. **クエリ**フィールドは空のままにし、**OK**をクリックします。

アクションを追加するには、次の手順を実行します。

1. **アクション**リストの下にある**追加**をクリックし、リストから**タイプ**を`Body`に構成します。
1. **対象**セクションで、**リクエスト**チェックボックスを選択します。
1. **一致**セクションで、**値**を`"data":{`に構成し、**値全体に一致**チェックボックスを選択します。
1. **置換**セクションで、**値**を`"data":{"cp.trace_id":"TRACE_ID",`に構成し、**最初のみ置換**チェックボックスを選択します。
1. **OK**をクリックし、変更を**適用**します。

手順の完了後、アプリケーションを操作し、CDPまたはイベントストリーミングのトレースセッションでリクエストを確認します。別のトレースを実行するには、Charlesを起動して既存のリライトルールを編集し、`TRACE_ID`プレースホルダーを新しいトレースID値に変更します。

## 手動

エミュレーターを使用した開発モードの場合、またはCharlesを使用しない場合は、ネイティブコードを使用して手動でトレースに参加したり、トレースから退出したりできます。
### トレースを開始する（手動）

トレースを手動で開始して実行するには、ネイティブコード内の揮発性データにトレースIDを追加します。




```kotlin
instance.getDataSources().getVolatileDataSources().put("tealium_trace_id", "TRACE_ID");
```




**Swift**    
```swift
tealium?.volatileData()?.add(data: ["tealium_trace_id": "TRACE_ID"])
```

**Objective-C**   
```obj-c
NSDictionary *tealiumTrace = @{@"tealium_trace_id":@"TRACE_ID"};
[[Tealium instanceForKey:TEALIUM_INSTANCE_ID] addVolatileDataSources: tealiumTrace];
```



### トレースを終了する（手動）

トレースを手動で終了し、「訪問の終了」エンリッチメントをシミュレートするには、アプリ内の任意の場所で、次のトラックをオプションデータに追加します。



```java
Map<String, Object> data = new HashMap<>(1);
data.put("event", "kill_visitor_session");
data.put("cp.trace_id", "TRACE_ID");
```


```swift
tealium?.trackViewWithTitle("SCREEN_NAME", dataSources: ["event":"kill_visitor_session", "cp.trace_id":"XXXXX"])
```

