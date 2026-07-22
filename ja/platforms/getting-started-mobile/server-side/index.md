---
title: サーバーサイド
description: モバイル向けのサーバーサイドソリューションの実装について学びます。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/server-side/
---
## Tealium Collect

Tealium Customer Data Hubのサーバーサイド製品を利用するためには、Tealium Collectサービスをインストールに追加する必要があります。

Tealium Collectは以下の方法のいずれかで有効化されます：

* Tealium iQタグ管理のTealium Collectタグ
* アプリのTealium Collectモジュール

追加されると、Tealium CollectはHTTPSリクエストをCustomer Data Hubデータ収集サーバーに送信し、以下のサーバーサイド製品で使用します：

* [Tealium EventStream](https://docs.tealium.com/introduction-to-eventstream/)
* [Tealium AudienceStream](https://docs.tealium.com/introduction-to-audiencestream/)
* [Tealium EventStore](https://docs.tealium.com/about-dataaccess/)
* [Tealium AudienceDB & EventDB](https://docs.tealium.com/audiencedb-and-eventdb/)

Tealium Collectはモバイルアプリケーションに多くの利点を提供します。Tealium EventStreamとCollectモジュールがインストールされていれば、サードパーティのベンダーSDKをアプリから削除し、代わりにサーバーサイドコネクタとして実装することができます。EventStreamのようなAPIハブにベンダーをオフロードすることで、アプリのサイズを減らし、ネットワークトラフィックを最小限に抑え、デバイスのバッテリー消費を節約します。

以下の図は、Tealium SDKがTealium Collectを使用してイベントを直接EventStreamとAudienceStreamにHTTPSリクエストで送信し、ベンダーにデータを送信したり、訪問をオーディエンスに入れたり、バッジを割り当てたり、属性を適用したりする方法を示しています。

![](https://docs.tealium.com/images/platforms/getting-started-mobile/tealium_collect_data_flow_diagram.png)

### JavaScriptタグ

Tealium CollectタグはiQタグ管理構成に追加され、タグ管理モジュール内のデバイスで実行されます。JavaScriptタグは隠されたwebviewで実行され、トラッキングコールをTealiumサーバーにディスパッチします。

**推奨されるのは：**

* タグ管理モジュールを既に使用しているインストール
* 拡張機能を使用してデータレイヤーをカスタマイズする必要がある実装

[Tealium Collectタグの構成方法](https://docs.tealium.com/tealium-collect-tag/)について詳しく学びましょう。

### ネイティブモジュール

Tealium Collectモジュールは、iQアカウントの[モバイル公開構成](https://docs.tealium.com/creating-a-mobile-profile/)を使用して有効化されます。Collectモジュールはアプリのネイティブコードとして実行され、HTTPSを使用してトラッキングコールを直接Tealiumサーバーにディスパッチします。

**推奨されるのは：**

* シンプルで軽量なインストール。
* iQタグ管理にアクセスできないインストール。


<blockquote>
Swiftライブラリの場合、Tealium Collectはネイティブコードで有効化および無効化する必要があります。
</blockquote>


### データレイヤーエンリッチメント（DLE）

Tealium AudienceStreamは、[Data Layer Enrichment (DLE)](https://docs.tealium.com/data-layer-enrichment-api/)と呼ばれる機能を使用して、訪問プロファイルデータをTealium Collectに返すという追加の利点を提供します。Collectモジュールでは、返された訪問属性に基づいてアプリをパーソナライズするためにDLEを使用します。

Tealium iQタグ管理では、Collectタグが実行されていると、隠されたwebview `mobile.html`がDLE訪問属性にアクセスを提供します。これらの属性は、拡張機能の構成、ローディングルールの構成などを行う際にアクセス可能です。DLE値に基づくアプリ内パーソナライゼーションのために、webviewとモバイルアプリ間で通信するために[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/)が必要です。

[VisitorServiceモジュール for Swift](https://docs.tealium.com/ja/platforms/ios-swift/module-list/visitor-service/)もデータレイヤーに訪問プロファイルを追加します。
