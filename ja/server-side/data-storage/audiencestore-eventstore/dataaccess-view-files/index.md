---
title: AudienceStore と EventStore のファイルを表示する
description: この記事では、AudienceStore と EventStore のファイルを表示する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/dataaccess-view-files/
---
## コンソールでファイルを表示およびダウンロードする

DataAccess コンソールを使用して、各オーディエンスまたはイベントフィードに関連付けられたファイルを参照できます。これにより、データがシステムを通じて流れていることを簡単に確認できるほか、サンプルファイルをすばやくダウンロードして、その形式を把握できます。

EventStore または AudienceStore を構成した直後は、ファイルのリストは空です。DataAccess コンソールでファイルにアクセスするには、次の手順を実行します。

1. サイドバーで、**Store > EventStore** または **Store > AudienceStore** に移動します。
1. 表示するデータの週数を選択します（1～4 週間、デフォルトは 1 週間）。
1. イベントフィードまたは AudienceStore アクションの名前を選択します。<br>EventStore の場合、EventStore に対して有効になっているフィードのみがリストに表示されます。AudienceStore の場合、構成したアクションに応じて、ファイル形式は JSON または CSV になります。
1. **Reload** をクリックします。  
    * EventStore の場合、ファイルのリストが表示されます。ファイルの詳細を確認するには、日付をクリックします。  
    * AudienceStore の場合、ファイルは日付別にグループ化され（日付ごとに複数のファイルが存在する場合があります）、作成日時の古い順に表示されます。日付をクリックすると、その日付のファイルのリストが表示されます。
1. ファイルをダウンロードするには、**Download** をクリックします。  
  `.gzip` ファイルがコンピューターに保存されます。解凍ユーティリティを使用してファイルを開き、内容を展開します。


<blockquote>
EventStore からファイルを削除することはできません。イベント、訪問、または訪問レコードが有効期限に達すると、そのレコードは自動的に消去されます。訪問レコードが更新された場合でも、有効期限は変わらず、レコードは引き続き消去されます。有効期限は EventStore の保持期間によって決まります。デフォルトの保持期間は 30 日です。詳細については、[サーバーサイドのアカウント構成]()を参照してください。
</blockquote>


## サードパーティ製ツールを使用してファイルを表示する

FTP クライアントや Amazon S3 コマンドラインインターフェイスなどのサードパーティ製ツールを使用して、ファイルにアクセスすることもできます。これらのツールからファイルにアクセスできるようにするには、S3 バケットの Amazon S3 アクセスキーが必要です。

### Amazon S3 アクセスキーを取得する

Amazon S3 アクセスキーを取得するには、次の手順を実行します。

1. サイドバーで、**Store > EventStore** または **Store > AudienceStore** に移動します。
1. **Get Amazon Access Key** をクリックします。次のフィールドが表示されます。
    * Access Key ID
    * Secret Access Key
    * Path

セキュリティ上の理由から、シークレットアクセスキーは一度しか表示されないため、後で使用できるように安全に保管することが重要です。


<blockquote>
アクセスキーを紛失した場合は、新しいキーを生成できます。ただし、新しいキーを生成すると、以前のアクセスキーを使用している既存の接続はすべて無効になります。
</blockquote>


### Amazon S3 をサポートする FTP クライアント

多数のファイルをより簡単にダウンロードする方法として、デスクトップアプリケーションの使用をお勧めします。

Amazon S3 では、次のクライアントアプリケーションを使用できます。

* Windows：Cyberduck、CrossFTP
* Mac：Cyberduck、CrossFTP、Transmit

S3 をサポートする GUI ベースの FTP クライアントを使用する主な利点は、個々のファイルやフォルダーをポイントしてクリックするだけで、Amazon S3 からダウンロードできることです。

次の Cyberduck のスクリーンキャプチャは、接続の構成方法を示しています。構成ウィザードには、Secret Access Key を入力するフィールドがないことに注意してください。接続を試みると、Secret Access Key の入力を求められます。Secret Access Key は、今後使用できるように保存されます。

![](https://docs.tealium.com/images/server-side/cyberduck.png)

## AWS コマンドラインインターフェイスを使用してファイルを表示する

技術知識のあるユーザーは、AWS コマンドラインインターフェイス（CLI）をインストールすることで、データファイルへのアクセスを完全に制御できます。Amazon CLI を使用する主な利点は、Amazon S3 からのファイル取得の同期や自動化など、特定のニーズに合わせてカスタマイズできることです。

Amazon CLI の用途には、次のようなものがあります。

* 過去のすべてのログファイルの初回一括ダウンロード
* 新しく生成されたログファイルのみを取得する、1 時間ごとの増分ダウンロードのスケジュール
* デスクトップまたはサーバー上のローカルフォルダーと S3 上のリモートフォルダーを同期し、両方にまったく同じログファイルの内容を保持
* 特定の LastModified 日付より前または後、あるいはその両方に該当するファイルのダウンロード

Amazon CLI をインストールするには、Amazon の手順「[AWS CLI のインストール、更新、アンインストール](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)」を参照してください。

`aws configure` を呼び出すと、Access Key と Access Key ID の入力を求められます（Region Name と Output Format は空白のままにできます）。

CLI を構成した後は、`s3` メソッドを使用してクエリを実行できます。次の CLI の例では、`s3` メソッドを使用しています。

### S3 内のオブジェクトを一覧表示する

`list-objects` メソッドは、S3 ディレクトリ内のオブジェクトを一覧表示します。これは、個々のファイルをダウンロードするために各オブジェクトのキーを取得する際に必要です。

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

`get-object` メソッドは、指定したリモートキーをデスクトップまたはサーバー上のローカルの場所にダウンロードします。

```
aws s3 cp s3://dataaccess-<region>.tealiumiq.com/<account>/<profile>/events/{feed-id}/{filename}.gz ./

```

#### 単一のオーディエンスオブジェクトを取得する

`get-object` メソッドは、指定したリモートキーをデスクトップまたはサーバー上のローカルの場所にダウンロードします。

```
aws s3 cp s3://dataaccess-<region>.tealiumiq.com/<account>/<profile>/audiences/{action-id}/{filename}.gz ./

```

### ローカルフォルダーとリモートフォルダーを同期する

`sync` メソッドは、Amazon S3 上のリモートフォルダーを、デスクトップまたはサーバー上のローカルフォルダーと同期します。次の例では、特定のリモート Event Streaming または Customer Data Platform（CDP）フォルダーを、デスクトップ上のローカルフォルダーと同期します。


<blockquote>
`--dryrun` 引数を使用すると、実際にダウンロードを実行せずに、同期されるファイルを確認できます。実際にダウンロードを実行するには、`--dryrun` 引数を削除します。
</blockquote>


```
aws s3 sync s3://uconnect.tealiumiq.com/{account}/{profile}/audiences// \
    ~/Desktop/temp --dryrun
```

最後に、`sync` メソッドをフィルタリングして、特定のフィルターに一致するファイルのみをダウンロードすることもできます。この例では、ワイルドカードフィルター「\*2015.06.14\*」に一致するファイルのみがダウンロードされます。

```
aws s3 sync s3://uconnect.tealiumiq.com/{account}/{profile}/events// \
    ~/Desktop/temp --exclude "*" --include "*2015.06.14*" --dryrun
```