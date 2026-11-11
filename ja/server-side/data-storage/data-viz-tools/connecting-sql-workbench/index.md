---
title: SQL Workbench/Jへの接続
description: このガイドでは、SQL Workbench/Jをダウンロードしてインストールし、DataAccessアカウントに関連付けられたデータベースへ接続する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/data-viz-tools/connecting-sql-workbench/
---
SQL Workbench/Jは、使いやすく、PostgreSQLやMySQLなどの多くのデータベース管理システム（DBMS）に接続できる無料のクエリツールです。SQL Workbench/Jを使用すると、データベースへの接続、データベーススキーマの表示、データの分析をすばやく簡単に行うことができます。

## インストールとセットアップ

### ダウンロードとインストール

以下の手順では、SQL WorkbenchとAmazon Redshift JDBCドライバーをダウンロードする方法について説明します。

1. [SQL Workbench](http://www.sql-workbench.net/getting-started.html)をダウンロードしてインストールします。
1. [Amazon Redshift JDBCドライバー](https://docs.aws.amazon.com/redshift/latest/mgmt/jdbc20-install-driver.html)をダウンロードしてインストールします。
1. `.jar`ファイルをコンピューター上の安全な場所に保存します。  
このファイルを削除すると、接続できなくなります。

### ドライバーの構成

データベースに接続する前に、Amazon Redshift JDBCドライバーをSQL Workbenchにインストールする必要があります。  
以下の手順では、Amazon Redshift JDBCドライバーをインストールする方法について説明します。

1. **SQL Workbench/J**を開きます。
2. 画面左下の**ドライバーの管理（Manage Drivers）**をクリックします。
3. **新しいエントリを作成（Create a new entry）**アイコンをクリックします。  
![](https://docs.tealium.com/images/server-side/sql-workbench-create-driver.jpg)
4. **名前（Name）**フィールドに`Redshift`と入力します。
5. ライブラリのテキスト領域の右側にある**フォルダー**アイコンをクリックします。  
![](https://docs.tealium.com/images/server-side/sql-workbench-folder.jpg)
6. ドライバーの保存場所に移動してドライバーを選択し、**開く（Open）**をクリックします。  
**クラス名（Classname）**フィールドが`com.amazon.redshift.jdbc_41_.Driver`に構成されます。ここで、`41`はドライバーのバージョンを示します。
7. **OK**をクリックして終了します。  
これでRedshiftデータベースが構成されました。

### 接続プロファイルの作成

以下の手順では、Tealiumデータベースへの接続認証情報をSQL Workbenchに入力し、接続プロファイルを作成する方法について説明します。

1. **SQL Workbench/J**インターフェイスで、**新しい接続プロファイルを作成（Create a new connection profile）**アイコンをクリックします。  
![](https://docs.tealium.com/images/server-side/sql-workbench-connection-profile.jpg)
2. 新しいプロファイルの名前を入力します。たとえば、`mycompany-main`のように、Tealiumのアカウント名とプロファイル名を組み合わせた名前を使用します。
3. **ドライバー（Driver）**ドロップダウンリストで、`Amazon Redshift JDBC Driver (com.amazon.redshift.jdbc41.Driver)`を選択します。  
  ![](https://docs.tealium.com/images/server-side/sql-workbench-connection-profile.jpg)
4. Tealiumアカウントで、**Store > EventDB**または**Store > AudienceDB**に移動します。
5. **DB接続の詳細を取得（Get DB Connection Details）**をクリックします。  
  **DB接続の詳細（DB Connection Detail）**ダイアログが表示されます。以降の手順を進める間、このウィンドウを開いたままにします。次の例では、機密保持のために認証情報が削除されています。  
    ![](https://docs.tealium.com/images/server-side/sql-workbench-connection-details.jpg)
6. SQL Workbenchに戻り、次の例に基づいてURLを入力します。`HOST`、`PORT`、`DATABASE`は、DataAccessの接続値に置き換えてください：`jdbc:redshift://HOST:PORT/DATABASE?ssl=true`。  
    ![](https://docs.tealium.com/images/server-side/sql-workbench-connection-url.jpg)
7. 認証情報を使用して、**ユーザー名（Username）**と**パスワード（Password）**を入力します。
8. **自動コミット（Autocommit）**チェックボックスをオンにします。  
      ![](https://docs.tealium.com/images/server-side/sql-workbench-connection-autocommit.jpg)
9. **プロファイルリストを保存（Save Profile List）**アイコンをクリックして保存します。  
        ![](https://docs.tealium.com/images/server-side/sql-workbench-connection-save.jpg)
10. **OK**をクリックして接続を試行します。

接続に成功すると、**ステートメント（Statement）**ページが表示されます。ここから、データをクエリするスクリプトの作成を開始できます。

EventDBまたはAudienceDBを最近有効にした場合、データが利用可能になるまで最大1時間かかることがあります。

### トラブルシューティング

以下のセクションでは、一般的なエラーとトラブルシューティングのヒントについて説明します。

#### 一般的なエラー

* **Redshift JARファイルの削除**  
  Redshift JARファイルを削除すると、接続できなくなります。ホームフォルダーなどの安全な場所に必ず保存してください。
* **ユーザー名とデータベース名の混同**
    * ユーザー名には`account_profile`が含まれます。
    * データベース名はTealiumのアカウント名です。
* **自動コミットチェックボックスをオンにしていない**  
  保存前に**自動コミット（Autocommit）**チェックボックスをオンにしなかった場合、接続インスタンスごとに1つのクエリしか実行できません。

#### ヒント

* **パスワードの表示**  
  パスワードを確認する必要がある場合は、SQL Workbench/Jのパスワード入力フィールドの横にある**パスワードを表示（Show password）**をクリックします。  
  ![](https://docs.tealium.com/images/server-side/sql-workbench-show-password.jpg)
* **EventDBのイベントフィードを有効にする**  
  EventDBを使用するには、EventDBに送信するイベントフィードを有効にする必要があります。詳細については、[イベントフィード](https://docs.tealium.com/about-event-feeds/)を参照してください。
* **AudienceDBの属性を有効にする**  
  AudienceDBを使用するには、AudienceDBに送信する属性を有効にする必要があります。詳細については、[AudienceDBへの属性の追加](https://docs.tealium.com/audiencedb-and-eventdb/#adjust-audiencedb-attributes)を参照してください。
    * 上記の手順を完了しない場合、多数の`visit_`および`visitor_`テーブルとビューが表示されますが、そこには基本的な訪問レベルのデータとオーディエンスしか含まれません。属性データは含まれません。
    * AudienceDBの属性数には250個というソフトリミットがあります。この数に達すると、パフォーマンスが低下する可能性があります。

## SQL Workbenchの使用

SQL Workbench/Jの接続プロファイルを作成したら、データのクエリを開始できます。このドキュメントの手順に従って開始してください。まず、データの列名と、テーブルおよびリストスキーマが何を表しているかを確認します。

接続やデータスキーマのサポートに関するその他の質問については、Tealiumのアカウントマネージャーにお問い合わせください。クエリのサポート、データのエクスポート、ビジネスインテリジェンス（BI）ツールへの統合についてさらに支援が必要な場合は、データサイエンティストやデータベース管理者など、チームの担当者にお問い合わせください。

以下のセクションでは、SQL Workbench/Jインターフェイスで最もよく使用される画面の概要を説明します。

### ステートメント

SQL Workbench/Jインターフェイスで**ステートメント（Statements）**タブをクリックすると、SQLステートメントを記述し、結果やエラーメッセージを確認できます。

![](https://docs.tealium.com/images/server-side/whiteui-dataaccess-running-queries-on-audiencedb-event-db-using-sql-workbench:j-statement-editor.jpg)
### データベースエクスプローラー

SQL Workbench/J のインターフェイスから **Database Explorer** に移動し、利用可能なデータを確認します。

![](https://docs.tealium.com/images/server-side/whiteui-dataaccess-running-queries-on-audiencedb-eventdb-using-sql-workbenchj.jpg)

左側のパネルには、Redshift インスタンス内でアクセス可能なテーブルとビューが表示されます。各テーブルまたはビューには、それぞれ異なるデータが格納されています。クエリを正しく作成するには、`udo_job_role` など、クエリで使用可能な列名を把握しておく必要があります。右側のペインでは、データの列名を確認しながらクエリを作成できます。

* **テーブル**  
テーブルは、データベースにデータを格納する標準的な方法です。テーブル数は、EventDB と AudienceDB で有効になっているフィルタ済みストリームの数によって異なります。
* **ビュー**  
各テーブルには、対応するビューがあります。ビューでは、テーブルの列がより人間にとって読みやすい形式で表示されます。
* **例**
    * テーブルでは `tags_main_1_executed` と表示されるのに対し、ビューでは `event - tags - tealium collect (main 1) - executed` と表示されます。
    * テーブルでは `udo_job_role` と表示されるのに対し、ビューでは `event - udo - job_role` と表示されます。
* **EventDB での使用**
    * `events__all_events` テーブルには、デフォルトですべてのイベントが格納されます。
    * 各フィルタ済みストリームには、`events__f84fc357_4ded_413d_d28a_de70624ff2d5` などのテーブルが作成されます。
* **AudienceDB での使用**
    * `visit_lists` には、クエリ対象となる現在の訪問スコープのリスト属性が格納されます。
    * `visit_tallies` には、クエリ対象となる現在の訪問スコープの集計属性が格納されます。
    * `visitor_lists` には、クエリ対象となる訪問スコープのリスト属性が格納されます。
    * `visitor_tallies` には、クエリ対象となる訪問スコープの集計属性が格納されます。
    * `visitor_replaces` には、統合された訪問プロファイルが格納されます。
    * `visitors` は最も一般的に使用されるテーブルで、各訪問の最新の訪問スコープデータと、その訪問が属するオーディエンスが格納されます。
    * `visits` には、各訪問の最新の現在の訪問スコープデータが格納されます。
* **制限事項**
    * [ファネル](https://docs.tealium.com/funnel-attribute/)属性と[タイムライン](https://docs.tealium.com/timeline-attribute/)属性はサポートされていません。

### 列名の表示

**Objects** タブをクリックすると、各テーブルまたはビューの列名が表示されます。インターフェイスで使用可能なフィルターを使って、結果を絞り込むことができます。デフォルトでは、`COLUMN_NAME` はアルファベット順に並んでいません。ヘッダー行をクリックすると、名前をアルファベット順に並べ替えられます。

![](https://docs.tealium.com/images/server-side/whiteui-dataaccess-running-queries-on-audencedb-eventdb-using-sql-workbenchj-search-tables-objects-tab.jpg)

### ランダムなサンプルデータの表示

**Search table data** タブをクリックすると、データのランダムなサンプルが表示されます。インターフェイスで使用可能なフィルターを使って、結果を絞り込むことができます。

![](https://docs.tealium.com/images/server-side/whiteui-dataaccess-running-queries-on-audencedb-eventdb-using-sql-workbenchj-search-table-data.jpg)

### 回避すべき一般的なエラー

以下は、回避すべき一般的なエラーです。

* タグ管理（TiQ）のデータレイヤーで、UDO 変数を `utag_data` 内に宣言していない。変数が宣言されていない場合、EventDB には表示されません。
* Customer Data Platform（CDP）属性を AudienceDB に送信する構成を有効にしていない。各属性は手動で選択する必要があります。属性数には 250 個のソフトリミットがあります。さらに多くの列が必要な場合は、Tealium のアカウントマネージャーにお問い合わせください。