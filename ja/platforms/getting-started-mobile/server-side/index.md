---
title: サーバーサイド
description: モバイル向けのサーバーサイドソリューションの実装について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/server-side/
---
## Tealium Collect

Tealium Customer Data Hubのサーバーサイド製品を利用するには、Tealium Collectサービスをインストールに追加する必要があります。

Tealium Collectは、次のいずれかの方法で有効にします。

* タグ管理のTealium Collectタグ
* アプリ内のTealium Collectモジュール

追加すると、Tealium CollectはHTTPSリクエストをCustomer Data Hubのデータ収集サーバーに送信し、次のサーバーサイド製品で使用できるようにします。

* [イベントストリーミング](https://docs.tealium.com/server-side/getting-started/tutorials/event-data-activation/introduction/)
* [顧客データプラットフォーム（CDP）](https://docs.tealium.com/server-side/getting-started/tutorials/visitor-profile-management/introduction/)
* [Tealium EventStore](https://docs.tealium.com/about-dataaccess/)
* [Tealium AudienceDBおよびEventDB](https://docs.tealium.com/audiencedb-and-eventdb/)

Tealium Collectは、モバイルアプリケーションに多くのメリットをもたらします。イベントストリーミングを利用し、Collectモジュールがインストールされている場合、サードパーティベンダーのSDKをアプリから削除し、代わりにサーバーサイドコネクタとして実装できます。ベンダーとの連携をイベントストリーミングなどのAPIハブにオフロードすると、アプリのサイズとネットワークトラフィックを削減し、デバイスのバッテリー消費を抑えることができます。

次の図は、Tealium SDKがTealium Collectを使用し、HTTPSリクエストによってイベントをイベントストリーミングおよび顧客データプラットフォーム（CDP）へ直接送信する仕組みを示しています。これにより、ベンダーへのデータ送信、訪問のオーディエンスへの追加、バッジの割り当て、および属性の適用が可能になります。

![](https://docs.tealium.com/images/platforms/getting-started-mobile/tealium_collect_data_flow_diagram.png)

### JavaScriptタグ

Tealium Collectタグはタグ管理構成に追加され、タグ管理モジュール内でデバイス上にて実行されます。このJavaScriptタグは非表示のWebビュー内で実行され、トラッキングコールをTealiumサーバーへ送信します。

**推奨されるケース：**

* タグ管理モジュールをすでに使用しているインストール
* 拡張機能を使用したデータレイヤーのカスタマイズが必要な実装

[Tealium Collectタグの構成方法](https://docs.tealium.com/tealium-collect-tag/)について詳しくご覧ください。

### ネイティブモジュール

Tealium Collectモジュールは、iQアカウントの[モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)を使用して有効にします。Collectモジュールはアプリ内でネイティブコードとして実行され、HTTPSを使用してトラッキングコールをTealiumサーバーへ直接送信します。

**推奨されるケース：**

* シンプルで軽量なインストール
* タグ管理を利用できないインストール


<blockquote>
Swiftライブラリでは、Tealium Collectをネイティブコード内で有効化および無効化する必要があります。
</blockquote>


### データレイヤーエンリッチメント（DLE）

CDPには、[データレイヤーエンリッチメント（DLE）](https://docs.tealium.com/data-layer-enrichment-api/)と呼ばれる機能を使用して、訪問プロファイルデータをTealium Collectへ返すという追加の利点があります。Collectモジュールでは、返された訪問属性に基づいてアプリをパーソナライズするためにDLEを使用します。

タグ管理でCollectタグを実行すると、非表示のWebビュー`mobile.html`からDLEの訪問属性にアクセスできます。これらの属性は、拡張機能やロードルールなどを構成する際に利用できます。DLE値に基づいてアプリ内のパーソナライゼーションを行うために、Webビューとモバイルアプリの間で通信するには[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/)が必要です。

[Swift向けVisitorServiceモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/visitor-service/)は、訪問プロファイルもデータレイヤーに追加します。