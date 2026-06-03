---
title: トラブルシューティング
description: モバイルインストールの検証方法について学びます。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/troubleshooting/
---
## 基本

モバイルアプリをテストする際は、Tealiumの「dev」環境でのみテストすることを推奨します。また、テスト用に特別に設計されたアプリのビルドを使用してください。本番ビルド（App Store/Play Store）を使用する必要がある場合は、ライブアプリケーションに変更を加えないようにするために、以下のセクションを参照して環境を切り替えてください。

デバッグ中に変更を公開すると、Tealiumのキャッシュに5分の有効期限があることに注意してください。この期間中、`utag.js`ファイルは公開後にTealiumのサーバーで更新されます。

アプリを冷たいスタート（アプリが以前にアプリトレイからスワイプされた状態）から起動するたびに、Tealium SDKは新しいファイルをチェックし、デフォルトでは15分ごとにチェックします（[モバイルパブリッシュ構成]()で制御されます）。ただし、公開してから5分未満の場合、アプリを再起動しても常に機能しない場合があります。テスト中に「dev」と「qa」の環境を切り替えると、キャッシュが5分以内に使用されない場合に環境のキャッシュが期限切れになり、新しいファイルがすぐに利用可能になります。


## Tealium EventStream ライブイベント

Tealium EventStreamの「ライブイベント」機能は、モバイルインストールのデバッグのためにすべてのTealiumの顧客に利用できます。

本番環境でこれを有効にすると、使用量に応じて料金が発生する場合があります。アプリが公開される前にこの機能を無効にしてください。

イベント収集機能を有効にするための次の方法のいずれかを使用します。

#### オプション1 - Tealium Collect タグ

タグマーケットプレースからTealium Collectタグを追加します。タグの詳細構成で、QA環境とProd環境をオフにして、タグを本番環境に公開して使用料金が発生しないようにします。リクエストはエンコードされたJSONデータとしてアプリから送信されるため、Charles Proxyとの併用はやや困難ですが、ウェブビューからのすべてのデータ（クッキーデータや拡張機能によって変更された変数など）を表示できる利点があります。タグの構成で特定のプロファイルを入力しない場合、データはアプリがターゲットにしている同じプロファイルに送信されます。特定のプロファイルにデータを送信する場合は、[Tealium collect tag setup guide]()を参照してください。

#### オプション2 - Tealium Collect モジュール

Tealium iQアカウントで「モバイルパブリッシュ構成」に移動し、「Tealium Collect」を有効にします。この方法の利点は、データがGETリクエストとして送信され、各データ変数が簡単に読み取り可能なクエリパラメータの形式でクエリ文字列に追加されることです。この方法は、データを検査するためにCharles Proxyを使用する場合に最適です。予期しない使用料金を避けるために、アプリを本番環境にプッシュする前にこの構成をオフにしてください。このリクエストで表示されるのは、アプリ開発者によってTealiumに渡された正確なデータのみであり、クッキーデータやウェブビューで生成されたデータは含まれません。

この機能を使用して送信されるデータは、アカウントの「main」プロファイルに送信され、現在選択されているプロファイルには送信されません。これを調整するには、アプリ内の次のコードスニペットを使用してディスパッチURLをオーバーライドし、適切なアカウント/プロファイルの組み合わせに置き換えます。



```java
Tealium.Config config = Tealium.Config.create(application, &#34;[ACCOUNT]&#34;, &#34;[PROFILE]&#34;, &#34;ENVIRONMENT&#34;);config.setOverrideCollectDispatchUrl(&#34;https://collect.tealiumiq.com/vdata/i.gif?tealium_account=[ACCOUNT]&amp;tealium_profile=[PROFILE]&#34;);
```


```obj-c
TEALConfiguration *configuration = [TEALConfiguration configurationWithAccount:@&#34;[account]&#34;profile:@&#34;[profile]&#34; environment:@&#34;dev&#34;];[configuration setOverrideCollectDispatchURL:@&#34;https://collect.tealiumiq.com/vdata/i.gif?tealium_account=[account]&amp;tealium_profile=[profile]&#34;];
```



上記のいずれかの収集方法を構成した後、EventStreamにログインし、ライブイベントに移動して受信イベントを確認します。

[ライブイベントの詳細]()について詳しく学びます。

## Charles Proxy

Charlesウェブデバッグプロキシは、Tealium iQタグ管理を介して構成したデバイスとサードパーティサービス間のすべてのHTTPおよびSSL/HTTPSトラフィックを検査します。

[Android](/ja/platforms/android-kotlin/charles-proxy-android)または[iOS](/ja/platforms/ios-swift/charles-proxy-iosdevice)デバイスでCharlesをプロキシとして構成します。

#### Tealium環境の切り替え

アプリがデフォルトの環境（例：「prod」）から別の環境に切り替える必要がある場合は、Charles Proxy（またはFiddlerなどの他のプロキシツール）でカスタムマッピングを追加し、アプリに提供されるファイルを透過的に切り替えます。たとえば、アプリは「prod」のutag.js (`https://tags.tiqcdn.com/utag/tealiummobile/demo/prod/utag.js`)を要求しますが、Charlesプロキシは「dev」のutag.js (`https://tags.tiqcdn.com/utag/tealiummobile/demo/dev/utag.js`)を返します。

次の構成手順で別のTealium環境に切り替えます。

1. Charles Proxyを開き、「Tools &gt; Map Remote」に移動します。**Map Remote Settings**画面で、「Enable Map Remote」をチェックし、「Add」をクリックします。
2. **Host**ボックスに、アカウントとプロファイルをURLに挿入して、`https://tags.tiqcdn.com/utag/&lt;account&gt;/&lt;profile&gt;/prod/*`とします。貼り付けた後、**Map From**セクションの**Port**または**Path**フィールドにカーソルを移動してクリックすると、CharlesがURLを自動的にコンポーネントに分割します。
3. **Map To**セクションでも同じプロセスを実行し、この時はURL内の環境を「prod」から「dev」（または「qa」）に変更します。URLの末尾のアスタリスク文字を削除します。たとえば：`https://tags.tiqcdn.com/utag/&lt;account&gt;/&lt;profile&gt;/dev/`
4. セットアップを完了するために、「OK」をクリックします。

これにより、Charles Proxyはすべての「prod」環境からのリクエストを「dev」環境に切り替えます。アプリのデフォルト環境に戻るには、Map Remoteルールを無効にするか削除するか、デバイスでプロキシをオフにします。

この構成が有効になるには、アプリを終了して再起動する必要があります。

#### トラフィック検査

以下は、Charlesプロキシを使用して検査する一般的なリクエストの例です。

| リクエスト | 説明 |
| :-- | :-- |
| `\*.tealiumiq.com` | Tealium AudienceStreamのライブイベント機能をデバッグに使用している場合、これらのヒットが送信されます（オプション1で説明）。 |
| `mobile.html` | Tealiumから構成を取得するための初期ヒット。 |
| `google-analytics.com, collect.gif` | Google Analyticsを使用している場合、ヒットは`collect.gif`に送信され、クエリパラメータが検査されます。 |
| `/b/ss` | このフィルタは、すべてのAdobe Analyticsへのヒットを受け取り、クエリ文字列にコンテキストデータと/またはプロパティ/eVarが表示されます。 |
| `tags.tiqcdn.com` | Tealiumのタグが発火したかどうかを確認するには、このサーバーへのヒットを確認します。バンドル化が無効になっている場合、各タグごとに個別のファイルが表示されます。たとえば、UID 123のタグは`utag.123.js`です。ファイルがキャッシュされている場合、キャッシュされたファイルは必ずしもCharles Proxyセッションに表示されないため、これは常に最も正確なテスト方法ではありません。 |

## トレース

トラブルシューティングには、[トレース](/ja/platforms/getting-started-mobile/trace/)の使用方法について学びます。

## アナリティクスツール

自分自身のためにテスト用のGoogle Analyticsアカウントを構成し、プロパティID（例：UA-12345678-1）をメモしてください。

[Google Analytics]()タグをTealium IQを介して追加し、関連する構成フィールドに新しいプロパティIDを入力します。

GAタグでスクリーンビューを有効にし、1つのデータ変数を`screenName`にマッピングします。

（オプション）GAでカスタムイベントを構成するには、2つの変数をイベントアクションとイベントカテゴリにそれぞれマッピングします。アプリが正常に機能している場合、スクリーンビューとカスタムイベントがGoogle Analyticsアカウントに表示されます。テスト目的でこれらの変数にどのようなデータを渡しても、カスタムイベントは自動的に生成されます。

## デバイスログ

#### 標準デバイスログ



1. マシンにAndroid Studioをインストールします。
2. Androidデバイスで[USBデバッグ](https://developer.android.com/studio/debug/dev-options#enable)を有効にします。
3. PC/MacでAndroid Studioを起動し、「Android Monitor」（v3.1以前）または「Run」（v3.2以降）が画面の下部に表示されることを確認します。これらのオプションのいずれかが表示されない場合は、「View &gt; Tool Windows &gt; Android Monitor/Run」を表示します。
4. AndroidデバイスをUSBケーブルで接続します。コンソールからデバイスのログが利用可能になります。これには、Androidシステム自体を含むすべてのアプリの出力が表示されます。本番ビルドをテストしている場合、重要なエラー/クラッシュのみがログに記録される可能性があります。
5. Android Studio 3.2以降がインストールされている場合、[その他のツール](https://developer.android.com/studio/profile/monitor)を使用してデバッグ/検証/トラブルシューティングを行うことができます。


1. マシンにXCodeをインストールします。
2. LightningケーブルでiPhone/iPadを接続します。
3. 「Window &gt; Devices and Simulators」に移動し、「Devices」タブでリストからデバイスを選択します。
4. デバイスコンソールを表示するには、右側のパネルの左下にある上向き三角形をクリックします。コンソールには、デバイス上のすべてのアプリのログが表示されます。アプリが本番ビルドの場合、重要なエラー/クラッシュのみがログに記録される可能性があります。



コンソールで「tealium」をフィルタリングすると、これらのログがより明確に表示される場合があります。

#### Tealiumデバッグログ



1. Android Studioを開き、デバイスを接続します。
3. `.setForceOverrideLogLevel()`メソッドを呼び出して、Tealiumデバッグレベルを最も詳細な構成（「dev」）に構成します（たとえば、`.setForceOverrideLogLevel(&#34;dev&#34;);`）。
3. プロジェクトを実行し、Logcatコンソールで出力を表示します。公開構成、構成構成、およびペイロードがコンソールに表示されます。

Logcatで「Sent queued dispatch」をフィルタリングすると、これらのログがより明確に表示される場合があります。



1. Xcodeを開き、デバイスを接続します。
2. `.setLogLevel()`メソッドを呼び出して、Tealiumデバッグレベルを最も詳細な構成（「dev」）に構成します。
	* iOS: `[tealConfig setLogLevel: TEALLogLevelDev];`
	* Swift: `setLogLevel(logLevel: TealiumLogLevel)`
3. プロジェクトを実行し、`lldb`コンソールで出力を表示します。公開構成、構成構成、およびペイロードがコンソールに表示されます。

IDEコンソールで「datasources payload」をフィルタリングすると、これらのログがより明確に表示される場合があります。



## mobile.htmlのデバッグ

このセクションでは、Tealium iQタグ管理のモバイル実装をトラブルシューティングする方法について説明します。公開されたファイル`mobile.html`を使用して、Tealium iQプロファイルのモバイルアプリケーションの実装に基づいています。

Tealium iQでモバイルプロファイルをアクティブにすると、次のパスに`mobile.html`という名前のファイルが公開されます。

`http://tags.tiqcdn.com/utag/{ACCOUNT}/{PROFILE}/{ENVIRONMENT}/mobile.html`

このファイルは、ネイティブモバイルライブラリがモバイルパブリッシュ構成を受け取り、タグ管理モジュールを実現するために使用されます。このファイルは、モバイル実装の基本的なトラブルシューティングを実行するために役立ちます。

#### mobile.htmlの検査

`mobile.html`ページ上の`utag.js`の動作は、標準のデスクトップウェブサイトページと似ています。`utag.js`ファイルがロードされ、その後のベンダータグが実行されます。

`mobile.html`ページを検査するには：

1. 新しいブラウザウィンドウでiQプロファイルの`mobile.html`URLを読み込みます。
2. ブラウザの開発者ツールまたはWebコンソールを開き、ページソースを検査します。

ここから、Tealiumの`utag.js`がインストールされたウェブサイトと同じトラブルシューティング手法を多く実行できます。

#### 公開タイムスタンプの確認

最初に確認することは、最新に公開された変更が`mobile.html`にロードされているかどうかです。これは、HTMLソースのタイムスタンプをiQのバージョン画面のタイムスタンプと一致させることで行われます。

公開タイムスタンプを確認するには：

1. `mobile.html`のページソースの先頭にある公開タイムスタンプを探します。`mobile.html`のタイムスタンプは次のパターンを持ちます：`ut.4.0.YYYYMMDDHHMM`（時間は常にGMTです）。
2. iQプロファイルで、バージョン画面に移動し、同じ環境の最新に公開されたバージョンを見つけます。この公開のタイムスタンプは、`mobile.html`内に見つかるタイムスタンプと一致します。

#### モバイルパブリッシュ構成JavaScriptオブジェクトの検査

`mobile.html`ページでは、JavaScriptオブジェクトである`mps`を使用して[モバイルパブリッシュ構成]()の値を格納します。このオブジェクトを検査して構成を確認します。

`mps`オブジェクトを検査するには：

1. Webコンソールに「mps」と入力し、Enterキーを押します。
2. 「4」と「5」とマークされたプロパティは、それぞれ4.xおよび5.xのバージョンのモバイルライブラリに対応しています。

#### トラッキングコールのシミュレーション

このページ上の`utag.js`の動作は、標準のデスクトップウェブサイトページと似ています。ブラウザのコンソールからトラッキングコールをトリガーし、タグが期待どおりに機能しているかを確認するために、ネットワークアクティビティを監視します。

`mobile.html`でトラッキングコールをシミュレートするには：

1. ブラウザのコンソールから、`utag.view({screen_title : &#34;Test Page&#34;})`と入力し、Enterキーを押します。
2. ネットワークアクティビティ画面に移動し、送信されるベンダートラッキングアクティビティを検査します。

## リモートデバッグ

上級ユーザーは、ChromeまたはSafariのリモートWebインスペクタを使用して、非表示のWebビューをデバッグできます。




アプリがTealiumのWebビューの[リモートデバッグ](https://developer.chrome.com/docs/devtools/remote-debugging/webviews/)を許可するように構成されていることを確認します（ビルド時にアプリ開発者によって行う必要があります）。

Chromeブラウザの[chrome://inspect/#devices](chrome://inspect/#devices)に移動します。

デバイスがUSBケーブルでマシンに接続されていることを確認します。

ウェブページのリストで、`tags.tiqcdn.com`でホストされているものを探します。これはTealiumのWebビュー（`mobile.html`）であり、上記と同様に検査されます。アプリがビューやリンクリクエストをトリガーするたびに、JavaScriptタグテンプレートで構成したブレークポイントがヒットし、データレイヤの値がデスクトップウェブサイトのように検査されます。




Appleの[Safari Developer Guide](https://developer.apple.com/library/content/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/GettingStarted/GettingStarted.html)に従って、Safari for Mac OSXおよびiPhone/iPadのデバイス構成でWebインスペクタを有効にします。

デバイスが**Develop**メニューに表示されるようになったら、デバイス上の`tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/mobile.html`を開き、上記の方法5の手順に従って操作を続けます。

これは、iOSシミュレータを使用してアプリをデバッグする場合にも機能します。&lt;br&gt;&lt;br&gt;App StoreまたはApple Configuratorを介してインストールされたアプリでは、Webビューをデバッグすることはできません。Webビューは、アプリがXCodeを介してインストールされ、iOSシミュレータまたは物理的なテストデバイスで実行されている場合にのみデバッグできます。



