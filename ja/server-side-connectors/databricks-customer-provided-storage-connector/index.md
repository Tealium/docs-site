---
title: Databricksコネクタ構成ガイド
description: この記事では、Databricksコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/databricks-customer-provided-storage-connector/
---

<blockquote>
このコネクタは、左側のナビゲーションで**コネクタ**をクリックしてアクセスできる[新しいコネクタインターフェイス](https://docs.tealium.com/about-connectors/)でのみ利用できます。
</blockquote>


## 要件

**Databricks OAuth**認証タイプを使用する場合は、コネクタを構成する前に、サービスプリンシパルに以下の権限を付与してください。これらの権限がない場合、接続テスト、ノートブックの作成、またはジョブの実行が失敗します。

* `MANAGE`権限を持つユーザーによって付与されるUnity Catalog権限：
    * カタログに対する`USE CATALOG`。
    * スキーマに対する`USE SCHEMA`。
    * ボリュームに対する`READ VOLUME`および`WRITE VOLUME`。
    * スキーマに対する`CREATE TABLE`、`MODIFY`、および`SELECT`。
* ワークスペースのエンタイトルメント：
    * サービスプリンシパルがワークスペースに表示されるようにするためのワークスペースアクセス権。
    * サービスプリンシパルがジョブを作成および管理できるようにするための、Jobsリソースに対する`CAN MANAGE`。
    * サービスプリンシパルとしてジョブを実行するために必要な**Service principal: User**ロール。
* **JDBC HTTPパス**フィールドで参照されるSQLウェアハウスに対する`CAN USE`。この権限がない場合、接続テストが失敗します。
* ノートブックを格納するワークスペースフォルダーに対する`CAN MANAGE`または`CAN EDIT`。これらの権限のいずれかがない場合、ノートブックの作成が失敗します。
* 生成されたジョブ用のコンピュート。デフォルトではサーバーレスコンピュートが使用されます。サービスプリンシパルがサーバーレスコンピュートにアクセスできる場合、クラスターの構成は必要ありません。ワークスペースでサーバーレスコンピュートが制限されているか、有効になっていない場合は、サービスプリンシパルにクラスターを作成する権限も必要です。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| イベントデータ全体を送信 | ✗ | ✓ |
| カスタムイベントデータを送信 | ✗ | ✓ |
| 訪問データ全体を送信 | ✓ | ✗ |
| カスタム訪問データを送信 | ✓ | ✗ |
| イベントデータ全体を送信（バッチ） | ✗ | ✓ |
| カスタムイベントデータを送信（バッチ） | ✗ | ✓ |
| 訪問データ全体を送信（バッチ） | ✓ | ✗ |
| カスタム訪問データを送信（バッチ） | ✓ | ✗ |
| ログイベントを送信 | ✗ | ✓ |
| ログイベント全体を送信 | ✗ | ✓ |


## 仕組み

Databricksコネクタは、次の2つの接続アーキテクチャをサポートしています。

* **Databricks Unity Catalogボリューム**：TealiumはUnity Catalogボリュームにファイルを直接書き込みます。Databricksから保存への接続を別途用意する必要はありません。
* **外部クラウド保存（AWS S3、Azure Blob Storage、Google Cloud Storage）**：Tealiumは外部保存バケットにファイルを書き込み、Databricksは保存資格情報と外部ロケーションを使用して同じバケットからファイルを読み取ります。

### 出力ファイル形式

**全体を送信**アクションでは、コネクタは各イベントまたは訪問レコードを、次の2つのトップレベルフィールドを持つ単一行のJSONファイルとしてクラウド保存の場所に書き込みます。

* `event_payload`：イベントまたは訪問のすべての属性を含むJSON文字列。このフィールドはシリアル化された文字列であり、ネストされたJSONオブジェクトではありません。
* `event_timestamp`：ISO 8601形式のイベント時刻。Tealiumによってこのフィールドが自動的に追加されます。

次の例は、1つのファイルの内容を示しています。

```json
{"event_payload":"{\"tealium_event\":\"purchase\",\"order_total\":\"129.99\"}","event_timestamp":"2026-09-14T10:32:11Z"}
```

コネクタはクラウド保存にのみファイルを書き込みます。アクションでDatabricksテーブルを選択しても、そのテーブルにデータは読み込まれません。Tealiumが作成するノートブックとジョブ、または独自に作成したノートブックとジョブを使用して、ファイルを読み取り、データを読み込む必要があります。詳細については、[ノートブックの作成](#create-a-notebook)および[ジョブの作成](#create-a-job)を参照してください。


<blockquote>
**全体を送信**アクションは、APIキーや測定シークレットなど、他のベンダーの資格情報を保持する属性を含め、イベントまたは訪問プロファイルのすべての属性を`event_payload`に書き込みます。コネクタを有効にする前にデータレイヤーを監査し、属性フィルタリングを使用して機密属性を除外してください。
</blockquote>


### Tealiumからクラウド保存への接続

Tealiumがバケットを一覧表示し、イベントデータとオーディエンスデータをクラウド保存のオブジェクトおよびファイルにアップロードするには、Databricks Unity Catalogボリューム、AWS S3、Azure Blob Storage、またはGoogle Cloud Storageインスタンスへの接続が必要です。Databricksコネクタでは、次の認証オプションを使用できます。

* [Databricks Unity Catalog](#databricks-unity-catalog-settings)
    * クライアントIDとクライアントシークレット（OAuth）を指定します。
* [AWS S3](#aws-s3-settings)
    * アクセスキーとアクセスシークレットを指定します。
    * STS（Security Token Service）の資格情報を指定します。
* [Azure Blob Storage](#azure-blob-storage-settings)
    * クライアント資格情報。
    * 認可コードフロー（SSO）。
    * Shared Access Signature（SAS）。
* [Google Cloud Storage](#google-cloud-storage-settings)
    * Googleでログイン（SSO）。

#### Databricks Unity Catalogの構成

##### クライアントIDとシークレットの資格情報

Databricksアカウント用の新しいOAuth資格情報を生成するには、次の手順を実行します。

1. Databricksインスタンスにログインします。
1. ワークスペースに移動します。
1. 画面右上隅で、**Settings > Identity and access > Service principals**に移動します。
1. 新しいサービスプリンシパルを作成するか、既存のサービスプリンシパルをクリックします。
1. **Secrets**タブをクリックし、**Generate secret**をクリックします。
1. **Permissions**タブをクリックし、サービスプリンシパルに**Service principal: User**ロールが割り当てられていることを確認します。

#### AWS S3の構成

##### アクセスキーとシークレットの資格情報

AWSアクセスキーとシークレットを確認するには、次の手順を実行します。

1. AWS Management Consoleにログインし、IAM（Identity and Access Management）サービスに移動します。
1. **Users**をクリックし、次に**Add user**をクリックします。
1. ユーザー名を入力します。例：`TealiumS3User`。
1. 作成したユーザーにポリシーをアタッチします。
    1. **Permissions**タブで、**Attach existing policies directly**をクリックします。
    1. フルアクセスを付与するには、`AmazonS3FullAccess`ポリシーを検索してアタッチします。特定のバケットへのアクセスに制限する場合は、次の例と同様のポリシーを作成できます。この例では、`YOUR_BUCKET_NAME`は、TealiumがイベントデータとオーディエンスデータをS3オブジェクトにアップロードするために使用するバケットです。
        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "s3:ListBucket",
                        "s3:PutObject",
                        "s3:GetObject",
                        "s3:ListBucketMultipartUploads",
                        "s3:ListMultipartUploadParts"
                    ],
                    "Resource": [
                        "arn:aws:s3:::YOUR_BUCKET_NAME",
                        "arn:aws:s3:::YOUR_BUCKET_NAME/*"
                    ]
                }
            ]
        }
        ```
1. キーを作成します。
    1. **Security credentials**タブに移動し、**Create Access Key**をクリックします。
    1. **Access Key ID**と**Secret Access Key**をコピーし、安全に保存します。
##### STS認証情報の構成

1. AWSマネジメントコンソールにログインし、IAM（Identity and Access Management）サービスに移動します。
1. **ロール**をクリックし、次に**ロールを作成**をクリックします。
1. **信頼されたエンティティタイプ**として、AWSアカウントを選択します。
1. **別のAWSアカウント**を選択し、TealiumのアカウントID `757913464184` を指定します。
1. （任意）**外部IDを要求する**チェックボックスをオンにし、使用する外部IDを指定します。外部IDは最大256文字で、英数字（`A-Z`、`a-z`、`0-9`）およびハイフン（`-`）、アンダースコア（`_`）、ピリオド（`.`）などの記号を使用できます。
1. ロールの名前を入力します。ロール名は `tealium-databricks` で始まる必要があります。例：`tealium-databricks-s3-test`
1. ロールにポリシーをアタッチします。
    1. **アクセス許可**タブで、**既存のポリシーを直接アタッチ**をクリックします。
    1. フルアクセスを許可するには、`AmazonS3FullAccess` ポリシーを検索してアタッチします。特定のバケットにアクセスを制限する場合は、以下の例のようなポリシーを作成できます。この例では、`YOUR_BUCKET_NAME` は、TealiumがイベントおよびオーディエンスデータをS3オブジェクトにアップロードするために使用するバケットです。
        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "s3:ListBucket",
                        "s3:PutObject",
                        "s3:GetObject",
                        "s3:ListBucketMultipartUploads",
                        "s3:ListMultipartUploadParts"
                    ],
                    "Resource": [
                        "arn:aws:s3:::YOUR_BUCKET_NAME",
                        "arn:aws:s3:::YOUR_BUCKET_NAME/*"
                    ]
                }
            ]
        }
        
        ```
1. 信頼ポリシーを作成します。
    1. **信頼関係**タブに移動し、**信頼関係を編集**をクリックします。
    1. 以下の例のように、作成したロールに対して特定の外部IDが信頼ポリシーで許可されていること、およびTealiumの本番環境のアカウントIDが `757913464184` であることを確認します。
    1. Tealiumへの接続に使用する `EXTERNAL_ID` の値を構成します。IDは最大256文字で、英数字（`A-Z`、`a-z`、`0-9`）およびハイフン（`-`）、アンダースコア（`_`）、ピリオド（`.`）などの記号を使用できます。
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

#### Azure Blob Storageの構成

##### クライアント認証情報

AzureでアプリケーションのテナントID、クライアントID、およびクライアントシークレットを取得するには、次の手順を実行します。

**手順1：Azure Portalにアクセスする**

1. Azure Portalに移動します。
1. Azureアカウントでサインインします。

**手順2：アプリの登録に移動する**

1. 画面上部の検索バーに `Azure Active Directory` と入力し、選択します。
1. 左側のメニューで、**アプリの登録**をクリックします。
1. 登録済みのアプリケーションを見つけます。

**手順3：テナントIDとクライアントIDを確認する**

1. アプリケーションをクリックします。
1. **概要**セクションで、次の情報を確認します。
    * **テナントID**（**ディレクトリID**とも呼ばれます）は、**テナントID**の下に表示されます。
    * **クライアントID**（**アプリケーションID**とも呼ばれます）は、**アプリケーション（クライアント）ID**として表示されます。

**手順4：クライアントシークレットを生成する**

1. 左側のメニューで、**証明書とシークレット**に移動します。
1. **クライアントシークレット**で、**新しいクライアントシークレット**をクリックします。
1. 説明を入力し、有効期限を選択します。
1. **追加**をクリックします。
1. シークレットを生成したら、すぐにコピーしてください。ページを離れると、再度表示することはできません。

##### Shared Access Signature（SAS）

AzureでShared Access Signature（SAS）トークンを生成するには、次の手順を実行します。

**手順1：Azure Portalにアクセスする**

1. Azure Portalに移動します。
1. Azureアカウントでサインインします。

**手順2：保存アカウントに移動する**

1. 検索バーに `Storage accounts` と入力し、選択します。
1. SASトークンを生成する保存アカウントを選択します。

**手順3：SASトークンを生成する**

オプション1：Azure Portalを使用する

1. **保存アカウント**で、**セキュリティとネットワーク**セクションにある**Shared Access Signature**に移動します。
1. 必要なアクセス許可（`Read`、`Write`、`Delete`、`List` など）を構成します。
1. トークンの有効期間を定義する有効期限の日時を構成します。
1. 許可するサービス（`Blob`、`File`、`Queue`、`Table`）を選択します。
1. **SASと接続文字列を生成する**をクリックします。
1. SASトークン、またはSASトークンを含む接続文字列をコピーします。

オプション2：Azure Storage Explorerを使用する

1. Azure Storage Explorerを開き、Azureアカウントにサインインします。
1. 保存アカウントを見つけ、*Blobコンテナー*またはファイル共有を右クリックします。
1. **Shared Access Signatureを取得する**を選択します。
1. アクセス許可と有効期限の構成を構成します。
1. **作成**をクリックし、生成されたSAS URLまたはトークンをコピーします。

オプション3：Azure CLIを使用する

1. Azure CLIで次のコマンドを実行し、SASトークンを生成します。
```sh
    az storage blob generate-sas \
        --account-name <your-storage-account> \
        --container-name <your-container> \
        --name <your-blob> \
        --permissions r \
        --expiry 2026-04-25T12:00:00Z \
        --output tsv
```

このコマンドはSASトークンを出力します。このトークンを保存URLに追加することで、制御されたアクセスを提供できます。

##### 認可コードフロー（SSO）

**接続を確立**をクリックすると、認可コードフローと呼ばれる安全な認証プロセスが開始されます。このプロセスにより、認証情報を手動で入力することなく、アプリケーションにAzure Blob Storageへのアクセスを許可できます。

次の処理が行われます。

1. **サインインへのリダイレクト：** Azure Active Directoryなど、組織のIDプロバイダー（IdP）に一時的にリダイレクトされ、既存の認証情報を使用してログインします。
1. **同意の付与**：認証後、Tealiumアプリが要求しているアクセス許可（具体的にはBlob Storageへのアクセス）を説明する同意画面が表示されます。
1. **Blob Storageへの安全なアクセス**：Tealiumアプリケーションは、Azureのセキュリティポリシーを維持しながら、保存を操作できるようになります。

#### Google Cloud Storageの構成

##### Googleでサインイン

**Googleでサインイン**をクリックすると、Googleアカウントを使用してアプリケーションからGoogle Cloud Storageへのアクセスを許可する、安全な認可プロセスが開始されます。

次の処理が行われます。

1. **Googleサインインへのリダイレクト**：Googleの認証ページに一時的にリダイレクトされ、Googleアカウントの認証情報を使用してログインします。
1. **同意の付与**：サインイン後、Cloud Storageへのアクセスなど、Tealiumアプリが要求しているアクセス許可の詳細を示す同意画面が表示されます。
1. **認可コードの受信**：承認すると、Googleが1回限りの認可コードを生成し、アプリケーションに返します。
1. **Cloud Storageへの安全なアクセス**：Tealiumアプリケーションは、Googleのセキュリティポリシーに従いながら、保存を操作できるようになります。

### DatabricksからAWS S3への接続

DatabricksをAWS S3インスタンスに接続するには、まずAWSインスタンスにIAMロールを作成する必要があります。このロールは、Databricksインスタンスで保存認証情報を作成するために使用されます。AWS IAMロールの作成方法について詳しくは、[Databricks：AWS S3に接続するための保存認証情報を作成する](https://docs.databricks.com/en/connect/unity-catalog/cloud-storage/storage-credentials.html)を参照してください。

保存認証情報を作成したら、データの取得元となるAWS S3インスタンス内の外部ロケーションを定義します。詳しくは、[Databricks：クラウド保存をDatabricksに接続するための外部ロケーションを作成する](https://docs.databricks.com/en/connect/unity-catalog/cloud-storage/external-locations.html)を参照してください。
### Databricks から Azure Blob Storage への接続

Databricks を Azure Blob Storage インスタンスに接続するには、Azure サービスプリンシパルまたはマネージド ID を使用して保存資格情報を作成する必要があります。これにより、Databricks は認証を行い、Blob Storage に安全にアクセスできます。詳細については、[Databricks：Azure Blob Storage に接続するための保存資格情報の作成](https://learn.microsoft.com/en-us/azure/databricks/connect/unity-catalog/cloud-storage/storage-credentials)を参照してください。

保存資格情報を構成した後、Databricks がデータの読み取りと書き込みに使用する外部ロケーションを Azure Blob Storage に定義します。詳細については、[Databricks：クラウド保存を Databricks に接続するための外部ロケーションの作成](https://learn.microsoft.com/en-us/azure/databricks/connect/unity-catalog/cloud-storage/external-locations)を参照してください。

### Databricks から Google Cloud Storage への接続

Google Cloud Storage を Databricks と統合するには、まず保存バケットへのアクセスに必要な権限を持つサービスアカウントを Google Cloud に構成する必要があります。次に、このサービスアカウントを認証に使用するための保存資格情報を Databricks で作成します。詳細については、[Databricks：Google Cloud Storage に接続するための保存資格情報の作成](https://docs.databricks.com/gcp/en/connect/unity-catalog/cloud-storage/storage-credentials)を参照してください。

保存資格情報を構成した後、Databricks がデータを操作するために必要なバケットと権限を指定して、Google Cloud Storage に外部ロケーションを定義する必要があります。詳細については、[Databricks：クラウド保存を Databricks に接続するための外部ロケーションの作成](https://docs.databricks.com/gcp/en/connect/unity-catalog/cloud-storage/external-locations)を参照してください。

## バッチの制限

このコネクターは、ベンダーへの大量のデータ転送に対応するため、リクエストをバッチ処理します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかのしきい値に達するか、プロファイルが公開されるまでキューに保持されます。

* リクエストの最大数：100,000
* 最も古いリクエストからの最大経過時間：1～60 分の範囲でカスタム TTL を構成できます。デフォルト値は 10 分です。
* リクエストの最大サイズ：10 MB

## 構成

コネクターマーケットプレイスに移動し、新しいコネクターを追加します。コネクターを追加する一般的な手順については、[コネクターについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクターを追加した後、以下の構成を構成します。コネクターと各アクションには、それぞれ個別の有効化スイッチがあります。


<blockquote>
アクションを保存した後、コネクターとアクションの両方が有効になっていることを確認してください。有効になっていない場合、データは送信されません。
</blockquote>


* **クラウドソリューション**：使用するクラウドソリューションを選択します。選択可能なオプションは、`Databricks Unity Catalog Volume`、`AWS S3`、`Azure Blob Storage`、`Google Cloud Storage` です。
* **Databricks ホスト URL**：Databricks ワークスペースの URL を指定します。例：`https://{ACCOUNT_NAME}.cloud.databricks.com`
* **Databricks トークン**：Databricks アクセストークンを指定します。Databricks Unity Catalog Volume にデータを送信する場合、このパラメーターは任意です。Databricks でアクセストークンを作成するには、Databricks のユーザーアバターをクリックし、**Settings > Developer > Access Tokens > Manage > Generate New Token** に移動します。

認証構成は、使用するクラウドソリューションによって異なります。

### Databricks Unity Catalog Volume


<blockquote>
1 分あたり 1,000 件を超えるイベントが見込まれる場合は、バッチアクションを使用してください。
</blockquote>


* **認証タイプ**：**Databricks OAuth** 認証タイプを選択します。
* **クライアント ID**：サービスプリンシパルシークレットに割り当てられた一意の識別子です。
* **シークレット**：パスワードのように機能する文字列で、アプリケーションがサービスプリンシパルとして Databricks で認証するために使用します。
* **JDBC HTTP パス**：コンピューティングリソースへの HTTP パスです。例：`/sql/1.0/warehouses/3fbc78304284503a`

### Amazon AWS S3

* **リージョン**：（必須）リージョンを選択します。
* **認証タイプ**：（必須）プラットフォームの認証タイプを選択します。
    * STS（Security Token Service）資格情報を指定します。
        * **STS - ロールの引き受け：ARN**：STS 認証では必須です。引き受けるロールの Amazon リソースネーム（ARN）を指定します。例：`arn:aws:iam:222222222222:role/myrole`。詳細については、[AWS Identity and Access Management：IAM ロールへの切り替え（AWS API）](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。
        * **STS - ロールの引き受け：セッション名**：STS 認証では必須です。引き受けるロールのセッション名を指定します。長さは 2～64 文字です。
        * **STS - ロールの引き受け：外部 ID**：STS 認証では必須です。サードパーティーの外部識別子を指定します。詳細については、[AWS Identity and Access Management：サードパーティーが所有する AWS アカウントへのアクセス](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html)を参照してください。
    * アクセスキーとアクセスシークレットを指定します。
        * **アクセスキー - AWS アクセスキー**：アクセスキー認証では必須です。AWS アクセスキーを指定します。
        * **アクセスキー - AWS シークレットアクセスキー**：アクセスキー認証では必須です。AWS シークレットアクセスキーを指定します。

### Google Cloud Storage

1. **Google でログイン**をクリックし、画面の指示に従います。
1. **プロジェクト ID**を選択します。

### Azure Blob Storage

* **認証タイプ**：認証タイプを選択します。選択可能なオプションは、クライアント資格情報、認可コードフロー（SSO）、共有アクセス署名（SAS）です。
    * クライアント資格情報を指定します。
        * **テナント ID**：組織を表す Azure Active Directory インスタンスの一意の識別子です。
        * **クライアント ID**：Azure Active Directory に登録されたアプリケーションに割り当てられた一意の識別子です。
        * **クライアントシークレット**：パスワードのように機能する文字列で、アプリケーションが Azure Active Directory で認証するために使用します。
        * **保存アカウント名**：Azure Storage アカウントの一意の名前で、Blob、File、Queue、Table などの保存サービスへのアクセスに使用します。
    * 認可コードフロー（SSO）を指定します。
        * **保存アカウント名**：Azure Storage アカウントの一意の名前です。**接続を確立**をクリックし、画面の指示に従います。
    * 共有アクセス署名（SAS）を指定します。
        * **共有アクセス署名**：Azure Storage アカウントの共有アクセス署名です。
        * **保存アカウント名**：Azure Storage アカウントの一意の名前です。
* **API バージョン**：Azure Storage インスタンスと互換性のある API バージョンです。
## ノートブックを作成する

Databricks のノートブックは、実行可能なコード、可視化、説明文を含むドキュメントです。データの探索、可視化、共同作業に使用されます。コネクターの構成時に、構成ステップで **Create Notebook** をクリックすると、新しいコネクターとともに新しいノートブックを作成できます。

1. コネクターの構成画面で **Create Notebook** をクリックします。
1. **Table Name** を入力します。スキーマはジョブの作成時に指定するため、このフィールドには含めないでください。
    * 名前には、英数字（`A-Z`、`a-z`、`0-9`）とアンダースコア（`_`）を使用できます。
    * スペース、および `!`、`@`、`#`、`-`、`.` などの特殊文字は使用できません。
    * 名前では大文字と小文字が区別されます。たとえば、`tableName` と `tablename` は異なる名前と見なされます。
    * 名前の先頭に数字は使用できません。たとえば、`1table` は無効です。
1. **Notebook Path** に、ノートブックの絶対パスを入力します。例：`/Workspace/Shared/data_ingestion/NOTEBOOK_NAME`。
    1. Databricks でノートブックの絶対パスを確認するには、Databricks ワークスペースに移動し、**Users** セクションを展開します。
    1. ユーザーをクリックし、オプションメニューを展開します。
    1. **Copy URL/Path > Full Path** をクリックします。パス名の形式は `/Workspace/Users/myemail@company.com` です。使用する仮想フォルダーとノートブック名を、スラッシュ `/` で区切って追加します。例：`/Workspace/Users/myemail@company.com/virtualfolder/virtualsubfolder/MyNotebook`。
1. **Cloud Bucket / Volume**：
    1. **Cloud Bucket** では、データの送信先として接続する Google Cloud Platform（GCP）、Azure Blob Storage、または AWS S3 の保存バケットを選択します。
    1. **Databricks OAuth** 認証タイプを使用している場合は、代わりに Databricks Unity Catalog Volume を指定します。
1. **Overwrite** オプションでは、指定したワークスペースに既存のノートブックがある場合に、そのノートブックを上書きするかどうかを指定します。


<blockquote>
ノートブックは、個人ユーザーフォルダーではなく、`/Workspace/Shared/data_ingestion` などの共有ワークスペースフォルダーまたは Git フォルダーに保存してください。個人フォルダー内のノートブックは、そのユーザーが無効化されるとアクセスできなくなり、ジョブが停止します。
</blockquote>


## ジョブを作成する

Databricks のジョブは、スケジュールまたは特定のトリガーに基づいてノートブックを自動実行します。ジョブを使用すると、データ処理、分析、レポート作成などのタスクを、一定の間隔または特定のイベントを契機として実行できます。

1. コネクターの構成画面で **Create Job** をクリックします。
1. 処理ジョブの名前を入力します。
1. **Catalog** では、パイプラインデータの公開先として使用する Unity Catalog のカタログを指定します。
1. **Target** では、上記のカタログ内でテーブルを公開または更新するスキーマを指定します。使用されるテーブルはノートブックで指定したテーブルであるため、ここではターゲットテーブルを指定しないでください。
1. **Notebook Path** に、ノートブックの絶対パスを入力します。例：`/Workspace/Shared/data_ingestion/NOTEBOOK_NAME`。
    1. Databricks でノートブックの絶対パスを確認するには、Databricks ワークスペースに移動し、**Users** セクションを展開します。
    1. ユーザーをクリックし、オプションメニューを展開します。
    1. **Copy URL/Path > Full Path** をクリックします。パス名の形式は `/Workspace/Users/myemail@company.com` です。使用する仮想フォルダーとノートブック名を、スラッシュ `/` で区切って追加します。例：`/Workspace/Users/myemail@company.com/virtualfolder/virtualsubfolder/MyNotebook`。
1. **Cloud Bucket** または **Volume** では、Databricks に接続するクラウド保存バケットまたは Databricks Unity Catalog Volume を選択します。
1. **Trigger Type** では、データを処理するタイミングを選択します。使用できるオプションは次のとおりです。
    * **File Arrived**：新しいファイルが到着するたびにデータを処理します。
    * **Scheduled**：指定した繰り返しスケジュールに従ってデータを処理します。
    * **Cron**：**Cron** フィールドで定義した繰り返しスケジュールに従ってデータを処理します。
1. **Start Time** では、ジョブ処理の開始時刻を `hh:mm` 形式で指定します。開始時刻のデフォルト値は `00:00` です。
1. **Timezone** では、タイムゾーンを `country/city` 形式で指定します。例：`Europe/London`。開始時刻を指定する場合、このフィールドは必須です。
1. **Cron** には、スケジュール処理に使用する Quartz cron 式を入力します。たとえば、`20 30 * * * ?` は、毎時30分20秒にファイルを処理します。詳細については、[Quartz：Cron トリガーのチュートリアル](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)を参照してください。

## ジョブとノートブックを作成する

ノートブックとジョブを同時に作成するには、**Create Notebook & Job** をクリックします。[ノートブックを作成する](#create-a-notebook)および[ジョブを作成する](#create-a-job)の各セクションの手順に従ってください。


<blockquote>
各作成ボタンをクリックすると、Databricks に新しいノートブックまたはジョブが作成されます。**Create** をクリックするとリソースが作成され、フォームは開いたままになります。**Create & Close** をクリックすると、別のリソース一式が作成されてからフォームが閉じます。**Create** をクリックした後にフォームを閉じる場合は、**Create & Close** ではなく上隅の **X** を使用してください。そうしないと、重複するジョブが作成されます。
</blockquote>


### ノートブックパスとジョブ ID を記録する

コネクターにはノートブックパスやジョブ ID が保存されず、作成フォームを開くたびに空の状態で表示されます。ノートブックまたはジョブを作成した後は、コネクターから構成を確認または編集できません。また、コネクターは既存のノートブックやジョブを検出しません。

後でパイプラインのトラブルシューティングを行う際にワークスペースを手動で検索する必要がないように、作成時に Databricks で次の値を記録してください。

* ノートブックの絶対パス。
* ジョブ ID とジョブ名。
* ジョブの書き込み先となるカタログ、スキーマ、テーブル。
* ジョブの読み取り元となるボリュームパス。

既存のノートブックまたはジョブを使用するには、ノートブックとジョブを Databricks で直接作成し、コネクターのボタンは使用しないでください。コネクターのボタンは、データエンジニアリング担当者がいないアカウント向けの補助機能であり、使用は必須ではありません。

### ターゲットテーブルごとに1つのコネクターを使用する

コネクターで使用されるのは、最初のノートブックと最初のジョブのみです。同じコネクターで2つ目のノートブックまたはジョブを作成しても、データの格納先には影響しません。複数の Databricks テーブルに書き込むには、テーブルごとに1つのコネクターを作成し、次のルールに従ってください。

1. **Files path** フィールドで、各コネクターにボリューム配下の固有のサブディレクトリを指定します。同じパスを共有する2つのコネクターでは、両方のテーブルに重複レコードが生成されます。
1. 1つのイベントが2つのコネクターに到達しないように、各コネクターに固有のデータソース、イベント仕様、またはイベントフィードを指定します。
1. コネクターごとに1つのノートブックと1つのジョブを作成します。

次の例は、2つのコネクターを使用する構成を示しています。

| コネクター | アクション | ファイルパス | ターゲットテーブル |
| --- | --- | --- | --- |
| 完全なペイロード | イベントデータ全体を送信 | `/Volumes/CATALOG/SCHEMA/VOLUME/purchase_events_full_payload` | `CATALOG.SCHEMA.purchase_events_raw` |
| フラット化 | カスタムイベントデータを送信 | `/Volumes/CATALOG/SCHEMA/VOLUME/purchase_events_flattened` | `CATALOG.SCHEMA.purchase_events_flattened_raw` |
### スキーマ変更後に Auto Loader のチェックポイントをリセットする

生成されたノートブックでは Auto Loader が使用され、すでに処理したファイルがボリュームのルートにある次のフォルダーに記録されます。

* `/Volumes/CATALOG/SCHEMA/VOLUME/_auto_loader_checkpoints`
* `/Volumes/CATALOG/SCHEMA/VOLUME/_auto_loader_schema`

Databricks は両方のフォルダーを自動的に作成します。列の型を変更するなど、テーブル定義を変更した後は、両方のフォルダーを削除してジョブを再実行してください。削除しない場合、Auto Loader はすでに検出したファイルをスキップするため、テーブルは空のままになります。


<blockquote>
チェックポイントフォルダーを削除すると、Auto Loader はすべてのソースファイルを最初から再処理します。これにより、ターゲットテーブルに重複レコードが作成される可能性があります。既存のチェックポイントとの互換性が失われるスキーマ変更を行った場合にのみチェックポイントを削除し、ジョブを実行する前に、ターゲットテーブルが空であるか、重複が排除されていることを確認してください。
</blockquote>


```python
dbutils.fs.rm("/Volumes/CATALOG/SCHEMA/VOLUME/_auto_loader_checkpoints", recurse=True)
dbutils.fs.rm("/Volumes/CATALOG/SCHEMA/VOLUME/_auto_loader_schema", recurse=True)
```

## アクション

以下のセクションでは、各アクションでサポートされているパラメータについて説明します。

### イベントデータ全体を送信する

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クラウドバケット | Databricks がデータを取得するクラウドバケットまたはコンテナを選択します。 |
| Databricks カタログ | Databricks カタログを選択するか、カスタム値を指定します。 |
| Databricks スキーマ | Databricks スキーマを選択するか、カスタム値を指定します。 |
| Databricks テーブル | Databricks テーブルを選択するか、カスタム値を指定します。 |
| ペイロードを記録する列 | ペイロードを記録する `STRING` 列を選択します。コネクタはペイロードをシリアル化された JSON 文字列として書き込むため、Delta 列は `STRING` である必要があります。列を `VARIANT` として宣言すると、読み込みは `DELTA_MERGE_INCOMPATIBLE_DATATYPE` で失敗します。個々のフィールドをクエリするには、`PARSE_JSON(column_name):field_name::TYPE` を使用します。 |
| タイムスタンプを記録する列 | タイムスタンプを記録する列を選択します。 |
| タイムスタンプ属性 | デフォルトでは、アクションの現在のタイムスタンプが送信されます。別の形式で送信する場合は、タイムスタンプとして割り当てる属性を選択します。属性が割り当てられていて、その値が空の場合は、現在のタイムスタンプが送信されます。 |

### カスタムイベントデータを送信する

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クラウドバケット | Databricks がデータを取得するクラウドバケットまたはコンテナを選択します。 |
| Databricks カタログ | Databricks カタログを選択するか、カスタム値を指定します。 |
| Databricks スキーマ | Databricks スキーマを選択するか、カスタム値を指定します。 |
| Databricks テーブル | Databricks テーブルを選択するか、カスタム値を指定します。 |
| イベントパラメータ | イベント属性を Databricks テーブルの列にマッピングします。少なくとも 1 つのイベント属性をマッピングする必要があります。 |


<blockquote>
このアクションでは、`event_timestamp` は自動的に追加されません。イベント時刻を記録するには、`tealium_timestamp_utc` 属性をタイムスタンプ列にマッピングし、列の型を `TIMESTAMP` に構成します。
</blockquote>


### ビジターデータ全体を送信する

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クラウドバケット | Databricks がデータを取得するクラウドバケットまたはコンテナを選択します。 |
| Databricks カタログ | Databricks カタログを選択するか、カスタム値を指定します。 |
| Databricks スキーマ | Databricks スキーマを選択するか、カスタム値を指定します。 |
| Databricks テーブル | Databricks テーブルを選択するか、カスタム値を指定します。 |
| ビジターデータを記録する列 | ビジターデータを記録する `STRING` 列を選択します。コネクタはビジターデータをシリアル化された JSON 文字列として書き込むため、Delta 列は `STRING` である必要があります。列を `VARIANT` として宣言すると、読み込みは `DELTA_MERGE_INCOMPATIBLE_DATATYPE` で失敗します。個々のフィールドをクエリするには、`PARSE_JSON(column_name):field_name::TYPE` を使用します。 |
| タイムスタンプを記録する列 | タイムスタンプを記録する列を選択します。 |
| タイムスタンプ属性 | デフォルトでは、アクションの現在のタイムスタンプが送信されます。別の形式で送信する場合は、タイムスタンプとして割り当てる属性を選択します。属性が割り当てられていて、その値が空の場合は、現在のタイムスタンプが送信されます。 |
| 現在の訪問データをビジターデータに含める | 現在の訪問データをビジターデータに含める場合に選択します。 |

### カスタムビジターデータを送信する

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クラウドバケット | Databricks がデータを取得するクラウドバケットまたはコンテナを選択します。 |
| Databricks カタログ | Databricks カタログを選択するか、カスタム値を指定します。 |
| Databricks スキーマ | Databricks スキーマを選択するか、カスタム値を指定します。 |
| Databricks テーブル | Databricks テーブルを選択するか、カスタム値を指定します。 |
| ビジターパラメータ | ビジター属性を Databricks テーブルの列にマッピングします。少なくとも 1 つのビジター属性をマッピングする必要があります。 |

### イベントデータ全体を送信する（バッチ）

#### バッチの制限

このアクションでは、ベンダーへの大量データ転送をサポートするため、バッチリクエストを使用します。次のいずれかのしきい値に達するまで、リクエストはキューに格納されます。

* リクエストの最大数：100,000
* 最も古いリクエストからの最大経過時間：60 分
* リクエストの最大サイズ：10 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クラウドバケット | Databricks がデータを取得するクラウドバケットまたはコンテナを選択します。 |
| Databricks カタログ | Databricks カタログを選択するか、カスタム値を指定します。 |
| Databricks スキーマ | Databricks スキーマを選択するか、カスタム値を指定します。 |
| Databricks テーブル | Databricks テーブルを選択するか、カスタム値を指定します。 |
| ペイロードを記録する列 | ペイロードを記録する `STRING` 列を選択します。コネクタはペイロードをシリアル化された JSON 文字列として書き込むため、Delta 列は `STRING` である必要があります。列を `VARIANT` として宣言すると、読み込みは `DELTA_MERGE_INCOMPATIBLE_DATATYPE` で失敗します。個々のフィールドをクエリするには、`PARSE_JSON(column_name):field_name::TYPE` を使用します。 |
| タイムスタンプを記録する列 | タイムスタンプを記録する列を選択します。 |
| タイムスタンプ属性 | デフォルトでは、アクションの現在のタイムスタンプが送信されます。別の形式で送信する場合は、タイムスタンプとして割り当てる属性を選択します。属性が割り当てられていて、その値が空の場合、コネクタは現在のタイムスタンプを送信します。 |
| バッチの有効期間 | バッチアクションを送信する頻度を指定するため、有効期間（TTL）を構成します。`1`～`60` 分の値を入力します。デフォルト値は `10` 分です。 |

### カスタムイベントデータを送信する（バッチ）

#### バッチの制限

このアクションでは、ベンダーへの大量データ転送をサポートするため、バッチリクエストを使用します。次のいずれかのしきい値に達するまで、リクエストはキューに格納されます。

* リクエストの最大数：100,000
* 最も古いリクエストからの最大経過時間：60 分
* リクエストの最大サイズ：10 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クラウドバケット | Databricks がデータを取得するクラウドバケットまたはコンテナを選択します。 |
| Databricks カタログ | Databricks カタログを選択するか、カスタム値を指定します。 |
| Databricks スキーマ | Databricks スキーマを選択するか、カスタム値を指定します。 |
| Databricks テーブル | Databricks テーブルを選択するか、カスタム値を指定します。 |
| イベントパラメータ | パラメータをテーブルの列にマッピングします。少なくとも 1 つのパラメータをマッピングする必要があります。 |
| バッチの有効期間 | バッチアクションを送信する頻度を指定するため、有効期間（TTL）を構成します。`1`～`60` 分の値を入力します。デフォルト値は `10` 分です。 |

### ビジターデータ全体を送信する（バッチ）

#### バッチの制限

このアクションでは、ベンダーへの大量データ転送をサポートするため、バッチリクエストを使用します。次のいずれかのしきい値に達するまで、リクエストはキューに格納されます。

* リクエストの最大数：100,000
* 最も古いリクエストからの最大経過時間：60 分
* リクエストの最大サイズ：10 MB
#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クラウドバケット | Databricks がデータを取得するクラウドバケットまたはコンテナを選択します。 |
| Databricks カタログ | Databricks カタログを選択するか、カスタム値を指定します。 |
| Databricks スキーマ | Databricks スキーマを選択するか、カスタム値を指定します。 |
| Databricks テーブル | Databricks テーブルを選択するか、カスタム値を指定します。 |
| 訪問データを記録する列 | 訪問データを記録する `STRING` 列を選択します。コネクタは訪問データをシリアル化された JSON 文字列として書き込むため、Delta 列は `STRING` である必要があります。列を `VARIANT` として宣言すると、`DELTA_MERGE_INCOMPATIBLE_DATATYPE` により読み込みが失敗します。個々のフィールドをクエリするには、`PARSE_JSON(column_name):field_name::TYPE` を使用します。 |
| タイムスタンプを記録する列 | タイムスタンプを記録する列を選択します。 |
| タイムスタンプ属性 | デフォルトでは、アクションの現在のタイムスタンプが送信されます。別の形式で送信する場合は、タイムスタンプとして割り当てる属性を選択します。属性が割り当てられていて、その値が空の場合は、現在のタイムスタンプが送信されます。 |
| 訪問データに現在の訪問データを含める | 訪問データに現在の訪問データを含める場合に選択します。 |
| バッチの有効期間 | バッチアクションを送信する頻度を指定するため、有効期間（TTL）を構成します。`1`～`60` 分の値を入力します。デフォルト値は `10` 分です。 |

### カスタム訪問データの送信（バッチ）

#### バッチの上限

このアクションでは、ベンダーへの大量データ転送に対応するため、バッチリクエストを使用します。次のいずれかのしきい値に達するまで、リクエストはキューに格納されます。

* リクエストの最大数：100,000
* 最も古いリクエストからの最大経過時間：60 分
* リクエストの最大サイズ：10 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クラウドバケット | Databricks がデータを取得するクラウドバケットまたはコンテナを選択します。 |
| Databricks カタログ | Databricks カタログを選択するか、カスタム値を指定します。 |
| Databricks スキーマ | Databricks スキーマを選択するか、カスタム値を指定します。 |
| Databricks テーブル | Databricks テーブルを選択するか、カスタム値を指定します。 |
| 訪問パラメータ | パラメータをテーブルの列にマッピングします。少なくとも 1 つのパラメータをマッピングする必要があります。 |
| バッチの有効期間 | バッチアクションを送信する頻度を指定するため、有効期間（TTL）を構成します。`1`～`60` 分の値を入力します。デフォルト値は `10` 分です。 |

### ログイベントの送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クラウドバケット | Databricks がデータを取得するクラウドバケットまたはコンテナを選択します。 |
| Databricks カタログ | Databricks カタログを選択するか、カスタム値を指定します。 |
| Databricks スキーマ | Databricks スキーマを選択するか、カスタム値を指定します。 |
| Databricks テーブル | Databricks テーブルを選択するか、カスタム値を指定します。 |
| イベントパラメータ | パラメータをテーブルの列にマッピングします。少なくとも 1 つのパラメータをマッピングする必要があります。 |
| バッチの有効期間 | バッチアクションを送信する頻度を指定するため、有効期間（TTL）を構成します。`1`～`60` 分の値を入力します。デフォルト値は `10` 分です。 |

### ログイベント全体の送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クラウドバケット | Databricks がデータを取得するクラウドバケットまたはコンテナを選択します。 |
| Databricks カタログ | Databricks カタログを選択するか、カスタム値を指定します。 |
| Databricks スキーマ | Databricks スキーマを選択するか、カスタム値を指定します。 |
| ボリューム | コネクタが出力ファイルを書き込む Databricks Unity Catalog ボリュームです。 |
| ファイルパス | コネクタがファイルをエクスポートするパスです。コネクタごとに一意のサブディレクトリ（例：`/Volumes/CATALOG/SCHEMA/VOLUME/my_connector`）を入力します。ボリュームのルートフォルダを直接指定することは避けてください。Auto Loader によってそこに `_auto_loader_checkpoints` フォルダと `_auto_loader_schema` フォルダが作成され、2 つのコネクタが同じパスを共有すると重複レコードが生成されるためです。 |
| Databricks テーブル | Databricks テーブルを選択するか、カスタム値を指定します。 |
| ペイロードを記録する列 | ペイロードを記録する `STRING` 列を選択します。コネクタはペイロードをシリアル化された JSON 文字列として書き込むため、Delta 列は `STRING` である必要があります。列を `VARIANT` として宣言すると、`DELTA_MERGE_INCOMPATIBLE_DATATYPE` により読み込みが失敗します。個々のフィールドをクエリするには、`PARSE_JSON(column_name):field_name::TYPE` を使用します。 |
| タイムスタンプを記録する列 | タイムスタンプを記録する列を選択します。 |
| タイムスタンプ属性 | デフォルトでは、アクションの現在のタイムスタンプが送信されます。別の形式で送信する場合は、タイムスタンプとして割り当てる属性を選択します。属性が割り当てられていて、その値が空の場合は、現在のタイムスタンプが送信されます。 |