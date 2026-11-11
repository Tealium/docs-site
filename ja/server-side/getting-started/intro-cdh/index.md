---
title: Customer Data Hub の概要
description: Customer Data Hub は、データの収集と管理を一元化し、すべての顧客接点やマーケティングテクノロジーベンダーがリアルタイムでデータを利用できるようにすることで、卓越した顧客体験とインサイトを実現します。
url: https://docs.tealium.com/ja/server-side/getting-started/intro-cdh/
---
Tealium Customer Data Hub は、次の機能を提供します。

* クライアント側のデータとタグベンダーを管理
* すべての顧客接点からデータを収集
* 強力な属性を使用してデータをエンリッチ
* 最も価値の高いオーディエンスを特定
* サーバー側のデータとベンダーコネクタを管理
* データを一元管理されたシステムに保存

Customer Data Hub 内の次の製品を使用することで、このような幅広い機能を利用できます。

* Tag Management
* Event Streaming API Hub
* CDP
* Tealium Predict ML
* Tealium DataAccess

## クライアント側のデータとタグを管理する

Tag Management を使用して、クライアント側のデータとベンダータグを構成および管理します。データプライバシーポリシーの適用、新しいベンダータグのデプロイ、データレイヤーのカスタマイズなど、Tag Management はクライアント側のあらゆるニーズに対応できます。タグ管理で特に重要なのは、実装が変わってもデータの一貫性とわかりやすさを維持できるよう、明確に定義されたデータレイヤーを用意することです。データレイヤーは、Customer Data Hub ソリューションの基盤です。

関連資料：

* [Tag Management の概要](https://docs.tealium.com/what-is-tealium-tag-management/)
* [Tag Management の概念](https://docs.tealium.com/tag-basics/)
* [データレイヤーの概要](https://docs.tealium.com/about-the-data-layer/)

## Tealium Collect でデータを収集する

すべてはデータから始まります。あらゆる顧客接点からデータを収集することが、Customer Data Hub の能力を最大限に引き出すための第一歩です。顧客とブランドとのエンゲージメントは、貴重なデータソースです。デスクトップWebサイト、ネイティブモバイルアプリ、コネクテッドデバイス、カスタムアプリケーションのいずれからでも、Tealium のインストールライブラリのいずれかを使用して、顧客データを Customer Data Hub にシームレスに送信できます。Tag Management ユーザーは、タグマーケットプレイスで提供されている公式の Tealium Collect タグを使用することで、Customer Data Hub へのデータ送信をさらに迅速に開始できます。

関連資料：

* [Tealium インストールライブラリ](https://docs.tealium.com/publish-configuration/#mobile-library-publishing)
* [Tealium Collect](https://docs.tealium.com/tealium-collect-tag/)

## 属性とエンリッチメントでデータをエンリッチメントする

Customer Data Hub にデータが取り込まれるようになると、そのデータをエンリッチできます。エンリッチメントとは、ビジネスロジックを適用して、データを静的な値から動的な値へと変換する処理です。エンリッチされたデータは、Customer Data Hub ソリューションのその他の機能を構築するための基礎となります。また、このデータは、すべてのプラットフォームにわたって訪問の統合プロファイルを作成するという重要な役割も担います。バッジと呼ばれる特殊な属性を使用すると、訪問の詳細な全体像を構築できます。Customer Data Hub に取り込まれるデータが増えるにつれて、訪問の行動を特徴付ける属性が蓄積され、そのプロファイルはより充実したものになります。

関連資料：

* [Event Streaming の概要](https://docs.tealium.com/server-side/getting-started/tutorials/event-data-activation/introduction/)
* [属性の使用](https://docs.tealium.com/about-attributes/)
* [エンリッチメントの使用](https://docs.tealium.com/about-enrichments/)
* [バッジ属性](https://docs.tealium.com/badge-attribute/)

## オーディエンスを特定する

オーディエンスとは、ブランドとのエンゲージメントを通じて、共通する一連の属性を獲得した訪問プロファイルの集合です。オーディエンスは、Customer Data Platform（CDP）エコシステムで利用できる多様な統合機能によって実行される、リアルタイムアクションの対象です。たとえば、メール、オンライン広告、ソーシャルメディア、顧客関係管理などがあります。Customer Data Hub は、最も価値の高いオーディエンスを特定し、エンゲージするためのさまざまなツールを提供します。

関連資料：

* [CDP の概要](https://docs.tealium.com/server-side/getting-started/tutorials/visitor-profile-management/introduction/)
* [オーディエンスの構築](https://docs.tealium.com/manage-audiences/)
* [オーディエンスサイジング](https://docs.tealium.com/about-audience-sizing/)

## コネクタでデータを送信する

Customer Data Hub にすべてのデータが流れるようになったら、次はコネクタを使用してアクションを実行し、デジタルマーケティングスタックを稼働させます。コネクタとは、データをリアルタイムで送信するための、ベンダーと Tealium 間の技術的な統合です。コネクタが処理するデータには、オーディエンスとイベントの2種類があります。Customer Data Hub を使用すると、ベンダーが必要とする特定のデータを送信するようにコネクタを簡単に構成できます。

関連資料：

* [コネクタについて](https://docs.tealium.com/about-connectors/)
* [Event Streaming コネクタ](https://docs.tealium.com/server-side-connectors/)

## DataAccess でデータを保存する

Customer Data Hub はシステムに出入りするデータの流れを処理しますが、このデータの所有者はお客様であり、データに直接アクセスできる必要があることも重要です。お客様の貴重なデータを長期間保存するという特定の目的に対応するため、エンタープライズクラスのソリューションとして DataAccess を提供しています。コネクタを動作させるオーディエンスデータとイベントデータは、データベース内の構造化データ、またはログファイル内の半構造化データとして保存することもできます。

関連資料：

* [DataAccess の概要](https://docs.tealium.com/about-dataaccess/)
* [AudienceDB/EventDB の操作](https://docs.tealium.com/audiencedb-and-eventdb/)