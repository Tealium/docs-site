---
title: EventDBとAudienceDBに接続する
description: この記事では、Redshiftに接続し、データベースの認証情報を取得し、SQLクエリを書く方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencedb-eventdb/connect/
---
## Redshiftに接続する

EventDBとAudienceDBのデータにアクセスするには、PostgreSQLスタイルのデータベースに接続できるサードパーティのツールが必要です。

* **初めてのユーザー**
EventDBとAudienceDBがアカウントで有効になると、Redshift Spectrumが自動的に有効になります。
* **既存の顧客** 
DataAccessを使用していた既存の顧客に対してSpectrumを有効にする前に、既存のデータと新しいデータが正しい場所に書き込まれるようにデータ移行が必要です。事前にチームと調整して進めてください。

## データベースの認証情報を取得する

PostgreSQLをサポートするサードパーティのツールは、接続するための認証情報が必要です。認証情報はDataAccess Consoleで提供されます。

データベースの認証情報は現在、各ユーザーごとに生成されます。以前は、すべてのユーザーがアカウントとプロファイルに対して生成された認証情報を共有していました。誰かがグローバルな認証情報を再生成すると、すべてのユーザーの接続が終了し、すべてのユーザーが再接続しなければなりませんでした。

ユーザー固有の認証情報の場合、生成される認証情報はアカウント、プロファイル、およびユーザーのメールアドレスに基づいています。ユーザーは他の接続を終了することなく自分の認証情報を再生成することができます。特定のユーザーのアクセスを削除しても他の接続は終了しません。特定のユーザーの認証情報を無効にするには、Tealiumサポートに連絡してください。


<blockquote>
以前に生成されたグローバルな認証情報は引き続き使用できますが、再生成することはできません。
</blockquote>


データベースの認証情報を取得するには、以下の手順を使用します：

1. **Store > EventDB** または **Store > AudienceDB** に移動します。
1. **Get DB Connection Details** をクリックします。
1. **Regenerate DB Credentials** をクリックします。  
これが初めての認証情報取得であっても、認証情報を再生成する必要があります。  
      ![](https://docs.tealium.com/images/server-side/connection-details.png)
1. 既存の認証情報を削除し、新しいものを生成することを確認するために **Yes** をクリックします。  
**DB Connection Details** 画面には以下のフィールドが表示されます：
    * **Username**  
    データベース接続のユーザー名。これはあなたのアカウント、プロファイル名、およびメールアドレスの組み合わせです。例えば、`account__profile__email`。
    * **Password**  
    データベース接続のパスワード。
    * **Database**  
    データベースの名前。通常はあなたのアカウントの名前です。
    * **Host**  
    データベースサーバーのホスト名。あなたのデータ保存地域に特化しています。
    * **Port**  
    接続のポート番号。
1. 将来の使用のために接続詳細を保存し、**Close** をクリックします。

### Redshiftデータベースを閲覧する

データベースの認証情報を取得したら、サードパーティのツールを使用してデータベースに接続できます。以下の例では、SQL Workbench/J（フリーウェアアプリケーション）を使用しています（[SQL Workbenchを使用してEventDBに接続する](https://docs.tealium.com/connecting-sql-workbench/)を参照）。スキーマの命名規則は `account__profile` です。

以下の例は、関連するすべてのテーブルと列を結合するビューを示しています。

![](https://docs.tealium.com/images/server-side/sql-workbench-db-explorer.jpg)

この例は、生のデータテーブルビューを示しています。列名は各テーブルで同じ位置にあり、ビューに関係なく同じです。これら二つのビューの主な違いはエントリの可読性です。

![](https://docs.tealium.com/images/server-side/sql-workbench-columns.jpg)

## SQLクエリの作成

以下の記事では、ベストプラクティスと有用なクエリの例を提供しています：

* [SQL Workbench/Jを使用してEventDBとAudienceDBに接続する](https://docs.tealium.com/connecting-sql-workbench/)
* [EventDBとAudienceDBのクエリ作成のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363364-best-practices-for-writing-queries-for-eventdb-and-audiencedb/preview)
* [EventDBとAudienceDBのための便利なSQLクエリ](https://support.tealiumiq.com/en/support/solutions/articles/36000363427-helpful-sql-queries-for-eventdb-and-audiencedb)