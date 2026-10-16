---
title: モバイルプロファイルを作成する
description: モバイルプロファイルの作成方法を学びます。
url: https://docs.tealium.com/ja/iq-tag-management/profiles/create-mobile-profile/
---
モバイルプロファイルを使用して、ウェブサイトとは別にモバイルアプリの構成とベンダートラッキングを管理します。

## Tealium Prism用

モバイルプロファイルは、以下のモバイルアプリケーションプラットフォームのいずれかのインストール時に使用されます：

* [Tealium Prism](https://docs.tealium.com/platforms/prism-mobile//)

### Tealium Prism用モバイルプロファイルの作成

[Tealium Prism](https://docs.tealium.com/platforms/prism-mobile//)の場合、プロファイルを作成する際にモバイルプロファイルを構成します。追加のアクティベーションステップは必要ありません。

1. タグ管理で、**管理メニュー > プロファイル管理**に移動します。
1. サイドパネルの**プロファイル**の下で、**+ 追加**をクリックします。
1. プロファイル名を入力します。
1. **モバイルプロファイル**を選択します。  
   ![](https://docs.tealium.com/images/platforms/prism/create-mobile-prism-profile.png)
1. **プロファイル作成**をクリックします。

Tealium Prismモバイルプロファイルの構成に関する詳細は、以下を参照してください：
* [Prism: モジュール](https://docs.tealium.com/platforms/prism-mobile/modules/)
* [Prism: ルール](https://docs.tealium.com/platforms/prism-mobile/rules/)
* [Prism: バリア](https://docs.tealium.com/platforms/prism-mobile/barriers/)
* [Prism: 変換](https://docs.tealium.com/platforms/prism-mobile/transformations/)

## Tealium for iOS (Swift) 2.xおよびTealium for Kotlin用

このセクションは、以下のライブラリのインストールに関するものです：

* [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/install/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/install/)

これらのSDKバージョンでは、最初にプロファイルを作成し、その後それをモバイルプロファイルに変換します。Tealiumをインストールする予定の各モバイルアプリケーションに対して別々のプロファイルを作成することをお勧めします。例えば、モバイルアプリの一般的なプロファイル名は、`mobile-ios`や`mobile-android`です。

### iOSおよびAndroid用モバイルプロファイルの作成とアクティベーション


<blockquote>
新しいモバイルインストールの場合、[Tealium Prism](#for-tealium-prism)の使用をお勧めします。
</blockquote>


Tealium for iOSまたはAndroid SDKで使用するプロファイルを作成およびアクティベートするには：

1. Tealiumタグ管理にログインします。
1. **管理メニュー > プロファイル管理**に移動します。
1. プロファイル名を入力し、**プロファイル作成**をクリックします。  
    
<blockquote>
Tealium Prism SDKを使用していない限り、**モバイルプロファイル**を選択しないでください。Swift 2.xおよびKotlin SDKでは、このチェックボックスを選択しないでください。
</blockquote>

1. プロファイルスイッチャーで、作成したばかりのプロファイルを選択します。
1. 管理メニューで**公開構成の構成**をクリックします。**公開構成の構成**ダイアログが表示されます。
1. **モバイルライブラリ公開**タブをクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-creating-a-mobile-profile-activate-mobile-library.jpg)
1. **モバイルライブラリをアクティベート**をクリックし、**アクティベート**をクリックして確認します。
1. **保存**をクリックします。
1. 構成を保存して公開します。  


<blockquote>
標準的なモバイル変数がプロファイルに追加され、タグや拡張機能で使用するためのデータレイヤー構成で利用可能になります。
</blockquote>


このプロファイルは、アカウント名、プロファイル名、および公開環境を参照することによって、モバイルアプリケーションで参照できるようになります。構成手順については、以下を参照してください：

* [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/install/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/install/)

### モバイル構成の調整

モバイル構成を調整するには、次の手順に従います：

1. Tealiumタグ管理にログオンし、モバイルアプリケーション用のアカウントとプロファイルを選択します。
1. 管理メニューで**公開構成の構成**をクリックします。**公開構成の構成**ダイアログが表示されます。
1. **モバイルライブラリ公開**タブをクリックします。  
モバイル公開構成はデフォルトで有効になっています。必要に応じてモバイル公開構成をスクロールして調整します。以下の表に説明されています。

| 構成          | 説明 |
|:------------ |:------------|
| タグ管理      | <ul><li>アプリケーションでクライアントサイドのイベントトラッキングのためにモバイルタグ管理を有効にします。</li><li>`utag.js`はwebviewで実行されます。</li></ul>|
| Tealium Collect | <ul><li>サーバーサイドのデータ管理のためにネイティブモバイルトラッキングを有効にします（EventStreamへのHTTPコールを直接行います）。</li><li>タグ管理を有効にした場合は**OFF**に構成します。</li></ul>|
| Tealium S2S Legacy | <ul><li>イベントとビューがTealium S2Sレガシープロトコルを通じて送信されるように**ON**に構成します。</li></ul>|

#### バッチ処理

| 構成          | 説明 |
|:------------ |:------------|
| 何件ごとにバッチデータを送信するか | <ul><li>データが送信される前に発生する必要があるイベントの数（バッチのサイズ）を構成します。</li><li>**1**またはそれ以下の値を入力すると、基本的にバッチ処理がオフになります。</li><li>デフォルト値は**1**です。</li></ul>|
| WiFiのみで送信                     | <ul><li>**ON**を有効にすると、ユーザーのデバイスがWiFiに接続されているときにのみイベントが送信されます。</li><li>デフォルト値は**OFF**です。</li></ul>|
| バッテリーセーバー                         | <ul><li>**ON**を有効にすると、デバイスのバッテリーが十分な電力を持っており、省電力モードではない場合にのみデータが送信されます。  <ul><li>iOS: バッテリーが20％で充電されていない場合。</li><li>Android: バッテリーが15％の場合</li></ul> </li><li>デフォルト値は**ON**です。</li></ul>|

#### データ保持

| 構成          | 説明 |
|:------------ |:------------|
| データの有効期限（#日）       | <ul><li>データが送信されない場合、アプリケーション内でデータが保持される期間（日数）を指定します。</li><li>**-1**の値はディスパッチの有効期限がないことを意味します。</li><li>デフォルト値は**-1**です。</li><li>ディスパッチの有効期限は、WiFiのみで送信またはバッテリーセーバーの構成によってキューに入れられたイベントにも適用されます。</li></ul>                                      |
| 同期間隔（分）       | <ul><li>構成チェックの間隔（起動とウェイク時にチェックが行われます）を分単位で指定します。</li><li>デフォルト値は**15.0**です。</li></ul>|
| キュー容量                        | <ul><li>デバイス上に保存され、送信の準備ができるまでのイベントとビューの数を指定します。  <ul><li>**0** = オフラインディスパッチなし</li><li>**-1** = 制限なし</li></ul> </li><li>デフォルト値は**-1**です。</li></ul>|

#### デバッグ

| 構成          | 説明 |
|:------------ |:------------|
| デバッグログレベルの構成               | <ul><li>ログを有効にすることができます。</li><li>以下の構成のいずれかを選択します：  <ul><li>**Default** – ログレベルを構成の環境構成に合わせて構成します。</li><li>**Dev** – 活動、情報、警告、エラーをログに記録します</li><li>**QA** – 情報、警告、エラーをログに記録します</li><li>**Prod** – エラーをログに記録します</li><li>**Silent** – ログを記録しません</li></ul> </li></ul> |

準備ができたら、**保存**をクリックし、構成を保存して公開します。

次回モバイルアプリケーションがロードされると、新しい構成が検出され、適用されます。