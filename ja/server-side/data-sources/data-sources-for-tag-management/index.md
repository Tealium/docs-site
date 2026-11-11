---
title: タグ管理向けデータソース
description: この記事では、既存のタグ管理アカウントでデータソースを使用する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/data-sources-for-tag-management/
---
## タグ管理でのデータソースの仕組み

データソースを使用するには、Tealium Collectをインストールする必要があります。WebサイトまたはモバイルアプリにTealiumをすでにインストールしているタグ管理アカウントの場合は、Tealium Collectタグまたはモバイル向けTealium Collectモジュールのいずれかをインストールします。

これらのTealium Collectインストール環境のいずれかにデータソースを接続するには、Tealium Collectタグの構成またはモバイルコードで**データソースキー**を構成する必要があります。

まだ作成していない場合は、タグ管理アカウント用の[データソースを作成](https://docs.tealium.com/create-data-source/)し、一意のデータソースキー値をコピーしてから、次のいずれかの方法に進みます。

* [単一サイトプロファイル](#single-site-profiles)
* [複数サイトプロファイル](#multi-site-profiles)
* [タグ管理モジュールとTealium Collectタグを使用するモバイルプロファイル](#tag-management-module-with-the-tealium-collect-tag)
* [Tealium Collectモジュールを使用するモバイルプロファイル](#tealium-collect-module)

## 単一サイトプロファイル

単一サイトプロファイルは、1つのWebプロパティにデプロイされているプロファイルです。プロファイルをデータソースに接続するには、有効なTealium Collectタグが必要です。

Tealium Collectタグにデータソースキーを追加するには、次の手順を実行します。

1. タグ管理でTealium Collectタグを追加します。  
      
<blockquote>
Tealium Collectタグをすでに使用している場合は、[最新バージョンであることを確認してください](https://docs.tealium.com/template-status-checker/)。
</blockquote>

1. 次の例のように、タグの構成にある**データソースキー**フィールドにデータソースキーを貼り付けます。  
      ![](https://docs.tealium.com/images/server-side/iq-data-source-key.jpg)
1. 変更を保存してパブリッシュします。

## 複数サイトプロファイル

複数サイトプロファイルは、複数のWebプロパティ（複数のドメインなど）にデプロイされ、サイトに基づいて値を動的に構成するよう構成されているプロファイルです。

最初に、クライアント側プロファイルが使用されているWebプロパティごとに、タグ管理データソースを作成する必要があります。これらのデータソースをクライアント側プロファイルが使用されている各サイトに接続するには、**ルックアップテーブル**拡張機能を使用し、サイト名またはドメインに基づいてデータレイヤー変数`tealium_datasource`を構成します。これにより、Tealium Collectタグで正しいデータソースキーが使用されます。


<blockquote>
Tealium Collectタグでは`tealium_datasource`変数が自動的に使用されるため、データマッピングは必要ありません。
</blockquote>


複数のデータソースキーをTealium Collectタグに追加するには、次の手順を実行します。

1. ルックアップテーブル拡張機能を追加します。
1. **検索値**を`domain`（またはサイトを相互に区別できる別の変数）に構成します。
1. **宛先**を`tealium_datasource`に構成します（まだ存在しない場合は、**+**ボタンをクリックして追加します）。
1. 各サイトで想定される値を**ルックアップ一致**フィールドに入力します。
1. 対応するデータソースキーを**出力**フィールドに入力します。
1. 変更を保存してパブリッシュします。

Tealium Collectタグでは、トラッキング呼び出しに`tealium_datasource`属性が自動的に含まれます。その値は、ルックアップテーブルの出力に基づいて動的に構成されます。

![](https://docs.tealium.com/images/server-side/datasourcekey-lookup-table.jpg)

## モバイルプロファイル

モバイルプロファイルは、Tealium for iOSまたはTealium for Androidのインストール環境で使用されます。モバイルのクライアント側プロファイルをAndroidまたはiOS向けのサーバー側データソースに接続するには、Tealium Collectモジュール、または有効なTealium Collectタグを備えたタグ管理モジュールのいずれかを有効にする必要があります。

### タグ管理モジュールとTealium Collectタグ

ネイティブのタグ管理モジュールとTealium Collectタグを使用するモバイル向けクライアント側プロファイルでは、[単一サイトプロファイル](#single-site-profiles)と同じ手順に従います。

### Tealium Collectモジュール

ネイティブのTealium Collectモジュールを使用するモバイル向けクライアント側プロファイルでは、初期化時にデータソースキーが含まれるようにモバイルライブラリのコードを更新する必要があります。この変更を行うには、選択したモバイルデータソースプラットフォームのインストール手順に従ってください。


<blockquote>
別の方法として、Tealium Collectモジュールを無効にしてタグ管理モジュールを有効にし、Tealium Collectタグを追加してから、[単一サイトプロファイル](#single-site-profiles)と同じ手順に従うこともできます。
</blockquote>
