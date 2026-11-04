---
title: トラブルシューティング
description: モバイルインストールを検証するさまざまな方法について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/troubleshooting/
---
## 基本事項

モバイルアプリをテストする場合は、Tealiumの`prod`環境ではなく、`dev`環境のみでテストすることをお勧めします。また、テスト専用に設計されたアプリのビルドを使用してください。App StoreやPlay Storeでアプリの表示をテストする場合など、テストに本番ビルドを使用する必要がある場合は、稼働中のアプリケーションに変更を加えないように環境を切り替える方法について、以下の[Charles Proxy](#charles-proxy)セクションを参照してください。

デバッグ中に変更をパブリッシュすると、Tealiumのキャッシュには5分間の有効期限が適用されます。パブリッシュ後、この期間中にTealiumのサーバー上の`utag.js`ファイルが更新されます。

アプリをコールドスタート（アプリトレイから以前にスワイプして終了した状態）で起動するたびに、Tealium SDKは新しいファイルを確認します。その後はデフォルトで15分ごとに確認します（[モバイルパブリッシュ構成](https://docs.tealium.com/publish-configuration/#mobile-library-publishing)で制御されます）。ただし、パブリッシュしてから5分未満の場合は、5分間の有効期限が切れるまで、アプリを再起動しても常に機能するとは限りません。テスト中に`dev`環境と`qa`環境を切り替えることで、この問題を軽減できる場合があります。環境のキャッシュは過去5分間使用されていなければ期限切れになり、新しいファイルをすぐに利用できるようになるためです。

## EventStreamのライブイベント

EventStreamの**ライブイベント**機能は、モバイルインストールをデバッグする目的で、すべてのTealiumユーザーが利用できます。


<blockquote>
このトラブルシューティング方法を本番環境で使用すると、使用量に応じた料金が発生する場合があります。アプリを公開する前に、必ずこの機能を無効にしてください。
</blockquote>


イベント収集機能を有効にするには、次のいずれかの方法を使用します。

#### オプション1 - Tealium Collectタグ

タグマーケットプレイスから[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)を追加します。タグの**詳細構成**で、QA環境とProd環境をオフに切り替え、タグが本番環境にパブリッシュされて使用料金が発生することを防ぎます。リクエストは、エンコードされたJSONデータとしてPOSTリクエストでアプリから送信されます。そのため、この方法をCharles Proxyと併用するのは比較的困難ですが、Cookieデータや拡張機能によって変更された変数を含め、WebViewからのすべてのデータを確認できるという利点があります。タグ構成で特定のプロファイルを入力しない場合、データはアプリが対象としているものと同じプロファイルに送信されます。特定のプロファイルにデータを送信する場合は、[Tealium Collectタグの構成ガイド](https://docs.tealium.com/tealium-collect-tag/)を参照してください。

#### オプション2 - Tealium Collectモジュール

タグ管理アカウントで、**モバイルパブリッシュ構成**に移動し、**Tealium Collect**を有効にします。この方法には、データが`GET`リクエストとして送信され、各データ変数が読みやすいクエリパラメータとしてクエリ文字列に追加されるという利点があります。Charles Proxyを使用してデータを調査する場合は、この方法が最適です。予期しない使用料金を避けるため、アプリを本番環境にリリースする前に、必ずこの構成をオフにしてください。このリクエストでは、アプリ開発者がTealiumに渡したデータのみが表示されます。Cookieデータや拡張機能で生成されたデータなど、WebViewからのデータは表示されません。

デフォルトでは、この機能を使用して送信されたデータは、アプリで現在選択されているプロファイルではなく、アカウントの「main」プロファイルに送信されます。この動作を調整するには、アプリで次のコードスニペットを使用してディスパッチURLを上書きし、適切なアカウントとプロファイルの組み合わせに置き換えます。



```java
Tealium.Config config = Tealium.Config.create(application, "[ACCOUNT]", "[PROFILE]", "ENVIRONMENT");config.setOverrideCollectDispatchUrl("https://collect.tealiumiq.com/vdata/i.gif?tealium_account=[ACCOUNT]&tealium_profile=[PROFILE]");
```


```obj-c
TEALConfiguration *configuration = [TEALConfiguration configurationWithAccount:@"[account]"profile:@"[profile]" environment:@"dev"];[configuration setOverrideCollectDispatchURL:@"https://collect.tealiumiq.com/vdata/i.gif?tealium_account=[account]&tealium_profile=[profile]"];
```



上記のいずれかの収集方法を構成したら、EventStreamにログインし、**ライブイベント**に移動して受信イベントを確認します。

詳細については、[ライブイベント](https://docs.tealium.com/about-live-events/)を参照してください。

## Charles Proxy

Charles Webデバッグプロキシは、デバイスとタグ管理で構成したサードパーティサービスとの間のすべてのHTTPおよびSSL/HTTPSトラフィックを調査します。

Charlesを構成して、[Android](https://docs.tealium.com/ja/platforms/android-kotlin/charles-proxy-android)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/charles-proxy-iosdevice)デバイスをプロキシ経由で接続します。

#### Tealium環境の切り替え

変更を確認するには、アプリが対象としているデフォルト環境（`prod`など）から別の環境に切り替える必要がある場合があります。環境を切り替えるには、Charles Proxy（またはFiddlerなどの別のプロキシツール）にカスタムマッピングを追加します。これにより、アプリに配信されるファイルが透過的に切り替えられます。たとえば、アプリが`prod`の`utag.js`ファイル（`https://tags.tiqcdn.com/utag/tealiummobile/demo/prod/utag.js`）をリクエストしても、Charles Proxyは`dev`の`utag.js`（`https://tags.tiqcdn.com/utag/tealiummobile/demo/dev/utag.js`）を返します。

次の構成手順で、別のTealium環境に切り替えます。

1. Charles Proxyを開き、**Tools > Map Remote**に移動します。**Map Remote Settings**画面で、**Enable Map Remote**をオンにしてから、**Add**をクリックします。
1. **Host**ボックスに`https://tags.tiqcdn.com/utag/<account>/<profile>/prod/*`を貼り付け、URL内のアカウントとプロファイルを自分のものに置き換えます。貼り付けた後、カーソルを移動して**Map From**セクションの**Port**または**Path**フィールドをクリックすると、CharlesによってURLが自動的に構成要素へ分割されます。
1. **Map To**セクションでも同じ操作を行います。今回は、対象とする環境に応じて、URL内の環境を`prod`から`dev`（または`qa`）に変更します。URLの末尾からアスタリスクを削除します。例：`https://tags.tiqcdn.com/utag/<account>/<profile>/dev/`
1. **OK**をクリックして構成を完了します。

これで、Charles Proxyはすべてのリクエストを`prod`環境から`dev`環境に切り替えます。アプリのデフォルト環境に戻すには、**Map Remote**ルールを無効化または削除するか、デバイスのプロキシをオフにします。


<blockquote>
この構成を有効にするには、アプリを終了して再起動してください。
</blockquote>


#### トラフィックの調査

次の表は、Charles Proxyを使用して調査する一般的なリクエストの例を示しています。

| リクエスト | 説明 |
| :-- | :-- |
| `\*.tealiumiq.com` | 上記のオプション1で説明したように、デバッグにライブイベント機能を使用している場合、これらのヒットが送信されます。 |
| `mobile.html` | Tealiumから構成を取得する最初のヒットです。 |
| `google-analytics.com, collect.gif` | Google Analyticsを使用している場合、ヒットは`collect.gif`に送信され、クエリパラメータを調査できます。 |
| `/b/ss` | このフィルターはAdobe Analyticsへのすべてのヒットを取得します。コンテキストデータやprops/eVarsはクエリ文字列に表示されます。 |
| `tags.tiqcdn.com` | どのTealiumタグが発火したかを確認するには、このサーバーへのヒットを確認します。バンドルを有効にしていない場合は、タグごとに個別のファイルが表示されます（たとえば、UIDが123のタグは`utag.123.js`です）。ファイルがキャッシュされている場合、タグが発火していてもCharles Proxyセッションに表示されないことがあります。そのため、これは必ずしも最も正確なテスト方法ではありません。 |

## Trace

詳細については、[Trace](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/)を参照してください。
## 分析ツール

構成のトラブルシューティングを行うために Google Analytics を構成するには、次の手順を実行します。

1. テスト用の Google Analytics アカウントを作成し、プロパティ ID（例：`UA-12345678-1`）をメモします。
1. Tealium IQ を通じて [Google Analytics](https://docs.tealium.com/google-analytics-gtagjs-tag/) タグを追加し、該当する構成フィールドに新しいプロパティ ID を入力します。
1. GA タグでスクリーンビューを有効にし、データ変数のいずれかを `screenName` にマッピングします。
1. （任意）任意の 2 つの変数をそれぞれ **Event Action** と **Event Category** にマッピングし、GA でカスタムイベントを構成します。アプリが正常に動作している場合、スクリーンビューとカスタムイベントが Google Analytics アカウントに表示されます。**Event Category** と **Event Action** が構成されていれば、カスタムイベントは自動的に生成されます。テスト目的では、これらの変数に渡す具体的なデータの内容は問いません。

## デバイスログ

#### 標準デバイスログ



1.  マシンに Android Studio をインストールします。
1.  Android デバイスで [USB デバッグを有効にします](https://developer.android.com/studio/debug/dev-options#enable)。
1.  PC／Mac で Android Studio を起動し、画面下部に **Android Monitor**（v3.1 以前）または **Run**（v3.2 以降）が表示されていることを確認します。どちらも表示されない場合は、**View > Tool Windows > Android Monitor/Run** に移動して、いずれかを表示します。
1.  USB ケーブルで Android デバイスを接続します。コンソールでデバイスのログを確認できるようになります。Android システム自体を含む、すべてのアプリからの出力が表示されます。本番ビルドをテストしている場合は、重大なエラーやクラッシュのみが記録される可能性があります。
1. Android Studio 3.2 以降がインストールされている場合は、デバッグ、検証、トラブルシューティングに使用できる[その他のツール](https://developer.android.com/studio/profile/monitor)もあります。


1.  マシンに Xcode をインストールします。
1.  Lightning ケーブルで iPhone／iPad を接続します。
1.  **Window > Devices and Simulators > Devices** に移動し、一覧からデバイスを選択します。
1.  デバイスコンソールを表示するには、右側のパネルの左下にある上向き三角形をクリックします。コンソールには、デバイス上のすべてのアプリからのログが表示されます。アプリが本番ビルドの場合は、重大なエラーやクラッシュのみが記録される可能性があります。




<blockquote>
コンソールを `tealium` でフィルタリングすると、これらのログがより見やすくなる場合があります。
</blockquote>


#### Tealium デバッグログ



1.  Android Studio を開き、デバイスを接続します。
1.  `.setForceOverrideLogLevel()` メソッドを呼び出して（例：`.setForceOverrideLogLevel("dev");`）、Tealium のデバッグレベルを最も詳細な構成（`dev`）に構成します。
1.  プロジェクトを実行し、Logcat コンソールで出力を確認します。公開構成、構成構成、ペイロードがコンソールに表示されます。


<blockquote>
Logcat を "Sent queued dispatch" でフィルタリングすると、これらのログがより見やすくなる場合があります。
</blockquote>




1.  Xcode を開き、デバイスを接続します。
1.  `.setLogLevel()` メソッドを呼び出して、Tealium のデバッグレベルを最も詳細な構成（`dev`）に構成します。
	* iOS：`[tealConfig setLogLevel: TEALLogLevelDev];`
	* Swift：`setLogLevel(logLevel: TealiumLogLevel)`
1.  プロジェクトを実行し、`lldb` コンソールで出力を確認します。公開構成、構成構成、ペイロードがコンソールに表示されます。


<blockquote>
IDE コンソールを `datasources payload` でフィルタリングすると、これらのログがより見やすくなる場合があります。
</blockquote>




## mobile.html のデバッグ

このセクションでは、公開済みファイル `mobile.html` を使用して、タグ管理のモバイル実装をトラブルシューティングする方法について説明します。

タグ管理でモバイルプロファイルを有効にすると、`mobile.html` という名前のファイルが次のパスに公開されます。

`http://tags.tiqcdn.com/utag/{ACCOUNT}/{PROFILE}/{ENVIRONMENT}/mobile.html`

ネイティブモジュールライブラリは、このファイルを使用してモバイル公開構成を受信し、タグ管理モジュールの動作を支援します。このファイルは、モバイル実装の基本的なトラブルシューティングに役立ちます。

#### mobile.html の調査

`mobile.html` ページ上の `utag.js` の動作は、標準的なデスクトップ Web サイトのページ上での動作と似ています。`utag.js` ファイルが読み込まれ、その後ベンダータグが実行されます。

`mobile.html` ページを調査するには、次の手順を実行します。

1.  新しいブラウザウィンドウで、iQ プロファイルの `mobile.html` URL を読み込みます。
1.  ブラウザの開発者ツールまたは Web コンソールを開き、ページソースを調査します。

ここでは、Tealium の `utag.js` がインストールされている Web サイトで使用するものと同じトラブルシューティング手法の多くを実行できます。

#### 公開タイムスタンプの確認

最初に確認する必要があるのは、直近に公開した変更が `mobile.html` に読み込まれていることです。HTML ソースのタイムスタンプと、iQ の Versions 画面にあるタイムスタンプを照合することで、変更を確認できます。

公開タイムスタンプを確認するには、次の手順を実行します。

1.  `mobile.html` のページソースの先頭で、1 行目にある公開タイムスタンプを確認します。`mobile.html` のタイムスタンプは、`ut.4.0.YYYYMMDDHHMM` というパターンです（時刻は常に GMT です）。
1.  iQ プロファイルで **Versions** 画面に移動し、同じ環境に直近で公開されたバージョンを探します。この公開のタイムスタンプが、`mobile.html` 内のタイムスタンプと一致することを確認します。

#### モバイル公開構成の JavaScript オブジェクトの調査

`mobile.html` ページでは、`mps` という名前の JavaScript オブジェクトを使用して、[モバイル公開構成](https://docs.tealium.com/create-mobile-profile/)の値を格納します。このオブジェクトを調査して構成を確認します。

`mps` オブジェクトを調査するには、次の手順を実行します。

1.  Web コンソールに `mps` と入力します。
1.  `4` および `5` と記されたプロパティは、それぞれモバイルライブラリのバージョン 4.x および 5.x に対応します。

#### トラッキング呼び出しのシミュレーション

このページ上の `utag.js` の動作は、標準的なデスクトップ Web サイトのページ上での動作と似ています。ネットワークアクティビティを監視して、どの `utag.\*.js` ファイルが読み込まれているかを確認します。また、ブラウザコンソールからトラッキング呼び出しをトリガーし、タグが想定どおりに動作していることを確認します。

`mobile.html` でトラッキング呼び出しをシミュレーションするには、次の手順を実行します。

1.  ブラウザコンソールで `utag.view({screen_title : "Test Page"})` と入力します。
1.  **Network Activity** 画面に移動し、送信されるベンダーのトラッキングアクティビティを調査します。
## リモートデバッグ

上級ユーザーは、Chrome または Safari のリモート Web インスペクターを使用して、非表示の WebView をデバッグできます。




Tealium WebView の[リモートデバッグ](https://developer.chrome.com/docs/devtools/remote-debugging/webviews/)を許可するようにアプリが構成されていることを確認します（アプリ開発者がビルド時に行う必要があります）。

Chrome ブラウザで [chrome://inspect/#devices](chrome://inspect/#devices) に移動します。

デバイスが USB ケーブルでマシンに接続されていることを確認します。

Web ページの一覧で、`tags.tiqcdn.com` でホストされているページを探します。このページが Tealium WebView（`mobile.html`）であり、上記と同じ方法で検査できます。アプリがビューリクエストまたはリンクリクエストをトリガーするたびに、JavaScript タグテンプレートに構成したブレークポイントで処理が停止し、デスクトップ Web サイトの場合と同様にデータレイヤーの値を確認できます。




iOS 16.4 以降を使用している場合は、WebView を検査可能にする構成を手動で行う必要があります。`getTagManagementWebView()` API 呼び出しを使用して、`isInspectable` プロパティを構成します。詳細については、[Tealium API リファレンス](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#gettagmanagementwebview)を参照してください。

Apple の [Safari 開発者ガイド](https://developer.apple.com/library/content/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/GettingStarted/GettingStarted.html)に従って、Mac OSX の Safari と iPhone/iPad のデバイス構成で Web インスペクターを有効にします。

**開発**メニューにデバイスが表示されたら、デバイス上で開いている Web ページの一覧から `tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/mobile.html` を開き、上記の「[mobile.html のデバッグ](#debugging-mobilehtml)」セクションの手順に従います。


<blockquote>
この手順は、iOS シミュレーターを使用してアプリをデバッグする場合にも利用できます。<br><br>App Store または Apple Configurator 経由でインストールされたアプリ内の WebView はデバッグできません。WebView をデバッグできるのは、XCode を使用してアプリをインストールし、iOS シミュレーターまたは物理テストデバイス上で実行した場合のみです。
</blockquote>


