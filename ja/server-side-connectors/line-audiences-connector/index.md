---
title: LINEオーディエンスコネクタ構成ガイド
description: この記事では、LINEオーディエンスコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/line-audiences-connector/
---
## API情報

このコネクタは、以下のベンダーAPIを使用します：

* API名：LINE Audience API
* APIバージョン：v2
* APIエンドポイント：`https://api.line.me/v2`
* ドキュメンテーション：[LINE Audience API](https://developers.line.biz/en/reference/messaging-api/#manage-audience-group)

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| ユーザーをオーディエンスに追加 | ✓ | ✗ |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **チャネルアクセストークン**  
必須。チャネルアクセストークンは、LINE Developers ConsoleのChannelsセクションで利用可能です。[長期間有効なチャネルアクセストークン](https://developers.line.biz/en/docs/messaging-api/channel-access-tokens/#long-lived-channel-access-tokens)を参照してください。

## アクション構成 - パラメータとオプション

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザーをオーディエンスに追加

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| オーディエンスグループID | オーディエンスグループを選択するか、オーディエンスグループIDをカスタムテキストとして提供します。 |
