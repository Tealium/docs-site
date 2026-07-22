---
title: Salesforce Audience Studio コネクタ構成ガイド
description: この記事では、Salesforce Audience Studioコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/salesforce-audience-studio-connector/
---
## サポートされているアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ピクセルを送信| ✓| ✓|
|イベントを送信| ✓| ✓|
|トランザクションを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ピクセルを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ドメイン|  <ul><li>必須。</li><li>この値を取得するには、Salesforce Audience Studioの担当者に連絡してください。</li></ul> |
|パブリッシャーUUID|  <ul><li>必須。</li><li>この値を取得するには、Salesforce Audience Studioの担当者に連絡してください。</li></ul> |
|サイト|  <ul><li>必須。</li><li>この値を取得するには、Salesforce Audience Studioの担当者に連絡してください。</li></ul> |
|ユニークユーザーID|  <ul><li>必須。</li><li>iOSの場合、これはユニークな広告主IDである必要があります（デバイスIDではありません）。</li></ul> |
|セクション|  <ul><li>データを送信したいアプリケーションのセクションです。</li><li>例えば、`open_app`や`home_page`など</li></ul> |
|ブラウザ属性|  <ul><li>ユーザーエージェントデータを補完するために送信する必要があるすべてのブラウザ属性データ。</li></ul> |
|追加情報|  <ul><li>追加情報については、[Salesforce Audience Studio](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API#trackingviews)のドキュメンテーションを参照してください。</li></ul> |

### アクション - イベントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントURLエンドポイント|  <ul><li>イベントURLは[Salesforce Audience Studio UI](https://console.krux.com/events/list)で作成されます。</li></ul> |
|ユニークユーザーID|  <ul><li>必須。</li><li>iOSの場合、これはユニークな広告主IDである必要があります（デバイスIDではありません）。</li></ul> |

### アクション - トランザクションを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ユニークユーザーID|  <ul><li>必須。</li><li>iOSの場合、これはユニークな広告主IDである必要があります（デバイスIDではありません）。</li></ul> |
|トランザクションURLエンドポイント|  <ul><li>トランザクションデータを送信するためにSalesforce Audience Studioの担当者から提供されるURL。</li></ul> |
|パブリッシャーUUID|  <ul><li>必須。</li><li>この値を取得するには、Salesforce Audience Studioの担当者に連絡してください。</li></ul> |
|注文合計|  <ul><li>必須。</li></ul> |
|数量|  <ul><li>必須。</li></ul> |
|トランザクション日|  <ul><li>必須。</li></ul> |
|追加情報|  <ul><li>追加情報については、[Salesforce Audience Studio](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API#trackingviews)のドキュメンテーションを参照してください。</li></ul> |
