---
title: Centro DSPコネクタ構成ガイド（廃止）
description: この記事では、Customer Data HubアカウントでCentro Demand-Side Platform（DSP）コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/centro-dsp-connector-setup-guide-deprecated/
---
このコネクタは廃止され、現在はタグマーケットプレイスで利用できません。現行のコネクタについては、[Basis Technologies DSP Connector]()をご覧ください。

Centro DSPは、複数のチャネルでリアルタイムに高度にターゲット指向の広告キャンペーンを構築し、最適化するための広告プラットフォームです。

データが送信される前に、セグメントの分類法をCentroに送信し、ロードされたことを確認する必要があります。認識しないセグメントIDのデータは破棄します。分類法を[dsp.newdata@centro.net](http://mailto:dsp.newdata@centro.net)に送信してください。

## サポートされているアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|オーディエンスセグメントを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[Connector Overview]()の記事をご覧ください。

コネクタを追加した後、以下の構成を構成します：

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - オーディエンスセグメントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Centro Cookie ID / ssi| 必須|
|セグメント / オーディエンス|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;CSV値として1つ以上のオーディエンスセグメントIDを提供します。例：`47598,47600,47601,47603,47604`&lt;/li&gt;&lt;/ul&gt; |

