---
title: SAS 360 Match コネクタ構成ガイド
description: この記事では、SAS 360 Match コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/sas-360-match-connector/
---
## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| ステートベクタータグを送信 | ✓ | ✓ |

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **API キー**: SAS によって提供される API キー。API を有効にするには、SAS テクニカルサポートに連絡してください。
* **ベース URL**: `/setsv/` を含まない SAS エンドポイントのベース URL。例えば、`https://mydomain.aimatch.com/mycompany`。

## アクション

以下のセクションでは、各アクションでサポートされているパラメータをリストアップしています。

### ステートベクタータグを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| ユーザー識別子（ステートベクター ID） | （必須）関連する訪問識別子をカスタムテキストとしてマッピングします。 |
| ステートベクタータグデータ | 1つ以上のタグに対してカスタムマッピングを追加します。 |

## ベンダー文書

* [SAS 360 Match: 高度な機能ガイド](https://support.sas.com/documentation/prod-p/iap/default/en/PDF/Advanced_Features_SASIA.pdf)