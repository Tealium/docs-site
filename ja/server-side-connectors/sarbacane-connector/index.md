---
title: Sarbacaneコネクタ構成ガイド
description: この記事では、Sarbacaneコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/sarbacane-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|連絡先の追加または編集| ✓| ✗|
|キャンペーンへの受信者の追加| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **アカウントID**
  * アカウントIDについての詳細は、[Sabracaneのドキュメンテーション](https://developers.sarbacane.com/#authentification)を参照してください。

* **APIキー**
  * APIキーについての詳細は、[Sabracaneのドキュメンテーション](https://developers.sarbacane.com/#authentification)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 連絡先の追加または編集

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID|  <ul><li>関連するリストのID。</li><li>詳細については、[Sabracaneのドキュメンテーション](https://developers.sarbacane.com/#ajouter-modifier-un-contact)を参照してください。</li></ul> |
|メール|  <ul><li>連絡先のメール。</li><li>メールと/または電話を使用する必要があります。</li></ul> |
|電話|  <ul><li>連絡先の電話番号。</li><li>メールと/または電話を使用する必要があります。</li></ul> |
|フィールドID|  <ul><li>IDのキー：値ペアと、それらの列に追加される値。</li><li>列IDの取得または追加方法についての詳細は、[Sabracaneのドキュメンテーション](https://developers.sarbacane.com/#lister-les-champs-personnalises)を参照してください。</li></ul> |

### アクション - キャンペーンへの受信者の追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|キャンペーンID|  <ul><li>キャンペーンのID</li><li>詳細については、[Sabracaneのドキュメンテーション](https://developers.sarbacane.com/#ajouter-des-destinataires)を参照してください。</li></ul> |
|メール|  <ul><li>連絡先のメール。</li><li>メールと/または電話を使用する必要があります。</li></ul> |
|電話|  <ul><li>連絡先の電話番号。</li><li>メールと/または電話を使用する必要があります。</li></ul> |
