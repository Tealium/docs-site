---
title: SnowflakeオーディエンスをTealiumに接続する
description: Tealium Audience Discovery for SnowflakeのオーディエンスをSnowflakeクラウドデータソースを使用してTealiumに接続します。
url: https://docs.tealium.com/ja/server-side/data-sources/cloud-data/snowflake-cloud-data-source/tealium-audience-discovery/connect-snowflake-audiences/
---
アプリでオーディエンスを作成した後、Tealiumに接続してオーディエンスレコードをロードし、コネクターやその他のダウンストリームワークフローを使用してアクティベートします。

## 必要条件

* Tealium Audience Discovery for Snowflakeでアクティブなオーディエンス。[オーディエンスの作成](https://docs.tealium.com/manage-discovery-audiences/)を参照してください。
* データソースを構成する権限を持つTealiumアカウント。
* アプリとインストール時に構成されたSnowflake接続値へのアクセス。
* （オプション）Webhookやその他のアウトバウンド統合を使用する場合、Snowflake管理者は目的地URLのネットワークルールと外部アクセス統合を構成する必要があります。Snowflakeはデフォルトでアウトバウンドトラフィックをブロックします。

## アプリから接続詳細を取得する

1. **Audiences**リストから、オーディエンスのアクションメニューを開きます。
1. **Share**をクリックします。
1. ダイアログから以下の値をメモしてください：
   * **Database** — データベース名（例：`TEALIUM_AUDIENCE_DISCOVERY_APP`）
   * **Schema** — スキーマ名（例：`TEALIUM_EXTERNAL_ACCESS`）
   * **View name** — オーディエンスの生成されたビュー名
   * **Audience view** — `DATABASE.SCHEMA.VIEW_NAME`形式の完全修飾ビュー名
   * **Query** — データソースを構成する際に使用する事前構築された`SELECT`ステートメント

![](https://docs.tealium.com/images/server-side/data-sources/tealium-audience-discovery-share-dialog.png)

## Snowflakeデータソースを作成する

1. Tealiumで**Connect > Data Sources**に移動します。
1. **Add Data Source**をクリックします。
1. **Data Cloud**の下で**Snowflake**を選択します。

接続を構成する際は、アプリからの値を使用します：

* **Database Name** — 共有ダイアログからの**Database**値（例：`TEALIUM_AUDIENCE_DISCOVERY_APP`）
* **Database Schema** — 共有ダイアログからの**Schema**値（例：`TEALIUM_EXTERNAL_ACCESS`）
* **Connection Role** — インストール時に構成されたロール（例：`TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE`）
* **Connection Warehouse** — インストール時に構成されたウェアハウス（例：`TEALIUM_AUDIENCE_DISCOVERY_WH`）

完全な構成手順については、[Snowflakeクラウドデータソース](https://docs.tealium.com/about-snowflake-cloud-data-source/)を参照してください。


<blockquote>
複数のオーディエンスがある場合は、同じSnowflake接続構成を再利用してください。各オーディエンスに対して別々のデータソースを作成します。
</blockquote>


## オーディエンステーブルのクエリモードを構成する

オーディエンステーブルには、レコードが追加されたり更新されたりしたときを追跡するシステム管理の制御列が含まれています。

オーディエンステーブルの場合、**Timestamp + Incrementing**を使用します。この構成は、オーディエンスに追加された新しいユーザーを確実にロードします。

列を次のようにマッピングします：

* **Timestamp column** — `TEALIUM_CTRL_COL_CREATED_AT`
* **Incrementing column** — `TEALIUM_CTRL_COL_INCREMENTAL_ID`

Tealiumはタイムスタンプ列を使用して、最後の実行以降に追加されたレコードをロードします。インクリメント列はレコードが順番に処理されることを保証します。

### メンバーシップの変更を追跡する

オーディエンスを離れ、後に再資格を得たユーザーを処理するには、異なるタイムスタンプ列を使用します：

* **Timestamp column** — `TEALIUM_CTRL_COL_LAST_UPDATED_AT`または`TEALIUM_CTRL_COL_MEMBERSHIP_CHANGED_AT`
* **Incrementing column** — `TEALIUM_CTRL_COL_INCREMENTAL_ID`
* **Filter condition (recommended)** — `TEALIUM_CTRL_COL_IS_ACTIVE = true`

このアプローチは、オーディエンスを離れた後に再資格を得たユーザーを処理します。

この構成により、Tealiumは：

* 新規または更新されたオーディエンスレコードをロードします
* データをインクリメンタルに処理します
* Snowflakeでのオーディエンステーブルの更新方法に合わせます


<blockquote>
データソースのスケジュールをアプリのオーディエンスリフレッシュスケジュールに合わせるか、それよりも頻度を低く構成してください。データソースをより頻繁に実行すると、ロードが空になります。
</blockquote>


## データソース構成を完了する

クエリモードを構成した後、残りの手順を完了します：

1. 共有ダイアログからの**View name**値を使用してオーディエンスビューを選択します。
1. クエリを検証します。
1. 列をイベント属性にマッピングします。
1. 訪問IDマッピングを構成します。

これらの手順は、標準のSnowflakeデータソースワークフローに従います。詳細については、[Snowflakeクラウドデータソース](https://docs.tealium.com/about-snowflake-cloud-data-source/)を参照してください。

## 次のステップ

データソースを構成した後：

* Tealiumの属性とオーディエンスを使用してオーディエンスデータを豊かにし、管理します
* オーディエンスセグメントをアクティブ化するためのコネクタを構成します