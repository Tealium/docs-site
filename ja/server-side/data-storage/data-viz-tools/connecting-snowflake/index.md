---
title: Snowflakeへの接続
description: この記事では、Snowflake Webインターフェースを使用してTealiumデータをSnowflakeにロードする方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/data-viz-tools/connecting-snowflake/
---
この記事はSnowflake Webインターフェースとデータロードウィザードに焦点を当てており、Snowflakeコマンドラインツールの概要を提供します。Snowflakeの使用に関する詳細情報については、[Snowflakeドキュメント](https://docs.snowflake.net/manuals/index.html)を参照してください。

## 動作原理

Tealium DataAccessの顧客は、Snowflake Webインターフェースを使用して、データを外部ソリューションに接続し、高度なクエリとデータ分析を行うことができます。Webインターフェースは直感的なウィザードを提供し、限られた量のデータを小さなフラットファイルのセットからテーブルにロードすることができます。このプロセスでは、PUTおよびCOPYコマンドを使用してデータをロードし、ステージングファイルとデータロードフェーズを一つの操作に統合することで、データロードプロセスを簡素化します。

Webインターフェースは、ファイルの数が少ない（最大50 MB）場合に適しています。この制限は、ハードウェア、ブラウザの種類、およびブラウザのバージョンによってブラウザのパフォーマンスが異なるため、最適なパフォーマンスを保証するためです。

## 前提条件

Tealiumが発行したAmazon S3バケットからDataAccessデータを接続するためには、以下の項目が必要です：

* AudienceStoreおよびEventStoreが有効になっているTealium DataAccess  
データがDataAccessバケットに配信されるように、AudienceStream内でAudienceStoreコネクタを構成する必要があります。AudienceStreamの構成についての詳細は、Tealiumの[AudienceStore構成ガイド]()を参照してください。
* EventStoreおよび/またはAudienceStore用の有効なTealium DataAccess認証情報。

## はじめに

次のセクションでは、SnowflakeデータロードWebインターフェースを使用してソースファイルを選択し、TealiumデータをSnowflakeにロードする手順を案内します。

DataAccessデータをJSONファイルの半構造化の性質に対応し、スキーマ要件を強制しないバリアントデータ型のテーブルにロードすることをお勧めします。データがロードされた後の解析に関する追加情報とヒントについては、このドキュメントのベストプラクティスセクションを参照してください。

### データロードウィザードを開く

データロードウィザードを開くには、次の手順に従います：

1. Snowflakeアカウントにログインします。
1. **Databases &gt; Tables**をクリックします。
1. 次のいずれかを行います：  
      * テーブル行をクリックして選択し、**Load Data**ボタンをクリックします。
      * テーブル名をクリックしてテーブルの詳細ページを開き、**Load Table**ボタンをクリックします。

1. ロードデータウィザードが表示されます。
1. 次のセクションに進み、DataAccessからソースファイルを選択して、選択したテーブルにデータのロードを開始します。

### DataAccessからソースファイルを選択する

ソースファイルを選択するように求められた場合、AWS S3にあるTealium DataAccessデータ用に新しいステージを作成します。

Tealium DataAccessからソースファイルを選択するには、次の手順に従います：

1. **Existing Amazon S3 Location**を選択します。
1. **Next**をクリックします。  
      ![](/images/server-side/snowflake-create-stage.jpg)
1. 次のセクションに進み、DataAccess認証情報を入力します。

### DataAccess認証情報を入力する

DataAccess認証情報を入力するには、次の手順に従います：

1. まだ行っていない場合は、EventStoreまたはAudienceStoreのDataAccess認証情報を取得します。  
認証情報はEventStoreとAudienceStoreの両方で同じです。  
      認証情報がすでに生成されている場合、Secret Access Keyは表示されません。既存のキーを取得するか、新しいキーを再生成する必要があるかを同僚と協議してください。

1. 有効な認証情報を取得したら、次のフィールドに入力します：  
    * **Access Key**  
    Tealiumが提供するAccess Key IDを入力します。例：`AKIA****************`
    * **Secret Key**  
    Tealiumが提供するSecret Access Keyを入力します。
    * **Bucket**  
    Tealiumのパスフィールドの最初の値のみを入力します。例：  
    Tealium Pathが：`/dataaccess-us-east-1.tealiumiq.com/myaccount/main`の場合  
    入力する値：`dataaccess-us-east-1.tealiumiq.com`（スラッシュなし）。
    * **Prefix**  
    Tealiumのパスフィールドから、アカウント名で始まりスラッシュ(/)で終わる残りの部分を入力します。  
    例：`myaccount/main/`
    * **Region**  
    バケット名に示されているリージョンを選択します。例：**us-east-1**.

1. 次のセクションに進み、ファイル形式を作成します。

### ファイル形式を作成する

ファイル形式を作成するには、次の手順に従います：

1. ドロップダウンリストの隣にあるプラス（**&#43;**）記号をクリックします。  
ファイル形式作成ダイアログが表示されます。  
      ![](/images/server-side/snowflake-create-file-format.jpg)
1. 次の情報を入力します：
    * 名前フィールドには、DataAccessデータ用に使用するファイル形式の名前を入力します。例：`TEALIUM_JSON`。  
    これは必須フィールドです。
    * ドロップダウンリストからスキーマ名のタイプを選択します。例：**Public**。
    * ドロップダウンリストから形式タイプを選択します。例：**JSON**。
    * ドロップダウンリストから圧縮方法を選択します。例：**Gzip**。
    * 次のいずれかのチェックボックスを選択します：
        * 8進数を有効にする
        * 重複を許可する
        * 外側の配列を削除する
        * Null値を削除する
        * UTF-8エラーを無視する
    * コメントフィールドに、このファイル形式についての説明コメントを入力します。  
    例：TealiumはGzip圧縮ファイルにJSONデータを保存します。

1. **Finish**をクリックします。
1. 次のセクションに進み、データをロードします。

### データをロードする

Webインターフェースを使用して手動でデータをロードするには、以下の手順を続けてください。コマンドラインからデータをロードする方法を選択する場合は、コマンドラインを使用してロードするセクションにスキップしてください。

1. ドロップダウンリストから以前に名前を付けたファイル形式を選択します。  
      ![](/images/server-side/snowflake-manually-load-data-via-web-interface.jpg)
1. **Load**をクリックしてすぐにデータをロードするか、**Next**をクリックして追加のロードオプションを構成します。  
倉庫が現在稼働していない場合、倉庫を再開するのに最大5分かかることがあります。これにはロードに必要な時間も含まれます。
### コマンドラインを使用したロード（オプション）

コマンドラインからデータをロードするには、以下の手順に従ってください：

1. **SnowSQLのインストール**  
コマンドラインからデータをロードする前に、マシンにSnowSQLをインストールする必要があります。[SnowSQLのインストールについての詳細はこちら](https://docs.snowflake.com/en/user-guide/snowsql-install-config.html)。
1. **SnowSQLの構成**  
SnowSQLのインストールが完了したら、Snowflakeインスタンスに接続できるように構成ファイルを編集する必要があります。
    1. 次のディレクトリにある構成ファイルを開きます：  
        * Linux/Mac OSの場合：`~/.snowsql/`
        * Windowsの場合：`%USERPROFILE%\.snowsql\`
    1. 接続セクションを編集して、認証情報を入力します。  
    例：  
          ```bash
          [connections.tealium_example]
          #SnowSqlでtealium_exampleとして接続できます
          accountname = MY_ACCOUNT_NAME
          username = MYUSER
          password = ********************
          ```
    1. 好みに応じてオプションや変数のセクションを変更します。詳細はこちら：[SnowSQLの構成](https://docs.snowflake.com/en/user-guide/snowsql-config.html)。

1. **SnowSQLを通じて接続**  
構成ファイルに接続詳細が保存されたら、シェルコマンドを使用してSnowSQLに接続します。接続名`tealium_example`をあなたのものに置き換えてください：  
`$ snowsql -c tealium_example`  
詳細はこちら：[SnowSQLを通じた接続](https://docs.snowflake.com/en/user-guide/snowsql-start.html)。
1. **COPY INTOコマンドを使用してデータをロード**  
接続されたら、`COPY INTO &lt;table&gt;`コマンドを実行してデータをターゲットテーブルにロードします。以下の例では、前の手順で作成された名前付きステージ`my_dataaccess_stage`のファイルからデータをロードします。  
パスを追加することで、ステートメントはイベントサブディレクトリにあるファイルのみをロードします：
      ```
      COPY INTO mytable
      FROM ‘@my_dataaccess_stage/events/’
      FILE_FORMAT ‘TEALIUM_JSON’;
      ```

## ベストプラクティス

このセクションでは、データがロードされた後のデータ解析に関する有益な情報を提供します。

### EventStoreデータの解析

EventStoreはフラット化されたJSONファイルでフォーマットされています。このドキュメントで説明されているデータロード手順に従った場合、EventStoreデータはバリアントタイプの列に構造化されているはずです。データをクエリにより使いやすい構造にフォーマットするためには、JSONを解析する必要があります。

以下のサンプルクエリは、すべてのデフォルトのEventStore属性列をデータベースビューの専用列に定義します：

```sql
CREATE OR REPLACE VIEW TEALIUM_STD_EVENTS AS
  SELECT
      JSON:&#34;visitorid&#34;::string                              as visitorid
  ,   JSON:&#34;eventid&#34;::string                                as eventid
  ,   JSON:&#34;useragent&#34;::string                              as useragent
  ,   JSON:&#34;device_type&#34;::string                            as device_type
  ,   JSON:&#34;eventtime&#34;::number                              as eventtime

  ,   JSON:&#34;dom_domain&#34;::string                             as dom_domain
  ,   JSON:&#34;dom_pathname&#34;::string                           as dom_pathname
  ,   JSON:&#34;dom_query_string&#34;::string                       as dom_query_string
  ,   JSON:&#34;dom_title&#34;::string                              as dom_title
  ,   JSON:&#34;dom_url&#34;::string                                as dom_url
  ,   JSON:&#34;dom_viewport_height&#34;::number                    as dom_viewport_height
  ,   JSON:&#34;dom_viewport_width&#34;::number                     as dom_viewport_width

  ,   JSON:&#34;pageurl_domain&#34;::string                         as pageurl_domain
  ,   JSON:&#34;pageurl_full_url&#34;::string                       as pageurl_full_url
  ,   JSON:&#34;pageurl_path&#34;::string                           as pageurl_path
  ,   JSON:&#34;pageurl_querystring&#34;::string                    as pageurl_querystring
  ,   JSON:&#34;pageurl_scheme&#34;::string                         as pageurl_scheme

  ,   JSON:&#34;referrerurl_domain&#34;::string                     as referrerurl_domain
  ,   JSON:&#34;referrerurl_full_url&#34;::string                   as referrerurl_full_url
  ,   JSON:&#34;referrerurl_path&#34;::string                       as referrerurl_path
  ,   JSON:&#34;referrerurl_querystring&#34;::string                as referrerurl_querystring
  ,   JSON:&#34;referrerurl_scheme&#34;::string                     as referrerurl_scheme

  ,   JSON:&#34;udo_ut_account&#34;::string                         as udo_ut_account
  ,   JSON:&#34;udo_ut_domain&#34;::string                          as udo_ut_domain
  ,   JSON:&#34;udo_ut_env&#34;::string                             as udo_ut_env
  ,   JSON:&#34;udo_ut_event&#34;::string                           as udo_ut_event
  ,   JSON:&#34;udo_ut_profile&#34;::string                         as udo_ut_profile
  ,   JSON:&#34;udo_ut_version&#34;::string                         as udo_ut_version

  ,   JSON:&#34;firstpartycookies_utag_main__pn&#34;::number        as cookie_utag_main__page_number
  ,   JSON:&#34;firstpartycookies_utag_main__sn&#34;::number        as cookie_utag_main__session_number
  ,   JSON:&#34;firstpartycookies_utag_main__ss&#34;::number        as cookie_utag_main__session_start_flag
  ,   JSON:&#34;firstpartycookies_utag_main__st&#34;::number        as cookie_utag_main__sessoin_timeout
  ,   JSON:&#34;firstpartycookies_utag_main_ses_id&#34;::number     as cookie_utag_main__session_id

  ,   JSON:&#34;udo_timing_pathname&#34;::string                    as timing_pathname
  ,   JSON:&#34;udo_timing_dns&#34;::number                         as timing_dns
  ,   JSON:&#34;udo_timing_load&#34;::number                        as timing_load
  ,   JSON:&#34;udo_timing_connect&#34;::number                     as timing_connect
  ,   JSON:&#34;udo_timing_response&#34;::number                    as timing_response
  ,   JSON:&#34;udo_timing_dom_interactive_to_complete&#34;::number as timing_dom_interactive_to_complete
  ,   JSON:&#34;udo_timing_front_end&#34;::number                   as timing_front_end
  ,   JSON:&#34;udo_timing_dom_loading_to_interactive&#34;::number  as timing_dom_loading_to_interactive
  ,   JSON:&#34;udo_timing_query_string&#34;::string                as timing_query_string
  ,   JSON:&#34;udo_timing_domain&#34;::string                      as timing_domain
  ,   JSON:&#34;udo_timing_fetch_to_interactive&#34;::              as timing_fetch_to_interactive
  ,   JSON:&#34;udo_timing_timestamp&#34;::number                   as timing_timestamp
  ,   JSON:&#34;udo_timing_fetch_to_complete&#34;::number           as timing_fetch_to_complete
  ,   JSON:&#34;udo_timing_fetch_to_response&#34;::number           as timing_fetch_to_response
  ,   JSON:&#34;udo_timing_time_to_first_byte&#34;::number          as timing_time_to_first_byte

  FROM EVENTSTORE_SAMPLE;
```

これらのフィールドに関する詳細情報は、[EventStoreデータガイド]()を参照してください。
### AudienceStore データの解析

AudienceStore データには、コネクタアクションの構成に応じていくつかのバリエーションがあります。前の構成ステップで、Snowflake ステージのファイル形式を JSON として定義しました。

以下のサンプルクエリを使用して、すべてのデフォルト訪問バッジ、日付、文字列、数値、ブール値を含むビューを作成できます。

```sql
CREATE OR REPLACE VIEW TEALIUM_STD_VISITORS AS
SELECT

JSON:_id::string as &#34;visitor_id&#34;
, JSON:metrics.&#34;Average visit duration in minutes&#34;::number as &#34;avg_visit_duration&#34;
, JSON:metrics.&#34;Average visits per week&#34;::number as &#34;avg_visits_per_week&#34;
, JSON:metrics.&#34;Lifetime event count&#34;::number as &#34;ltm_event_count&#34;
, JSON:metrics.&#34;Lifetime visit count&#34;::number as &#34;ltm_visit_count&#34;
, JSON:metrics.&#34;Total direct visits&#34;::number as &#34;total_direct_visits&#34;
, JSON:metrics.&#34;Total referred visits&#34;::number as &#34;total_referred_visits&#34;
, JSON:metrics.&#34;Total time spent on site in minutes&#34;::number as &#34;total_time_onsite&#34;
, JSON:metrics.&#34;Weeks since first visit&#34;::number as &#34;weeks_since_first_visit&#34;
, JSON:dates.&#34;First visit&#34;::number as &#34;first_visit_date&#34;
, JSON:dates.&#34;Last visit&#34;::number as &#34;last_visit_date&#34;
, JSON:properties.&#34;Last event url&#34;::string as &#34;last_event_url&#34;
, JSON:properties.&#34;Lifetime browser types used (favorite)&#34;::string as &#34;ltm_browser_types_used_fav&#34;
, JSON:properties.&#34;Lifetime browser versions used (favorite)&#34;::string as &#34;ltm_browser_versions_used_fav&#34;
, JSON:properties.&#34;Lifetime devices used (favorite)&#34;::string as &#34;ltm_devices_used_fav&#34;
, JSON:properties.&#34;Lifetime operating systems used (favorite)&#34;::string as &#34;ltm_os_used_fav&#34;
, JSON:properties.&#34;Lifetime platforms used (favorite)&#34;::string as &#34;ltm_platforms_used_fav&#34;
, JSON:badges.&#34;Fan&#34;::boolean as &#34;fan_badge&#34;
, JSON:badges.&#34;Frequent visitor&#34;::boolean as &#34;frequent_visitor_badge&#34;
, JSON:badges.&#34;Unbadged&#34;::boolean as &#34;unbadged&#34;
, .&#34;Returning visitor&#34;::boolean as &#34;returning_visitor_flag&#34;

FROM AUDIENCESTORE_SAMPLE;

```

訪問プロファイルオブジェクトのより高度な解析については、[Snowflake 半構造化データ](https://docs.snowflake.com/en/user-guide/semistructured-concepts.html)のドキュメントを参照してください。

## 関連トピック

追加情報については、以下のリソースを参照してください：

* [AudienceStore および EventStore の操作 - Tealium ]()
* [EventStore データガイド - Tealium]()
* [データのロード準備 - Snowflake](https://docs.snowflake.com/en/user-guide/data-load-prepare.html)
* [データロードの考慮事項 - Snowflake](https://docs.snowflake.com/en/user-guide/data-load-considerations.html)
