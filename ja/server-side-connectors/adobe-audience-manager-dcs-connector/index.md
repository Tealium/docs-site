---
title: Adobe Audience Manager DCS コネクタ構成ガイド
description: Adobeのデータ収集サーバー（DCS）は、Adobe Audience Managerで管理するための視聴者ユーザーデータを収集するためのサーバー間APIを提供します。この記事では、Customer Data Hubプロファイルでのサービスの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-audience-manager-dcs-connector/
---## 必要条件

* Adobe Audience Managerによって割り当てられたドメインエイリアス

## サポートされるアクション

|**アクション名**| **視聴者にトリガー**| **ストリームにトリガー**|
|---| ---| ---|
|データ収集イベントを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()の記事を参照してください。

ベンダーを構成するには、次の手順に従います：

* **構成**タブで、コネクタインスタンスにタイトルを提供します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - データ収集イベントを送信

#### パラメータ

1. **ドメインエイリアス** (必須): Audience Managerによって割り当てられたドメインエイリアスを提供します。
1. **リージョンID** (必須): イベントを送信するユーザーに割り当てられたリージョンIDを提供します。詳細については、[ユーザーIDとリージョンの取得](https://marketing.adobe.com/resources/help/en_US/aam/dcs-aam-ids.html)および[リージョンとホスト名](https://marketing.adobe.com/resources/help/en_US/aam/dcs-regions.html)を参照してください。
1. **イベントデータ** (必須): 属性をイベントパラメータにマップします（参照：[サポートされるイベントパラメータ](https://marketing.adobe.com/resources/help/en_US/aam/dcs-keys.html)）。オプション`Data Provider ID `と`Data Provider User ID`/`Integration Code`は、それぞれ`d_cid`と`d_cid_ic`パラメータのために`%01`セパレータで自動的に組み合わせられます（参照：[CIDとCID_IC](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)）

詳細情報については、[イベントAPI呼び出しの作成](https://marketing.adobe.com/resources/help/en_US/aam/dcs-s2s-calls.html)を参照してください。

## ベンダー文書

* [イベントAPI呼び出しの作成](https://marketing.adobe.com/resources/help/en_US/aam/dcs-s2s-calls.html)
* [ユーザーIDとリージョンの取得](https://marketing.adobe.com/resources/help/en_US/aam/dcs-aam-ids.html)
* [リージョンとホスト名](https://marketing.adobe.com/resources/help/en_US/aam/dcs-regions.html)
* [サポートされるイベントパラメータ](https://marketing.adobe.com/resources/help/en_US/aam/dcs-keys.html)
* [CIDとCID\_IC](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)

