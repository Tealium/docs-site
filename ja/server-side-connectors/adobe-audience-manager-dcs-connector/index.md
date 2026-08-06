---
title: Adobe Audience Manager DCSコネクタ構成ガイド
description: Adobeのデータ収集サーバー（DCS）は、サーバー間APIを提供して、Adobe Audience Managerで管理されるオーディエンスユーザーデータを収集します。この記事では、お客様のCustomer Data Hubプロファイルでサービスを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-audience-manager-dcs-connector/
---## 必要条件

* Adobe Audience Managerによって割り当てられたドメインエイリアス

## サポートされるアクション

|**アクション名**| **オーディエンスに対するトリガー**| **ストリームに対するトリガー**|
|---| ---| ---|
|データ収集イベントの送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)の記事を参照してください。

ベンダーを構成するには、次の手順に従います：

* **構成**タブで、コネクタインスタンスのタイトルを提供します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - データ収集イベントの送信

#### パラメータ

1. **ドメインエイリアス**: (必須) Audience Managerによって割り当てられたドメインエイリアスを提供します。
1. **リージョンID**: (必須) イベントを送信するユーザーに割り当てられたリージョンIDを提供します。詳細は[ユーザーIDとリージョンの取得](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-url-receive)および[リージョンとホスト名](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions)を参照してください。
1. **イベントデータ**: (必須) 属性をイベントパラメータにマッピングします（参照：[サポートされるイベントパラメータ](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-keys)）。オプションの`Data Provider ID`と`Data Provider User ID`/`Integration Code`は、それぞれ`d_cid`および`d_cid_ic`パラメータに`%01`セパレータで自動的に組み合わされます（参照：[CIDとCID_IC](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/reference/cid)）


<blockquote>
詳細については、[イベントAPIコールの作成](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-event-calls)を参照してください。
</blockquote>


## ベンダー文書

* [イベントAPIコールの作成](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-event-calls)
* [ユーザーIDとリージョンの取得](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-url-receive)
* [リージョンとホスト名](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions)
* [サポートされるイベントパラメータ](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-keys)
* [CIDとCID\_IC](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/reference/cid)