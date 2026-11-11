---
title: Tealium Audience Discovery for Snowflake について
description: Tealium Audience Discovery for Snowflake の概要、機能、およびオーディエンスアクティベーションのための Tealium との統合方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/cloud-data/snowflake-cloud-data-source/tealium-audience-discovery/about/
---
Tealium Audience Discovery for Snowflake は、Snowflake のデータからオーディエンスを作成し、データを Snowflake の外部に移動することなく Tealium でアクティベートできる、Snowflake ネイティブアプリケーションです。

## 仕組み

このアプリは、Snowflake アカウント内で完全に動作します。データからオーディエンスを定義し、各オーディエンスを Snowflake テーブルとして保存するとともに、外部アクセス用の対応するビューを作成します。オーディエンスデータは、構成したスケジュールに従って更新されます。Tealium は Snowflake データソースを使用してビューからデータを読み取り、アクティベーション用のレコードを読み込みます。

全体的な流れは次のとおりです。

1. Tealium Audience Discovery for Snowflake でオーディエンスを作成します。
1. アプリがオーディエンスを Snowflake テーブルとして保存し、対応するビューを作成します。
1. アプリが、構成したスケジュールに従ってテーブルを更新します。
1. Tealium で、オーディエンスに接続する Snowflake データソースを作成します。
1. Tealium が、コネクタとデータワークフローを通じてアクティベーション用のデータを読み込みます。

![](https://docs.tealium.com/images/server-side/data-sources/tealium-audience-discovery-architecture.png)


<blockquote>
アプリは Snowflake からデータを読み取り、オーディエンステーブルを作成します。既存の顧客データは変更しません。オーディエンスのアクティベーションと後続のワークフローは Tealium で実行されます。
</blockquote>


## 要件

* アプリをインストールし、ユーザーアクセスとデータアクセスを管理するための Snowflake アカウント所有者または管理者ロール。
* オーディエンスの作成に使用する Snowflake データベースおよびスキーマへのアクセス権。
* データソースを構成する権限を持つ Tealium アカウント。


<blockquote>
受信データに基づいて属性が自動的に作成されるため、より簡単に構成するには Data Cloud Activation の使用を推奨します。Customer Data Platform（CDP）を使用する場合は、属性とオーディエンスを手動で作成する必要があります。
</blockquote>


インストール手順については、[Tealium Audience Discovery for Snowflake のインストール](https://docs.tealium.com/install-tealium-audience-discovery/)を参照してください。

## ユースケース

* データチームが、ウェアハウスデータを探索およびクエリして、価値の高い顧客や離反顧客を特定する。
* マーケターが、SQL を記述せずにポイント＆クリック形式のフィルターを Snowflake データに適用する。
* チームが Cortex の自然言語クエリを使用してオーディエンスのアイデアを探索し、アクティベーション用のデータセットとしてスケジュールする。

## 次のステップ

* [Tealium Audience Discovery for Snowflake を使い始める](https://docs.tealium.com/get-started/)
* [Tealium Audience Discovery for Snowflake をインストールする](https://docs.tealium.com/install-tealium-audience-discovery/)
* [Tealium Audience Discovery for Snowflake でオーディエンスを管理する](https://docs.tealium.com/manage-discovery-audiences/)
* [Snowflake オーディエンスを Tealium に接続する](https://docs.tealium.com/connect-snowflake-audiences/)