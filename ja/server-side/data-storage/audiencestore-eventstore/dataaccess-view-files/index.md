---
title: AudienceStoreとEventStoreでファイルを表示する
description: この記事では、AudienceStoreとEventStoreでファイルを表示する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/dataaccess-view-files/
---
## コンソールでファイルを表示およびダウンロードする

DataAccessコンソールを使用して、各オーディエンスまたはイベントフィードに関連付けられたファイルを閲覧できます。これは、システムを通じてデータが流れていることを確認し、フォーマットに慣れるためにサンプルファイルをダウンロードする簡単な方法です。

EventStoreまたはAudienceStoreを構成直後は、ファイルのリストは空です。DataAccessコンソールでファイルにアクセスするには、次の手順に従ってください：

1. サイドバーから **Store &gt; EventStore** または **Store &gt; AudienceStore** に移動します。
1. 表示するデータの週数を選択します（1週間から4週間、デフォルトは1週間です）。
1. イベントフィードまたはAudienceStoreアクションの名前を選択します。&lt;br&gt;EventStoreの場合、リストにはEventStore用に有効化されたフィードのみが表示されます。AudienceStoreの場合、ファイルは構成されたアクションに応じてJSONまたはCSVのいずれかです。
1. **リロード**をクリックします。
    * EventStoreの場合、ファイルのリストが表示されます。日付をクリックしてファイルの詳細を見ます。
    * AudienceStoreの場合、ファイルは日付ごとにグループ化され（1日に複数のファイルがある場合があります）、作成日が早いものから順にリストされます。その日のファイルリストを見るために日付をクリックします。
1. ファイルをダウンロードするには、**ダウンロード**をクリックします。
  `.gzip`ファイルがコンピュータに保存されます。解凍ユーティリティを使用してファイルを開き、内容を抽出します。

EventStoreからファイルを削除することはできません。イベント、訪問、または訪問レコードがその有効期限に達すると、そのレコードは自動的に削除されます。訪問レコードが更新された場合でも、有効期限は変わらず、レコードは削除されます。有効期限はEventStoreの保持時間によって決まります。デフォルトの保持時間は390日（13ヶ月）です。詳細については、[サーバーサイドアカウント構成]()を参照してください。

## サードパーティツールを使用してファイルを表示する

FTPクライアントやAmazon S3コマンドラインインターフェースなどのサードパーティツールを使用してファイルにアクセスすることもできます。これらのツールがファイルにアクセスできるようにするには、S3バケットのAmazon S3アクセスキーが必要です。

### Amazon S3アクセスキーを取得する

Amazon S3アクセスキーを取得するには：

1. サイドバーから **Store &gt; EventStore** または **Store &gt; AudienceStore** に移動します。
1. **Amazonアクセスキーを取得**をクリックします。次のフィールドが表示されます：
    * アクセスキーID
    * シークレットアクセスキー
    * パス

セキュリティ上の理由から、シークレットアクセスキーは一度だけ表示されるため、後で使用するために安全に保管することが重要です。

アクセスキーを紛失した場合は、新しいキーを生成することができます。ただし、新しいキーを生成すると、以前のアクセスキーを使用していたすべての接続が無効になります。

### Amazon S3をサポートするFTPクライアント

大量のファイルをダウンロードするためのより便利な方法として、デスクトップアプリケーションの使用をお勧めします。

Amazon S3で使用できるクライアントアプリケーションは次のとおりです：

* Windows: Cyberduck, CrossFTP
* Mac: Cyberduck, CrossFTP, Transmit

GUIベースのFTPクライアントをS3サポートで使用する主な利点は、Amazon S3から個々のファイルやフォルダをポイントアンドクリックでダウンロードできることです。

Cyberduckの次のスクリーンキャプチャは、接続を構成する方法を示しています。構成ウィザードにはシークレットアクセスキーのフィールドがありません。接続試行時にシークレットアクセスキーの入力を求められます。シークレットアクセスキーは将来の使用のために保存されます。

![](/images/server-side/cyberduck.png)

## AWSコマンドラインインターフェースを使用してファイルを表示する

より技術的なユーザーの場合、AWSコマンドラインインターフェース（CLI）をインストールして、データファイルへのアクセスを完全に制御できます。Amazon CLIを使用する主な利点は、Amazon S3からのファイルの取得を同期および自動化するなど、特定のニーズに合わせてカスタマイズできることです。

Amazon CLIの使用例は次のとおりです：

* すべての歴史的ログファイルの初回一括ダウンロード
* 時間ごとの増分ダウンロードをスケジュールして、最新の生成されたログファイルのみを取得する
* デスクトップまたはサーバー上のローカルフォルダとS3上のリモートフォルダを同期して、両方にまったく同じログファイルの内容が含まれるようにする
* 特定のLastModified日付の前後のファイルをダウンロードする

Amazon CLIをインストールするには、次のAmazonの指示に従ってください：[AWS CLIのインストール、更新、およびアンインストール](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)

`aws configure`を呼び出すと、アクセスキーとアクセスキーIDの入力を求められます（地域名と出力形式は空白のままにしておくことができます）。

CLIを構成した後、`s3`メソッドを使用してクエリを実行できます。`s3`メソッドは、次のCLI例で使用されます。

### S3のオブジェクトをリストする

`list-objects`メソッドは、S3ディレクトリ内のオブジェクトをリストします。これは、個々のファイルをダウンロードするために各オブジェクトのキーを取得するために必要です。

#### ルートフォルダ内のすべてのオブジェクトをリストする：

```
aws s3 ls s3://dataaccess-&lt;region&gt;.tealiumiq.com/&lt;account&gt;/&lt;profile&gt;/
```

#### すべてのイベントフィードをリストする

```
aws s3 ls s3://dataaccess-&lt;region&gt;.tealiumiq.com/&lt;account&gt;/&lt;profile&gt;/events/
```

#### 特定のイベントフォルダ内のすべてのオブジェクトをリストする

```
aws s3 ls s3://dataaccess-&lt;region&gt;.tealiumiq.com/&lt;account&gt;/&lt;profile&gt;/events/&lt;feed-id&gt;/
```

#### すべてのオーディエンスをリストする

```
aws s3 ls s3://dataaccess-eu-west-1.tealiumiq.com/&lt;account&gt;/&lt;profile&gt;/audiences/
```

#### 特定のオーディエンスフォルダ内のすべてのオブジェクトをリストする

```
aws s3 ls s3://dataaccess-&lt;region&gt;.tealiumiq.com/&lt;account&gt;/&lt;profile&gt;/&lt;action-id&gt;/
```

#### 単一のイベントオブジェクトを取得する

`get-object`メソッドは、特定のリモートキーをデスクトップまたはサーバーのローカル位置にダウンロードします。

```
aws s3 cp s3://dataaccess-&lt;region&gt;.tealiumiq.com/&lt;account&gt;/&lt;profile&gt;/events/{feed-id}/{filename}.gz ./

```

#### 単一のオーディエンスオブジェクトを取得する

`get-object`メソッドは、特定のリモートキーをデスクトップまたはサーバーのローカル位置にダウンロードします。

```
aws s3 cp s3://dataaccess-&lt;region&gt;.tealiumiq.com/&lt;account&gt;/&lt;profile&gt;/audiences/{action-id}/{filename}.gz ./

```

### ローカルとリモートのフォルダを同期する

`sync`メソッドは、Amazon S3のリモートフォルダをデスクトップまたはサーバーのローカルフォルダと同期します。次の例では、特定のリモートEventStreamまたはAudienceStreamフォルダをデスクトップのローカルフォルダと同期します。

`--dryrun`引数は、実際にダウンロードすることなく、どのファイルが実際に同期されるかを表示します。実際のダウンロードを実行するには、`--dryrun`引数を削除します。

```
aws s3 sync s3://uconnect.tealiumiq.com/{account}/{profile}/audiences// \
    ~/Desktop/temp --dryrun
```

最後に、特定のフィルターに一致するファイルのみをダウンロードするように`sync`メソッドをフィルタリングすることもできます。この例では、ワイルドカードフィルター &#34;\*2015.06.14\*&#34; に一致するファイルのみがダウンロードされます。

```
aws s3 sync s3://uconnect.tealiumiq.com/{account}/{profile}/events// \
    ~/Desktop/temp --exclude &#34;*&#34; --include &#34;*2015.06.14*&#34; --dryrun
```