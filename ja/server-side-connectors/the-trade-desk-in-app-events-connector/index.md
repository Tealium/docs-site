---
title: The Trade Desk アプリ内イベントコネクタ構成ガイド
description: この記事では、The Trade Desk アプリ内イベントコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/the-trade-desk-in-app-events-connector/
---## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|アプリ内イベントを送信| ✓| ✓|

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **広告主ID（adv）**
  * The Trade Deskの広告主IDを表します。

## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション — アプリ内イベントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
| TTDイベントトラッカーID（`upid`） |  <ul><li>TTDイベントトラッカーID（`upid`）</li></ul> |
| モバイルアプリイベント（`ref`） |  <ul><li>イベント名と同じ名前にする必要があります。</li><li>この特定のイベントについて、The Trade Deskの構成ページで構成した値（`ref`）と同じにします。</li></ul> |
| モバイルクライアントIPアドレス（`client_ip`） |  <ul><li>モバイルクライアントIPアドレス（`client_ip`）</li></ul> |
| iOS用モバイルIDFA（`idfa`） |  <ul><li>IDFAは、iOSの広告主向けIDです（`idfa`）。</li></ul> |
| Android用モバイルGPS ADID（`gps_adid`） |  <ul><li>ADIDは、Google Playの広告主IDです（`gps_adid`）。</li></ul> |
| Windows用モバイルNAID（`win_naid`） |  <ul><li>Windows NAIDは、Windows PhoneのデバイスIDです（`win_naid`）。</li></ul> |
| 収益トラッキング値（`v`） |  <ul><li>収益トラッキングパラメータ`v`および`vf`は、UIが有効な場合にのみ送信されます。</li><li>`vf`フィールドにはISO 4217通貨コードが使用されます。</li><li>`v`フィールドには浮動小数点数を指定する必要があります。</li><li>例：`0.99`、`3.99`</li></ul> |
| 収益トラッキング通貨（`vf`） |  <ul><li>収益トラッキングパラメータ`v`および`vf`は、UIが有効な場合にのみ送信されます。</li><li>`vf`フィールドにはISO 4217通貨コードが使用されることに注意してください。</li><li>`v`フィールドには浮動小数点数を指定する必要があります。</li><li>例：`0.99`、`3.99`</li></ul> |
|追加のクエリデータ|  <ul><li>必要に応じて、追加のURLクエリパラメータデータを指定します。</li></ul> |