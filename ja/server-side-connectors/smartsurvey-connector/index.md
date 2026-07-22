---
title: SmartSurveyコネクタ構成ガイド
description: この記事では、SmartSurveyコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/smartsurvey-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|リストに連絡先を追加| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/ja/server-side/connectors/manage/)の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **APIトークン**
  * APIトークンとトークンシークレットは、各リクエストに伴って渡される必要があります。\\
  * 詳細については、[SmartSurvey: Getting Started](https://docs.smartsurvey.io/docs)を参照してください。

* **APIトークンシークレット**
  * APIトークンとトークンシークレットは、各リクエストに伴って渡される必要があります。
  * 詳細については、[SmartSurvey: Getting Started](https://docs.smartsurvey.io/docs)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - リストに連絡先を追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先リストID|  <ul><li>連絡先リストの一意のID。</li><li>詳細については、[SmartSurveyのドキュメンテーション](https://docs.smartsurvey.io/v1/reference#contactlists_contacts_insert)を参照してください。</li></ul> |
|メール|  <ul><li>連絡先のメールアドレス。</li></ul> |
|名前|  <ul><li>連絡先の名前。</li></ul> |
|カスタムフィールド|  <ul><li>連絡先に関連するカスタムデータフィールド。</li></ul> |
