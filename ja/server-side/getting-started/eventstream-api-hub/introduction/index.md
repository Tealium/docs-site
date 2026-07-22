---
title: EventStreamへの導入
description: この記事は、データサプライチェーンの中心に位置するデータ収集およびAPIハブであるTealium EventStreamへの導入です。
url: https://docs.tealium.com/ja/server-side/getting-started/eventstream-api-hub/introduction/
---
## Tealium EventStreamとは何ですか？

![](https://docs.tealium.com/images/tutorials/eventstream-icon.jpg)

Tealium EventStream APIハブは、他のサーバーサイドアプリケーションとの統合のためにデータを収集し変換するサーバーサイドプラットフォームです。

Tealium EventStreamは以下の主な利点を提供します：

* モバイルアプリのサイズを削減します。
* クライアントサイドのネットワークリクエストを最小限に抑えます。
* コードリリースなしで新しいベンダーをデプロイします。

Tealium EventStreamを使用して、受信データを管理し、イベント要件を定義し、データ品質を検査し、コネクタ統合を構成します。

## それはどのように動作しますか

EventStreamは、データソースの構成と受信データの検証から、エンリッチメントによるエンリッチメントとイベントフィードとコネクタを通じたリアルタイムアクションの有効化まで、データサプライチェーン全体を処理します。

EventStreamは、以下の機能を備えて、この全体的なデータワークフローをサポートします：

* データソース（インストールとデータ収集）
* ライブイベント（リアルタイムデータ検査）
* イベント仕様と属性（データレイヤー要件と検証）
* イベントフィード（フィルタリングされたイベントタイプ）
* イベントコネクタ（APIハブアクション）


<blockquote>
EventStreamはストリーミング製品であり、データをディスクに保存しません。 EventStreamは、データが次の目的地に送信されるまでメモリにデータを保持します。
</blockquote>


## データソース

![](https://docs.tealium.com/images/server-side/introduction-to-eventstream-data-sources.png)

データソースは、Tealiumをインストールしてデータを収集するプラットフォームを表します。 EventStreamを使用する最初のステップは、データソースを追加することです。 データソースを追加すると、選択したプラットフォームのインストール手順が表示されます。 各データソースには、そのインストールからのデータを識別するためにコードで使用する必要がある一意のキーがあります。

データソースは、イベント仕様にリンクして、指定したプラットフォームで定義したイベントをトラッキングする方法を示すより詳細なコードサンプルを提供できます。 データソースを使用すると、インストールが正常に動作していることを確認し、データ品質を検査するために、簡単に受信イベントをフィルタリングできます。

[データソース](https://docs.tealium.com/about-data-sources/)について詳しく学びましょう。

## イベント仕様と属性

イベント仕様を作成することで、堅固なデータ基盤を確立します。 仕様は、トラッキングしたいイベントとそれらに関連する属性を識別することでデータレイヤーを定義します。 仕様は、EventStreamが処理するための高品質なデータを維持することを保証します。 仕様と属性は、すべてのデジタルプロパティにわたるユニバーサルなデータ戦略を確立するのに役立ちます。

[イベント仕様](https://docs.tealium.com/about-event-specifications/)と[属性](https://docs.tealium.com/about-attributes/)について詳しく学びましょう。

## ライブイベント

**ライブイベント**は、データソースからの受信データを表示するリアルタイムチャートです。 データソースがインストールされ、データを送信した後、イベントがこの画面に表示されます。 **ライブイベント**チャートでバーをクリックすると、受信したイベントの詳細が表示されます。 そこから、イベント属性を定義したり、イベントのデータ検証を見たり、受信イベントに基づいて新しい仕様を定義したりできます。

![](https://docs.tealium.com/images/server-side/white-ui-event-feed-live-events.png)

さらに、仕様を有効にすると、受信イベントのデータ品質がバーチャートに反映され、修正が必要な無効なイベントがすぐにわかります。

[ライブイベント](https://docs.tealium.com/about-live-events/)について詳しく学びましょう。

## イベントフィード

イベントフィードは、その属性に基づいて特定の条件に一致するイベントのグループです。 フィードは、ベンダーコネクタにターゲットを絞ることができるすべてのイベントのサブセットです。 フィードを使用すると、**ライブイベント**チャートで受信イベントを簡単に検査し、時間経過に伴うアクティビティ量を確認することが容易になります。

![](https://docs.tealium.com/images/server-side/white-ui-event-specification-search.png)

[イベントフィード](https://docs.tealium.com/about-event-feeds/)について詳しく学びましょう。

## イベントコネクタ

イベントコネクタは、リアルタイムでイベントフィードからデータを送信するベンダーとのAPI統合です。 コネクタは、ベンダーアカウントの資格情報とデータマッピングで構成され、イベント属性をベンダーが期待する対応するパラメータに送信します。

![](https://docs.tealium.com/images/server-side/white-ui-event-connectors-google-analytics.png)

[イベントコネクタ](https://docs.tealium.com/about-connectors/)について詳しく学びましょう。
