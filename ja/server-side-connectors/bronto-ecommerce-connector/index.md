---
title: Bronto Ecommerceコネクタ構成ガイド
description: Brontoの最新の提供物は、RESTの利便性と柔軟性を活用しています。BrontoのRESTクライアントを使用すると、製品データと注文データにアクセスし、作業することができます。この記事では、Customer Data HubアカウントでBrontoを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/bronto-ecommerce-connector/
---
## 必要条件

* Brontoクライアントキー
* Brontoクライアントシークレット

(クライアントキーとシークレットを見つける必要がありますか？[ここから始めてください](http://dev.bronto.com/category/api/rest/getting-started-rest/)。)

## サポートされるアクション

|**アクション名**| **オーディエンスにトリガー**| **ストリームにトリガー**|
|---| ---| ---|
|カートの作成または更新| ✓| ✗|
|カートの削除| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいBronto ECommerceコネクタを追加します。コネクタの追加方法については、[コネクタ概要]()記事を参照してください。

ベンダーを構成するには、次の手順に従います：

1. **構成**タブで、コネクタインスタンスにタイトルを提供します。

1. Brontoアカウントに関連付けられた**クライアントキー**を入力します。

1. Brontoアカウントに関連付けられた**クライアントシークレット**を入力します。

1. 実装に関する追加のメモを提供します。

## アクション構成：パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでアクションを構成し、トリガーします。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション：カートの作成または更新

#### パラメータ

1. **更新戦略** (必須): カートを更新または作成するために使用したい戦略を選択します。Create Onlyはカートを作成しようとしますが、すでに存在する場合はアクションが失敗します。Create or Updateはカートが存在するかどうかを判断します：存在する場合は更新され、存在しない場合は作成されます。Update Onlyはカートが存在するかどうかを判断します：存在する場合は更新され、存在しない場合はアクションが失敗します。
1. **連絡先の作成**: メールがカートの作成に使用され、Brontoの連絡先内にカートが存在しない場合、これをチェックするとトランザクション連絡先が作成されます。
1. **無効なTIDを無視**: リクエストの一部として含まれるTIDまたは`TrackingCookieName`と`TrackingCookieValue`のペアが無効な場合、これをチェックすると無効な値を無視してカートの作成または更新を続けます。
1. **カートデータの作成**: Create Only StrategyまたはCreate or Update Strategyの一部としてカートを作成する場合、カートを説明する値がここにマッピングされます。カートを作成するにはCustomer Cart IDが必要ですが、他のすべてのフィールドはオプションです。空白のままのフィールドは、カートを作成するときにnullになります。
1. **カートアイテムデータの作成**: Create Only StrategyまたはCreate or Update Strategyの一部としてカートを作成する場合、カート内のアイテムを説明する値がここにマッピングされます。アイテムは各キーの値の配列としてマッピングされます。カートにアイテムが含まれている場合、アイテムには数量と合計価格が必要です。他のすべてのフィールドはオプションです。空白のままのフィールドは、アイテムを作成するときにnullになります。
1. **カートデータの更新**: Update Only StrategyまたはCreate or Update Strategyの一部としてカートを更新する場合、カートを説明する値がここにマッピングされます。すべてのフィールドはオプションです。空白のままのフィールドは更新時に変更されません。
1. **カートアイテムデータの更新**: Update Only StrategyまたはCreate or Update Strategyの一部としてカートを更新する場合、カート内のアイテムを説明する値がここにマッピングされます。アイテムは各キーの値の配列としてマッピングされます。空白のままのフィールドは、アイテムを更新するときに変更されません。
1. **カートの検索**: Update Only StrategyまたはCreate or Update Strategyを使用する場合に必要です。Tealiumは、Cart IDまたはCustomer IDを使用してカートを検索しようとします。

### アクション：カートの削除

#### パラメータ

1. **カートの検索** (必須): Tealiumは、Cart IDまたはCustomer IDを使用してカートを検索しようとします。カートが存在しない場合、アクションは失敗します。

## ベンダー文書

### 一般

* [アカウントの作成方法は？](http://dev.bronto.com/category/api/rest/getting-started-rest/)

### API

* [Brontoカート作成API](http://dev.bronto.com/api/rest/order-service/add-cart/)
* [Brontoカート更新API](http://dev.bronto.com/api/rest/order-service/update-cart/)
* [Brontoカート削除API](http://dev.bronto.com/api/rest/order-service/delete-cart/)
