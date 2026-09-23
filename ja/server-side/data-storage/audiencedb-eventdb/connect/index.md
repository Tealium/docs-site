---
title: EventDBおよびAudienceDBへの接続
description: この記事では、Redshiftへの接続、データベース認証情報の取得、およびSQLクエリの記述に関する情報を提供します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencedb-eventdb/connect/
---
## Redshiftへの接続

EventDBおよびAudienceDBデータにアクセスするには、PostgreSQL形式のデータベースに接続できるサードパーティツールが必要です。

## データベース認証情報の取得

PostgreSQLをサポートするサードパーティツールは、接続するために認証情報が必要です。認証情報はDataAccess Consoleで提供されます。

データベース認証情報は現在、各ユーザーごとに生成されます。以前は、すべてのユーザーがアカウントとプロファイルに対して生成された認証情報を共有していました。誰かがグローバル認証情報を再生成すると、すべてのユーザーの接続が切断され、すべてのユーザーが再接続する必要がありました。

ユーザー固有の認証情報の場合、生成された認証情報はアカウント、プロファイル、およびユーザーのメールアドレスに基づいています。ユーザーは自分の認証情報を再生成しても他の接続を終了することなく、特定のユーザーのアクセスを削除することができます。特定のユーザーの認証情報を無効にするには、Tealiumサポートに連絡してください。


<blockquote>
以前に生成されたグローバル認証情報はまだ使用できますが、再生成はできません。
</blockquote>


データベース認証情報を取得するには、次の手順に従ってください：

1. **Store > EventDB** または **Store > AudienceDB** に移動します。
1. **Get DB Connection Details** をクリックします。
1. **Regenerate DB Credentials** をクリックします。  
認証情報を取得するのが初めてであっても、認証情報を再生成する必要があります。  
      ![](https://docs.tealium.com/images/server-side/connection-details.png)
1. 既存の認証情報を削除して新しいものを生成したいことを確認するために **Yes** をクリックします。  
**DB Connection Details** 画面には以下のフィールドが表示されます：
    * **Username**  
    データベース接続のユーザー名で、アカウント、プロファイル名、およびメールアドレスの組み合わせです。例えば、`account__profile__email`。
    * **Password**  
    データベース接続のパスワード。
    * **Database**  
    データベースの名前は通常、アカウントの名前です。
    * **Host**  
    データ保存地域に特有のデータベースサーバーのホスト名。
    * **Port**  
    接続のポート番号。
1. 接続詳細を保存してから **Close** をクリックします。

### Redshiftデータベースの閲覧

データベース認証情報を取得した後、サードパーティツールを使用してデータベースに接続できます。以下の例では、フリーウェアアプリケーションであるSQL Workbench/Jを使用しています（[SQL Workbenchを使用してEventDBに接続する](https://docs.tealium.com/connecting-sql-workbench/)を参照）。スキーマの命名規則は `account__profile` です。

以下の例は、関連するすべてのテーブルと列を結合するビューを示しています。

![](https://docs.tealium.com/images/server-side/sql-workbench-db-explorer.jpg)

この例は生データテーブルビューを示しています。列名はビューに関係なく各テーブルで同じ位置にあります。これら二つのビューの主な違いはエントリの可読性です。

![](https://docs.tealium.com/images/server-side/sql-workbench-columns.jpg)

## SQLクエリの記述

以下の記事では、ベストプラクティスと有用なクエリの例を提供しています：

* [SQL Workbench/Jを使用してEventDBおよびAudienceDBに接続する](https://docs.tealium.com/connecting-sql-workbench/)
* [EventDBおよびAudienceDBのクエリ記述のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363364-best-practices-for-writing-queries-for-eventdb-and-audiencedb/preview)
* [EventDBおよびAudienceDBのための役立つSQLクエリ](https://support.tealiumiq.com/en/support/solutions/articles/36000363427-helpful-sql-queries-for-eventdb-and-audiencedb)