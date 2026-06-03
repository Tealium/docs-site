---
title: Snowflake用Tealium Audience Discoveryについて
description: Snowflake用Tealium Audience Discoveryの概要、機能、およびTealiumでのオーディエンスアクティベーションとの統合方法。
url: https://docs.tealium.com/ja/server-side/data-sources/cloud-data/snowflake-cloud-data-source/tealium-audience-discovery/about/
---
Snowflake用Tealium Audience Discoveryは、Snowflakeデータからオーディエンスを構築し、Snowflakeからデータを移動させることなくTealiumでそれらをアクティブ化することができるネイティブSnowflakeアプリケーションです。

## 動作方法

このアプリは完全にあなたのSnowflakeアカウント内で動作します。データからオーディエンスを定義し、各オーディエンスをSnowflakeテーブルとして保存し、外部アクセス用の対応するビューを持ちます。オーディエンスデータは、あなたが構成したスケジュールに基づいて更新されます。TealiumはSnowflakeデータソースを使用してビューからレコードを読み込み、アクティベーションのためにロードします。

全体の流れは以下の通りです：

1. Snowflake用Tealium Audience Discoveryでオーディエンスを作成します。
1. アプリはオーディエンスをSnowflakeテーブルと対応するビューとして保存します。
1. アプリはあなたが構成したスケジュールに基づいてテーブルを更新します。
1. Tealiumで、オーディエンスに接続するSnowflakeデータソースを作成します。
1. Tealiumはコネクタとデータワークフローを通じてデータをアクティベーションのためにロードします。

![](/images/server-side/data-sources/tealium-audience-discovery-architecture.png)


アプリはSnowflakeからデータを読み取り、オーディエンステーブルを作成します。既存の顧客データを変更することはありません。オーディエンスアクティベーションと下流のワークフローはTealiumで実行されます。


## 要件

* アプリをインストールし、ユーザーとデータアクセスを管理するためのSnowflakeアカウント所有者または管理者ロール。
* オーディエンス作成に使用するSnowflakeデータベースとスキーマへのアクセス。
* データソースを構成する権限を持つTealiumアカウント。


CloudStreamは、自動的に受信データに基づいて属性を作成するため、セットアップが容易です。AudienceStreamを使用する場合は、属性とオーディエンスを手動で作成する必要があります。


インストール手順については、[Snowflake用Tealium Audience Discoveryのインストール]()を参照してください。

## 使用例

* 倉庫データを探索およびクエリして、高価値または失客顧客を特定するデータチーム。
* SQLを書かずにSnowflakeデータにポイントアンドクリックフィルタを適用するマーケター。
* Cortexの自然言語クエリを使用してオーディエンスのアイデアを探索し、それをデータセットとしてアクティベーションのスケジュールにするチーム。

## 次のステップ

* [Snowflake用Tealium Audience Discoveryの使い始め]()
* [Snowflake用Tealium Audience Discoveryのインストール]()
* [Snowflake用Tealium Audience Discoveryでオーディエンスを管理する]()
* [SnowflakeオーディエンスをTealiumに接続する]()