---
title: Web用インストールオプション
description: この記事では、Tealium AudienceStream CDPのインストールオプションについて説明します。
url: https://docs.tealium.com/ja/server-side/getting-started/audiencestream-cdp/install/
---
この記事は、Tealium iQタグ管理やTealium EventStream APIハブをまだ使用していないお客様がTealium AudienceStreamをインストールしたい場合のためのものです。

## オプション1: Tealium Universal Tag &#43; Tealium Collect

タグマネージャーをまだ使用していない場合は、Tealium iQタグ管理とTealium Collectタグを使用した基本的なセットアップをお勧めします。これにより、データをAudienceStreamに送信できます。

Tealium iQは、サイトのすべてのページにUniversal Tag（`utag.js`）をインストールし、タグマーケットプレイスから数クリックで簡単に追加できるTealium Collectタグが必要です。このオプションの追加利点には、[拡張マーケットプレイス]()へのアクセスが含まれ、AudienceStreamに送信する前にデータの準備や変換を行うことができます。また、[Web Companion]()や[Tealium Tools]()を使用してインストールを検証し、拡張することもできます。

インストールコンポーネント:

* [Tealium iQタグ管理]()
* [Tealium Universal Tag (`utag.js`)](/ja/platforms/javascript/install/)
* [Tealium Collectタグ]()

## オプション2: Google Tag Manager &#43; Tealium Collect

Google Tag Managerを使用しており、データレイヤーとイベントトラッキングに満足している場合は、Google Tag Manager用Tealium Collectタグのデプロイをお勧めします。Tealium Collectタグは、Google Tag Managerによって処理されたすべてのデータ、`dataLayer`オブジェクト全体を直接AudienceStreamに送信します。

インストールコンポーネント:

* [Google Tag Manager用Tealium Collect](/ja/platforms/google-tag-manager/)

## オプション3: Google Tag Manager &#43; Tealium Universal Tag

Google Tag Managerを使用してベンダーをデプロイすることを好む場合（または必要とされる場合）、Google Tag ManagerでCustom HTMLタグとしてTealium Universal Tagをデプロイすることをお勧めします。このアプローチは、Google Tag Managerの実装がビジネスにとって重要な行動やデータポイント（例えば、コンバージョンファネルの活動やeコマースのチェックアウトステップなど）を追跡していない場合にも推奨されます。Tealium Universal Tagをデプロイすることで、iQタグ管理の完全な利点を活用し、高度なイベントトラッキングと補足的なデータレイヤー変数を完全に実装することができます。

このアプローチは、iQタグ管理をデプロイする利点と、Google Tag Managerの既存のイベントトラッキングを利用してインストールを迅速化する能力を提供します。

インストールコンポーネント:

* [Tealium iQタグ管理]()
* [Google Tag ManagerのCustom HTMLタグ](https://support.google.com/tagmanager/answer/6107167?hl=en)

## 詳細を学ぶ

以下のリソースを利用して、実装体験を続けることができます:

### ライブイベント

インストールオプションに関わらず、Tealium [Live Events]()を使用してAudienceStreamに流れ込むデータを検証します。**ライブイベント**はリアルタイムで受信データを表示するため、追跡されたイベントと収集されたデータ属性を評価することができます。

### Tealium教育

[education.tealium.com](https://education.tealium.com/)でTealiumの充実したオンデマンド学習を探索し、[AudienceStream Basic eLearning course](https://education.tealium.com/learn/course/en-as-bsc-elrn)を含むコースを利用して、Tealiumの知識とスキルを向上させることができます。