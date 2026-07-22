---
title: The Trade Deskインアプリイベントコネクタ構成ガイド
description: この記事では、The Trade Deskインアプリイベントコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/the-trade-desk-in-app-events-connector/
---## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|インアプリイベントを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

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
| TTDイベントトラッカーID (`upid`) |  <ul><li>TTDイベントトラッカーID (`upid`)</li></ul> |
| モバイルアプリイベント (`ref`) |  <ul><li>これはイベントの名前と同じであるべきです。</li><li>この特定のイベント (`ref`) に対してThe Trade Desk構成ページで構成した値と同じです。</li></ul> |
| モバイルクライアントIPアドレス (`client_ip`) |  <ul><li>モバイルクライアントIPアドレス (`client_ip`)</li></ul> |
| iOS用モバイルIDFA (`idfa`) |  <ul><li>IDFAはiOSの広告主ID (`idfa`)</li></ul> |
| Android用モバイルGPS ADID (`gps_adid`) |  <ul><li>ADIDはGoogle Play広告主ID (`gps_adid`)</li></ul> |
| Windows用モバイルNAID (`win_naid`) |  <ul><li>Windows NAIDはWindows PhoneデバイスID (`win_naid`)</li></ul> |
| 収益追跡値 ( `v` ) |  <ul><li>収益追跡パラメータ `v` と `vf` はUIが有効になっている場合にのみ送信されます。</li><li>`vf` フィールドにはISO 4217通貨コードが使用されます</li><li>`v` フィールドには浮動小数点数が期待されます。</li><li>例：`0.99` , `3.99`</li></ul> |
| 収益追跡通貨 (`vf`) |  <ul><li>収益追跡パラメータ `v` と `vf` はUIが有効になっている場合にのみ送信されます</li><li>`vf` フィールドにはISO 4217通貨コードが使用されます</li><li>`v` フィールドには浮動小数点数が期待されます。</li><li>例：`0.99` , `3.99`</li></ul> |
|追加のクエリデータ|  <ul><li>必要に応じて追加のURLクエリパラメータデータを提供します</li></ul> |