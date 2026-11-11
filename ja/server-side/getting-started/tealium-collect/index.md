---
title: Tealium Collectのインストール
description: Tealium Collectのインストール方法について説明します。
url: https://docs.tealium.com/ja/server-side/getting-started/tealium-collect/
---
Tealium Collectは、Webサイト、モバイルアプリ、サーバーアプリケーション向けのサーバーサイドデータ収集における主要な方法です。Tealium Collectは、プラットフォームに応じてさまざまな方法でインストールできます。

## Webとモバイル

![](https://docs.tealium.com/images/server-side/tag-management-01.png)

タグ管理アカウントをご利用のお客様は、Tealium Collectタグを使用してください。このタグをクライアントサイドプロファイルに追加すると、Tealium Universal Tagの実装がサーバーサイドプロファイルのデータソースになります。

Tealium Collectタグは、各イベントトラッキング呼び出しをサーバーサイドプロファイルに送信します。そこでデータが処理され、訪問プロファイル、オーディエンス、クラウドベースのコネクタ、データ保存ソリューションに反映されます。

[クライアントサイドプロファイルでTealium Collectタグを構成する方法](https://docs.tealium.com/data-sources-for-tag-management/)をご覧ください。



<blockquote>
タグマネージャーをまだ使用していない場合でも、タグ管理の基本構成とTealium Collectタグを使用することをお勧めします。
</blockquote>


モバイルプロファイルでは、アプリ内でTealium Collectモジュールを使用することをお勧めします。

[Tealium Collectをモバイルアプリに直接インストールする方法](https://docs.tealium.com/ja/platforms/getting-started-mobile/server-side/)の詳細をご覧ください。

## サーバーアプリケーション

タグ管理で管理されていないその他のプラットフォーム向けに、サーバーサイドプロファイルへデータを送信するためのインストールライブラリを提供しています。

一般的なサーバーアプリケーションプラットフォームは次のとおりです。

* [Python](https://docs.tealium.com/ja/platforms/python/)
* [Node](https://docs.tealium.com/ja/platforms/node/)
* [C#](https://docs.tealium.com/ja/platforms/csharp/)
* [Java](https://docs.tealium.com/ja/platforms/java/)
* [HTTP API](https://docs.tealium.com/ja/platforms/http-api/)

## Googleタグマネージャー

### Tealium Collectを使用する場合

Googleタグマネージャーを使用しており、現在のデータレイヤーとイベントトラッキングに満足している場合は、Googleタグマネージャー用Tealium Collectタグをデプロイすることをお勧めします。Tealium Collectタグは、完全な`dataLayer`オブジェクトを含め、Googleタグマネージャーで処理されたすべてのデータを顧客データプラットフォーム（CDP）へ直接送信します。

インストールコンポーネント：

* [Googleタグマネージャー用Tealium Collect](https://docs.tealium.com/ja/platforms/google-tag-manager/)

### Tealium Universal Tagを使用する場合

Googleタグマネージャーを使用してベンダーをデプロイする場合は、GoogleタグマネージャーのカスタムHTMLタグとしてTealium Universal Tagをデプロイすることをお勧めします。この方法は、コンバージョンファネルのアクティビティやEコマースのチェックアウト手順など、ビジネスに不可欠な行動やデータポイントをGoogleタグマネージャーの実装でトラッキングしていない場合にも推奨されます。Tealium Universal Tagをデプロイすると、タグ管理の機能を最大限に活用し、高度なイベントトラッキングと補足的なデータレイヤー変数を完全に実装できます。

この方法では、タグ管理をデプロイする利点に加えて、Googleタグマネージャーの既存のイベントトラッキングを利用して、インストールを迅速化できます。

インストールコンポーネント：

* [タグ管理](https://docs.tealium.com/ja/tag-management/)
* [GoogleタグマネージャーのカスタムHTMLタグ](https://support.google.com/tagmanager/answer/6107167?hl=en)