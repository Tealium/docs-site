---
title: Snowflake用Tealium Audience Discoveryの使い方
description: Snowflake用Tealium Audience Discoveryを構成し、最初のオーディエンスをTealiumに接続します。
url: https://docs.tealium.com/ja/server-side/data-sources/cloud-data/snowflake-cloud-data-source/tealium-audience-discovery/get-started/
---
このガイドでは、Snowflake用Tealium Audience Discoveryを初めて構成する手順を説明します。最後には、Snowflakeでオーディエンスが稼働し、Tealiumに接続されている状態になります。

## 必要条件

* アプリをインストールし、アクセスを構成するための所有者または管理者権限を持つSnowflakeアカウント。
* オーディエンス作成に使用するSnowflakeのデータベース、スキーマ、テーブルへのアクセス。
* データソースを構成する権限を持つTealiumアカウント。

## ステップ1: アプリのインストール

SnowflakeマーケットプレイスからSnowflake用Tealium Audience Discoveryをインストールし、使用したいデータベースとスキーマへのアクセスを許可します。

詳しい手順については、[Snowflake用Tealium Audience Discoveryのインストール]()を参照してください。

## ステップ2: 最初のオーディエンスを作成する

1. Snowflake用Tealium Audience Discoveryを開きます。
1. **Audiences**に移動し、**&#43; Create new audience**をクリックします。
1. オーディエンス名と説明を入力します。
1. **Point &amp; Click**を選択します。
1. **Database**、**Schema**、**Table / View**を選択します。
1. 各ユーザーを一意に識別する**User ID column**を選択します。
1. **Next**をクリックします。
1. （オプション）オーディエンスを絞り込むためのフィルター条件を追加します。
1. **Next**をクリックします。
1. 更新スケジュールを構成し、**Next**をクリックします。
1. 構成を確認して**Create audience**をクリックします。

アプリは初期ロードを実行し、構成したスケジュールに従ってオーディエンスの更新を開始します。オーディエンス詳細ビューから進行状況を監視します。

詳細な構成オプションについては、[Snowflake用Tealium Audience Discoveryでオーディエンスを管理する]()を参照してください。

## ステップ3: オーディエンスをTealiumに接続する

1. オーディエンスリストでアクションメニューを開き、**Share**をクリックします。
1. **Database**、**Schema**、**Role**の値をコピーします。
1. Tealiumで**Sources &gt; Data Sources**に移動し、**Add Data Source**をクリックします。
1. **Data Cloud**の下で**Snowflake**を選択します。
1. 名前を入力し、コピーした値を使用して接続を構成します。
1. 処理を有効にし、処理構成を構成します。
1. **Build query**の下で、オーディエンステーブルとインポートする列を選択します。
1. クエリモードを**Timestamp &#43; Incrementing**に構成し、以下の列をマッピングします：

   * **Timestamp column** — `TEALIUM_CTRL_COL_CREATED_AT`
   * **Incrementing column** — `TEALIUM_CTRL_COL_INCREMENTAL_ID`

1. **Test query**をクリックして、続行する前にプレビュー結果を確認します。
1. インポートした列をTealiumイベント属性にマッピングします。
1. 訪問IDマッピングを構成して、既存の訪問プロファイルとレコードを結合します。
1. 概要を確認してデータソースを保存します。

Tealiumは構成したスケジュールに従ってオーディエンスレコードのロードを開始します。

詳細な構成オプションについては、[SnowflakeオーディエンスをTealiumに接続する]()を参照してください。

## 次のステップ

* オーディエンスセグメントをアクティブ化するためのコネクタを構成する
* Tealiumの属性とオーディエンスを使用してオーディエンスデータをエンリッチする
* `TEALIUM_CTRL_COL_IS_ACTIVE`列を使用して[メンバーシップの変更を追跡する]()、ユーザーがオーディエンスから離れたり、再び資格を得たりしたときにアクションをトリガーする
