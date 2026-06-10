---
title: Cyberduckを使用してSFTPまたはAmazon S3経由でファイルをアップロードする
description: この記事では、SFTPまたはAmazon S3経由でファイルをアップロードするためにCyberduckを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/file-import/file-transfer-service/cyberduck/
---
1. Cyberduckを実行します。
1. 新しい接続を作成し、接続に名前を入力します。
1. ファイルサービスの構成で使用されるファイル転送サービスを選択します。
1. サービスの資格情報（ユーザー名とパスワード）を入力します。  
    * **Tealium S3バケット** - Tealium S3バケットの資格情報は、ファイルサービスをファイルインポートデータソースで構成すると自動的に生成されます。
        * Tealium S3の資格情報は、**データソースダッシュボード**でデータソースを展開し、**サービス構成**タブをクリックすることで見つけることができます。  
        ![](/images/server-side/data-sources/tealium-s3-bucket-credentials.png)
        * Cyberduckで以下を入力します：
            * **サーバー**: `s3.amazonaws.com`
            * **アクセスキーID**: Tealium S3 **アクセスキー**
            * **シークレットアクセスキー**: Tealium S3 **シークレットキー**
            * **パス**: Tealium S3 **バケット/プレフィックス**。例えば、  
            `collect-us-east-1.tealium.com/bulk-downloader/{{ACCOUNT-PROFILE}}`
1. サービスに必要な他の詳細（サーバー、パス、ポートなど）を提供します。Cyberduckを使用してサードパーティのS3バケットにアクセスする方法について詳しくは、[Cyberduck: Amazon S3](https://docs.cyberduck.io/protocols/s3/#Accessthirdpartybuckets)を参照してください。
1. 接続を保存します。

CyberduckにCSVファイルをドラッグアンドドロップしてファイルをアップロードします。これが新しいS3バケット（空のバケット）の場合は、最初のファイルをアップロードする方法については[空のS3バケットにファイルをアップロードする]()を参照してください。

SFTPを使用する場合、ファイルはルートフォルダに配置する必要があります。SFTP接続のサブフォルダにはファイルを配置できません。
