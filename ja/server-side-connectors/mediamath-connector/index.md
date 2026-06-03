---
title: MediaMathコネクタ構成ガイド
description: この記事では、MediaMathコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/mediamath-connector/
---## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|カスタムデータを送信| ✓| ✗|

## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：MediaMath Ingest API
* APIバージョン：v1
* APIエンドポイント：`https://ingest-default.prod.octane.mediamath.com`


## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて](/ja/server-side/connectors/manage/)の記事を参照してください。

オーディエンスとトリガーを選択した後、**続行**をクリックし、次に**コネクタを追加**をクリックします。コネクタの名前を入力し、以下の構成を構成します：

* **MediaMath** **広告主ID**  
必須：あなたのMediaMath広告主ID。

コネクタの構成が完了したら、**完了**をクリックします。

## アクション構成 — パラメータとオプション

**続行**をクリックしてコネクタのアクションを構成します。アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

Tealiumの属性をMediaMathのカスタム属性にマッピングして、データをキーと値のペアとして渡すことができます。カスタム属性は、送信前にMediaMathで作成およびホワイトリスト化する必要があります。

### アクション — カスタムデータを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|マッピングID| (必須) MediaMathによって提供されるマッピングID。|
|MediaMathユーザーID| (必須) 訪問のMediaMath識別子。[MediaMath Cookie Matching tag]()を実装して、訪問のMediaMath Unique User ID (UUID)を`mediamathid`としてTealium EventStream API Hubに送信します。|
|ピクセルID| (必須) MediaMathによって構成されたピクセルID。|
