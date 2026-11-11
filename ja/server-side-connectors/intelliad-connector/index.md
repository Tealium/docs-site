---
title: Customer Data Platform（CDP）向けintealliAdコネクタ構成ガイド
description: この記事では、intealliAdコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/intelliad-connector/
---
## 要件

クライアントID（intelliAd CSMチームから提供されます）

## サポートされているアクション

|**アクション名**| **オーディエンスによるトリガー**| **ストリームによるトリガー**|
|---| ---| ---|
|ユーザーをセグメントに追加| ✓| ✗|

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

ベンダーを構成するには、次の手順に従います。

1. **Configure**タブで、コネクタインスタンスのタイトルを指定します。

1. アカウント用にintelliAdから受け取った**Client ID**を入力します。

1. 実装に関する追加のメモを入力します。

## アクション構成 — パラメータとオプション

**Continue**をクリックして、コネクタのアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション — ユーザーをセグメントに追加

#### パラメータ

1. **Client ID**：（任意）**Configuration**タブで指定した値を上書きします。
1. **Add to Segment Config**：（必須）有用な情報を提供するデータフィールドに属性をマッピングします。以下のオプションを参照してください。

|**オプション**| **説明**|
|---| ---|
|セグメント（seg）| セグメントIDのカンマ区切りリスト。セグメントIDは、intelliAd CSMチームまたはintelliAdのフロントエンドから提供されます。|
|intelliAdユーザーID（`iauuid`）| コネクタに渡されるintelliAdユーザーID|
|除外（exclude）| 現在のユーザーについて、指定したセグメントを除外します。指定できる値は`1`のみです。|