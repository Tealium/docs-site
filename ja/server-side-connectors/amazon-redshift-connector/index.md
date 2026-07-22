---
title: Amazon Redshift コネクタ構成ガイド
description: この記事では、Amazon Redshift コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/amazon-redshift-connector/
---
## 大規模な訪問プロファイルの取り扱い

[**Send Entire Visitor Data** アクション](#send-entire-visitor-data-micro-batch)は、各SQL INSERT文に訪問のJSON全体を埋め込みます。Redshift Data APIはSQL文ごとに100kBの制限を課しているため、訪問プロファイルがこの制限を超えると、コネクタアクションは `ValidationException: Query string size exceeds 100 kB` エラーで失敗します。

この問題を避けるために、以下のガイドラインに従ってください：

* **小規模な訪問プロファイルにはSend Entire Visitor Dataを使用します。**  
数キロバイトを超える訪問プロファイルは制限を超えるリスクが高まります。訪問プロファイルが100kBの制限を大幅に下回る場合にこのアクションを使用してください。[訪問検索](https://docs.tealium.com/visitor-search/)を使用して完全なプロファイルを取得し、そのサイズを評価してください。
* **プロファイル全体ではなく、マッピングされた属性を送信します。**  
[**Send Custom Visitor Data**](#send-custom-visitor-data-micro-batch) アクションを使用して、必要な属性のみを選択し、訪問のJSON全体を送信するのではなく、必要な属性のみを送信します。
* **S3およびRedshiftを使用して、大量または履歴データをロードします。**  
大規模な訪問JSONペイロードや一度きりの大量アップロードの場合、訪問データを [S3コネクタ](https://docs.tealium.com/amazon-s3-connector/) に送信し、COPYコマンドを使用してRedshiftにデータをロードします。詳細については、[Amazon Redshift: Amazon S3からのCOPYコマンドを使用したロード](https://docs.aws.amazon.com/redshift/latest/dg/t_loading-tables-from-s3.html)を参照してください。
* **大規模なペイロードにはWebhook (JDBC) コネクタを使用します。**
[Webhook (JDBC) コネクタ](https://docs.tealium.com/webhook-jdbc/)はJDBCを介して直接Redshiftに接続し、Redshift Data APIの100kB制限を回避します。訪問プロファイルが100kBを超える場合はこのオプションを使用してください。

## 構成

コネクタマーケットプレイスにアクセスして新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **認証タイプ**  
  * 認証タイプを選択します：
    * **STS**：次のフィールドが必要です **Assume Role: ARN**, **Assume Role: Session Name**。詳細については、[STS credentials](#sts-credentials)を参照してください。
    * **Access Key**：次のフィールドが必要です **AWS Access Key** および **AWS Secret Access Key**。詳細については、[Access Key and Secret credentials](#access-key-and-secret-credentials)を参照してください。
* **STS - Assume Role: ARN**  
  * STS認証に必要です。役割を引き受けるためのAmazonリソース名（ARN）を提供してください。
  * 例：`arn:aws:iam:222222222222:role/myrole`。
  * 詳細については、[AWS: IAMロールへの切り替え](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。
* **STS - Assume Role: Session Name**  
  * STS認証に必要です。役割を引き受けるためのセッション名を提供してください。
  * 最小長2、最大長64。
* **STS - Assume Role: External ID**  
  * 第三者の外部識別子を提供してください。
  * 詳細については、[AWS: 第三者が所有するAWSアカウントへのアクセス](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html)を参照してください。
* **Access Key - AWS Access Key**  
  * Access Key認証に必要です。AWSアクセスキーを提供してください。
* **Access Key - AWS Secret Access Key**  
  * Access Key認証に必要です。AWSシークレットアクセスキーを提供してください。
* **Region**  
  * （必須）リージョンを選択してください。
* **Secret Name**  
  * （オプション）AWS Secrets Managerメソッドを使用してRedshiftにアクセスする場合、TealiumがRedshift接続に使用するSecret ARNを動的に取得するために、Secret Nameを提供してください。
* **Workgroup Name**  
  * **Cluster Identifier**が提供されていない場合に必要です。Redshift SERVERLESSインスタンスにアクセスする場合は、ワークグループ名を提供してください。
* **Cluster Identifier**  
  * **Workgroup Name**が提videdされていない場合に必要です。Redshiftクラスターを使用している場合は、クラスター識別子を提供してください。
* **Database Name**  
  * （オプション）データベース名を提供してください。デフォルト値：`dev`。

### AWS Redshiftへの接続を作成する

Tealiumは、クラスター、ワークスペース、データベースのリストを表示し、イベントおよびオーディエンスデータをRedshiftテーブルにアップロードするために、AWS Redshiftインスタンスへの接続を必要とします。認証には2つのオプションがあります：

* [Access KeyとAccess Secretを提供する](#access-key-and-secret-credentials)。
* [STS認証情報を提供する](#sts-credentials)。

#### Access KeyとSecret認証情報

AWS Access KeyとSecretを見つけるには：

1. AWS管理コンソールにログインし、**IAM**（Identity and Access Management）サービスにアクセスします。
1. **ユーザー**をクリックし、**ユーザーを追加**をクリックします。
1. ユーザー名を入力します。例：`TealiumRedshiftUser`。
1. 役割にポリシーをアタッチします。詳細については、[ポリシーのアタッチ](#attach-policies)を参照してください。
1. キーを作成します。
    * **セキュリティ認証情報**タブに移動し、**アクセスキーの作成**をクリックします。
    * **アクセスキーID**と**シークレットアクセスキー**をコピーし、安全に保存します。

#### STS認証情報

STS認証情報を見つけるには：

1. AWS管理コンソールにログインし、**IAM**（Identity and Access Management）サービスにアクセスします。
1. **ロール**をクリックし、**ロールの作成**をクリックします。
1. **信頼されたエンティティタイプ**の下で、AWSアカウントを選択します。
1. 別のAWSアカウントを選択し、TealiumアカウントID：`757913464184`を入力します。
1. （オプション）**外部IDが必要**チェックボックスを選択し、使用したい外部IDを指定します。外部IDは256文字までの長さで、英数字（`A-Z`, `a-z`, `0-9`）およびハイフン（`-`）、アンダースコア（`_`）、ピリオド（`.`）などの記号を含むことができます。
1. ロールの名前を入力します。ロール名は`TealiumRedshift`で始まる必要があります。例：`TealiumRedshift-test`。
1. ロールにポリシーをアタッチします。詳細については、[ポリシーのアタッチ](#attach-policies)を参照してください。
1. 信頼ポリシーを作成します。
    * **信頼関係**タブに移動し、**信頼関係の編集**をクリックします。
    * 作成したロールを使用する特定の外部IDが信頼ポリシーに許可されていること、およびTealiumの本番アカウントIDが`757913464184`であることを確認します。
    * Tealiumへの接続に使用する`EXTERNAL_ID`値を構成します。IDは256文字までの長さで、英数字（`A-Z`, `a-z`, `0-9`）およびハイフン（`-`）、アンダースコア（`_`）、ピリオド（`.`）などの記号を含むことができます。
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": {
            "AWS": "arn:aws:iam::757913464184:root"
          },
          "Action": "sts:AssumeRole",
          "Condition": {
            "StringEquals": {
              "sts:ExternalId": "EXTERNAL_ID"
            }
          }
        }
      ]
    }
    ```
#### ポリシーのアタッチ

ポリシーをアタッチするには：

1. **権限**タブで、**既存のポリシーを直接アタッチ**をクリックします。
    1. フルアクセス
        * `SecretsManagerReadWrite`、`AmazonRedshiftAllCommandsFullAccess`、`AmazonRedshiftDataFullAccess` ポリシーを検索してアタッチし、フルアクセスを許可します。
    1. 制限されたアクセス
        * 特定のクラスターへのアクセスを制限するには、以下の例のようなポリシーを作成します。例では、`YOUR_CLUSTER_ARN` が Tealium がイベントおよびオーディエンスデータを `YOUR_DATABASE_ARN` Redshift テーブルに挿入するために使用するクラスターです：
        ```json
        {
          "Version": "2012-10-17",
          "Statement": [
            {
              "Sid": "RedshiftClusterManagement",
              "Effect": "Allow",
              "Action": [
                "redshift:DescribeClusters",
                "redshift:GetClusterCredentials",
                "redshift:GetClusterCredentialsWithIAM"
              ],
              "Resource": "arn:aws:redshift:YOUR_REGION:YOUR_ACCOUNT_ID:cluster/YOUR_CLUSTER_ARN"
            },
            {
              "Sid": "RedshiftDataAPI",
              "Effect": "Allow",
              "Action": [
                "redshift-data:ExecuteStatement",
                "redshift-data:BatchExecuteStatement",
                "redshift-data:DescribeStatement",
                "redshift-data:GetStatementResult",
                "redshift-data:ListStatements"
              ],
              "Resource": "arn:aws:redshift:YOUR_REGION:YOUR_ACCOUNT_ID:database/YOUR_DATABASE_ARN"
            },
            {
              "Sid": "SecretsManagerAccess",
              "Effect": "Allow",
              "Action": [
                "secretsmanager:GetSecretValue",
                "secretsmanager:DescribeSecret",
                "secretsmanager:ListSecrets"
              ],
              "Resource": "arn:aws:secretsmanager:YOUR_REGION:YOUR_ACCOUNT_ID:secret/YOUR_SECRET_ARN"
            }
          ]
        }
        ```

        * 特定のワークグループへのアクセスを制限するには、以下の例のようなポリシーを作成します。例では、`YOUR_WORKGROUP_ARN` が Tealium がイベントおよびオーディエンスデータを `YOUR_DATABASE_ARN` Redshift テーブルに挿入するために使用するクラスターです：

        ```json
        {
          "Version": "2012-10-17",
          "Statement": [
            {
              "Sid": "RedshiftServerlessAccess",
              "Effect": "Allow",
              "Action": [
                "redshift-serverless:GetWorkgroup",
                "redshift-serverless:GetCredentials",
                "redshift-serverless:ListWorkgroups"
              ],
              "Resource": "arn:aws:redshift-serverless:YOUR_REGION:YOUR_ACCOUNT_ID:workgroup/YOUR_WORKGROUP_ARN"
            },
            {
              "Sid": "RedshiftDataAPI",
              "Effect": "Allow",
              "Action": [
                "redshift-data:ExecuteStatement",
                "redshift-data:BatchExecuteStatement",
                "redshift-data:DescribeStatement",
                "redshift-data:GetStatementResult",
                "redshift-data:ListStatements"
              ],
              "Resource": "arn:aws:redshift:YOUR_REGION:YOUR_ACCOUNT_ID:database/YOUR_DATABASE_ARN"
            },
            {
              "Sid": "SecretsManagerAccess",
              "Effect": "Allow",
              "Action": [
                "secretsmanager:GetSecretValue",
                "secretsmanager:DescribeSecret",
                "secretsmanager:ListSecrets"
              ],
              "Resource": "arn:aws:secretsmanager:YOUR_REGION:YOUR_ACCOUNT_ID:secret/YOUR_SECRET_ARN"
            }
          ]
        }
        ```

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| 全イベントデータ送信（マイクロバッチ） | ✗ | ✓ |
| 全イベントデータ送信（バッチ） | ✗ | ✓ |
| カスタムイベントデータ送信（マイクロバッチ） | ✗ | ✓ |
| カスタムイベントデータ送信（バッチ） | ✗ | ✓ |
| 全訪問データ送信（マイクロバッチ） | ✓ | ✗ |
| 全訪問データ送信（バッチ） | ✓ | ✗ |
| カスタム訪問データ送信（マイクロバッチ） | ✓ | ✗ |
| カスタム訪問データ送信（バッチ） | ✓ | ✗ |
| カスタムステートメント実行（バッチ） | ✓ | ✓ |
| 全ログイベントデータ送信（マイクロバッチ） | ✗ | ✓ |
| ログイベントデータ送信（マイクロバッチ） | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### 全イベントデータ送信（マイクロバッチ）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：50
* 最古のリクエストからの最大時間：16分

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を提供します。 |
| テーブル | 接続したいテーブル名を提供します。 |
| ペイロードを記録するカラム | ペイロードを記録するために `SUPER` カラムを選択します。 |
| タイムスタンプを記録するカラム | タイムスタンプを記録するカラムを選択します。テーブルに **timestamp** カラムが **default sysdate** に構成されている場合は不要です。 |
| 属性名の印刷 | デフォルトでは、属性キーが使用されます。代わりに属性名をキーとして使用したい場合は、このチェックボックスを有効にします。属性名が更新されるとペイロード名も更新されることに注意してください。 |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するために有効期限（TTL）を構成します。`1`から`16`分の間の値を入力します。デフォルト値は`5`分です。 |

### 全イベントデータ送信（バッチ）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：2,000
* 最古のリクエストからの最大時間：60分

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を提供します。 |
| テーブル | 接続したいテーブル名を提供します。 |
| ペイロードを記録するカラム | ペイロードを記録するために `SUPER` カラムを選択します。 |
| タイムスタンプを記録するカラム | タイムスタンプを記録するカラムを選択します。テーブルに **timestamp** カラムが **default sysdate** に構成されている場合は不要です。 |
| 属性名の印刷 | デフォルトでは、属性キーが使用されます。代わりに属性名をキーとして使用したい場合は、このチェックボックスを有効にします。属性名が更新されるとペイロード名も更新されることに注意してください。 |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するために有効期限（TTL）を構成します。`15`から`60`分の間の値を入力します。デフォルト値は`30`分です。 |

### カスタムイベントデータ送信（マイクロバッチ）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：50
* 最古のリクエストからの最大時間：16分

#### パラメータ

テーブルのカラムに属性をマッピングします。

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を提供します。 |
| テーブル | 接続したいテーブル名を提供します。 |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するために有効期限（TTL）を構成します。`1`から`16`分の間の値を入力します。デフォルト値は`5`分です。 |

### カスタムイベントデータ送信（バッチ）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：2,000
* 最古のリクエストからの最大時間：60分
#### パラメータ

テーブルの列に属性をマッピングします。

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を指定してください。 |
| テーブル | 接続したいテーブル名を指定してください。 |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するための有効期限（TTL）を構成します。`15`分から`60`分の間で値を入力してください。デフォルト値は`30`分です。 |

### 全訪問データの送信（マイクロバッチ）


<blockquote>
Redshift Data APIはSQLステートメントを100 kBに制限しています。訪問のJSONペイロードがこの制限を超えると、コネクタアクションが失敗します。
この問題を回避するためのガイドラインについては、[大きな訪問プロファイルの取り扱い](#working-with-large-visitor-profiles)を参照してください。
</blockquote>


#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストがキューに入ります：

* 最大リクエスト数：50
* 最古のリクエストからの最大時間：16分

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を指定してください。 |
| テーブル | 接続したいテーブル名を指定してください。 |
| ペイロードを記録する列 | ペイロードを記録するために`SUPER`列を選択してください。 |
| タイムスタンプを記録する列 | タイムスタンプを記録する列を選択してください。テーブルに**timestamp**列が**default sysdate**に構成されている場合は不要です。 |
| 全訪問イベントを含む | 訪問データに現在の訪問データを含めます。 |
| 属性名を印刷 | デフォルトでは属性キーが使用されます。代わりに属性名をキーとして使用したい場合は、このチェックボックスを有効にしてください。属性名が更新されるとペイロード名が更新を反映することに注意してください。 |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するための有効期限（TTL）を構成します。`1`分から`16`分の間で値を入力してください。デフォルト値は`5`分です。 |

### 全訪問データの送信（バッチ）


<blockquote>
Redshift Data APIはSQLステートメントを100 kBに制限しています。訪問のJSONペイロードがこの制限を超えると、コネクタアクションが失敗します。
この問題を回避するためのガイドラインについては、[大きな訪問プロファイルの取り扱い](#working-with-large-visitor-profiles)を参照してください。
</blockquote>


#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストがキューに入ります：

* 最大リクエスト数：2,000
* 最古のリクエストからの最大時間：60分

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を指定してください。 |
| テーブル | 接続したいテーブル名を指定してください。 |
| ペイロードを記録する列 | ペイロードを記録するために`SUPER`列を選択してください。 |
| タイムスタンプを記録する列 | タイムスタンプを記録する列を選択してください。テーブルに**timestamp**列が**default sysdate**に構成されている場合は不要です。 |
| 全訪問イベントを含む | 訪問データに現在の訪問データを含めます。 |
| 属性名を印刷 | デフォルトでは属性キーが使用されます。代わりに属性名をキーとして使用したい場合は、このチェックボックスを有効にしてください。属性名が更新されるとペイロード名が更新を反映することに注意してください。 |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するための有効期限（TTL）を構成します。`15`分から`60`分の間で値を入力してください。デフォルト値は`30`分です。 |

### カスタム訪問データの送信（マイクロバッチ）

#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストがキューに入ります：

* 最大リクエスト数：50
* 最古のリクエストからの最大時間：16分

#### パラメータ

テーブルの列に属性をマッピングします。

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を指定してください。 |
| テーブル | 接続したいテーブル名を指定してください。 |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するための有効期限（TTL）を構成します。`1`分から`16`分の間で値を入力してください。デフォルト値は`5`分です。 |

### カスタム訪問データの送信（バッチ）

#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストがキューに入ります：

* 最大リクエスト数：2,000
* 最古のリクエストからの最大時間：60分

#### パラメータ

テーブルの列に属性をマッピングします。

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を指定してください。 |
| テーブル | 接続したいテーブル名を指定してください。 |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するための有効期限（TTL）を構成します。`15`分から`60`分の間で値を入力してください。デフォルト値は`15`分です。 |

### カスタムステートメントの実行（バッチ）

#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストがキューに入ります：

* 最大リクエスト数：40
* 最古のリクエストからの最大時間：60分

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を指定してください。 |
| テーブル | 接続したいテーブル名を指定してください。 |
| クエリパラメータ | クエリ内のプレースホルダーに置き換えるパラメータをマッピングしてください。少なくとも1つのパラメータをマッピングする必要があります。 |
| クエリ | `SQL`属性に渡す生のステートメントを指定してください。`INSERT`、`UPDATE`、または`MERGE`ステートメントのみが許可されます。変数を参照するには属性名の前に`:`を追加してください。詳細については、[クエリ例](#query-example)を参照してください。|
| バッチの有効期限 | バッチを送信するまでの待ち時間です。この値は`1`分から`60`分の間で構成できます。デフォルト値は`15`分です。 |

#### クエリ例

**クエリパラメータ**セクションでマッピングを追加した場合、例えば`my_boolean_tealium_attribute = MY_BOOLEAN_PARAM`とした場合、クエリ内でそのパラメータを`:MY_BOOLEAN_PARAM`を使用して参照します。

クエリの例では、次のクエリパラメータがマッピングされています：`MY_STRING_PARAM`, `MY_BOOLEAN_PARAM`, `ANOTHER_PARAM`, `MY_PARAM`.

```sql
INSERT INTO redshift_table
  (key1, key2) VALUES (':MY_STRING_PARAM', :MY_BOOLEAN_PARAM);
UPDATE redshift_table SET
  key1 = ':MY_STRING_PARAM',
  key2 = :MY_BOOLEAN_PARAM
WHERE
  key3 = ':ANOTHER_PARAM';
UPDATE redshift_table
  SET key2 = (SELECT new_key2 FROM source_table WHERE source_table.key1 = redshift_table.key1)
WHERE EXISTS
  (SELECT 1 FROM source_table WHERE source_table.key1 LIKE %:MY_PARAM%);
```

#### デバッグ

Tealiumが成功したレスポンスを返してもRedshiftにデータが表示されない場合、SQLステートメントがTealiumによって受け入れられた後にRedshiftによって拒否されている可能性があります。

調査するには：

1. [トレース](https://docs.tealium.com/about-trace/)を実行し、成功した呼び出しのレスポンスボディからIDをメモします。
1. [Amazon Redshift Data API](https://docs.aws.amazon.com/redshift-data/latest/APIReference/API_DescribeStatement.html)を使用して、SQLステートメントの詳細を確認します。

トレースからのID値を置き換えて、次のリクエストを送信します：

```http
POST / HTTP/1.1
Host: redshift-data.us-east-1.amazonaws.com
X-Amz-Target: RedshiftData.DescribeStatement
Content-Type: application/x-amz-json-1.1
Authorization: AUTHORIZATION_HEADER
X-Amz-Date: TIMESTAMP

{
    "Id": "37eb2735-b467-4852-884b-0f536970bf7e"
}
```

レスポンスにはステートメントのステータスとRedshiftによって返されたエラーメッセージが含まれます。

### 全ログイベントの送信（マイクロバッチ）
#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。並列処理により、イベントが順不同でベンダーに到達する可能性があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：50
* 最古のリクエストからの最大時間：16分

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を指定してください。 |
| テーブル | 接続したいテーブル名を指定してください。 |
| ペイロードを記録するカラム | ペイロードを記録するために `SUPER` カラムを選択してください。 |
| タイムスタンプを記録するカラム | タイムスタンプを記録するカラムを選択してください。テーブルに `default sysdate` で構成された `timestamp` カラムが既にある場合は不要です。 |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するための有効期限（TTL）を構成してください。`1`分から`16`分の間で値を入力してください。デフォルト値は`5`分です。 |

### ログイベント送信（マイクロバッチ）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。並列処理により、イベントが順不同でベンダーに到達する可能性があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：50
* 最古のリクエストからの最大時間：16分

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| スキーマ | 接続したいスキーマ名を指定してください。 |
| テーブル | 接続したいテーブル名を指定してください。 |
| ログイベントリソース属性 | テレメトリが記録されるエンティティに関する情報をキャプチャするフィールドです。 |
| ログイベントHTTP属性 | ログシステム内のHTTPリクエストとレスポンスを記録するフィールドです。`http`配列全体を単一のカラムにマッピングするには、`http`属性をマッピングしてください。 |
| ログイベント結果属性 | 操作の結果を記録するフィールドで、成功したかエラーが発生したかを詳細に説明します。 |
| ログイベントその他の属性 | ログされたイベントに関する追加のメタデータを提供するフィールドです。 |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するための有効期限（TTL）を構成してください。`1`分から`16`分の間で値を入力してください。デフォルト値は`5`分です。 |