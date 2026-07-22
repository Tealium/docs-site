---
title: Mailrelayコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでMailrelayコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/mailrelay-connector/
---## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|購読者を追加| ✓| ✗|

## 構成を構成する

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタのアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 購読者を追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|あなたのアカウント|  <ul><li>あなたのMailrelayアドレスまたはアカウント名。</li><li>詳細については、次を参照してください：<https://mailrelay.com/en/api-documentation></li></ul> |
|APIキー|  <ul><li>あなたのAPIキー。</li><li>アカウントの構成の下にあります。</li></ul> |
|メール|  <ul><li>購読者のメールアドレス。</li></ul> |
|名前|  <ul><li>購読者の名前。</li></ul> |
