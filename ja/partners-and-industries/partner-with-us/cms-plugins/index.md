---
title: CMSプラグイン
description: コンテンツ管理システムとTealium Universal Tag（utag.js）を統合する方法を学びます。
url: https://docs.tealium.com/ja/partners-and-industries/partner-with-us/cms-plugins/
---


Tealiumは、各マーケットプレイスまたはGitHubからインストールできる、いくつかの人気のあるCMSプラットフォーム用の事前構築されたプラグインを提供しています。TealiumのCMSプラグインは、数回のクリックと構成で、サイトのすべてのページにTealium Universal Tag（`utag.js`）とUniversal Data Object（`utag_data`）をインストールします。

## 仕組み

CMSプラグインは、成功したTealiumのインストールの以下の部分を実装します：

* **コード配置**  
サイトのすべてのページにUniversal Tag（`utag.js`）を[正しく配置します](/ja/platforms/javascript/install/#universal-tag-utag-js)。
* **データレイヤー**  
CMSページのメタデータを使用して、[データレイヤーオブジェクトを](/ja/platforms/javascript/install/#universal-data-object-utag-data)動的かつ正確に生成します。
* **構成オプション**  
アカウント名、プロファイル名、環境などの構成を提供します。

例として、[Tealium WordPressプラグインセットアップガイド](/ja/platforms/wordpress/install/)をご覧ください。

## データレイヤーバンドル

Tealium iQタグ管理のデータレイヤーバンドルは、CMSプラグインによって生成される対応する変数のリストです。例えば、eコマースCMSは自動的にデータレイヤーに製品と注文の変数を入力します。Tealiumユーザーは、関連するバンドルを追加することで、これらの変数をすばやくアカウント構成に追加できます。

[CMSデータレイヤーバンドルについてもっと学ぶ]()。

## Tealium CMSプラグインのリスト

以下のCMSベンダーに対してTealiumプラグインが利用可能です：

| CMS  | リンク |
| -------- | ------- |
| Magento 1.x | [Tealium](/ja/platforms/magento-v1/install/) |
| Magento 2.x | [Tealium](/ja/platforms/magento/install/), [Magento Marketplace](https://marketplace.magento.com/tealium-tags.html) |
| Shopify | [Tealium](/ja/platforms/shopify/install/) |
| Sitecore | [GitHub](https://github.com/Tealium/integration-sitecore) |
| Unity | [GitHub](https://github.com/Tealium/unity-plugin), [Tealium](/ja/platforms/unity/install/) |
| WordPress | [GitHub](https://github.com/wp-plugins/tealium), [Tealium](/ja/platforms/wordpress/install/), [WPプラグインページ](https://wordpress.org/plugins/tealium/) |

## パートナーになる

[お問い合わせください](https://tealium.com/tealium-partner-network/)、あなたのテクノロジーを統合します。