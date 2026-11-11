---
title: Insightly CRMコネクタ構成ガイド
description: この記事では、Insightly CRMコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/insightly-crm-connector/
---
## サポートされているアクション

|**アクション名**| **オーディエンスでトリガー**| **ストリームでトリガー**|
|---| ---| ---|
|連絡先を追加| ✓| ✓|
|連絡先を更新| ✓| ✓|
|リードを追加| ✓| ✓|
|リードを更新| ✓| ✓|

### API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Insightly API
* APIバージョン：v3.1
* APIエンドポイント：`https://api..insightly.com/`
* ドキュメント：[Insightly API](https://api.insightly.com/v3.1/Help)

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを構成するには、次の手順に従います。

1. **Configure**タブで、InsightlyアカウントのAPI PodとAPIキーを入力します。  
この情報を取得するには、Insightlyアカウントにログインし、**User Settings**セクションを選択します。
1. APIサブセクションで、APIキーとAPI URLを確認します。
  * API URLの形式は次のとおりです：`https://api.{pod}.insightly.com/v3.1/`
  * 例：API URLが`https://api.na1.insightly.com`の場合、API Podは`na1`です。
  * 詳細については、[Insightly：APIキーまたはURLの確認とキーのリセット](https://support.insight.ly/hc/en-us/articles/204864594-Finding-your-Insightly-API-key)を参照してください。

## アクション構成：パラメータとオプション

**Continue**をクリックして、コネクタのアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション：連絡先を追加

このアクションでは、Insightly CRMに新しい連絡先を作成できます。

#### パラメータ

* **属性**
  * 必須
  * 連絡先の属性。
  * First Nameは必須です。その他の属性は任意です。

* **カスタムフィールド**
  * 任意
  * 指定した場合、これらのフィールドは`CUSTOMFIELDS`オブジェクトのリストとして送信されます。

* **タグ**
  * 任意
  * 指定した場合、これらのフィールドは`TAGS`オブジェクトのリストとして送信されます。

### アクション：連絡先を更新

このアクションでは、Insightly CRM内の既存の連絡先を更新できます。

#### パラメータ

* **属性**
  * 必須
  * 連絡先の属性。
  * Contact IDは必須です。その他の属性は任意です。

* **カスタムフィールド**
  * 任意
  * 指定した場合、これらのフィールドは`CUSTOMFIELDS`オブジェクトのリストとして送信されます。

* **タグ**
  * 任意
  * 指定した場合、これらのフィールドは`TAGS`オブジェクトのリストとして送信されます。

### アクション：リードを追加

このアクションでは、Insightly CRMに新しいリードを作成できます。

#### パラメータ

* **属性**
  * 必須
  * リードの属性。
  * Last Nameは必須です。その他の属性は任意です。

* **カスタムフィールド**
  * 任意
  * 指定した場合、これらのフィールドは`CUSTOMFIELDS`オブジェクトのリストとして送信されます。

* **タグ**
  * 任意
  * 指定した場合、これらのフィールドは`TAGS`オブジェクトのリストとして送信されます。

### アクション：リードを更新

このアクションでは、Insightly CRM内の既存のリードを更新できます。

#### パラメータ

* **属性**
  * 必須
  * リードの属性。
  * Lead IDは必須です。その他の属性は任意です。

* **カスタムフィールド**
  * 任意
  * 指定した場合、これらのフィールドは`CUSTOMFIELDS`オブジェクトのリストとして送信されます。

* **タグ**
  * 任意
  * 指定した場合、これらのフィールドは`TAGS`オブジェクトのリストとして送信されます。

## ベンダーのドキュメント

* [Insightlyホームページ](https://www.insightly.com/)
* [Insightly APIドキュメント](https://api.insightly.com/v3.1/Help#!)