---
title: EventStream入門
description: この記事は、データサプライチェーンの中心に位置するデータ収集およびAPIハブであるTealium EventStreamの紹介です。
url: https://docs.tealium.com/ja/server-side/getting-started/eventstream-api-hub/introduction/
---
## Tealium EventStreamとは何ですか？

![](https://docs.tealium.com/images/tutorials/eventstream-icon.jpg)

Tealium EventStream API Hubは、他のサーバーサイドアプリケーションとの統合のためにデータを収集および変換するサーバーサイドプラットフォームです。

Tealium EventStreamは以下の主な利点を提供します：

* モバイルアプリのサイズを削減します。
* クライアントサイドのネットワークリクエストを最小限に抑えます。
* コードリリースなしで新しいベンダーを導入します。

Tealium EventStreamを使用して、受信データを管理し、イベント要件を定義し、データ品質を検査し、コネクタ統合を構成します。

## 仕組み

EventStreamは、データソースの構成や受信データの検証から、エンリッチメントによるデータのエンリッチメント、イベントフィードおよびコネクタを通じたリアルタイムアクションの有効化まで、データサプライチェーン全体を処理します。

EventStreamは、以下の機能をサポートしてこのデータワークフロー全体を支えます：

* データソース（インストールとデータ収集）
* ライブイベント（リアルタイムデータ検査）
* イベント仕様と属性（データレイヤー要件と検証）
* イベントフィード（フィルターされたイベントタイプ）
* イベントコネクタ（APIハブアクション）


<blockquote>
EventStreamはディスクにデータを保存しないストリーミング製品です。EventStreamは次の送信先に送信されるまでデータをメモリ内にのみ保持します。
</blockquote>


## データソース

![](https://docs.tealium.com/images/server-side/introduction-to-eventstream-data-sources.png)

データソースは、データを収集するためにTealiumをインストールするプラットフォームを表します。EventStreamを使用する最初のステップは、データソースを追加することです。データソースを追加すると、選択したプラットフォームのインストール手順が提供されます。各データソースには、そのインストールからのデータを識別するためにコードで使用する必要がある一意のキーがあります。

データソースは、指定されたプラットフォームで定義されたイベントを追跡する方法を示す詳細なコードサンプルを提供するイベント仕様にリンクすることができます。データソースを使用すると、インストールが機能していることを確認し、データ品質を検査するために受信イベントを簡単にフィルタリングできます。

[データソース](https://docs.tealium.com/about-data-sources/)についてもっと学びましょう。

## イベント仕様と属性

イベント仕様を作成することで、堅牢なデータ基盤を確立します。仕様は、追跡したいイベントとそれに関連する属性を特定することでデータレイヤーを定義します。仕様は、EventStreamが処理するデータの高品質を維持することを保証します。仕様と属性は、すべてのデジタルプロパティにわたる普遍的なデータ戦略を確立するのに役立ちます。

<!-- GAP: add a screenshot of the Event Specifications overview page showing the Total Volume, Valid Events, Warn Events, Invalid Events, and No Spec metric tiles and the Defined Events table -->

[イベント仕様](https://docs.tealium.com/about-event-specifications/)と[属性](https://docs.tealium.com/about-attributes/)についてもっと学びましょう。

## ライブイベント

**ライブイベント**は、データソースからの受信データをリアルタイムで表示するチャートです。データソースがインストールされデータを送信した後、イベントはこの画面に表示されます。**ライブイベント**チャートでは、バーをクリックして受信したイベントの詳細を確認できます。そこから、イベント属性を定義したり、イベントのデータ検証を見たり、受信イベントに基づいて新しい仕様を定義したりすることができます。

![](https://docs.tealium.com/images/server-side/white-ui-event-feed-live-events.png)
<!-- GAP: replace white-ui-event-feed-live-events.png with a screenshot of the live events chart showing all four status segments including Warn (yellow) in the chart legend -->

さらに、仕様をアクティブにすると、受信イベントのデータ品質がバーチャートに反映されるため、注意が必要な警告または無効なイベントをすぐに確認できます。

[ライブイベント](https://docs.tealium.com/about-live-events/)についてもっと学びましょう。

## イベントフィード

イベントフィードは、属性に基づいて特定の条件に一致するイベントのグループです。フィードは、すべてのイベントのサブセットであり、ベンダーコネクタにターゲットを絞ることができます。フィードを使用すると、**ライブイベント**チャートで受信イベントを簡単に検査し、時間の経過に伴う活動量を確認することが容易になります。

![](https://docs.tealium.com/images/server-side/white-ui-event-specification-search.png)

[イベントフィード](https://docs.tealium.com/about-event-feeds/)についてもっと学びましょう。

## イベントコネクタ

イベントコネクタは、イベントフィードからリアルタイムでデータを送信するベンダーとのAPI統合です。コネクタは、ベンダーアカウントの認証情報とデータマッピングを構成して、イベント属性をベンダーが期待する対応するパラメータに送信します。

![](https://docs.tealium.com/images/server-side/white-ui-event-connectors-google-analytics.png)

[イベントコネクタ](https://docs.tealium.com/about-connectors/)についてもっと学びましょう。