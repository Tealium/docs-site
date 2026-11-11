---
title: SAS 360 Matchコネクタ構成ガイド
description: この記事では、SAS 360 Matchコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/sas-360-match-connector/
---
## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| 状態ベクトルタグを送信 | ✓ | ✓ |

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を行います。

* **APIキー**：SASから提供されたAPIキー。APIを有効にするには、SASテクニカルサポートにお問い合わせください。
* **ベースURL**：`/setsv/`より前の部分までを含むSASエンドポイントのベースURL。例：`https://mydomain.aimatch.com/mycompany`

コネクタを構成したら、**完了**をクリックします。

## アクション

以下のセクションでは、各アクションでサポートされるパラメータについて説明します。

### 状態ベクトルタグを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| ユーザー識別子（状態ベクトルID） | （必須）関連する訪問識別子をカスタムテキストとしてマッピングします。 |
| 状態ベクトルタグデータ | 1つ以上のタグにカスタムマッピングを追加します。 |

## ベンダーのドキュメント

* [SAS 360 Match：高度な機能ガイド](https://support.sas.com/documentation/prod-p/iap/default/en/PDF/Advanced_Features_SASIA.pdf)