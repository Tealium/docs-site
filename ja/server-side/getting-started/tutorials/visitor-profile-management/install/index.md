---
title: Web向けのインストールオプション
description: この記事では、Tealiumの訪問プロファイル管理のインストールオプションについて説明します。
url: https://docs.tealium.com/ja/server-side/getting-started/tutorials/visitor-profile-management/install/
---
この記事は、Tealiumをインストールしたいものの、タグ管理またはTealiumイベントデータアクティベーションをまだ使用していないお客様を対象としています。

## オプション1：Tealium Universal Tag + Tealium Collect

タグマネージャーをまだ使用していない場合は、タグ管理の基本構成とTealium Collectタグを使用して、プラットフォームにデータを送信することをお勧めします。

タグ管理を使用するには、サイトのすべてのページにUniversal Tag（`utag.js`）をインストールし、タグマーケットプレイスから数回クリックするだけで簡単に追加できるTealium Collectタグを導入する必要があります。このオプションには、プラットフォームへ送信する前にデータを準備および変換するための[拡張機能マーケットプレイス](https://docs.tealium.com/extensions-list/)へのアクセスや、インストールの検証と拡張に使用できる[Web Companion](https://docs.tealium.com/web-companion/)および[Tealium Tools](https://docs.tealium.com/tealium-tools-browser-extension/)などの利点もあります。

インストールコンポーネント：

* [タグ管理](https://docs.tealium.com/what-is-tealium-tag-management/)
* [Tealium Universal Tag（`utag.js`）](https://docs.tealium.com/ja/platforms/javascript/install/)
* [Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)

## オプション2：Google Tag Manager + Tealium Collect

Google Tag Managerを使用しており、現在のデータレイヤーとイベントトラッキングに満足している場合は、Google Tag Manager向けTealium Collectタグをデプロイすることをお勧めします。Tealium Collectタグは、完全な`dataLayer`オブジェクトを含め、Google Tag Managerによって処理されたすべてのデータをプラットフォームへ直接送信します。

インストールコンポーネント：

* [Google Tag Manager向けTealium Collect](https://docs.tealium.com/ja/platforms/google-tag-manager/)

## オプション3：Google Tag Manager + Tealium Universal Tag

Google Tag Managerを使用してベンダーをデプロイすることを希望する場合（またはそうする必要がある場合）は、Google Tag ManagerでTealium Universal TagをカスタムHTMLタグとしてデプロイすることをお勧めします。また、Google Tag Managerの実装で、コンバージョンファネルのアクティビティやEコマースのチェックアウト手順など、ビジネスに不可欠な行動やデータポイントをトラッキングしていない場合にも、この方法をお勧めします。Tealium Universal Tagをデプロイすると、タグ管理の利点を最大限に活用して、高度なイベントトラッキングと補足的なデータレイヤー変数を完全に実装できます。

この方法では、タグ管理をデプロイする利点に加え、Google Tag Managerの既存のイベントトラッキングを利用してインストールを迅速化できます。

インストールコンポーネント：

* [タグ管理](https://docs.tealium.com/what-is-tealium-tag-management/)
* [Google Tag ManagerのカスタムHTMLタグ](https://support.google.com/tagmanager/answer/6107167?hl=en)

## 詳細情報

実装を引き続き進めるために、以下のリソースを利用できます。

### Live Events

どのインストールオプションを選択した場合でも、Tealiumの[Live Events]()を使用して、プラットフォームに流入するデータを検証します。**Live Events**では受信データがリアルタイムで表示されるため、トラッキング対象のイベントと収集したデータ属性を評価できます。

### Tealium Education

[education.tealium.com](https://education.tealium.com/)でTealiumの充実したオンデマンド学習コンテンツをご覧ください。[訪問プロファイル管理コース](https://education.tealium.com/learn/course/en-as-bsc-elrn)などのコースを活用して、Tealiumに関する知識とスキルを向上できます。