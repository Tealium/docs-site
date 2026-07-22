---
title: SQL Workbench/Jへの接続
description: このガイドでは、SQL Workbench/Jをダウンロードしてインストールし、DataAccessアカウントに関連付けられたデータベースに接続する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/data-viz-tools/connecting-sql-workbench/
---
SQL Workbench/Jは、PostgreSQLやMySQLなどの多くのデータベース管理システム（DBMS）に接続できるシンプルで使いやすい無料のクエリツールです。SQL Workbench/Jを使用してデータベースに簡単に接続し、データベーススキーマを表示し、データを分析します。

## インストールと構成

### ダウンロードとインストール

以下の手順では、SQL WorkbenchとAmazon Redshift JDBCドライバのダウンロード方法について説明します：

1. [SQL Workbench](http://www.sql-workbench.net/getting-started.html)をダウンロードしてインストールします。
1. [Amazon Redshift JDBCドライバ](https://docs.aws.amazon.com/redshift/latest/mgmt/jdbc20-install-driver.html)をダウンロードしてインストールします。
1. `.jar`ファイルをコンピュータの安全な場所に保存します。
このファイルを削除すると、接続が切断されます。

### ドライバのビルド

Amazon Redshift JDBCのドライバは、データベースに接続する前にSQL Workbenchにインストールする必要があります。
以下の手順では、Amazon Redshift JDBCドライバのインストール方法について説明します：

1.  **SQL Workbench/J**を開きます。
2.  画面の左下にある**ドライバの管理**をクリックします。
3.  **新しいエントリを作成**アイコンをクリックします。  
![](https://docs.tealium.com/images/server-side/sql-workbench-create-driver.jpg)
4.  **名前**フィールドに`Redshift`と入力します。
5.  ライブラリテキストエリアの右側にある**フォルダ**アイコンをクリックします。  
![](https://docs.tealium.com/images/server-side/sql-workbench-folder.jpg)
6.  ドライバの場所に移動し、それをクリックして選択し、**開く**をクリックします。  
**クラス名**フィールドは、`41`がドライババージョンを示す`com.amazon.redshift.jdbc_41_.Driver`に構成されます。
7.  **OK**をクリックして終了します。  
これで、Redshiftデータベースが構成されました。

### 接続プロファイルの作成

以下の手順では、SQL Workbenchに接続資格情報を提供して接続プロファイルを作成する方法について説明します：

1.  **SQL Workbench/J**インターフェースで、**新しい接続プロファイルを作成**アイコンをクリックします。  
![](https://docs.tealium.com/images/server-side/sql-workbench-connection-profile.jpg)
2.  新しいプロファイルに名前を付けます。例えば、Tealiumアカウントとプロファイルを組み合わせた名前、`mycompany-main`など。
3.  **ドライバ**ドロップダウンリストから`Amazon Redshift JDBC Driver (com.amazon.redshift.jdbc41.Driver)`を選択します。  
  ![](https://docs.tealium.com/images/server-side/sql-workbench-connection-profile.jpg)
4.  Tealiumアカウントで、**Store > EventDB**または**Store > AudienceDB**に移動します。
5.  **DB接続詳細を取得**をクリックします。  
  **DB接続詳細**ダイアログが表示されます。このウィンドウを開いたまま進行します。以下の例では、機密性を保つために資格情報が削除されています。  
    ![](https://docs.tealium.com/images/server-side/sql-workbench-connection-details.jpg)
6.  SQL Workbenchに戻り、DataAccessからの接続値で`HOST`、`PORT`、`DATABASE`を置き換えた以下の例に基づいたURLを入力します：`jdbc:redshift://HOST:PORT/DATABASE?ssl=true`。  
    ![](https://docs.tealium.com/images/server-side/sql-workbench-connection-url.jpg)
7.  資格情報を使用して**ユーザ名**と**パスワード**を入力します。
8.  **Autocommit**チェックボックスをチェックします。  
      ![](https://docs.tealium.com/images/server-side/sql-workbench-connection-autocommit.jpg)
9.  **プロファイルリストを保存**アイコンをクリックして保存します。  
        ![](https://docs.tealium.com/images/server-side/sql-workbench-connection-save.jpg)
10.  **OK**をクリックして接続を試みます。  

成功すると、**ステートメント**ページが表示されます。ここから、データをクエリするスクリプトの作成を開始できます。  

EventDBまたはAudienceDBを最近有効にした場合、データが利用可能になるまでに最大1時間かかる場合があります。

### トラブルシューティング

以下のセクションでは、一般的なエラーとトラブルシューティングのヒントについて情報を提供します。

#### 一般的なエラー
*   **Redshift JARファイルの削除**  
  Redshift JARファイルが削除されると、接続が切断されます。ホームフォルダなど、安全な場所に保存しておくようにしてください。
*   **ユーザ名とデータベース名の混同**
    *   ユーザ名には`account_profile`が含まれています。
    *   データベースはTealiumアカウント名です。
*   **Autocommitチェックボックスをチェックしない**  
  保存する前に**Autocommit**チェックボックスをチェックしないと、接続インスタンスごとに1つのクエリしか行えません。

#### ヒント
*   **パスワードの表示**  
  パスワードを表示する必要がある場合は、SQLWorkbench/Jのパスワード入力フィールドの隣にある**パスワードを表示**をクリックします。  
  ![](https://docs.tealium.com/images/server-side/sql-workbench-show-password.jpg)
*   **EventDBのイベントフィードを有効にする**  
  EventDBでは、EventDBに送信するイベントフィードを有効にする必要があります。詳細については、[イベントフィード](https://docs.tealium.com/about-event-feeds/)を参照してください。
*   **AudienceDBの属性を有効にする**  
  AudienceDBでは、AudienceDBに送信する属性を有効にする必要があります。詳細については、[AudienceDBへの属性の追加](https://docs.tealium.com/audiencedb-and-eventdb/#adjust-audiencedb-attributes)を参照してください。
    *   上記の手順を完了しないと、基本的な訪問レベルのデータとオーディエンスのみを含む多くの`visit_`と`visitor_`テーブルとビューが表示されます。属性データは含まれません。
    *   AudienceDBには250属性のソフトリミットがあります。この数に達すると、パフォーマンスが低下する可能性があります。


## SQL Workbenchの使用

SQL Workbench/Jの接続プロファイルを作成したら、データのクエリを開始する準備が整いました。このドキュメントに従って開始します。まず、データ列名とテーブルとリストスキーマが何を表しているかを学びます。

接続とデータスキーマサポートに関する追加の質問がある場合は、Tealiumアカウントマネージャーに連絡してください。クエリサポート、データエクスポート、ビジネスインテリジェンス（BI）ツールへの統合に関する追加のヘルプが必要な場合は、データサイエンティストやデータベース管理者などのチームメンバーに連絡してください。

以下のセクションでは、SQL Workbench/Jインターフェースで最もよく使用される画面についての一般的な情報を提供します。

### ステートメント

SQL Workbench/Jインターフェースから、**ステートメント**タブをクリックしてSQLステートメントを作成し、結果やエラーメッセージを表示します。

![](https://docs.tealium.com/images/server-side/whiteui-dataaccess-running-queries-on-audiencedb-event-db-using-sql-workbench:j-statement-editor.jpg)

### データベースエクスプローラ

SQL Workbench/Jインターフェースから、**データベースエクスプローラ**に移動して利用可能なデータを確認します。

![](https://docs.tealium.com/images/server-side/whiteui-dataaccess-running-queries-on-audiencedb-eventdb-using-sql-workbenchj.jpg)

左パネルには、Redshiftインスタンス内でアクセス可能なテーブルとビューが表示されます。各テーブルやビューには異なるデータが含まれています。クエリを正しく構築するためには、クエリ可能な列名、例えば`udo_job_role`などを知る必要があります。右パネルは、データ列名をナビゲートし、クエリを構築するのに役立ちます。

* **テーブル**  
テーブルは、データベースでデータを格納するための標準的な方法です。テーブルの数は、EventDBとAudienceDBで有効にしたフィルタリングされたストリームの数によります。
* **ビュー**  
各テーブルには対応するビューがあります。ビューは、テーブル列のより人間が読みやすいバージョンを提供します。
* **例**
    * テーブルは`tags_main_1_executed`を表示しますが、ビューは`event - tags - tealium collect (main 1) - executed`を表示します。
    * テーブルは`udo_job_role`を表示しますが、ビューは`event - udo - job_role`を表示します。
* **EventDBでの使用**
    * `events__all_events`テーブルは、デフォルトですべてのイベントを保持します。
    * それぞれのフィルタリングされたストリームにはテーブルがあります。例えば`events__f84fc357_4ded_413d_d28a_de70624ff2d5`など。
* **AudienceDBでの使用**
    * `visit_lists`には、クエリのための現在の訪問スコープのリスト属性が含まれています。
* `visit_tallies`は、クエリのための現在の訪問範囲の集計属性を含みます。
    * `visitor_lists`は、クエリのための訪問範囲のリスト属性を含みます。
    * `visitor_tallies`は、クエリのための訪問範囲の集計属性を含みます。
    * `visitor_replaces`は、ステッチされた訪問プロファイルを含みます。
    * `visitors`は最も一般的に使用されるテーブルで、各訪問と彼らが所属する任意のオーディエンスの最新の訪問範囲のデータを含みます。
    * `visits`は、各訪問の最新の訪問範囲のデータを含みます。
* **制限事項**
    * [ファネル](https://docs.tealium.com/funnel-attribute/)と[タイムライン](https://docs.tealium.com/timeline-attribute/)の属性はサポートされていません。

### 列名の表示

**オブジェクト**タブをクリックして、各テーブルまたはビューの列名を表示します。インターフェースの利用可能なフィルタを使用して結果を微調整できます。デフォルトでは、`COLUMN_NAME`はアルファベット順ではありません。ヘッダー行をクリックして名前をアルファベット順に並べ替えます。

![](https://docs.tealium.com/images/server-side/whiteui-dataaccess-running-queries-on-audencedb-eventdb-using-sql-workbenchj-search-tables-objects-tab.jpg)

### ランダムなサンプルデータの表示

**テーブルデータの検索**タブをクリックして、ランダムなデータのサンプルを表示します。インターフェースの利用可能なフィルタを使用して結果を微調整できます。

![](https://docs.tealium.com/images/server-side/whiteui-dataaccess-running-queries-on-audencedb-eventdb-using-sql-workbenchj-search-table-data.jpg)

### 避けるべき一般的なエラー

以下の項目は、避けるべき一般的なエラーとして注意されています：

* iQタグ管理（TiQ）データレイヤー内の`utag_data`でUDO変数を宣言しないこと。変数が宣言されていない場合、それらはEventDBに表示されません。
* AudienceStream属性をAudienceDBに送信するように構成しないこと。各属性は手動で選択する必要があります。属性のソフトリミットは250です。もしもっと多くの列が必要な場合は、Tealiumのアカウントマネージャーに連絡してください。