---
title: モバイルプロファイルの作成
description: このドキュメントでは、モバイルプロファイルの作成方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/profiles/creating-a-mobile-profile/
---
モバイルプロファイルは、以下のモバイルアプリケーションプラットフォームのいずれかのインストールに使用されます：

* [Tealium for iOS](/ja/platforms/ios-swift/install/)
* [Tealium for Android](/ja/platforms/android-kotlin/install/)

## 仕組み

iQタグ管理アカウントのプロファイルは、デフォルトでウェブサイトでの使用に構成されています。任意のプロファイルをネイティブモバイルインストールで使用するために有効化することができます。既存のプロファイルをモバイル用に有効化するか、新しいプロファイルを作成することができます。モバイルアプリケーションごとに別々のプロファイルを使用することで、各モバイルアプリケーションにデプロイされる構成とベンダートラッキングを管理することができます。

## モバイルアプリケーション用の新しいプロファイルを作成する

Tealiumをインストールする予定の各モバイルアプリケーションに対して別々のプロファイルを作成することをお勧めします。例えば、モバイルアプリケーションのための最も一般的なプロファイル名は、`mobile-ios`と`mobile-android`です。

[プロファイルの管理]()について詳しく学びましょう。

## モバイルプロファイルを有効化する

以下の手順を使用して、モバイルでの使用のためのプロファイルを有効化します：

1. ログインし、モバイルアプリケーションで使用する予定のプロファイルをロードします。
1. 管理メニューで、**Configure Publish Settings**をクリックします。**Publish Configuration**ダイアログが表示されます。
1. **Mobile Library Publishing**タブをクリックします。  
    ![](/images/iq-tag-management/whiteui-tiq-creating-a-mobile-profile-activate-mobile-library.jpg)
1. **Activate Mobile Library**をクリックし、**Activate**をクリックして確認します。
1. **Save**をクリックします。
1. 構成を保存し、公開します。  

このプロファイルは、アカウント名、プロファイル名、および公開環境を参照することで、Tealium for Mobileアプリケーションで参照することができます。

標準的なモバイル変数がプロファイルに追加され、タグと拡張機能の使用に対してデータレイヤー構成で利用可能になります。

## モバイル構成の構成

モバイルプロファイルを使用して、モバイルインストールの動作を決定する構成の構成を調整します。

以下の手順を使用して、モバイル構成構成を調整します：

1. モバイルアプリケーションで使用する予定のプロファイルを使用して、Tealium iQにログオンします。
1. 管理メニューで、**Configure Publish Settings**をクリックします。**Publish Configuration**ダイアログが表示されます。
1. **Mobile Library Publishing**タブをクリックします。  
モバイル公開構成はデフォルトで有効になっています。必要に応じて、以下の表に記載されているように、モバイル公開構成をスクロールして調整することができます。

| 構成| 説明|
|:------------ |:------------|
| タグ管理                        | &lt;ul&gt;&lt;li&gt;クライアントサイドのイベントトラッキングのために、アプリケーションでモバイルタグ管理を有効にします。&lt;/li&gt;&lt;li&gt;`utag.js`はwebviewで実行されます。&lt;/li&gt;&lt;/ul&gt;|
| Tealium Collect                       | &lt;ul&gt;&lt;li&gt;サーバーサイドのデータ管理（EventStreamへの直接のHTTP呼び出し）のためのネイティブモバイルトラッキングを有効にします。&lt;/li&gt;&lt;li&gt;タグ管理を有効にした場合は**OFF**に構成します。&lt;/li&gt;&lt;/ul&gt;|
| Tealium S2S Legacy                    | &lt;ul&gt;&lt;li&gt;イベントとビューがTealium S2Sレガシープロトコルを介して送信されるように**ON**に構成します。&lt;/li&gt;&lt;/ul&gt;|

### バッチング

| 構成| 説明|
|:------------ |:------------|
| Send Batch Data after every (#) event | &lt;ul&gt;&lt;li&gt;データが送信される前に発生しなければならないイベント（バッチのサイズ）の数を構成することができます。&lt;/li&gt;&lt;li&gt;値を または **1**に構成すると、バッチングが基本的にオフになります。&lt;/li&gt;&lt;li&gt;デフォルト値は**1**に構成されています。&lt;/li&gt;&lt;/ul&gt;|
| WiFi Only Sending                     | &lt;ul&gt;&lt;li&gt;**ON**を有効にすると、ユーザーのデバイスがWiFiに接続しているときにのみイベントが送信されます。&lt;/li&gt;&lt;li&gt;デフォルト値は**OFF**です。&lt;/li&gt;&lt;/ul&gt;|
| Battery Saver                         | &lt;ul&gt;&lt;li&gt;**ON**を有効にすると、デバイスが十分なバッテリーパワーを持っており、省電力モードにないときにのみデータが送信されます。  &lt;ul&gt;&lt;li&gt;iOS: バッテリーが20%で充電されていない。&lt;/li&gt;&lt;li&gt;Android: バッテリーが15%&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;デフォルト値は**ON**です。&lt;/li&gt;&lt;/ul&gt;|

### データ保持

| 構成| 説明|
|:------------ |:------------|
| Dispatch Expiration in (#) days       | &lt;ul&gt;&lt;li&gt;データが送信されない場合、アプリケーション内にデータがどのくらいの期間（日数）保持されるかを指定します。&lt;/li&gt;&lt;li&gt;値が**-1**の場合、ディスパッチの有効期限はありません。&lt;/li&gt;&lt;li&gt;デフォルト値は**-1**に構成されています。&lt;/li&gt;&lt;li&gt;ディスパッチの有効期限は、WiFiのみの送信またはバッテリーセーバーの構成によりキューに入れられたイベントにも適用されます。&lt;/li&gt;&lt;/ul&gt;                                      |
| Minutes Between Synchronization       | &lt;ul&gt;&lt;li&gt;構成チェック間の分数（チェックは起動とスリープ解除時に行われます）。&lt;/li&gt;&lt;li&gt;デフォルト値は**15.0**です。&lt;/li&gt;&lt;/ul&gt;|
| Queue Capacity                        | &lt;ul&gt;&lt;li&gt;デバイスに保存して送信する準備ができるまでのイベントとビューの数。  &lt;ul&gt;&lt;li&gt;**0** = オフラインディスパッチングなし&lt;/li&gt;&lt;li&gt;**-1** = 制限なし&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;デフォルト値は**-1**です。&lt;/li&gt;&lt;/ul&gt;|

### デバッグ

| 構成| 説明|
|:------------ |:------------|
| Set Debugging Log Level               | &lt;ul&gt;&lt;li&gt;ログを有効にすることができます。&lt;/li&gt;&lt;li&gt;以下の構成のいずれかを選択します：  &lt;ul&gt;&lt;li&gt;**Default** – ログレベルを構成の環境構成に合わせて構成します。&lt;/li&gt;&lt;li&gt;**Dev** – ログアクティビティ、情報、警告、エラー&lt;/li&gt;&lt;li&gt;**QA** – ログ情報、警告、エラー&lt;/li&gt;&lt;li&gt;**Prod** – ログエラー&lt;/li&gt;&lt;li&gt;**Silent** – ログを記録しない&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |

準備ができたら、**Save**をクリックし、構成を保存して公開します。  

次回モバイルアプリケーションがロードされると、新しい構成が検出されて適用されます。


