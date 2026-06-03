---
title: Snowflake用Tealium Audience Discoveryのインストール
description: SnowflakeマーケットプレイスからSnowflake用Tealium Audience Discoveryをインストールし、必要なロールと権限を構成します。
url: https://docs.tealium.com/ja/server-side/data-sources/cloud-data/snowflake-cloud-data-source/tealium-audience-discovery/install/
---
このガイドでは、SnowflakeマーケットプレイスからSnowflake用Tealium Audience Discoveryをインストールし、それを使用するために必要なロールと権限を構成する方法について説明します。

## 要件

* Snowflakeのアカウント所有者または管理者ロール。
* オーディエンス作成に使用したいSnowflakeのデータベースとスキーマへのアクセス。

## アプリのインストール

SnowflakeマーケットプレイスからSnowflake用Tealium Audience Discoveryをインストールします。インストール後、次のセクションのSQLを実行してアプリを構成し、起動します。

## サービスの構成

インストール後、以下のSQLを実行してアプリを構成し、開始します。`&lt;SOURCE_DATABASE&gt;`をデータが含まれているデータベースに置き換えてください。インストール時に異なるアプリケーション名を選択した場合は、`TEALIUM_AUDIENCE_DISCOVERY_APP`をそれに応じて置き換えてください。

1. アプリ専用のコンピュートプールを作成します。

   `CPU_X64_XS`（2 vCPU、8 GB）はほとんどのワークロードに適しています。大規模なオーディエンスや重い同時使用の場合は`CPU_X64_S`（4 vCPU、16 GB）を使用してください。

   ```sql
   CREATE COMPUTE POOL IF NOT EXISTS TEALIUM_AUDIENCE_DISCOVERY_POOL
     FOR APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP
     MIN_NODES = 1
     MAX_NODES = 1
     INSTANCE_FAMILY = CPU_X64_XS;
   ```

1. 倉庫を作成するか、既存のものを使用します。

   ```sql
   CREATE WAREHOUSE IF NOT EXISTS TEALIUM_AUDIENCE_DISCOVERY_WH
     WAREHOUSE_SIZE = &#39;X-SMALL&#39;;
   ```

1. アプリにコンピュートプールと倉庫へのアクセスを許可します。

   ```sql
   GRANT USAGE ON COMPUTE POOL TEALIUM_AUDIENCE_DISCOVERY_POOL TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT USAGE ON WAREHOUSE TEALIUM_AUDIENCE_DISCOVERY_WH TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. アプリにソースデータへの読み取りアクセスを許可します。

   ```sql
   GRANT USAGE ON DATABASE &lt;SOURCE_DATABASE&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT USAGE ON ALL SCHEMAS IN DATABASE &lt;SOURCE_DATABASE&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON ALL TABLES IN DATABASE &lt;SOURCE_DATABASE&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON ALL VIEWS IN DATABASE &lt;SOURCE_DATABASE&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. サービスを開始します。

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.create_app_service(
       &#39;TEALIUM_AUDIENCE_DISCOVERY_POOL&#39;,
       &#39;TEALIUM_AUDIENCE_DISCOVERY_WH&#39;
   );
   ```

1. サービスの状態を確認します。状態が`READY`になるまで待ってから続行します。

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.check_service_status();
   ```

1. アプリケーションのURLを取得します。

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.get_app_url();
   ```

## アプリを開く

1. ステップ7で返されたURLを開くか、**Snowsight &gt; Data Products &gt; Apps &gt; TEALIUM_AUDIENCE_DISCOVERY_APP &gt; Endpoints**に移動します。
1. **audience-discovery-endpoint**をクリックしてウェブインターフェースを開きます。
1. **Data Explorer**を使用して利用可能なテーブルを閲覧します。

## 追加の構成

### 追加のデータベースへのアクセスを許可する

アプリは、オーディエンスを構築したいすべてのデータベースからの読み取りアクセスが必要です。以下を各追加データベースに対して繰り返します。

```sql
GRANT USAGE ON DATABASE &lt;SOURCE_DATABASE&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
GRANT USAGE ON ALL SCHEMAS IN DATABASE &lt;SOURCE_DATABASE&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
GRANT SELECT ON ALL TABLES IN DATABASE &lt;SOURCE_DATABASE&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
GRANT SELECT ON ALL VIEWS IN DATABASE &lt;SOURCE_DATABASE&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
```


アプリはソースデータを読み取るだけで、テーブルを変更することはありません。


### Cortex AIの有効化（オプション）

アプリには、ユーザーが自然言語でオーディエンスセグメンテーションルールを記述できるCortexモードが含まれています。Cortex Analystは、Snowflakeのセマンティックビューを使用してSQLクエリを自動的に生成します。


この機能には、アプリケーションに割り当てられたセマンティックビューが必要です。


1. Cortex AIデータベースロールを付与します。

   ```sql
   GRANT DATABASE ROLE SNOWFLAKE.CORTEX_USER TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. セマンティックビューへのアクセスを許可します。

   ```sql
   GRANT USAGE ON DATABASE &lt;SEMANTIC_VIEW_DB&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT USAGE ON SCHEMA &lt;SEMANTIC_VIEW_DB&gt;.&lt;SEMANTIC_VIEW_SCHEMA&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON ALL VIEWS IN SCHEMA &lt;SEMANTIC_VIEW_DB&gt;.&lt;SEMANTIC_VIEW_SCHEMA&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON SEMANTIC VIEW &lt;SEMANTIC_VIEW_NAME&gt; TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. （オプション）利用可能な大規模言語モデル（LLMs）を構成します。モデルリストを管理するために、役割に`app_admin`を付与します。

   ```sql
   GRANT APPLICATION ROLE TEALIUM_AUDIENCE_DISCOVERY_APP.app_admin TO ROLE &lt;ADMIN_ROLE&gt;;
   ```

   インストール中にシードされたデフォルトモデルを表示します。

   ```sql
   SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUDIENCE_DISCOVERY_SCHEMA.AVAILABLE_LLMS;
   ```

   リストを自分のモデルに置き換えます。

   ```sql
   DELETE FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUDIENCE_DISCOVERY_SCHEMA.AVAILABLE_LLMS;
   INSERT INTO TEALIUM_AUDIENCE_DISCOVERY_APP.AUDIENCE_DISCOVERY_SCHEMA.AVAILABLE_LLMS (MODEL_NAME)
   VALUES
       (&#39;mistral-large2&#39;),
       (&#39;llama3.1-70b&#39;),
       (&#39;llama3.1-405b&#39;),
       (&#39;snowflake-arctic&#39;),
       (&#39;claude-3-5-sonnet&#39;);
   ```

   
   Snowflakeリージョンで有効になっているモデルのみをリストに含めてください。モデルをテストするには、`SELECT AI_COMPLETE(model =&gt; &#39;&lt;model_name&gt;&#39;, prompt =&gt; &#39;Hello&#39;);`を実行します。
   

### Webhook配信の有効化（オプション）

アプリは、外部HTTPエンドポイントにオーディエンスデータを送信できます。この機能はデフォルトで無効になっており、管理者の構成が必要です。


この機能には、構成されたネットワークルールと外部アクセス統合が必要です。


1. Webhookホスト用のネットワークルールを作成します。

   ```sql
   CREATE OR REPLACE NETWORK RULE webhook_egress_rule
     TYPE = HOST_PORT
     MODE = EGRESS
     VALUE_LIST = (&#39;your-webhook-host.example.com:443&#39;);
   ```

1. 外部アクセス統合を作成します。

   ```sql
   CREATE OR REPLACE EXTERNAL ACCESS INTEGRATION webhook_external_access
     ALLOWED_NETWORK_RULES = (webhook_egress_rule)
     ENABLED = TRUE;
   ```

1. アプリケーションに統合の使用を許可します。

   ```sql
   GRANT USAGE ON INTEGRATION webhook_external_access TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. 機能を有効にします。これにより、外部アクセス統合が実行中のサービスに自動的に添付されます。

   ```sql
   -- デフォルトの統合名WEBHOOK_EXTERNAL_ACCESSを使用します
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.set_webhook_enabled(TRUE);

   -- カスタム統合名を指定します
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.set_webhook_enabled(TRUE, &#39;MY_CUSTOM_INTEGRATION&#39;);
   ```

   後でWebhook配信を無効にするには：

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.set_webhook_enabled(FALSE);
   ```

オーディエンスデータを送信するには：

1. オーディエンスを開き、三点リーダーメニューをクリックします。
1. **Send to Webhook**を選択します。
1. HTTPS webhook URLを入力し、必要に応じて基本認証資格情報を入力します。
1. **Send**をクリックします。データはデフォルトで1,000行のバッチでJSON形式で配信され、最大1,000,000行までです。

すべての配信は`AUDIENCE_DISCOVERY_SCHEMA.WEBHOOK_LOG`に記録されます。

```sql
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUDIENCE_DISCOVERY_SCHEMA.WEBHOOK_LOG
ORDER BY STARTED_AT DESC;
```
### Tealiumアプリケーションへのユーザーアクセスの構成

Snowflakeユーザーにアプリへのアクセスを許可するために、専用のロールを作成し、そのロールにアプリケーションロールを割り当てます。

1. アプリケーションユーザー用の専用ロールを作成します。

   ```sql
   CREATE ROLE IF NOT EXISTS TEALIUM_APP_USER;
   ```

1. 専用ロールに`app_user`アプリケーションロールを付与します。

   ```sql
   GRANT APPLICATION ROLE TEALIUM_AUDIENCE_DISCOVERY_APP.app_user TO ROLE TEALIUM_APP_USER;
   ```

   ユーザーのニーズに合わせてアプリケーションロールを選択します：

      * `app_user`: アプリへのアクセスとオーディエンスの作成が可能
      * `app_admin`: アプリへのアクセス、オーディエンスの作成、アプリ構成の変更、Snowsightでのアプリオブジェクトへのアクセスが可能
      * `app_viewer`: オーディエンスの作成機能なしでアプリへのアクセスが可能

1. アプリへのアクセスが必要なユーザーに専用ロールを付与します。

   ```sql
   GRANT ROLE TEALIUM_APP_USER TO USER &lt;user&gt;;
   ```

### Tealiumコネクタの外部アクセスの構成

各オーディエンスには、Tealium Snowflakeコネクタなどの外部消費者用に`USERS_EXTERNAL`セキュアビューが含まれています。このビューは、オーディエンスが非アクティブ化されたときに自動的にゼロ行を返し、再アクティブ化されたときに再開します。

1. 外部サービスアカウント用の専用ロールを作成します。

   ```sql
   CREATE ROLE IF NOT EXISTS TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE;
   ```

1. `app_external`アプリケーションロールを付与します。このロールはセキュアビューのみへのアクセスを提供し、テーブルへのアクセスは提供しません。

   ```sql
   GRANT APPLICATION ROLE TEALIUM_AUDIENCE_DISCOVERY_APP.app_external TO ROLE TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE;
   ```

1. クエリ実行のためのウェアハウス使用を許可します。

   ```sql
   GRANT USAGE ON WAREHOUSE TEALIUM_AUDIENCE_DISCOVERY_WH TO ROLE TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE;
   ```

1. Tealiumサービスアカウントユーザーにロールを付与します。

   ```sql
   GRANT ROLE TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE TO USER &lt;TEALIUM_SERVICE_USER&gt;;
   ```

Tealiumコネクタは次のようにオーディエンスをクエリします：

```sql
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.&lt;AUDIENCE_SCHEMA&gt;.USERS_EXTERNAL;
```

ロール制限を確認するために、テスト前にセカンダリロールを無効にします。

```sql
USE SECONDARY ROLES NONE;
USE ROLE TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE;

-- アクティブなオーディエンスのデータを返すべきです
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUD_XXXXXXXXXXXXXXXX.USERS_EXTERNAL;

-- 権限不足で失敗するべきです
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUD_XXXXXXXXXXXXXXXX.USERS;

-- 完了したらセカンダリロールを再有効化します
USE SECONDARY ROLES ALL;
USE ROLE SYSADMIN;
```