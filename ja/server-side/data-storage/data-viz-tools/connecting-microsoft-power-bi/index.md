---
title: Microsoft Power BIの接続
description: この記事では、Microsoft Power BIをTealium DataAccessに接続する方法について説明します
url: https://docs.tealium.com/ja/server-side/data-storage/data-viz-tools/connecting-microsoft-power-bi/
---### ODBCデータソースの作成

Power BIをDataAccessに接続するには、ODBCデータソース接続が必要です。

Power BIでODBCデータソースを作成するには：

1. [Windows用Amazon Redshiftドライバーをインストールする](http://docs.aws.amazon.com/redshift/latest/mgmt/install-odbc-driver-windows.html#odbc-driver-windows-how-to-install)
1. [ODBC接続のためのシステムDSNエントリを作成する](http://docs.aws.amazon.com/redshift/latest/mgmt/install-odbc-driver-windows.html#create-dsn-odbc-windows)
    * `System DSN`を使用することを確認してください
1. 構成は以下のようになります：  
      ![](/images/server-side/example-odbc-setup.png)
1. ODBCデータソースが構成された後、**Test**をクリックします。クライアントコンピュータがAmazon Redshiftデータベースに接続できる場合、次のメッセージが表示されます：**接続成功**。
1. ODBC構成を閉じます。

### Microsoft Power BIをTealium DataAccessに接続する

1. Power BI内で、**Home**タブを選択し、**Get Data**をクリックします（ドロップダウンではなくアイコンをクリック）
1. **Other**を選択し、**ODBC**を選び、**Connect**をクリックします。  
      ![](/images/server-side/get-data.png)
1. ドロップダウンからデータソース名を選択します。  
      ![](/images/server-side/from-odbc.png)
1. データベース全体を取得すると、接続後にクエリを正常に実行できない場合があります。**Advanced options**をクリックし、SQLステートメント（オプション）フィールドに制限ステートメントを入力して、必要なデータのみを取得することをお勧めします。以下のようになります：  
      ![](/images/server-side/power-bi-limiting-query.png)
1. **OK**をクリックします。データナビゲーターが表示されます。
1. ディレクトリ構造を展開し、クエリしたいテーブルを選択して**Load**をクリックします。  
      ![](/images/server-side/data-navigator.png)
1. Power BIはデータに接続し、データをモデリング用にロードし、属性で列を埋めます。  
      ![](/images/server-side/data-fields-aka-attributes.png)

これで、Tealium DataAccess上でMicrosoft Power BIを使用してレポートを作成する準備が整いました。

### トラブルシューティング

&#34;サーバー証明書と&amp;lt;クラスタ名&amp;gt;のホスト名が一致しません。&#34;

まず、接続構成で完全なクラスタ名を使用してみてください。それでもエラーが解決しない場合は、**sslmode**構成を`verify-full`から`verify-ca`に変更してみてください。[Redshift SSLサポート](https://docs.aws.amazon.com/redshift/latest/mgmt/connecting-ssl-support.html)についてもっと学びましょう。