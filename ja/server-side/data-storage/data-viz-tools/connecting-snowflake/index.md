---
title: Snowflakeへの接続
description: この記事では、SnowflakeのWebインターフェイスを使用してTealiumデータをSnowflakeに読み込む方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/data-viz-tools/connecting-snowflake/
---

<blockquote>
この記事では、SnowflakeのWebインターフェイスとData Loadウィザードを中心に説明し、Snowflakeのコマンドラインツールの概要も紹介します。Snowflakeの使用方法の詳細については、[Snowflakeドキュメント](https://docs.snowflake.net/manuals/index.html)を参照してください。
</blockquote>


## 仕組み

Tealium DataAccessをご利用のお客様は、SnowflakeのWebインターフェイスを使用してデータを外部ソリューションに接続し、高度なクエリやデータ分析を行うことができます。Webインターフェイスには直感的に操作できるウィザードが用意されており、少数のフラットファイルから限られた量のデータをテーブルに読み込めます。このウィザードでは、PUTコマンドとCOPYコマンドを使用してデータを読み込み、ステージングファイルの作成とデータの読み込みを1つの操作にまとめることで、データ読み込みプロセスを簡素化します。

Webインターフェイスは、少数のファイル（最大50 MB）を読み込むことを目的としています。ブラウザーのパフォーマンスは、ハードウェア、ブラウザーの種類、ブラウザーのバージョンによって異なるため、この制限によって最適なパフォーマンスが確保されます。

## 前提条件

Tealiumから提供されたAmazon S3バケット内のDataAccessデータに接続するには、以下が必要です。

* AudienceStoreとEventStoreが有効になっているTealium DataAccess  
データをDataAccessバケットに配信するには、Customer Data Platform（CDP）内でAudienceStoreコネクタを構成する必要があります。CDP構成の詳細については、Tealiumの[AudienceStore構成ガイド](https://docs.tealium.com/audiencestore-and-eventstore/)を参照してください。
* EventStoreまたはAudienceStore、あるいはその両方に対する有効なTealium DataAccess認証情報。

## はじめに

以降のセクションでは、Snowflake Data LoadのWebインターフェイスを使用してソースファイルを選択し、TealiumデータをSnowflakeに読み込むために必要な手順を説明します。


<blockquote>
DataAccessデータは、バリアントデータ型のテーブルに読み込むことをお勧めします。バリアントデータ型は、スキーマ要件を強制することなく、JSONファイルの半構造化された特性に対応できます。データ読み込み後の解析に関する詳細とヒントについては、このドキュメントの「ベストプラクティス」セクションを参照してください。
</blockquote>


### Data Loadウィザードを開く

次の手順に従って、Snowflake Data Loadウィザードを開きます。

1. Snowflakeアカウントにログインします。
1. **Databases > Tables**をクリックします。
1. 次のいずれかを実行します。  
      * テーブルの行をクリックして選択し、**Load Data**ボタンをクリックします。
      * テーブル名をクリックしてテーブルの詳細ページを開き、**Load Table**ボタンをクリックします。

1. Load Dataウィザードが表示されます。
1. 次のセクションに進み、DataAccessからソースファイルを選択します。これにより、選択したテーブルへのデータの読み込みを開始できます。

### DataAccessからソースファイルを選択する

ソースファイルを選択するよう求められたら、AWS S3に保存されているTealium DataAccessデータ用の新しいステージを作成します。

次の手順に従って、Tealium DataAccessからソースファイルを選択します。

1. **Existing Amazon S3 Location**を選択します。
1. **Next**をクリックします。  
      ![](https://docs.tealium.com/images/server-side/snowflake-create-stage.jpg)
1. 次のセクションに進み、DataAccessの認証情報を入力します。

### DataAccessの認証情報を入力する

次の手順に従って、DataAccessの認証情報を入力します。

1. EventStoreまたはAudienceStoreのDataAccess認証情報をまだ取得していない場合は、取得します。  
認証情報は、EventStoreとAudienceStoreの両方で共通です。  
      
<blockquote>
認証情報がすでに生成されている場合、シークレットアクセスキーは表示されません。既存のキーを取得するか、新しいキーを再生成する必要があるかを判断するには、同僚に確認してください。
</blockquote>


1. 有効な認証情報を取得したら、以下のフィールドに入力します。  
    * **Access Key**  
    Tealiumから提供されたアクセスキーIDを入力します。例：`AKIA****************`
    * **Secret Key**  
    Tealiumから提供されたシークレットアクセスキーを入力します。
    * **Bucket**  
    Tealiumのパスフィールドにある最初の値のみを入力します。例：  
    Tealiumのパスが `/dataaccess-us-east-1.tealiumiq.com/myaccount/main` の場合  
    `dataaccess-us-east-1.tealiumiq.com` と入力します（スラッシュは含めません）。
    * **Prefix**  
    Tealiumのパスフィールドの残りの部分を、アカウント名から始め、末尾にスラッシュ（/）を付けて入力します。  
    例：`myaccount/main/`
    * **Region**  
    バケット名で示されているリージョンを選択します。例：**us-east-1**

1. 次のセクションに進み、ファイル形式を作成します。

### ファイル形式を作成する

次の手順に従って、ファイル形式を作成します。

1. ドロップダウンリストの横にあるプラス（**+**）記号をクリックします。  
Create File Formatダイアログが表示されます。  
      ![](https://docs.tealium.com/images/server-side/snowflake-create-file-format.jpg)
1. 以下の情報を入力します。
    * Nameフィールドに、DataAccessデータで使用するファイル形式の名前を入力します。例：`TEALIUM_JSON`  
    このフィールドは必須です。
    * ドロップダウンリストからSchema Nameの種類を選択します。例：**Public**
    * ドロップダウンリストからFormat Typeを選択します。例：**JSON**
    * ドロップダウンリストからCompression Methodを選択します。例：**Gzip**
    * 次のチェックボックスを1つ以上選択します。
        * Enable Octal
        * Allow Duplicate
        * Strip Outer Array
        * Strip Null Values
        * Ignore UTF-8 Errors
    * Commentフィールドに、このファイル形式に関する説明を入力します。  
    例：TealiumはJSONデータをGzip圧縮ファイルに保存します。

1. **Finish**をクリックします。
1. 次のセクションに進み、データを読み込みます。

### データを読み込む

Webインターフェイスを使用して手動でデータを読み込むには、以下の手順を続行します。必要に応じて、コマンドラインからデータを読み込むこともできます。この方法を選択する場合は、「コマンドラインを使用した読み込み」セクションに進んでください。

1. 先ほど名前を付けたファイル形式をドロップダウンリストから選択します。  
      ![](https://docs.tealium.com/images/server-side/snowflake-manually-load-data-via-web-interface.jpg)
1. データをすぐに読み込むには**Load**をクリックし、追加の読み込みオプションを構成するには**Next**をクリックします。  

<blockquote>
ウェアハウスが現在稼働していない場合、読み込みに必要な時間に加えて、ウェアハウスの再開に最大5分かかることがあります。
</blockquote>

### コマンドラインを使用して読み込む（任意）

コマンドラインからデータを読み込むには、次の手順に従います。

1. **SnowSQL をインストールする**  
コマンドラインからデータを読み込むには、事前に SnowSQL をマシンへインストールする必要があります。詳しくは、[SnowSQL のインストール](https://docs.snowflake.com/en/user-guide/snowsql-install-config.html)を参照してください。
1. **SnowSQL を構成する**  
SnowSQL のインストールが完了したら、Snowflake インスタンスに接続できるように、認証情報を構成ファイルへ追加する必要があります。
    1. 次のディレクトリにある構成ファイルを開きます。  
        * Linux/Mac OS の場合：`~/.snowsql/`
        * Windows の場合：`%USERPROFILE%\.snowsql\`
    1. ファイルの connections セクションを編集し、認証情報を入力します。  
    例：  
          ```bash
          [connections.tealium_example]
          #Can be used in SnowSql as connect tealium_example
          accountname = MY_ACCOUNT_NAME
          username = MYUSER
          password = ********************
          ```
    1. 必要に応じて、options セクションまたは variables セクションを変更します。詳しくは、[SnowSQL の構成](https://docs.snowflake.com/en/user-guide/snowsql-config.html)を参照してください。

1. **SnowSQL 経由で接続する**  
接続情報を構成ファイルに保存したら、シェルコマンドを使用して SnowSQL に接続します。`tealium_example` を実際の接続名に置き換えてください。  
`$ snowsql -c tealium_example`  
詳しくは、[SnowSQL 経由での接続](https://docs.snowflake.com/en/user-guide/snowsql-start.html)を参照してください。
1. **COPY INTO コマンドを使用してデータを読み込む**  
接続したら、`COPY INTO <table>` コマンドを実行して、ターゲットテーブルにデータを読み込みます。次の例では、前の手順で作成した名前付きステージ `my_dataaccess_stage` 内のファイルからデータを読み込みます。  
パスを追加することで、このステートメントは events サブディレクトリにあるファイルのみを読み込みます。
      ```
      COPY INTO mytable
      FROM ‘@my_dataaccess_stage/events/’
      FILE_FORMAT ‘TEALIUM_JSON’;
      ```

## ベストプラクティス

このセクションでは、データの読み込み後にデータを解析する際のベストプラクティスについて説明します。

### EventStore データを解析する

EventStore は、フラット化された JSON ファイルとしてフォーマットされています。このドキュメントに記載されているデータ読み込み手順に従った場合、EventStore データは variant 型の列に格納されているはずです。クエリで利用しやすい構造にデータを整形するには、JSON を解析する必要があります。

次のサンプルクエリでは、デフォルトのすべての EventStore 属性を、データベースビュー内の専用列として定義します。

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

これらのフィールドについて詳しくは、[EventStore データガイド](https://docs.tealium.com/eventstore-data-guide/)を参照してください。
### AudienceStore データを解析する

AudienceStore データには、コネクタアクションの構成に応じて複数のバリエーションがあります。前の構成手順では、Snowflake ステージのファイル形式として JSON を定義しました。

次のサンプルクエリを使用すると、デフォルトのすべての訪問バッジ、日付、文字列、数値、およびブール値を含むビューを作成できます。

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

訪問プロファイルオブジェクトのより高度な解析については、[Snowflake の半構造化データ](https://docs.snowflake.com/en/user-guide/semistructured-concepts.html)のドキュメントを参照してください。

## 関連トピック

詳細については、次のリソースを参照してください。

* [AudienceStore と EventStore の使用方法 - Tealium](https://docs.tealium.com/audiencestore-and-eventstore/)
* [EventStore データガイド - Tealium](https://docs.tealium.com/eventstore-data-guide/)
* [データ読み込みの準備 - Snowflake](https://docs.snowflake.com/en/user-guide/data-load-prepare.html)
* [データ読み込みに関する考慮事項 - Snowflake](https://docs.snowflake.com/en/user-guide/data-load-considerations.html)