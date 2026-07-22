---
title: AdFormコネクタ構成ガイド
description: Adformは、エージェンシーと広告主がパーソナライズされたターゲティング、リアルタイム入札、リッチメディアを使用してディスプレイ広告を最高のパフォーマンスチャネルにするために構築されたクラウドテクノロジーです。プラットフォームには、キャンペーンの計画、広告配信、最適化、分析、レポートなどが含まれています。この記事では、お客様のCustomer Data HubアカウントでAdformコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adform-connector/
---## サポートされているアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|製品情報を送信| ✓| ✗|

## 構成の構成

**Connector Marketplace**に移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[Connector Overview](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 製品情報を送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Adform Id| 必須|
|Tracking Point Id| (必須)|
|Tracking Setup Id| (必須)|
|Product Id| (必須)|
