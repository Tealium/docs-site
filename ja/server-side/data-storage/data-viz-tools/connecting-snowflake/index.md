---
title: Snowflakeへの接続
description: この記事では、Snowflake Webインターフェースを使用してTealiumデータをSnowflakeにロードする方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/data-viz-tools/connecting-snowflake/
---

<blockquote>
この記事はSnowflake Webインターフェースとデータロードウィザードに焦点を当てており、Snowflakeコマンドラインツールの概要を提供します。Snowflakeの使用に関する詳細情報については、[Snowflakeドキュメント](https://docs.snowflake.net/manuals/index.html)を参照してください。
</blockquote>


## 動作原理

Tealium DataAccessの顧客は、Snowflake Webインターフェースを使用して、データを外部ソリューションに接続し、高度なクエリとデータ分析を行うことができます。Webインターフェースは直感的なウィザードを提供し、限られた量のデータを小さなフラットファイルのセットからテーブルにロードすることができます。このプロセスでは、PUTおよびCOPYコマンドを使用してデータをロードし、ステージングファイルとデータロードフェーズを一つの操作に統合することで、データロードプロセスを簡素化します。

Webインターフェースは、ファイルの数が少ない（最大50 MB）場合に適しています。この制限は、ハードウェア、ブラウザの種類、およびブラウザのバージョンによってブラウザのパフォーマンスが異なるため、最適なパフォーマンスを保証するためです。

## 前提条件

Tealiumが発行したAmazon S3バケットからDataAccessデータを接続するためには、以下の項目が必要です：

* AudienceStoreおよびEventStoreが有効になっているTealium DataAccess  
データがDataAccessバケットに配信されるように、AudienceStream内でAudienceStoreコネクタを構成する必要があります。AudienceStreamの構成についての詳細は、Tealiumの[AudienceStore構成ガイド](https://docs.tealium.com/audiencestore-and-eventstore/)を参照してください。
* EventStoreおよび/またはAudienceStore用の有効なTealium DataAccess認証情報。

## はじめに

次のセクションでは、SnowflakeデータロードWebインターフェースを使用してソースファイルを選択し、TealiumデータをSnowflakeにロードする手順を案内します。


<blockquote>
DataAccessデータをJSONファイルの半構造化の性質に対応し、スキーマ要件を強制しないバリアントデータ型のテーブルにロードすることをお勧めします。データがロードされた後の解析に関する追加情報とヒントについては、このドキュメントのベストプラクティスセクションを参照してください。
</blockquote>


### データロードウィザードを開く

データロードウィザードを開くには、次の手順に従います：

1. Snowflakeアカウントにログインします。
1. **Databases > Tables**をクリックします。
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
      ![](https://docs.tealium.com/images/server-side/snowflake-create-stage.jpg)
1. 次のセクションに進み、DataAccess認証情報を入力します。

### DataAccess認証情報を入力する

DataAccess認証情報を入力するには、次の手順に従います：

1. まだ行っていない場合は、EventStoreまたはAudienceStoreのDataAccess認証情報を取得します。  
認証情報はEventStoreとAudienceStoreの両方で同じです。  
      
<blockquote>
認証情報がすでに生成されている場合、Secret Access Keyは表示されません。既存のキーを取得するか、新しいキーを再生成する必要があるかを同僚と協議してください。
</blockquote>


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

1. ドロップダウンリストの隣にあるプラス（**+**）記号をクリックします。  
ファイル形式作成ダイアログが表示されます。  
      ![](https://docs.tealium.com/images/server-side/snowflake-create-file-format.jpg)
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
      ![](https://docs.tealium.com/images/server-side/snowflake-manually-load-data-via-web-interface.jpg)
1. **Load**をクリックしてすぐにデータをロードするか、**Next**をクリックして追加のロードオプションを構成します。  

<blockquote>
倉庫が現在稼働していない場合、倉庫を再開するのに最大5分かかることがあります。これにはロードに必要な時間も含まれます。
</blockquote>

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
接続されたら、`COPY INTO <table>`コマンドを実行してデータをターゲットテーブルにロードします。以下の例では、前の手順で作成された名前付きステージ`my_dataaccess_stage`のファイルからデータをロードします。  
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
      JSON:"visitorid"::string                              as visitorid
  ,   JSON:"eventid"::string                                as eventid
  ,   JSON:"useragent"::string                              as useragent
  ,   JSON:"device_type"::string                            as device_type
  ,   JSON:"eventtime"::number                              as eventtime

  ,   JSON:"dom_domain"::string                             as dom_domain
  ,   JSON:"dom_pathname"::string                           as dom_pathname
  ,   JSON:"dom_query_string"::string                       as dom_query_string
  ,   JSON:"dom_title"::string                              as dom_title
  ,   JSON:"dom_url"::string                                as dom_url
  ,   JSON:"dom_viewport_height"::number                    as dom_viewport_height
  ,   JSON:"dom_viewport_width"::number                     as dom_viewport_width

  ,   JSON:"pageurl_domain"::string                         as pageurl_domain
  ,   JSON:"pageurl_full_url"::string                       as pageurl_full_url
  ,   JSON:"pageurl_path"::string                           as pageurl_path
  ,   JSON:"pageurl_querystring"::string                    as pageurl_querystring
  ,   JSON:"pageurl_scheme"::string                         as pageurl_scheme

  ,   JSON:"referrerurl_domain"::string                     as referrerurl_domain
  ,   JSON:"referrerurl_full_url"::string                   as referrerurl_full_url
  ,   JSON:"referrerurl_path"::string                       as referrerurl_path
  ,   JSON:"referrerurl_querystring"::string                as referrerurl_querystring
  ,   JSON:"referrerurl_scheme"::string                     as referrerurl_scheme

  ,   JSON:"udo_ut_account"::string                         as udo_ut_account
  ,   JSON:"udo_ut_domain"::string                          as udo_ut_domain
  ,   JSON:"udo_ut_env"::string                             as udo_ut_env
  ,   JSON:"udo_ut_event"::string                           as udo_ut_event
  ,   JSON:"udo_ut_profile"::string                         as udo_ut_profile
  ,   JSON:"udo_ut_version"::string                         as udo_ut_version

  ,   JSON:"firstpartycookies_utag_main__pn"::number        as cookie_utag_main__page_number
  ,   JSON:"firstpartycookies_utag_main__sn"::number        as cookie_utag_main__session_number
  ,   JSON:"firstpartycookies_utag_main__ss"::number        as cookie_utag_main__session_start_flag
  ,   JSON:"firstpartycookies_utag_main__st"::number        as cookie_utag_main__sessoin_timeout
  ,   JSON:"firstpartycookies_utag_main_ses_id"::number     as cookie_utag_main__session_id

  ,   JSON:"udo_timing_pathname"::string                    as timing_pathname
  ,   JSON:"udo_timing_dns"::number                         as timing_dns
  ,   JSON:"udo_timing_load"::number                        as timing_load
  ,   JSON:"udo_timing_connect"::number                     as timing_connect
  ,   JSON:"udo_timing_response"::number                    as timing_response
  ,   JSON:"udo_timing_dom_interactive_to_complete"::number as timing_dom_interactive_to_complete
  ,   JSON:"udo_timing_front_end"::number                   as timing_front_end
  ,   JSON:"udo_timing_dom_loading_to_interactive"::number  as timing_dom_loading_to_interactive
  ,   JSON:"udo_timing_query_string"::string                as timing_query_string
  ,   JSON:"udo_timing_domain"::string                      as timing_domain
  ,   JSON:"udo_timing_fetch_to_interactive"::              as timing_fetch_to_interactive
  ,   JSON:"udo_timing_timestamp"::number                   as timing_timestamp
  ,   JSON:"udo_timing_fetch_to_complete"::number           as timing_fetch_to_complete
  ,   JSON:"udo_timing_fetch_to_response"::number           as timing_fetch_to_response
  ,   JSON:"udo_timing_time_to_first_byte"::number          as timing_time_to_first_byte

  FROM EVENTSTORE_SAMPLE;
```

これらのフィールドに関する詳細情報は、[EventStoreデータガイド](https://docs.tealium.com/eventstore-data-guide/)を参照してください。
### AudienceStore データの解析

AudienceStore データには、コネクタアクションの構成に応じていくつかのバリエーションがあります。前の構成ステップで、Snowflake ステージのファイル形式を JSON として定義しました。

以下のサンプルクエリを使用して、すべてのデフォルト訪問バッジ、日付、文字列、数値、ブール値を含むビューを作成できます。

```sql
CREATE OR REPLACE VIEW TEALIUM_STD_VISITORS AS
SELECT

JSON:_id::string as "visitor_id"
, JSON:metrics."Average visit duration in minutes"::number as "avg_visit_duration"
, JSON:metrics."Average visits per week"::number as "avg_visits_per_week"
, JSON:metrics."Lifetime event count"::number as "ltm_event_count"
, JSON:metrics."Lifetime visit count"::number as "ltm_visit_count"
, JSON:metrics."Total direct visits"::number as "total_direct_visits"
, JSON:metrics."Total referred visits"::number as "total_referred_visits"
, JSON:metrics."Total time spent on site in minutes"::number as "total_time_onsite"
, JSON:metrics."Weeks since first visit"::number as "weeks_since_first_visit"
, JSON:dates."First visit"::number as "first_visit_date"
, JSON:dates."Last visit"::number as "last_visit_date"
, JSON:properties."Last event url"::string as "last_event_url"
, JSON:properties."Lifetime browser types used (favorite)"::string as "ltm_browser_types_used_fav"
, JSON:properties."Lifetime browser versions used (favorite)"::string as "ltm_browser_versions_used_fav"
, JSON:properties."Lifetime devices used (favorite)"::string as "ltm_devices_used_fav"
, JSON:properties."Lifetime operating systems used (favorite)"::string as "ltm_os_used_fav"
, JSON:properties."Lifetime platforms used (favorite)"::string as "ltm_platforms_used_fav"
, JSON:badges."Fan"::boolean as "fan_badge"
, JSON:badges."Frequent visitor"::boolean as "frequent_visitor_badge"
, JSON:badges."Unbadged"::boolean as "unbadged"
, ."Returning visitor"::boolean as "returning_visitor_flag"

FROM AUDIENCESTORE_SAMPLE;

```

訪問プロファイルオブジェクトのより高度な解析については、[Snowflake 半構造化データ](https://docs.snowflake.com/en/user-guide/semistructured-concepts.html)のドキュメントを参照してください。

## 関連トピック

追加情報については、以下のリソースを参照してください：

* [AudienceStore および EventStore の操作 - Tealium ](https://docs.tealium.com/audiencestore-and-eventstore/)
* [EventStore データガイド - Tealium](https://docs.tealium.com/eventstore-data-guide/)
* [データのロード準備 - Snowflake](https://docs.snowflake.com/en/user-guide/data-load-prepare.html)
* [データロードの考慮事項 - Snowflake](https://docs.snowflake.com/en/user-guide/data-load-considerations.html)
