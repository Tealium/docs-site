---
title: データソースについて
description: Tealiumで利用可能なデータソースの種類の概要、リアルタイム、スケジュール構成、バッチ取り込みオプションを含む。
url: https://docs.tealium.com/ja/server-side/data-sources/about-data-sources/
---
データソースは、外部システムとTealiumとの間に構成された接続であり、サーバーサイドプロファイルレベルで定義されます。

作成するデータソースのタイプは、データの起源とリアルタイムで届く必要があるか、スケジュールに従って届く必要があるかによって異なります。

## タグ管理とWebベースの収集

Tealiumタグ管理を使用する場合、WebデータソースはTealium Collectタグです。Tealium Collectは、各Webトラッキングコールをサーバーサイドプロファイルに送信します。詳細については、[タグ管理のためのデータソース](https://docs.tealium.com/data-sources-for-iq-tag-management/)を参照してください。

また、他の多くのWebプラットフォーム用のTealium Collectライブラリを使用してイベントを収集することもできます。セットアップ手順については、[Webにインストール](https://docs.tealium.com/platforms//#install-on-web)を参照してください。

## モバイルおよびアプリSDK

TealiumはiOSおよびAndroid用のネイティブSDKを提供しており、他の多くのプラットフォームもサポートしています。Tealium Collectライブラリはアプリのライフサイクルイベント、ユーザーインタラクション、カスタムイベントを直接サーバーサイドプロファイルに送信します。

セットアップ手順については、[モバイルの開始](https://docs.tealium.com/getting-started-mobile/)を参照してください。

## サーバーサイドおよびHTTP API

任意のサーバーアプリケーション、バックエンドシステム、またはAPIゲートウェイは、Tealium Collect HTTP APIを使用してイベントを直接サーバーサイドプロファイルに投稿できます。この方法は、ブラウザーやアプリの外部でデータが発生する場合に使用します。たとえば、注文管理システム、CRMエクスポート、IoTデバイス、カスタムバックエンド統合などです。

セットアップ手順については、[サーバーにインストール](https://docs.tealium.com/platforms//#server)を参照してください。

## インカミングWebhooks

一部のパートナーシステムは、Tealiumが提供するWebhook URLにイベントを投稿してTealiumに送信します。このタイプのデータソースを作成するとき、TealiumはURLと構成コードを生成し、送信システムを構成するために使用します。

詳細については、[インカミングWebhooks](https://docs.tealium.com/server-side/data-sources/webhooks/setup-guides/)を参照してください。

## クラウドデータソース

クラウドデータソースは、定義されたスケジュールに従って倉庫またはデータベースからデータを読み取ります。イベントパイプラインは、インポートされた各行をイベントとして処理し、Tealiumにコピーしてエンリッチメント、プロファイル構築、およびアクティベーションを行います。

訪問プロファイルをエンリッチするか、倉庫データからコネクタアクションをトリガーする必要がある場合は、クラウドデータソースを使用してください。

詳細については、[クラウドデータソースについて](https://docs.tealium.com/about-cloud-data-sources/)を参照してください。


<blockquote>
Tealiumにデータを複製せずにゼロコピークラウドデータソースを使用するには、[Tealium CloudStream](https://docs.tealium.com/about-cloudstream/)を使用してください。
</blockquote>


## オフラインおよびバッチインポート

Tealiumにデータをインポートするための次のオプションがあります。直接のSDKまたはAPI統合以外：

* [**CSVファイルインポート**](https://docs.tealium.com/about-file-import/)  
10分ごとにCSVファイルからオフラインデータを読み取るポーリングベースのインポートです。イベントデータおよび顧客データ処理をサポートしています。ファイル転送サービス（Tealium S3またはご自身のプロバイダー）が必要です。
* [**Data Connect**](https://docs.tealium.com/about-data-connect/)  
外部システム（SaaSアプリ、CRM、データウェアハウス）を構成可能なレシピを使用してTealiumに接続するローコード統合です。スケジュール構成、トリガー、またはほぼリアルタイムの取り込みをサポートしています。イベントデータおよび顧客データ処理をサポートしています。