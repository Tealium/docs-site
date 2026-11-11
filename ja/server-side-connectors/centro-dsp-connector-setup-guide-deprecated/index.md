---
title: Centro DSPコネクタ構成ガイド（非推奨）
description: この記事では、Customer Data HubアカウントでCentroデマンドサイドプラットフォーム（DSP）コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/centro-dsp-connector-setup-guide-deprecated/
---

<blockquote>
このコネクタは非推奨となり、コネクタマーケットプレイスでは提供されていません。現在のコネクタについては、[Basis Technologies DSPコネクタ](https://docs.tealium.com/basis-technologies-dsp-connector/)を参照してください。
</blockquote>


Centro DSPは、複数のチャネルにわたって、ターゲットを高度に絞り込んだ広告キャンペーンをリアルタイムで構築および最適化するための広告プラットフォームです。


<blockquote>
データを送信する前に、セグメントタクソノミーをCentroへ送信し、読み込みが完了したことを確認する必要があります。認識されないセグメントIDのデータは破棄されます。タクソノミーを[dsp.newdata@centro.net](http://mailto:dsp.newdata@centro.net)へ送信してください。
</blockquote>


## サポートされているアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|オーディエンスセグメントを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します。

## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタのアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション — オーディエンスセグメントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Centro Cookie ID / ssi| 必須|
|セグメント／オーディエンス| <ul><li>（必須）1つ以上のオーディエンスセグメントIDをCSV値として指定します。例：`47598,47600,47601,47603,47604`</li></ul> |