---
title: iQタグ管理のデータソース
description: この記事では、既存のiQタグ管理アカウントでデータソースを使用する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/data-sources-for-iq-tag-management/
---
## iQタグ管理とデータソースの連携方法

データソースを使用するには、Tealium Collectのインストールが必要です。iQタグ管理アカウントでは、すでにウェブサイトやモバイルアプリにTealiumをインストールしている場合、Tealium Collectタグまたはモバイル用のTealium Collectモジュールをインストールします。

これらのTealium Collectインストールにデータソースを接続するには、**データソースキー**を構成する必要があります。これは、Tealium Collectタグの構成またはモバイルコード内で構成します。

まだ行っていない場合は、iQタグ管理アカウントの[データソースを作成]()し、一意のデータソースキー値をコピーしてから、以下の方法のいずれかを進めてください：

* [シングルサイトプロファイル](#single-site-profiles)
* [マルチサイトプロファイル](#multi-site-profiles) 
* [タグ管理モジュールとTealium Collectタグを使用したモバイルプロファイル](#tag-management-module-with-the-tealium-collect-tag)
* [Tealium Collectモジュールを使用したモバイルプロファイル](#tealium-collect-module)

## シングルサイトプロファイル

シングルサイトプロファイルは、1つのウェブプロパティにデプロイされています。プロファイルをデータソースに接続するには、アクティブなTealium Collectタグが必要です。

Tealium Collectタグにデータソースキーを追加するには：

1. iQタグ管理で、Tealium Collectタグを追加します。  
      すでにTealium Collectタグを持っている場合は、[最新バージョンであることを確認]()してください。
1. タグ構成の**Data Source Key**フィールドにデータソースキーを貼り付けます。ここに示すように：  
      ![](/images/server-side/iq-data-source-key.jpg)
1. 変更を保存し、公開します。

## マルチサイトプロファイル

マルチサイトプロファイルは、複数のウェブプロパティ（例えば、複数のドメイン）にデプロイされ、サイトに基づいて動的に値を構成するように構成されています。

始めるには、クライアントサイドプロファイルがサービスする各ウェブプロパティに対してiQタグ管理データソースを作成する必要があります。これらのデータソースをクライアントサイドプロファイルがサービスする各サイトに接続するには、**Lookup Table**拡張機能を使用して、サイト名またはドメインに基づいてデータレイヤー変数`tealium_datasource`を構成します。これにより、Tealium Collectタグが正しいデータソースキーを使用することが保証されます。

データマッピングは必要ありません。なぜなら、Tealium Collectタグは自動的に`tealium_datasource`変数を使用するからです。

Tealium Collectタグに複数のデータソースキーを追加するには：

1. Lookup Table拡張機能を追加します。
1. **Lookup Value In**を`domain`（またはあなたのサイトを互いに区別する別の変数）に構成します。
1. **Destination**を`tealium_datasource`に構成します（まだ存在しない場合は、**&#43;**ボタンをクリックして追加します）。
1. **Lookup Match**フィールドに各サイトの予想値を入力します。
1. **Output**フィールドに一致するデータソースキーを入力します。
1. 変更を保存し、公開します。

Tealium Collectタグは自動的にトラッキングコールに`tealium_datasource`属性を含めます。その値はLookup Tableの出力に基づいて動的に構成されます。

![](/images/server-side/datasourcekey-lookup-table.jpg)

## モバイルプロファイル

モバイルプロファイルは、Tealium for iOSまたはTealium for Androidのインストールに使用されます。モバイルのクライアントサイドプロファイルをAndroidまたはiOSのサーバーサイドデータソースに接続するには、Tealium CollectモジュールまたはアクティブなTealium Collectタグを持つタグ管理モジュールを有効にする必要があります。

### タグ管理モジュールとTealium Collectタグ

ネイティブのタグ管理モジュールとTealium Collectタグを使用するモバイルのクライアントサイドプロファイルは、[シングルサイトプロファイル](#single-site-profiles)のプロセスと同じです。

### Tealium Collectモジュール

ネイティブのTealium Collectモジュールを使用するモバイルのクライアントサイドプロファイルは、初期化時にデータソースキーを含めるようにモバイルライブラリコードを更新する必要があります。選択したモバイルデータソースプラットフォームのインストール手順に従ってこの変更を行ってください。

代わりに、Tealium Collectモジュールを無効にし、タグ管理モジュールを有効にし、Tealium Collectタグを追加し、[シングルサイトプロファイル](#single-site-profiles)のプロセスを同じように進めることもできます。