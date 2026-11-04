---
title: AudienceStoreとEventStoreでファイルを表示する
description: この記事では、AudienceStoreとEventStoreでファイルを表示する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/dataaccess-view-files/
---
## コンソールでファイルを表示およびダウンロードする

DataAccessコンソールを使用して、各オーディエンスまたはイベントフィードに関連付けられたファイルを参照できます。これは、データがシステムを通じて流れていることを簡単に確認し、サンプルファイルをすばやくダウンロードして形式を把握するための方法です。

EventStoreまたはAudienceStoreを構成した直後は、ファイルのリストは空です。DataAccessコンソールでファイルにアクセスするには、次の手順を実行します。

1. サイドバーで、**Store > EventStore**または**Store > AudienceStore**に移動します。
1. 表示するデータの週数を選択します（1～4週間。デフォルトは1週間です）。
1. Event FeedまたはAudienceStore Actionの名前を選択します。<br>EventStoreの場合、EventStoreで有効になっているフィードのみがリストに表示されます。AudienceStoreの場合、構成されたアクションに応じて、ファイル形式はJSONまたはCSVになります。
1. **Reload**をクリックします。  
    * EventStoreの場合、ファイルのリストが表示されます。日付をクリックすると、ファイルの詳細が表示されます。  
    * AudienceStoreの場合、ファイルは日付別にグループ化され（1つの日付に複数のファイルが存在する場合があります）、作成日時が古い順に表示されます。日付をクリックすると、その日付のファイルリストが表示されます。
1. ファイルをダウンロードするには、**Download**をクリックします。  
  `.gzip`ファイルがコンピューターに保存されます。解凍ユーティリティを使用してファイルを開き、内容を抽出します。


<blockquote>
EventStoreからファイルを削除することはできません。イベント、訪問、または訪問レコードが有効期限に達すると、そのレコードは自動的に消去されます。訪問レコードが更新された場合でも有効期限は変わらず、レコードは引き続き消去されます。有効期限はEventStoreの保持期間によって決まります。デフォルトの保持期間は30日です。詳細については、[サーバーサイドのアカウント構成]()を参照してください。
</blockquote>


## サードパーティ製ツールを使用してファイルを表示する

FTPクライアントやAmazon S3コマンドラインインターフェイスなどのサードパーティ製ツールを使用して、ファイルにアクセスすることもできます。これらのツールからファイルへのアクセスを許可するには、S3バケットのAmazon S3アクセスキーが必要です。

### Amazon S3アクセスキーを取得する

Amazon S3アクセスキーを取得するには、次の手順を実行します。

1. サイドバーで、**Store > EventStore**または**Store > AudienceStore**に移動します。
1. **Get Amazon Access Key**をクリックします。次のフィールドが表示されます。
    * Access Key ID
    * Secret Access Key
    * Path

セキュリティ上の理由から、シークレットアクセスキーは一度しか表示されません。後で使用できるよう、安全に保管することが重要です。


<blockquote>
アクセスキーを紛失した場合は、新しいキーを生成できます。ただし、新しいキーを生成すると、以前のアクセスキーを使用している既存の接続はすべて無効になります。
</blockquote>


### Amazon S3をサポートするFTPクライアント

多数のファイルをより簡単にダウンロードするには、デスクトップアプリケーションの使用をお勧めします。

Amazon S3では、次のクライアントアプリケーションを使用できます。

* Windows：Cyberduck、CrossFTP
* Mac：Cyberduck、CrossFTP、Transmit

S3をサポートするGUIベースのFTPクライアントを使用する主な利点は、個々のファイルやフォルダーをポイントアンドクリックしてAmazon S3からダウンロードできることです。

次のCyberduckの画面キャプチャは、接続の構成方法を示しています。構成ウィザードには、Secret Access Key用のフィールドがないことに注意してください。接続を試行すると、Secret Access Keyの入力を求められます。Secret Access Keyは、今後の使用に備えて保存されます。

![](https://docs.tealium.com/images/server-side/cyberduck.png)

## AWSコマンドラインインターフェイスを使用してファイルを表示する

より技術的な知識を持つユーザーは、AWS Command Line Interface（CLI）をインストールすることで、データファイルへのアクセスを完全に制御できます。Amazon CLIを使用する主な利点は、Amazon S3からのファイル取得の同期や自動化など、特定のニーズに合わせてカスタマイズできることです。

Amazon CLIの用途には、次のようなものがあります。

* 過去のすべてのログファイルを初回に一括ダウンロードする
* 新しく生成されたログファイルのみを取得する増分ダウンロードを1時間ごとにスケジュールする
* デスクトップまたはサーバー上のローカルフォルダーをS3上のリモートフォルダーと同期し、両方のログファイルの内容を完全に一致させる
* 特定のLastModified日時より前または後のファイルをダウンロードする

Amazon CLIをインストールするには、Amazonの次の手順を参照してください：[AWS CLIのインストール、更新、アンインストール](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)

`aws configure`を呼び出すと、Access KeyとAccess Key IDの入力を求められます（Region NameとOutput Formatは空欄のままにできます）。

CLIを構成した後、`s3`メソッドを使用してクエリを実行できます。次のCLIの例では、`s3`メソッドを使用します。

### S3内のオブジェクトを一覧表示する

`list-objects`メソッドは、S3ディレクトリ内のオブジェクトを一覧表示します。個々のファイルをダウンロードするために、各オブジェクトのキーを取得する際に必要です。

#### ルートフォルダー内のすべてのオブジェクトを一覧表示する

```
aws s3 ls s3://dataaccess-<region>.tealiumiq.com/<account>/<profile>/
```

#### すべてのイベントフィードを一覧表示する

```
aws s3 ls s3://dataaccess-<region>.tealiumiq.com/<account>/<profile>/events/
```

#### 特定のイベントフォルダー内のすべてのオブジェクトを一覧表示する

```
aws s3 ls s3://dataaccess-<region>.tealiumiq.com/<account>/<profile>/events/<feed-id>/
```

#### すべてのオーディエンスを一覧表示する

```
aws s3 ls s3://dataaccess-eu-west-1.tealiumiq.com/<account>/<profile>/audiences/
```

#### 特定のオーディエンスフォルダー内のすべてのオブジェクトを一覧表示する

```
aws s3 ls s3://dataaccess-<region>.tealiumiq.com/<account>/<profile>/<action-id>/
```

#### 単一のイベントオブジェクトを取得する

`get-object`メソッドは、特定のリモートキーをデスクトップまたはサーバー上のローカルの場所にダウンロードします。

```
aws s3 cp s3://dataaccess-<region>.tealiumiq.com/<account>/<profile>/events/{feed-id}/{filename}.gz ./

```

#### 単一のオーディエンスオブジェクトを取得する

`get-object`メソッドは、特定のリモートキーをデスクトップまたはサーバー上のローカルの場所にダウンロードします。

```
aws s3 cp s3://dataaccess-<region>.tealiumiq.com/<account>/<profile>/audiences/{action-id}/{filename}.gz ./

```

### ローカルフォルダーとリモートフォルダーを同期する

`sync`メソッドは、Amazon S3上のリモートフォルダーをデスクトップまたはサーバー上のローカルフォルダーと同期します。次の例では、特定のリモートEventStreamまたはAudienceStreamフォルダーをデスクトップ上のローカルフォルダーと同期します。


<blockquote>
`--dryrun`引数を使用すると、実際にダウンロードせずに、同期対象となるファイルを確認できます。実際にダウンロードするには、`--dryrun`引数を削除します。
</blockquote>


```
aws s3 sync s3://uconnect.tealiumiq.com/{account}/{profile}/audiences// \
    ~/Desktop/temp --dryrun
```

また、`sync`メソッドをフィルタリングして、特定のフィルターに一致するファイルのみをダウンロードすることもできます。この例では、ワイルドカードフィルター「\*2015.06.14\*」に一致するファイルのみがダウンロードされます。

```
aws s3 sync s3://uconnect.tealiumiq.com/{account}/{profile}/events// \
    ~/Desktop/temp --exclude "*" --include "*2015.06.14*" --dryrun
```