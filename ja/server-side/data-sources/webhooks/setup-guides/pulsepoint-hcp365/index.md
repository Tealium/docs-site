---
title: PulsePoint HCP365 インカミングウェブフック構成ガイド
description: この記事では、PulsePoint HCP365 データソースを使用して、PulsePoint アカウントにウェブフックを作成し、Tealium にアクション可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/pulsepoint-hcp365/
---
PulsePoint HCP365 ピクセルは、製薬ウェブサイトを訪れる医療提供者（HCP）の身元を特定するために使用されます。PulsePoint HCP 365 データソースの目的は、HCP の解決された身元と、HCP に関連するその他のデータ要素を取り込むことです。

## 前提条件

* PulsePoint HCP365 アカウント
* Tealium for Pharma

## 動作原理

PulsePoint HCP365 はウェブフック機能を提供し、指定したエンドポイントに送信する構成が可能です。これらのリクエストは、PulsePoint アカウントの活動について Tealium に通知します。Tealium 内で PulsePoint データソースを追加すると、PulsePoint HCP365 でウェブフックを構成するために使用できるユニークなエンドポイントが生成されます。

## PulsePoint データソース

PulsePoint データソースを構成するには、以下の手順を実行します：

1. **Connect > Data Sources** に移動します。
1. **+Add Data Source** をクリックします。
1. **Select a Platform** 画面で、**Categories** の下にある **Pharma** を選択し、次に **PulsePoint HCP365** を選択します。
1. **Summary** の下にある **Name** フィールドに名前を入力し、**Continue** をクリックします。
1. **Continue** をクリックします。
1. **Pharma** カテゴリの下で `pulsepoint_hcp_identity` イベント仕様を選択し、**Continue** をクリックします： ![](https://docs.tealium.com/images/server-side/data-sources/webhooks/pulsepoint1.png)
1. （オプション）データソースキー、ベースコード、イベントトラッキングコードを含むインストール手順をダウンロードするには、**Download as PDF** をクリックします。
1. **Save & Continue** をクリックします。
データソースの概要が表示されます。
1. **Close** をクリックします。

詳細については、[Create a data source](https://docs.tealium.com/create-data-source/) を参照してください。

PulsePoint データソースは、PulsePoint の構成で使用するウェブフック URL として使用するユニークな URL を生成します。生成された URL は次の形式を使用します：

```
https://{collect_subdomain}.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

`{collect_subdomain}` は標準アカウントの場合は `collect` です。プライベートクラウドの顧客は、環境に特有のサブドメイン（例：`pc-xwy`）を使用します。

PulsePoint HCP365 データソースを作成した後、次の値をメモしてください：**Tealium Account Name**、**Tealium Profile Name**、および **Data Source Key**。これらは PulsePoint HCP365 内でウェブフックを構成する際に必要になります。

## PulsePoint の構成

データソースエンドポイントを構成した後、PulsePoint アカウントでウェブフックを構成します。

1. PulsePoint HCP365 アプリケーションにログインします。
1. **Smart Actions > Response > Trigger a Webhook** に移動します。
1. **Request Method** として `GET` または `POST` を選択します。
1. **URL** フィールドに、Tealium でデータソースを作成する際に生成されたエンドポイント URL を入力します。
1. **Body** フィールドに、次の例を参考にウェブフックボディを構成します：

```json
{
  "tealium_account": "YOUR_TEALIUM_ACCOUNT",
  "tealium_profile": "YOUR_TEALIUM_PROFILE",
  "tealium_datasource": "TEALIUM_DATASOURCE_KEY",
  "tealium_event": "pulsepoint_hcp_identity",
  "pulsepoint_npi": "%%NPI%%",
  "pulsepoint_url": "%%URL%%",
  "pulsepoint_channel": "%%CHANNEL%%",
  "pulsepoint_param1": "%%PARAM1%%"
}
```

## イベント属性

各接続リクエストには次のパラメータが含まれている必要があります：

* `tealium_account` - あなたの **Tealium Account Name**。
* `tealium_profile` - あなたの **Tealium Profile Name**。
* `tealium_datasource` - あなたの **Data Source Key**。

以下の属性は PulsePoint 特有のもので、ウェブフックを通じて送信できます。各属性が以下の表に示すように `pulsepoint_` 接頭辞を含むことを確認してください。HCP365 データ要素についてのサポートが必要な場合は、PulsePoint のドキュメントを参照するか、PulsePoint サポートチームに連絡してください。

|イベント属性| タイプ| 定義 | 例|
|---| ---| ---| ---|
| `pulsepoint_npi` | 文字列 |個々の国ホームプロバイダー識別子 (NPI)。 | `12345` |
| `pulsepoint_url` | 文字列| イベントが発生したページの URL。| `https://www.brandhcp.com/psoriatic-arthritis/3-year-data/` |
| `pulsepoint_channel` | 文字列 | チャンネルインジケーター (`1` - サイト, `2` - 検索)。 | `1` |
| `pulsepoint_token` | 文字列 | ピクセルおよび/または配置のためのユニークな識別子。 | `J7CYWG18ZB3F`|
| `pulsepoint_param1` | 文字列 | イベントを説明するために使用できるオプションのパラメータ。 | key action |
| `pulsepoint_param2` | 文字列 | イベントを説明するために使用できるオプションのパラメータ。 | key action |
| `pulsepoint_param3` | 文字列 | イベントを説明するために使用できるオプションのパラメータ。 | key action |
| `pulsepoint_param4` | 文字列 | イベントを説明するために使用できるオプションのパラメータ。 | key action |
| `pulsepoint_param5` | 文字列 | イベントを説明するために使用できるオプションのパラメータ。 | key action |