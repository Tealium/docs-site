---
title: Tealium Collectのインストール
description: Tealium Collectのインストール方法を学びましょう。
url: https://docs.tealium.com/ja/server-side/getting-started/tealium-collect/
---
Tealium Collectは、ウェブサイト、モバイルアプリ、サーバーアプリケーションのサーバーサイドデータ収集の主要な方法です。Tealium Collectは、プラットフォームにより、多くの方法でインストールできます。

## Webとモバイル

![](/images/server-side/tag-management-01.png)

iQタグ管理アカウントを持つお客様は、Tealium Collectタグを使用します。このタグをクライアントサイドのプロファイルに追加すると、Tealium Universal Tagのインストールがサーバーサイドプロファイルのデータソースになります。

Tealium Collectタグは、各イベントトラッキングコールをサーバーサイドプロファイルに送信し、データは訪問プロファイル、オーディエンス、クラウドベースのコネクタ、データストレージソリューションに処理されます。

[クライアントサイドプロファイルでTealium Collectタグを構成する方法]()を学びましょう。

タグマネージャーをまだ使用していない場合でも、Tealium iQタグ管理とTealium Collectタグの基本的な構成を使用することをお勧めします。

モバイルプロファイルの場合、アプリ内でTealium Collectモジュールを使用することをお勧めします。

[モバイルアプリ内で直接Tealium Collectをインストールする方法](/ja/platforms/getting-started-mobile/server-side/)について詳しく学びましょう。

## サーバーアプリケーション

iQタグ管理を通じて管理されていない他のプラットフォームについては、サーバーサイドプロファイルにデータを送信するためのインストールライブラリを提供しています。

人気のあるサーバーアプリプラットフォームには以下のものがあります：

* [Python](/ja/platforms/python/)
* [Node](/ja/platforms/node/)
* [C#](/ja/platforms/csharp/)
* [Java](/ja/platforms/java/)
* [HTTP API](/ja/platforms/http-api/)

## Google Tag Manager

### Tealium Collectと一緒に

Google Tag Managerを使用しており、データレイヤーとイベントトラッキングに満足している場合、Google Tag Manager用のTealium Collectタグをデプロイすることをお勧めします。Tealium Collectタグは、Google Tag Managerによって処理されたすべてのデータ、完全な`dataLayer`オブジェクトを含む、直接AudienceStreamに送信します。

インストールコンポーネント：

* [Google Tag Manager用Tealium Collect](/ja/platforms/google-tag-manager/)

### Tealium Universalタグと一緒に

Google Tag Managerを使用してベンダーをデプロイすることを好む場合、またはGoogle Tag Managerの実装がビジネスにとって重要な行動やデータポイント、例えばコンバージョンファネルの活動やeコマースのチェックアウトステップを追跡していない場合、Tealium UniversalタグをGoogle Tag ManagerのカスタムHTMLタグとしてデプロイすることをお勧めします。Tealium Universalタグをデプロイすることで、iQタグ管理の全ての利点を活用し、高度なイベントトラッキングと補足的なデータレイヤー変数を完全に実装することができます。

このアプローチは、iQタグ管理をデプロイする利点を提供し、Google Tag Managerの既存のイベントトラッキングを利用してインストールを迅速化する能力も提供します。

インストールコンポーネント：

* [Tealium iQタグ管理](/ja/iq-tag-management/)
* [Google Tag ManagerのカスタムHTMLタグ](https://support.google.com/tagmanager/answer/6107167?hl=en)
