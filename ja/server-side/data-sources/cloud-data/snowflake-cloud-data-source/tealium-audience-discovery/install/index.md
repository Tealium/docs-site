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

インストール後、以下のSQLを実行してアプリを構成し、開始します。`<SOURCE_DATABASE>`をデータが含まれているデータベースに置き換えてください。インストール時に異なるアプリケーション名を選択した場合は、`TEALIUM_AUDIENCE_DISCOVERY_APP`をそれに応じて置き換えてください。

1. アプリ専用のコンピュートプールを作成します。

   `CPU_X64_XS`（2 vCPU、8 GB）はほとんどのワークロードに適しています。大規模なオーディエンスや重い同時使用の場合は、`CPU_X64_S`（4 vCPU、16 GB）を使用してください。

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
     WAREHOUSE_SIZE = 'X-SMALL';
   ```

1. アプリにコンピュートプールと倉庫へのアクセスを許可します。

   ```sql
   GRANT USAGE ON COMPUTE POOL TEALIUM_AUDIENCE_DISCOVERY_POOL TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT USAGE ON WAREHOUSE TEALIUM_AUDIENCE_DISCOVERY_WH TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. アプリにソースデータへの読み取りアクセスを許可します。

   ```sql
   GRANT USAGE ON DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT USAGE ON ALL SCHEMAS IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON ALL TABLES IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON ALL VIEWS IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. サービスを開始します。

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.create_app_service(
       'TEALIUM_AUDIENCE_DISCOVERY_POOL',
       'TEALIUM_AUDIENCE_DISCOVERY_WH'
   );
   ```

1. サービスの状態を確認します。状態が `READY` になるまで待ってから続行します。

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.check_service_status();
   ```

1. アプリケーションのURLを取得します。

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.get_app_url();
   ```

## アプリを開く

1. ステップ7で返されたURLを開くか、**Snowsight > Data Products > Apps > TEALIUM_AUDIENCE_DISCOVERY_APP > Endpoints**に移動します。
1. **audience-discovery-endpoint**をクリックしてウェブインターフェースを開きます。
1. **Data Explorer**を使用して利用可能なテーブルを閲覧します。

## 追加の構成

### 追加のデータベースへのアクセスを許可する

アプリは、オーディエンスを構築したいすべてのデータベースへの読み取りアクセスが必要です。以下を各追加データベースに対して繰り返します。

```sql
GRANT USAGE ON DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
GRANT USAGE ON ALL SCHEMAS IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
GRANT SELECT ON ALL TABLES IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
GRANT SELECT ON ALL VIEWS IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
```


<blockquote>
アプリはソースデータを読み取るだけで、テーブルを変更することはありません。
</blockquote>


### Cortex AIの有効化（オプション）

アプリには、ユーザーが自然言語でオーディエンスセグメンテーションルールを記述できるCortexモードが含まれています。Cortex Analystは、Snowflakeのセマンティックビューを使用してSQLクエリを自動的に生成します。


<blockquote>
この機能には、アプリケーションに割り当てられたセマンティックビューが必要です。
</blockquote>


1. Cortex AIデータベースロールを付与します。

   ```sql
   GRANT DATABASE ROLE SNOWFLAKE.CORTEX_USER TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. セマンティックビューへのアクセスを許可します。

   ```sql
   GRANT USAGE ON DATABASE <SEMANTIC_VIEW_DB> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT USAGE ON SCHEMA <SEMANTIC_VIEW_DB>.<SEMANTIC_VIEW_SCHEMA> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON ALL VIEWS IN SCHEMA <SEMANTIC_VIEW_DB>.<SEMANTIC_VIEW_SCHEMA> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON SEMANTIC VIEW <SEMANTIC_VIEW_NAME> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. （オプション）利用可能な大規模言語モデル（LLMs）を構成します。モデルリストを管理するために、役割に `app_admin` を付与します。

   ```sql
   GRANT APPLICATION ROLE TEALIUM_AUDIENCE_DISCOVERY_APP.app_admin TO ROLE <ADMIN_ROLE>;
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
       ('mistral-large2'),
       ('llama3.1-70b'),
       ('llama3.1-405b'),
       ('snowflake-arctic'),
       ('claude-3-5-sonnet');
   ```

   
<blockquote>
Snowflakeリージョンで有効になっているモデルのみをリストに含めてください。モデルをテストするには、`SELECT AI_COMPLETE(model => '<model_name>', prompt => 'Hello');` を実行します。
</blockquote>


### Webhook配信の有効化（オプション）

アプリは、オーディエンスデータを外部HTTPエンドポイントに送信できます。この機能はデフォルトで無効になっており、管理者の構成が必要です。


<blockquote>
この機能には、構成されたネットワークルールと外部アクセス統合が必要です。
</blockquote>


1. Webhookホストのためのネットワークルールを作成します。

   ```sql
   CREATE OR REPLACE NETWORK RULE webhook_egress_rule
     TYPE = HOST_PORT
     MODE = EGRESS
     VALUE_LIST = ('your-webhook-host.example.com:443');
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
   -- デフォルトの統合名 WEBHOOK_EXTERNAL_ACCESS を使用します
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.set_webhook_enabled(TRUE);

   -- カスタム統合名を指定します
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.set_webhook_enabled(TRUE, 'MY_CUSTOM_INTEGRATION');
   ```

   後でWebhook配信を無効にする場合：

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.set_webhook_enabled(FALSE);
   ```

オーディエンスデータを送信するには：

1. オーディエンスを開き、三点リーダーメニューをクリックします。
1. **Send to Webhook**を選択します。
1. HTTPS webhook URLを入力し、必要に応じて基本認証資格情報を入力します。
1. **Send**をクリックします。データはデフォルトで1,000行のバッチでJSON形式で配信され、最大1,000,000行までです。

すべての配信は`AUDIENCE_DISCOVERY_SCHEMA.WEBHOOK_LOG`にログされます。

```sql
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUDIENCE_DISCOVERY_SCHEMA.WEBHOOK_LOG
ORDER BY STARTED_AT DESC;
```
### Tealiumアプリケーションへのユーザーアクセスの構成

Snowflakeのユーザーにアプリへのアクセスを許可するために、専用のロールを作成し、そのロールにアプリケーションロールを割り当てます。

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
   GRANT ROLE TEALIUM_APP_USER TO USER <user>;
   ```

### Tealiumコネクターの外部アクセスの構成

各オーディエンスには、Tealium Snowflakeコネクターなどの外部消費者用に`USERS_EXTERNAL`セキュアビューが含まれています。このビューは、オーディエンスが非アクティブ化されたときに自動的にゼロ行を返し、再アクティブ化されたときに再開します。

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
   GRANT ROLE TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE TO USER <TEALIUM_SERVICE_USER>;
   ```

Tealiumコネクターは次のクエリを使用してオーディエンスを照会します：

```sql
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.<AUDIENCE_SCHEMA>.USERS_EXTERNAL;
```

ロール制限を確認するために、テスト前にセカンダリロールを無効にします。

```sql
USE SECONDARY ROLES NONE;
USE ROLE TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE;

-- アクティブなオーディエンスのデータを返すべきです
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUD_XXXXXXXXXXXXXXXX.USERS_EXTERNAL;

-- 権限不足で失敗するべきです
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUD_XXXXXXXXXXXXXXXX.USERS;

-- テスト後にセカンダリロールを再有効化します
USE SECONDARY ROLES ALL;
USE ROLE SYSADMIN;
```

## サービスの管理

アプリサービスのライフサイクルを管理するために、以下のストアドプロシージャを使用します。サービスを初めて作成する場合は、[サービスの構成](#set-up-the-service)を参照してください。削除後に再作成する場合は、同じSQLを実行します。

### サービスの停止

サービスを削除せずに一時停止します。コンテナは停止しますが、サービス定義は保持されます。

```sql
CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.stop_app_service();
```

### サービスの再開

以前に一時停止したサービスを再開します。

```sql
CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.resume_app_service();
```

### サービスの更新

アプリケーションのアップグレード後に新しいコンテナイメージを取り入れるために、サービス仕様を再適用します。

```sql
CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.refresh_app_service('TEALIUM_AUDIENCE_DISCOVERY_WH');
```

### サービスの削除

サービスを永久に削除します。再作成するには`create_app_service()`を使用します。

```sql
CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.drop_app_service();
```

### サービスの状態確認

```sql
CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.check_service_status();
```

### サービスログの表示

```sql
CALL SYSTEM$GET_SERVICE_LOGS('TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.audience_discovery_service', 0, 'audience-discovery-app', 100);
```

## トラブルシューティング

| 問題 | 解決策 |
|---|---|
| サービスがまだ作成されていない | コンピュートプールとウェアハウスを指定して`create_app_service()`を実行します。 |
| アプリケーションには専用のコンピュートプールが必要です | プールは`FOR APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP`で作成する必要があります。 |
| コンピュートプールが存在しないか、認証されていません | `FOR APPLICATION`でプールを作成し、アプリに`USAGE`を付与します。 |
| ソースデータが表示されない | ソースデータベースに対してアプリケーションに`USAGE`と`SELECT`を付与します。 |
| サービスの状態がPENDINGのままです | `DESCRIBE COMPUTE POOL <pool>`を実行し、状態が`ACTIVE`になるのを待ちます。 |
| エンドポイントにアクセスできません | `BIND SERVICE ENDPOINT`を付与し、Snowsightを更新してみてください。 |
| アプリケーションのURLにアクセスできません | ファイアウォールの[System Allowlist](https://docs.snowflake.com/en/sql-reference/functions/system_allowlist)がアプリのIDをSnowflake URLの先頭でブロックしていないことを確認してください。 |
| Webhookの配信が有効になっていません | `CALL main_schema.set_webhook_enabled(TRUE)`を実行します。これにより、外部アクセス統合もサービスにアタッチされます。 |
| Webhook接続エラー | ネットワークルールの`VALUE_LIST`を更新して、webhookホストを含めます。 |

## セキュリティとデータ取扱い

### データの居住地

すべてのデータはお客様のSnowflakeアカウント内に留まります。アプリは：

* デフォルトでは外部ネットワークリクエストを行いません。唯一の組み込みHTTPコールは、同じSnowflakeインフラストラクチャ上のSnowflake Cortex Analyst REST APIへのものです。
* テレメトリ、アナリティクス、自動データ流出を含みません。
* クッキーを使用しません。
* 平文でのシークレットの保存は行いません。認証はSnowpark Container Services (SPCS)のSnowflakeのOAuthトークンメカニズムを通じて処理されます。
* ビルド時にコンテナイメージにバンドルされた自己ホスト型フォントを使用します。実行時に外部サーバーへのリクエストは行われません。

管理者がネットワークルールと外部アクセス統合を使用してオプションのwebhook配信機能を有効にすると、ユーザーは指定されたHTTPSエンドポイントにオーディエンスデータを送信できます。この機能が管理者によって有効にされ、ユーザーが送信を開始した場合にのみ、送信が行われます。

### 認証

すべてのアクセスにはSnowflake認証が必要です。Web UIはSnowflakeのイングレスエンドポイントを通じて提供されます。公開されている未認証のエンドポイントはありません。

### 作成されるオブジェクト

アプリはお客様のSnowflakeアカウント内に以下のオブジェクトを作成します。

**スキーマ：**

* `MAIN_SCHEMA`: インフラストラクチャ
* `AUDIENCE_DISCOVERY_SCHEMA`: メタデータ
* `TEALIUM_EXTERNAL_ACCESS`: 外部アクセス用のセキュアビュー
* オーディエンスごとに1つの`AUD_*`スキーマ

**テーブル：**

* `AUDIENCES`: オーディエンスメタデータ
* `AVAILABLE_LLMS`: LLM構成
* `WEBHOOK_CONFIG`: 機能フラグ
* `WEBHOOK_LOG`: webhook配信監査ログ
* オーディエンスごとに1つの`USERS`テーブル

**ビュー：**

* オーディエンスごとに1つの`USERS_EXTERNAL`セキュアビュー。オーディエンスが非アクティブ化されたときにゼロ行を返し、再アクティブ化されたときに再開します。

**プロシージャ：** サービス管理およびオーディエンスライフサイクルのための所有者特権DDL実行者。

**タスク：** アクティブなオーディエンスごとに1つの`REFRESH_TASK`がスケジュールされたリフレッシュのためにあります。

**サービス：** コンテナ化されたアプリケーションを実行する`audience_discovery_service`。

### データ保持

オーディエンスメタデータ（名前、説明、構成、ユーザー数、タイムスタンプを含む）は`AUDIENCES`テーブルに無期限に保存されます。各オーディエンスバージョンは履歴追跡のために別の行として保存されます。オーディエンスを削除すると、関連するすべてのデータ（メタデータ行およびオーディエンススキーマを含む）が削除されます。