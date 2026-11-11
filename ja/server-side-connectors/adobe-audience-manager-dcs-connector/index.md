---
title: Adobe Audience Manager DCS コネクタ構成ガイド
description: Adobe のデータ収集サーバー（DCS）は、Adobe Audience Manager で管理するオーディエンスユーザーデータを収集するためのサーバー間 API を提供します。この記事では、Customer Data Hub プロファイルでサービスを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-audience-manager-dcs-connector/
---## 要件

* Adobe Audience Manager によって割り当てられたドメインエイリアス

## サポートされているアクション

|**アクション名**| **オーディエンスでトリガー**| **ストリームでトリガー**|
|---| ---| ---|
|データ収集イベントを送信| ✓| ✓|

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

ベンダーを構成するには、次の手順に従います。

* **Configure** タブで、コネクタインスタンスのタイトルを入力します。

## アクション構成 — パラメータとオプション

**Continue** をクリックして、コネクタのアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション — データ収集イベントを送信

#### パラメータ

1. **ドメインエイリアス**：（必須）Audience Manager によって割り当てられたドメインエイリアスを指定します。
1. **リージョン ID**：（必須）イベントを送信するユーザーに割り当てられたリージョン ID を指定します。詳細については、[ユーザー ID とリージョンの取得](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-url-receive)および[リージョンとホスト名](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions)を参照してください。
1. **イベントデータ**：（必須）属性をイベントパラメータにマッピングします（[サポートされているイベントパラメータ](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-keys)を参照）。オプションの `Data Provider ID ` と `Data Provider User ID`／`Integration Code` は、それぞれ `d_cid` パラメータと `d_cid_ic` パラメータ用に、区切り文字 `%01` を使用して自動的に結合されます（[CID と CID_IC](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/reference/cid)を参照）。


<blockquote>
詳細については、[イベント API 呼び出しの実行](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-event-calls)を参照してください。
</blockquote>


## ベンダーのドキュメント

* [イベント API 呼び出しの実行](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-event-calls)
* [ユーザー ID とリージョンの取得](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-event-calls/dcs-url-receive)
* [リージョンとホスト名](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions)
* [サポートされているイベントパラメータ](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-keys)
* [CID と CID\_IC](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/reference/cid)