---
title: トレース
description: トレースを使用してデバッグする方法を学びます。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/
---
[トレース]()は、Tealium EventStreamおよびTealium AudienceStreamの構成をテストおよび検査するためのツールです。トレースを使用して訪問のワークフローをキャプチャし、イベントと顧客データがリアルタイムでどのように処理されるかを確認します。

## モバイルトレースツール

### 対応プラットフォーム

以下のプラットフォームがモバイルトレースツールをサポートしています：

* [Android (Kotlin)](/ja/platforms/android-kotlin/)
* [iOS (Swift v2.x)](/ja/platforms/ios-swift/)

大量のイベントにトレースを追加しないでください。&lt;br&gt;本番データを監視するためにトレースを永続的なパラメータとして追加しないでください。

### 使い方

モバイルトレースツールは、デバイスでスキャン可能なQRコードを提供することでトレース機能をエンリッチメントします。

ツールで**トレース開始**をクリックした後、Tealiumプラットフォームのセッションごとに一度、新しいトレースを開始するたびにメインブラウザウィンドウに自動的にQRコードが挿入されます。

QRコードは各プラットフォーム（[Android](/ja/platforms/android-kotlin/)または[iOS](/ja/platforms/ios-swift/)）ごとに生成されます。適切なQRコードをモバイルデバイスのカメラでスキャンした後、QRコードからのリンクをクリックしてアプリを起動し、トレースパラメータをTealium SDKに渡します。Tealium SDKはトレースID（その他のパラメータと共に）を受け取り、現在のセッションのデータレイヤーにトレースIDを挿入します。

その後のすべてのイベントは、セッションを終了するかトレースを離れるまでトレースセッションに記録されます。

次の図は、その動作を示しています：

![](/images/platforms/getting-started-mobile/trace-tool-overview.png)

### インストール

このツールを使用するには：

1. ブラウザ用の[Tealium Toolsブラウザ拡張機能]()をインストールします。
1. インストールが完了したら、Tealium Tools拡張機能を開きます。
1. **ツールカタログ**タブをクリックします。
1. **モバイルトレースツール**をクリックします。

![](/images/platforms/getting-started-mobile/mobile-trace-tool.png)

### URLスキーム

モバイルトレースツールを使用するには、モバイルアプリが処理するURLを特定して、URLスキームを構成します。

QRコードトレース機能は、URLからアプリを起動し、特定のクエリパラメータをリッスンします。URLから直接アプリを起動するには、アプリが特定のドメインを処理するように登録されている必要があります。

通常、ほとんどのアプリはすでに特定のURLを処理しています。たとえば、ウェブサイトのドメインが[https://mycompany.com](https://mycompany.com)である場合、アプリはこのドメインのハンドラとして自身を登録し、ユーザーのデバイスにアプリがインストールされている場合、ユーザーはブラウザではなくアプリでリンクを起動するように促されます。

一部のアプリは`mycompanyapp://`のようなカスタムURLスキームを登録している場合がありますが、これらもモバイルトレースツールで機能します。

アプリを起動するURLスキームを確立したら、モバイルトレースツールの入力フィールドにこれらを入力します。ツールは必要に応じてAndroidとiOSで異なるスキームをサポートしますが、通常は両プラットフォームで同じです。

![](/images/platforms/getting-started-mobile/trace-tool.png)

各URLスキームの横にある**保存**をクリックして、構成をブラウザの`localStorage`に保存します。URLスキームを必要に応じて編集するには、青い鉛筆アイコンをクリックします。

### トレースを開始する

トレースを開始する前に、Tealiumのサーバーサイドプラットフォームにいることを確認します。モバイルトレースツールで**トレース開始**をクリックして新しいトレースを開始し、トレースウィンドウにモバイルトレースQRコードを追加します。

![](/images/platforms/getting-started-mobile/trace-tool-start.png)

トレースを開始した後、Tealium ToolsのUIを閉じます。それ以降のセッションでは必要ありません。

次のトレースは直接Tealiumから開始され、QRコードは新しいトレースが開始されるたびに自動的に更新されます。QRコードをデバイスのカメラでスキャンし、リンクをクリックしてアプリを起動し、自動的にトレースを開始します。トレースに参加した後にアプリが生成するTealiumイベントは、トレースセッションに記録されます。

![](/images/platforms/getting-started-mobile/trace-qr-code.png)

### トレースを離れる

トレースセッションを終了せずに離れる場合、別のデバイスから同じトレースに再参加することができ、そのトレースセッションの履歴を失うことはありません。

トレースを離れるには：

1. トレースUIで**トレースを離れる**チェックボックスを選択します。
1. QRコードを再度デバイスのカメラでスキャンします。
1. デバイスがトレースセッションに参加しないようにするためのリンクをクリックします。

### 訪問の終了（AudienceStream）

Tealium AudienceStreamで「訪問の終了」アクションをテストするには、訪問のセッションを即座に終了するシグナルが必要です。そうでなければ、通常のセッションの有効期限が切れるのを待つ必要があります。

モバイルトレースツールでは、**訪問セッションの終了**チェックボックスを選択することで、SDKが`kill_visitor_session`イベントを送信するようにQRコードにパラメータを追加し、セッションを即座に終了します。

![](/images/platforms/getting-started-mobile/trace-end-visit.png)

## Charles Proxy

Charles Webデバッグプロキシを使用して、モバイルSDKとTealium Collectタグを使用するアプリケーションからトレースを開始します。

### 必要条件

* [Charles Proxy](https://www.charlesproxy.com)
* [Tealiumサーバーサイドアカウント]()

### 構成

Charlesをコンピューターを介してトラフィックをプロキシするようにモバイルデバイスを構成するには、[Android](/ja/platforms/android-kotlin/charles-proxy-android)または[iOS](/ja/platforms/ios-swift/charles-proxy-iosdevice)デバイスの指示に従ってください。

### リライトを使用する

Charlesをプロキシとして使用してアプリケーションを実行し、`teal`のネットワークトラフィックをフィルタリングします。リクエストを右クリックして**URLをコピー**を選択します。

Charlesメニューから**ツール &gt; リライト**を選択して**リライト構成**ダイアログを開きます。

ロケーションを追加するには：

1. **リライトを有効にする**チェックボックスを選択し、**ロケーション**リストの下にある**追加**をクリックします。
1. **名前**フィールドに`トレースIDを追加`と入力し、**追加**をクリックしてロケーションを追加します。
1. ロケーションフィールドに必要な情報を入力し、**ホスト**にCollectタグのURLを入力します。
       **編集ロケーション**ダイアログボックスの外をクリックすると、Charlesが追加のURLコンポーネントを自動的に決定します。
1. **クエリ**フィールドを空のままにして**OK**をクリックします。

アクションを追加するには：

1. **アクション**リストの下にある**追加**をクリックし、リストから**タイプ**を`Body`に構成します。
1. **どこで**セクションで**リクエスト**チェックボックスを選択します。
1. **一致**セクションで**値**を`&#34;data&#34;:{`に構成し、**値全体を一致**チェックボックスを選択します。
1. **置換**セクションで**値**を`&#34;data&#34;:{&#34;cp.trace_id&#34;:&#34;TRACE_ID&#34;,`に構成し、**最初のものを置換**チェックボックスを選択します。
1. **OK**をクリックして変更を**適用**します。

手順を完了した後、アプリケーションを参照し、AudienceStreamまたはEventStreamのトレースセッションでリクエストを表示します。別のトレースを実行するには、Charlesを起動し、既存のリライトルールを編集して`TRACE_ID`プレースホルダを新しいトレースID値に変更します。

## マニュアル

エミュレータを使用して開発モードにある場合、またはCharlesを使用したくない場合は、ネイティブコードでトレースを手動で追加および離れることができます。
### トレースの開始（手動）

トレースを手動で開始し実行するには、ネイティブコード内の揮発性データにトレースIDを追加します。




```kotlin
instance.getDataSources().getVolatileDataSources().put(&#34;tealium_trace_id&#34;, &#34;TRACE_ID&#34;);
```




**Swift**    
```swift
tealium?.volatileData()?.add(data: [&#34;tealium_trace_id&#34;: &#34;TRACE_ID&#34;])
```

**Objective-C**   
```obj-c
NSDictionary *tealiumTrace = @{@&#34;tealium_trace_id&#34;:@&#34;TRACE_ID&#34;};
[[Tealium instanceForKey:TEALIUM_INSTANCE_ID] addVolatileDataSources: tealiumTrace];
```



### トレースの終了（手動）

トレースを手動で終了し、「訪問終了」のエンリッチメントをシミュレートするには、アプリ内の任意の場所に以下のトラックを追加します：



```java
Map&lt;String, Object&gt; data = new HashMap&lt;&gt;(1);
data.put(&#34;event&#34;, &#34;kill_visitor_session&#34;);
data.put(&#34;cp.trace_id&#34;, &#34;TRACE_ID&#34;);
```


```swift
tealium?.trackViewWithTitle(&#34;SCREEN_NAME&#34;, dataSources: [&#34;event&#34;:&#34;kill_visitor_session&#34;, &#34;cp.trace_id&#34;:&#34;XXXXX&#34;])
```

