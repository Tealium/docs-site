---
title: The Trade Deskインアプリイベントコネクタ構成ガイド
description: この記事では、The Trade Deskインアプリイベントコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/the-trade-desk-in-app-events-connector/
---## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|インアプリイベントを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **広告主ID (adv)**
  * The Trade Desk上の広告主IDを表します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - インアプリイベントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
| TTDイベントトラッカーID (`upid`) |  &lt;ul&gt;&lt;li&gt;TTDイベントトラッカーID (`upid`)&lt;/li&gt;&lt;/ul&gt; |
| モバイルアプリイベント (`ref`) |  &lt;ul&gt;&lt;li&gt;これはイベントの名前と同じであるべきです。&lt;/li&gt;&lt;li&gt;この特定のイベント (`ref`) に対してThe Trade Desk構成ページで構成した値と同じです。&lt;/li&gt;&lt;/ul&gt; |
| モバイルクライアントIPアドレス (`client_ip`) |  &lt;ul&gt;&lt;li&gt;モバイルクライアントIPアドレス (`client_ip`)&lt;/li&gt;&lt;/ul&gt; |
| iOS用モバイルIDFA (`idfa`) |  &lt;ul&gt;&lt;li&gt;IDFAはiOSの広告主ID (`idfa`)&lt;/li&gt;&lt;/ul&gt; |
| Android用モバイルGPS ADID (`gps_adid`) |  &lt;ul&gt;&lt;li&gt;ADIDはGoogle Play広告主ID (`gps_adid`)&lt;/li&gt;&lt;/ul&gt; |
| Windows用モバイルNAID (`win_naid`) |  &lt;ul&gt;&lt;li&gt;Windows NAIDはWindows PhoneデバイスID (`win_naid`)&lt;/li&gt;&lt;/ul&gt; |
| 収益追跡値 ( `v` ) |  &lt;ul&gt;&lt;li&gt;収益追跡パラメータ `v` と `vf` はUIが有効になっている場合にのみ送信されます。&lt;/li&gt;&lt;li&gt;`vf` フィールドにはISO 4217通貨コードが使用されます&lt;/li&gt;&lt;li&gt;`v` フィールドには浮動小数点数が期待されます。&lt;/li&gt;&lt;li&gt;例：`0.99` , `3.99`&lt;/li&gt;&lt;/ul&gt; |
| 収益追跡通貨 (`vf`) |  &lt;ul&gt;&lt;li&gt;収益追跡パラメータ `v` と `vf` はUIが有効になっている場合にのみ送信されます&lt;/li&gt;&lt;li&gt;`vf` フィールドにはISO 4217通貨コードが使用されます&lt;/li&gt;&lt;li&gt;`v` フィールドには浮動小数点数が期待されます。&lt;/li&gt;&lt;li&gt;例：`0.99` , `3.99`&lt;/li&gt;&lt;/ul&gt; |
|追加のクエリデータ|  &lt;ul&gt;&lt;li&gt;必要に応じて追加のURLクエリパラメータデータを提供します&lt;/li&gt;&lt;/ul&gt; |