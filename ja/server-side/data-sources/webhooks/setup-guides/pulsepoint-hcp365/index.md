---
title: PulsePoint HCP365受信Webhook構成ガイド
description: この記事では、PulsePoint HCP365データソースを使用してPulsePointアカウントにWebhookを作成し、Tealiumに対してアクション可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/pulsepoint-hcp365/
---
PulsePoint HCP365ピクセルは、医薬品ウェブサイトを訪れるヘルスケアプロバイダー（HCP）の身元を特定するために使用されます。PulsePoint HCP 365データソースの目的は、HCPの解決された身元と、HCPに関連する他のデータ要素を取り込むことです。

## 前提条件

* PulsePoint HCP365アカウント
* Tealium for Pharma

## 仕組み

PulsePoint HCP365は、指定したエンドポイントに対して送信リクエストを送るように構成できるWebhook機能を提供しています。これらのリクエストは、PulsePointアカウント内のアクティビティについてTealiumに通知します。Tealium内でPulsePointデータソースを追加すると、PulsePoint HCP365内でPulsePoint Webhookを構成するために使用できるユニークなエンドポイントが生成されます。

## PulsePointデータソース

PulsePointデータソースを構成するには、以下の手順を実行します：

1. **Sources**に移動します。
1. サイドバーで、**Connect &gt; Data Sources**を選択します。
1. **&#43;Add Data Source**をクリックします。
1. **Select a Platform**画面で、**Categories**の下の**Pharma**を選択し、次に**PulsePoint HCP365**を選択します。
1. **Summary**の下の**Name**フィールドに名前を入力し、**Continue**をクリックします。
1. **Continue**をクリックします。
1. **Pharma**カテゴリの下の`pulsepoint_hcp_identity`イベント仕様を選択し、**Continue**をクリックします：![](/images/server-side/data-sources/webhooks/pulsepoint1.png)
1. （オプション）データソースキー、ベースコード、イベントトラッキングコードを含むインストール手順をダウンロードするには、**Download as PDF**をクリックします。
1. **Save &amp; Continue**をクリックします。
データソースの概要が表示されます。
1. **Close**をクリックします。

詳細については、[Create a data source]()を参照してください。

PulsePointデータソースは、PulsePoint構成内のHTTP GETまたはPOST URLとして使用するためのユニークなURLを生成します。生成されたURLは次の形式を使用します：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

PulsePoint HCP365データソースを作成した後、次の値をメモしてください：**Tealium Account Name**、**Tealium Profile Name**、および**Data Source Key**。これらはPulsePoint HCP365内でWebhookを構成する際に必要となります。

## PulsePoint構成

データソースエンドポイントを構成した後、PulsePointアカウント内でWebhookを構成します。

1. PulsePoint HCP365アプリケーションにログインします。
1. **Webhook Support**に移動します。
1. **Request Method**として`GET`または`POST`を選択します。
1. **URL**フィールドに、Tealiumでデータソースを作成する際に生成されたエンドポイントURLを入力します。
1. **Body**フィールドでは、イベントパラメーターを各リクエストに含める必要があります。これにより、Tealiumインスタンスと特定のデータソースに接続します。イベントパラメーターのリストについては、[Event attributes](#event-attributes)セクションを参照してください。  

## イベント属性

次のパラメーターは、各接続リクエストに含める必要があります：

* `tealium_account` - あなたの**Tealium Account Name**。
* `tealium_profile` - あなたの**Tealium Profile Name**。
* `tealium_datasource` - あなたの**Data Source Key**。

以下の属性はPulsePoint特有のもので、Webhookを通じて送信できます。各属性が以下の表に示すように`pulsepoint_`プレフィックスを含むことを確認してください。HCP365データ要素についてのヘルプが必要な場合は、PulsePointのドキュメンテーションを参照するか、PulsePointサポートチームに連絡してください。

|イベント属性| タイプ| 定義 | 例|
|---| ---| ---| ---|
| `pulsepoint_npi` | String |個々のNational Provider Identifier (NPI)。 | `12345` |
| `pulsepoint_url` | String| イベントが発生したページのURL。| `https://www.brandhcp.com/psoriatic-arthritis/3-year-data/` |
| `pulsepoint_channel` | String | チャンネルインジケーター（`1` - サイト、`2` - 検索）。 | `1` |
| `pulsepoint_token` | String | ピクセルおよび/または配置の一意の識別子。 | `J7CYWG18ZB3F`|
| `pulsepoint_param1` | String | イベントを説明するために使用できるオプションのパラメーター。 | key action |
| `pulsepoint_param2` | String | イベントを説明するために使用できるオプションのパラメーター。 | key action |
| `pulsepoint_param3` | String | イベントを説明するために使用できるオプションのパラメーター。 | key action |
| `pulsepoint_param4` | String | イベントを説明するために使用できるオプションのパラメーター。 | key action |
| `pulsepoint_param5` | String | イベントを説明するために使用できるオプションのパラメーター。 | key action |