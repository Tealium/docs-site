---
title: Mailrelayコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでMailrelayコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/mailrelay-connector/
---## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|購読者を追加| ✓| ✗|

## 構成を構成する

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタのアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 購読者を追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|あなたのアカウント|  &lt;ul&gt;&lt;li&gt;あなたのMailrelayアドレスまたはアカウント名。&lt;/li&gt;&lt;li&gt;詳細については、次を参照してください：&lt;https://mailrelay.com/en/api-documentation&gt;&lt;/li&gt;&lt;/ul&gt; |
|APIキー|  &lt;ul&gt;&lt;li&gt;あなたのAPIキー。&lt;/li&gt;&lt;li&gt;アカウントの構成の下にあります。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;購読者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|名前|  &lt;ul&gt;&lt;li&gt;購読者の名前。&lt;/li&gt;&lt;/ul&gt; |
