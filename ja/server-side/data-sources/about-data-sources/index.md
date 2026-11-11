---
title: データソースについて
description: リアルタイム、スケジュール、バッチ取り込みオプションなど、Tealium で利用できるデータソースタイプの概要。
url: https://docs.tealium.com/ja/server-side/data-sources/about-data-sources/
---
データソースとは、サーバーサイドプロファイルレベルで定義される、外部システムと Tealium の間に構成された接続です。

作成するデータソースのタイプは、データの発生元と、データをリアルタイムまたはスケジュールに従って取り込む必要があるかどうかによって異なります。

## タグ管理と Web ベースの収集

Tealium Tag Management を使用している場合、Web データソースは Tealium Collect タグです。Tealium Collect は、各 Web トラッキング呼び出しをサーバーサイドプロファイルに送信します。詳細については、[Tag Management のデータソース](https://docs.tealium.com/data-sources-for-tag-management/)を参照してください。

Tealium Collect ライブラリを使用して、その他多くの Web プラットフォームからイベントを収集することもできます。構成手順については、[Web へのインストール](https://docs.tealium.com/platforms//#install-on-web)を参照してください。

## モバイルおよびアプリ SDK

Tealium は iOS および Android 向けのネイティブ SDK を提供し、その他多くのプラットフォームもサポートしています。Tealium Collect ライブラリは、アプリのライフサイクルイベント、ユーザーインタラクション、カスタムイベントをサーバーサイドプロファイルに直接送信します。

構成手順については、[モバイルの使用を開始する](https://docs.tealium.com/getting-started-mobile/)を参照してください。

## サーバーサイドおよび HTTP API

あらゆるサーバーアプリケーション、バックエンドシステム、API ゲートウェイから、Tealium Collect HTTP API を使用してサーバーサイドプロファイルにイベントを直接送信できます。注文管理システム、CRM エクスポート、IoT デバイス、カスタムバックエンド統合など、ブラウザやアプリ以外でデータが生成される場合は、この方法を使用します。

構成手順については、[サーバーへのインストール](https://docs.tealium.com/platforms//#server)を参照してください。

## 受信 Webhook

一部のパートナーシステムは、Tealium が提供する Webhook URL にデータを送信することで、イベントを Tealium に送信します。これらのデータソースのいずれかを作成すると、Tealium は送信元システムの構成に使用する URL と構成コードを生成します。

詳細については、[受信 Webhook](https://docs.tealium.com/server-side/data-sources/webhooks/)を参照してください。

## クラウドデータソース

クラウドデータソースは、定義されたスケジュールに従ってウェアハウスまたはデータベースからデータを読み取ります。イベントパイプラインは、インポートされた各行をイベントとして処理し、データのエンリッチメント、プロファイルの構築、アクティベーションのために Tealium にコピーします。

ウェアハウスのデータを使用して訪問プロファイルをエンリッチしたり、コネクタアクションをトリガーしたりする必要がある場合は、クラウドデータソースを使用します。

詳細については、[クラウドデータソースについて](https://docs.tealium.com/about-cloud-data-sources/)を参照してください。


<blockquote>
データを Tealium に複製せずにゼロコピーのクラウドデータソースを使用するには、[Data Cloud Activation](https://docs.tealium.com/about-data-cloud-activation/)を使用してください。
</blockquote>


## オフラインおよびバッチインポート

SDK または API を直接統合せずに Tealium にデータをインポートするには、次のオプションを利用できます。

* [**CSV ファイルインポート**](https://docs.tealium.com/about-file-import/)  
CSV ファイルからオフラインデータを 10 分ごとに読み取る、ポーリングベースのインポートです。イベントデータと顧客データの処理をサポートします。ファイル転送サービス（Tealium S3 または独自のプロバイダー）が必要です。
* [**Data Connect**](https://docs.tealium.com/about-data-connect/)  
構成可能なレシピを使用して、外部システム（SaaS アプリ、CRM、データウェアハウス）を Tealium に接続するローコード統合です。スケジュール、トリガー、または準リアルタイムでの取り込みをサポートします。イベントデータと顧客データの処理をサポートします。