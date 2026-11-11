---
title: PulsePoint NPI Listコネクタ構成ガイド
description: この記事では、PulsePoint NPI Listコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/pulsepoint-npi-list-connector/
---
この統合により、PulsePointのLifeに接続できます。Lifeはヘルスケア広告に特化したDSPで、医療分野および非医療分野のパブリッシャーを通じてHCPを対象とするデジタルヘルスケア広告キャンペーンを計画、実施、分析できます。PulsePoint NPI Listコネクタでは、LifeのNPI Listに直接アクセスして完全に制御できるため、[Tealium for Pharma CDP](https://docs.tealium.com/ja/industries/tealium-for-pharma/)とのシームレスな統合が実現します。

## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：PulsePoint API
* APIバージョン：v2
* APIエンドポイント：`https://lifeapi.pulsepoint.com/RestApi/v2/npi/npi-list/`

## コネクタアクション

| アクション名 | ビジタープロファイル | イベントデータ |
| --- | :---: | :---: |
| NPIリストを作成 | ✓ | ✗ |
| リストにNPIを追加 | ✓ | ✗ |
| リストからNPIを削除 | ✓ | ✗ |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **クライアントID**  
（必須）PulsePointのアカウントID。
* **クライアントシークレット**  
（必須）PulsePointの担当者から提供される、PulsePointアカウントのシークレット。
* **ユーザー名**  
（必須）クライアントのPulsePoint Lifeユーザー名。
* **パスワード**  
（必須）クライアントのユーザー名に対応するPulsePoint Lifeパスワード。
* **アカウントID**  
（必須）クライアントに関連付けられ、すべてのNPIリストを保持するアカウントID。

## アクション

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### NPIリストを作成

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 名前 | （必須）NPIリストに関連付けられている広告主の名前。 |
| 広告主 | （必須）NPIリスト名。 |
| NPI | （必須）NPIリストに含めるNPIのリスト。 |

### リストにNPIを追加

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| リストID | （必須）追加するNPIが属するリストの番号。 |
| NPI | （必須）NPIリストに含めるNPIのリスト。 |

### リストからNPIを削除

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| リストID | （必須）削除するNPIが属するリストの番号。 |
| NPI | （必須）NPIリストから削除するNPIのリスト。 |