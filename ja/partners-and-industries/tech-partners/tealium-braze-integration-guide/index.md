---
title: Tealium + Braze 統合ガイド
description: この記事では、TealiumとBrazeを最大限に活用する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-braze-integration-guide/
---
[Braze](https://www.braze.com)は、メール、モバイル、ウェブ向けの包括的な顧客エンゲージメントプラットフォームで、消費者と彼らが愛するブランドとの間の関連性が高く記憶に残る体験を提供します。2019年には、HBO、Walmart、Postmatesなどの主要ブランドのために、6000億以上のパーソナライズされたメール、プッシュ通知、アプリ内メッセージ、SMSメッセージなどを数十億の消費者に送信しました。

## クライアントサイド統合

以下の表は、クライアントサイドのBraze統合タイプの説明と前提条件をリストアップし、詳細なセットアップドキュメントへのリンクを提供します。

|統合タイプ| この統合から期待できること| 製品要件| セットアップガイド|
|---| ---| ---| ---|
|Braze Web SDK Tag|  Braze Web SDKを使用すると、次のことができます：<ul><li>セッションデータを収集する</li><li>ユーザーを特定する（Tealium統合データレイヤーを使用）</li><li>ウェブ/モバイルブラウザー経由で購入やカスタムイベントを記録する。</li></ul> Braze Web SDKを実装することで、ウェブとモバイルチャネルを通じてユーザーのより完全なビューを作成できます。また、Web SDKを使用して、アプリ内ウェブメッセージやウェブプッシュ通知を送信することでユーザーとのエンゲージメントを図ることができます。 |  Tealium Tag Management |  [Braze Web SDK Tag セットアップガイド](https://docs.tealium.com/braze-web-sdk-tag/) |

## サーバーサイド統合

以下の表は、サーバーサイドのBraze統合タイプの説明と前提条件をリストアップし、詳細なセットアップドキュメントへのリンクを提供します。

|統合タイプ| この統合から期待できること| 製品要件| セットアップガイド|
|---| ---| ---| ---|
|Braze Connector|  このBraze統合を使用すると、AudienceStreamおよび/またはEventStreamを通じてBrazeデータをさらにエンリッチすることができ、リアルタイムでパーソナライズされたオムニチャネル体験を顧客と共に構築できます。**Track User** アクションには、AudienceStreamとEventStreamで同じ機能が含まれています。ベストプラクティスとして、AudienceStreamではユーザー属性機能を、EventStreamではイベントと購入機能を使用することをお勧めします。これらの基準に合わないユースケースは、このベストプラクティスを無視しても構いません。 |  Tealium EventStream and/or Tealium AudienceStream |  [Braze Connector セットアップガイド](https://docs.tealium.com/braze-connector/) |

## モバイル統合

以下の表は、モバイルBraze統合タイプの説明と前提条件をリストアップし、詳細なセットアップドキュメントへのリンクを提供します。

|統合タイプ| この統合から期待できること| 製品要件| セットアップガイド|
|---| ---| ---| ---|
|Braze Remote Commands|  このBraze統合は、次のものを使用します：<ul><li>**Native Braze SDK** - Brazeメソッドをラップするリモートコマンドモジュール。</li><li>**Braze Remote Command Tag** - イベントトラッキングをネイティブのBrazeコールに変換するタグ。</li></ul> このソリューションは、Tag Managementの利便性を活用して、ベンダー固有のコードをアプリに追加することなくネイティブのBraze実装を構成します。アプリにBrazeリモートコマンドモジュールを追加すると、必要なBrazeライブラリが自動的にインストールされ、ビルドされます。依存関係マネージャーのインストールを使用している場合、別途Braze SDKをインストールする必要はありません。 |  Tealium Tag Management |  [Remote Command: Braze](https://docs.tealium.com/platforms/remote-commands/integrations/braze/) |

